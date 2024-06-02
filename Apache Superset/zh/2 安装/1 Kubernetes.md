[TOC]

## 在 Kubernetes 上安装

在官方 [Superset helm 存储库](https://apache.github.io/superset/index.yaml) 中找到的 [Helm](https://helm.sh/) 图表支持在 Kubernetes 上运行 Superset。

### 先决条件

- 一个 Kubernetes 集群
- 安装 Helm

> 对于更简单的单主机环境，我们建议使用 [minikube](https://minikube.sigs.k8s.io/docs/start/)，它可以在许多平台上轻松设置，并且与此处引用的 Helm 图表配合得非常好。

### 运行

1. 添加 Superset helm 仓库

```sh
helm repo add superset https://apache.github.io/superset
"superset" has been added to your repositories
```

2. 查看存储库中的图表

```sh
helm search repo superset
NAME                    CHART VERSION   APP VERSION     DESCRIPTION
superset/superset       0.1.1           1.0             Apache Superset is a modern, enterprise-ready b...
```

3. 配置您的设置

就像任何典型的 Helm 图表一样，您需要制作一个 `values.yaml` 文件，该文件将定义/覆盖默认 [values.yaml](https://github.com/apache/superset/tree/master/helm/superset/values.yaml)，或来自它所依赖的任何依赖图表：

- [bitnami/redis](https://artifacthub.io/packages/helm/bitnami/redis)
- [bitnami/postgresql](https://artifacthub.io/packages/helm/bitnami/postgresql)

下面是有关您可能需要的一些重要覆盖的更多信息。

4. 安装并运行

```sh
helm upgrade --install --values my-values.yaml superset superset/superset
```

您应该会看到弹出各种 pod，例如：

```sh
kubectl get pods
NAME                                    READY   STATUS      RESTARTS   AGE
superset-celerybeat-7cdcc9575f-k6xmc    1/1     Running     0          119s
superset-f5c9c667-dw9lp                 1/1     Running     0          4m7s
superset-f5c9c667-fk8bk                 1/1     Running     0          4m11s
superset-init-db-zlm9z                  0/1     Completed   0          111s
superset-postgresql-0                   1/1     Running     0          6d20h
superset-redis-master-0                 1/1     Running     0          6d20h
superset-worker-75b48bbcc-jmmjr         1/1     Running     0          4m8s
superset-worker-75b48bbcc-qrq49         1/1     Running     0          4m12s
```

确切的列表将取决于您的一些特定配置覆盖，但您通常应该期望：

- N `superset-xxxx-yyyy` 和 `superset-worker-xxxx-yyyy` pods (取决于您的 `supersetNode.replicaCount` 和 `supersetWorker.replicaCount` 值)
- 1 `superset-postgresql-0` 取决于你的 postgres 设置
- 1 `superset-redis-master-0` 取决于你的 redis设置
- 1 `superset-celerybeat-xxxx-yyyy` pod 如果您的值覆盖中有 `supersetCeleryBeat.enabled = true`

1. 访问它

该图表将发布适当的服务，以在 k8s 集群内部公开 Superset UI。要从外部访问它，您必须：

- 将服务配置为 `LoadBalancer` 或 `NodePort`
- 为其设置一个 `Ingress` - 图表包含定义，但需要根据您的需求进行调整（主机名、tls、注释等...）
- 运行 `kubectl port-forward superset-xxxx-yyyy :8088` 直接将一个 Pod 的端口隧道连接到本地主机

根据您配置外部访问的方式，URL 会有所不同。一旦您确定了适当的 URL，您就可以使用以下方式登录：

- 用户: `admin`
- 密码: `admin`

### 重要设置

#### 安全设定

包含默认安全设置和密码，但您**必须**更新它们才能运行 `prod` 实例，特别是：

```yaml
postgresql:
  postgresqlPassword: superset
```

确保为 SECRET_KEY 设置一个独特的、强大的复杂字母数字字符串，并使用工具来帮助您生成足够随机的序列。

- 要生成一个好的密钥，您可以运行 `openssl rand -base64 42`

```yaml
configOverrides:
  secret: |
    SECRET_KEY = 'YOUR_OWN_RANDOM_GENERATED_SECRET_KEY'
```

如果您想更改以前的密钥，则应该轮换密钥。 kubernetes 部署的默认密钥是 `thisISaSECRET_1234`

```yaml
configOverrides:
  my_override: |
    PREVIOUS_SECRET_KEY = 'YOUR_PREVIOUS_SECRET_KEY'
    SECRET_KEY = 'YOUR_OWN_RANDOM_GENERATED_SECRET_KEY'
init:
  command:
    - /bin/sh
    - -c
    - |
      . {{ .Values.configMountPath }}/superset_bootstrap.sh
      superset re-encrypt-secrets
      . {{ .Values.configMountPath }}/superset_init.sh
```

> Superset使用 [Scarf Gateway](https://about.scarf.sh/scarf-gateway) 来收集遥测数据。了解不同 Superset 版本的安装数量可以帮助项目做出有关修补和长期支持的决策。 Scarf 会清除个人身份信息 (PII)，并仅提供汇总统计数据。

> 要在基于 Helm 的安装中选择退出此数据收集，请编辑 `helm/superset/values.yaml` 文件中的 `repository:` 行，将 `apachesuperset.docker.scarf.sh/apache/superset` 替换为 `apache/superset` 直接从 Docker Hub 拉取镜像。


#### 依赖关系

安装其他软件包并在引导脚本中执行任何其他引导配置。对于生产集群，建议在 CI 中完成此步骤来构建自己的映像。

> Superset 需要为要连接的每个数据存储安装 Python DB-API 数据库驱动程序和 SQLAlchemy 方言。

> 有关详细信息，请参阅 [安装数据库驱动程序]($InstallDatabaseDrivers)。

以下示例安装 Big Query 和 Elasticsearch 数据库驱动程序，以便您可以连接到 Superset 安装中的这些数据源：

```yaml
bootstrapScript: |
  #!/bin/bash
  pip install psycopg2==2.9.6 \
    sqlalchemy-bigquery==1.6.1 \
    elasticsearch-dbapi==0.2.5 &&\
  if [ ! -f ~/bootstrap ]; then echo "Running Superset with uid {{ .Values.runAsUser }}" > ~/bootstrap; fi
```

#### superset_config.py

默认的 `superset_config.py` 相当小，您很可能需要扩展它。这是通过在 `configOverrides` 中指定一个或多个键/值条目来完成的，例如：

```yaml
configOverrides:
  my_override: |
    # This will make sure the redirect_uri is properly computed, even with SSL offloading
    ENABLE_PROXY_FIX = True
    FEATURE_FLAGS = {
        "DYNAMIC_PLUGINS": True
    }
```

这些将被评估为 Helm 模板，因此将能够引用其他 `values.yaml` 变量，例如 `{{ .Values.ingress.hosts[0] }}` 将解析为您的入口外部域。

整个 `superset_config.py` 将作为秘密安装，因此直接传递敏感参数是安全的……但是为此使用秘密环境变量可能更具可读性。

可以通过运行 `helm upgrade --install --values my-values.yaml --set-file configOverrides.oauth=set_oauth.py` 来提供完整的 python 文件

#### 环境变量

如果它们敏感，可以使用 `extraEnv` 或 `extraSecretEnv` 作为键/值传递。然后可以使用例如从 `superset_config.py` 引用它们 `os.environ.get("VAR")`。

```yaml
extraEnv:
  SMTP_HOST: smtp.gmail.com
  SMTP_USER: user@gmail.com
  SMTP_PORT: "587"
  SMTP_MAIL_FROM: user@gmail.com

extraSecretEnv:
  SMTP_PASSWORD: xxxx

configOverrides:
  smtp: |
    import ast
    SMTP_HOST = os.getenv("SMTP_HOST","localhost")
    SMTP_STARTTLS = ast.literal_eval(os.getenv("SMTP_STARTTLS", "True"))
    SMTP_SSL = ast.literal_eval(os.getenv("SMTP_SSL", "False"))
    SMTP_USER = os.getenv("SMTP_USER","superset")
    SMTP_PORT = os.getenv("SMTP_PORT",25)
    SMTP_PASSWORD = os.getenv("SMTP_PASSWORD","superset")
```

#### 系统包

如果需要新的系统包，可以通过覆盖容器的 `command` 在应用程序启动之前安装它们，例如：

```yaml
supersetWorker:
  command:
    - /bin/sh
    - -c
    - |
      apt update
      apt install -y somepackage
      apt autoremove -yqq --purge
      apt clean

      # Run celery worker
      . {{ .Values.configMountPath }}/superset_bootstrap.sh; celery --app=superset.tasks.celery_app:app worker
```

#### 数据源

可以通过在 `extraConfigs` 中提供键/值yaml定义来自动声明数据源定义：

```yaml
extraConfigs:
  import_datasources.yaml: |
    databases:
    - allow_file_upload: true
      allow_ctas: true
      allow_cvas: true
      database_name: example-db
      extra: "{\r\n    \"metadata_params\": {},\r\n    \"engine_params\": {},\r\n    \"\
        metadata_cache_timeout\": {},\r\n    \"schemas_allowed_for_file_upload\": []\r\n\
        }"
      sqlalchemy_uri: example://example-db.local
      tables: []
```

这些也将作为秘密安装，并且可以包含敏感参数。

### 配置举例

#### 设置 OAuth

> OAuth 设置需要安装 [authlib](https://authlib.org/) Python 库。这可以通过更新 `bootstrapScript` 使用 `pip` 来完成。有关详细信息，请参阅[依赖项](#dependency) 部分。

```yaml
extraEnv:
  AUTH_DOMAIN: example.com

extraSecretEnv:
  GOOGLE_KEY: xxxxxxxxxxxx-xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx.apps.googleusercontent.com
  GOOGLE_SECRET: xxxxxxxxxxxxxxxxxxxxxxxx

configOverrides:
  enable_oauth: |
    # This will make sure the redirect_uri is properly computed, even with SSL offloading
    ENABLE_PROXY_FIX = True

    from flask_appbuilder.security.manager import AUTH_OAUTH
    AUTH_TYPE = AUTH_OAUTH
    OAUTH_PROVIDERS = [
        {
            "name": "google",
            "icon": "fa-google",
            "token_key": "access_token",
            "remote_app": {
                "client_id": os.getenv("GOOGLE_KEY"),
                "client_secret": os.getenv("GOOGLE_SECRET"),
                "api_base_url": "https://www.googleapis.com/oauth2/v2/",
                "client_kwargs": {"scope": "email profile"},
                "request_token_url": None,
                "access_token_url": "https://accounts.google.com/o/oauth2/token",
                "authorize_url": "https://accounts.google.com/o/oauth2/auth",
                "authorize_params": {"hd": os.getenv("AUTH_DOMAIN", "")}
            },
        }
    ]

    # Map Authlib roles to superset roles
    AUTH_ROLE_ADMIN = 'Admin'
    AUTH_ROLE_PUBLIC = 'Public'

    # Will allow user self registration, allowing to create Flask users from Authorized User
    AUTH_USER_REGISTRATION = True

    # The default user self registration role
    AUTH_USER_REGISTRATION_ROLE = "Admin"
```

#### 启用警报和报告

为此，根据[警报和报告文档]($AlertsAndReports)，您将需要：

##### 在 Celery Worker 中安装受支持的网络驱动程序

这可以通过使用预安装了 Webdriver 的自定义映像来完成，也可以通过覆盖 `command` 在启动时进行安装来完成。这是 `chromedriver` 的一个工作示例：

```yaml
supersetWorker:
  command:
    - /bin/sh
    - -c
    - |
      # Install chrome webdriver
      # See https://github.com/apache/superset/blob/4fa3b6c7185629b87c27fc2c0e5435d458f7b73d/docs/src/pages/docs/installation/email_reports.mdx
      apt-get update
      apt-get install -y wget
      wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
      apt-get install -y --no-install-recommends ./google-chrome-stable_current_amd64.deb
      wget https://chromedriver.storage.googleapis.com/88.0.4324.96/chromedriver_linux64.zip
      apt-get install -y zip
      unzip chromedriver_linux64.zip
      chmod +x chromedriver
      mv chromedriver /usr/bin
      apt-get autoremove -yqq --purge
      apt-get clean
      rm -f google-chrome-stable_current_amd64.deb chromedriver_linux64.zip

      # Run
      . {{ .Values.configMountPath }}/superset_bootstrap.sh; celery --app=superset.tasks.celery_app:app worker
```

##### 运行 Celery beat

此 Pod 将触发警报和报告 UI 部分中配置的计划任务：

```yaml
supersetCeleryBeat:
  enabled: true
```

##### 配置适当的 Celery 作业和 SMTP/Slack 设置

```yaml
extraEnv:
  SMTP_HOST: smtp.gmail.com
  SMTP_USER: user@gmail.com
  SMTP_PORT: "587"
  SMTP_MAIL_FROM: user@gmail.com

extraSecretEnv:
  SLACK_API_TOKEN: xoxb-xxxx-yyyy
  SMTP_PASSWORD: xxxx-yyyy

configOverrides:
  feature_flags: |
    import ast

    FEATURE_FLAGS = {
        "ALERT_REPORTS": True
    }

    SMTP_HOST = os.getenv("SMTP_HOST","localhost")
    SMTP_STARTTLS = ast.literal_eval(os.getenv("SMTP_STARTTLS", "True"))
    SMTP_SSL = ast.literal_eval(os.getenv("SMTP_SSL", "False"))
    SMTP_USER = os.getenv("SMTP_USER","superset")
    SMTP_PORT = os.getenv("SMTP_PORT",25)
    SMTP_PASSWORD = os.getenv("SMTP_PASSWORD","superset")
    SMTP_MAIL_FROM = os.getenv("SMTP_MAIL_FROM","superset@superset.com")

    SLACK_API_TOKEN = os.getenv("SLACK_API_TOKEN",None)
  celery_conf: |
    from celery.schedules import crontab

    class CeleryConfig:
      broker_url = f"redis://{env('REDIS_HOST')}:{env('REDIS_PORT')}/0"
      imports = (
          "superset.sql_lab",
          "superset.tasks.cache",
          "superset.tasks.scheduler",
      )
      result_backend = f"redis://{env('REDIS_HOST')}:{env('REDIS_PORT')}/0"
      task_annotations = {
          "sql_lab.get_sql_results": {
              "rate_limit": "100/s",
          },
      }
      beat_schedule = {
          "reports.scheduler": {
              "task": "reports.scheduler",
              "schedule": crontab(minute="*", hour="*"),
          },
          "reports.prune_log": {
              "task": "reports.prune_log",
              'schedule': crontab(minute=0, hour=0),
          },
          'cache-warmup-hourly': {
              "task": "cache-warmup",
              "schedule": crontab(minute="*/30", hour="*"),
              "kwargs": {
                  "strategy_name": "top_n_dashboards",
                  "top_n": 10,
                  "since": "7 days ago",
              },
          }
      }

    CELERY_CONFIG = CeleryConfig
  reports: |
    EMAIL_PAGE_RENDER_WAIT = 60
    WEBDRIVER_BASEURL = "http://{{ template "superset.fullname" . }}:{{ .Values.service.port }}/"
    WEBDRIVER_BASEURL_USER_FRIENDLY = "https://www.example.com/"
    WEBDRIVER_TYPE= "chrome"
    WEBDRIVER_OPTION_ARGS = [
        "--force-device-scale-factor=2.0",
        "--high-dpi-support=2.0",
        "--headless",
        "--disable-gpu",
        "--disable-dev-shm-usage",
        # This is required because our process runs as root (in order to install pip packages)
        "--no-sandbox",
        "--disable-setuid-sandbox",
        "--disable-extensions",
    ]
```

#### 加载示例数据和仪表板

如果您正在尝试 Superset 并希望探索一些数据和仪表板，您可以通过创建 `my_values.yaml` 并按照上面 **运行的 **配置您的设置覆盖** 步骤中所述进行部署来加载一些示例** 部分。要加载示例，请将以下内容添加到 `my_values.yaml 文件中：

```yaml
init:
  loadExamples: true
```
