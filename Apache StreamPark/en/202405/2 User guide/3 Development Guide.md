[TOC]

### Environment Requirements

| Item | Version | Required | Other |
| --- | --- | --- | --- |
| OS | Linux |  | Supports Windows, recommended to use Mac/Linux. |
| IDE | Intellij IDEA |  | Recommended to use Intellij IDEA |
| JAVA | 1.8 + |  |  |
| Scala | 2.12.x |  | install scala-plugin in Intellij IDEA |
| Nodejs | 16.14.x ~ 18 |  | https://nodejs.org |
| pnpm | 7.11.2 |  | npm install -g pnpm |
| Flink | 1.12.0 + |  | Flink >= 1.12, just download and unpack it. |
| MySQL | 5.6 + |  |  |
| Hadoop | 2 + |  | Optional, If on yarn, hadoop envs is required. |

### Clone the Source Code

```bash
git clone https://github.com/apache/incubator-streampark.git
```

### Build the Project

```bash
cd incubator-streampark/
./build.sh
```

### Open the Project

Here, we are using `idea` to open the project.

```bash
open -a /Applications/IntelliJ\ IDEA\ CE.app/ ./
```

### Extract the Package

```bash
cd ./dist
tar -zxvf apache-streampark-2.2.0-incubating-bin.tar.gz
```

### Copy the Path

Copy the path of the extracted directory, for example: `${workspace}/incubator-streampark/dist/apache-streampark-2.2.0-incubating-bin`

### Start the Backend Service

Navigate to `streampark-console/streampark-console-service/src/main/java/org/apache/streampark/console/StreamParkConsoleBootstrap.java`

Modify the launch configuration

![Streampark Modify Run Configuration](https://streampark.apache.org/doc/image/streampark_modify_run_configuration.jpg)

Check `Add VM options` and `Add dependencies with "provided" scope to classpath`, and input the parameter `-Dapp.home=$path`, where `$path` is the path we just copied.

```bash
-Dapp.home=${workspace}/incubator-streampark/dist/apache-streampark-2.2.0-incubating-bin
```

![Streampark Run Config](https://streampark.apache.org/doc/image/streampark_run_config.jpeg)

Then, start the backend service.

### Start the Frontend Service

```bash
cd ../streampark-console/streampark-console-webapp
pnpm serve
```

![Streampark Frontend Running](https://streampark.apache.org/doc/image/streampark_frontend_running.png)

Visit `http://localhost:10001/`, enter the username `admin` and the password `streampark`, then choose a `team` to proceed.

![Streampark Select Team](https://streampark.apache.org/doc/image/streampark_select_team.jpg)

### Demonstrate Debugging Code

1.Start the project in debug mode in Idea

2.Add breakpoints in the link/app/list of the Application Controller

![Streampark Project Build](https://streampark.apache.org/doc/image/streampark_debug_build.png)

3.Entering your account password to log in to streampark and selecting team will trigger a breakpoint

![Streampark Project Build](https://streampark.apache.org/doc/image/streampark_debugging.png)
