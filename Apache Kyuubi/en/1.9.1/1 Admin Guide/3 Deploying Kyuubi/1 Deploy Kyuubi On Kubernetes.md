[TOC]

## Requirements

To deploy Kyuubi on Kubernetes, you'd better have cognition upon the following things.

* Use Kyuubi official docker image or build Kyuubi docker image
* An active Kubernetes cluster
* Reading About [Deploy Kyuubi engines on Kubernetes]($Deploy-Kyuubi-Engines-On-Kubernetes)
* [Kubectl](https://kubernetes.io/docs/reference/kubectl/overview/)
* KubeConfig of the target cluster

## Kyuubi Official Docker Image

You can find the official docker image at [Docker Hub - apache/kyuubi](https://registry.hub.docker.com/r/apache/kyuubi).

## Build Kyuubi Docker Image

You can build custom Docker images from the `${KYUUBI_HOME}/bin/docker-image-tool.sh` contained in the binary package.

Examples:

```shell
  - Build and push image with tag "v1.8.1" to docker.io/myrepo
    $0 -r docker.io/myrepo -t v1.8.1 build
    $0 -r docker.io/myrepo -t v1.8.1 push

  - Build and push with tag "v1.8.1" and Spark-3.5.1 as base image to docker.io/myrepo
    $0 -r docker.io/myrepo -t v1.8.1 -b BASE_IMAGE=repo/spark:3.5.1 build
    $0 -r docker.io/myrepo -t v1.8.1 push

  - Build and push for multiple archs to docker.io/myrepo
    $0 -r docker.io/myrepo -t v1.8.1 -X build

  - Build with Spark placed "/path/spark"
    $0 -s /path/spark build
    
  - Build with Spark Image myrepo/spark:3.4.2
    $0 -S /opt/spark -b BASE_IMAGE=myrepo/spark:3.4.2 build
```

`${KYUUBI_HOME}/bin/docker-image-tool.sh` use `Kyuubi Version` as default docker tag and always build `${repo}/kyuubi:${tag}` image.

The script can also help build external Spark into a Kyuubi image that acts as a client for submitting tasks by `-s ${SPARK_HOME}`.

Of course, if you have an image that contains the Spark binary package, you don't have to copy Spark locally. Make your Spark Image as BASE_IMAGE by using the `-S ${SPARK_HOME_IN_DOCKER}` and `-b BASE_IMAGE=${SPARK_IMAGE}` arguments.

You can use `${KYUUBI_HOME}/bin/docker-image-tool.sh -h` for more parameters.

## Deploy

It's recommended to [use Helm Chart to run Kyuubi on Kubernetes]($Getting-Started-With-Helm).

### [Optional] ServiceAccount

According to [Kubernetes RBAC](https://kubernetes.io/docs/reference/access-authn-authz/rbac/), you need to grant to Kyuubi server the corresponding kubernetes privileges for `created/list/delete` engine pods in Kubernetes.

You should create your ServiceAccount(or reuse account with the appropriate privileges) and set your ServiceAccountName for Kyuubi pod, which you can find template in `${KYUUBI_HOME}/docker/kyuubi-deployment.yaml` or `${KYUUBI_HOME}/docker/kyuubi-pod.yaml`.

For example, you can create ServiceAccount by following command:

```shell
kubectl create serviceAccount kyuubi -n <your namespace>
kubectl create rolebinding kyuubi-role --role=edit --serviceAccount=<your namespace>:kyuubi --namespace=<your namespace>
```

See more related details in [Using RBAC Authorization](https://kubernetes.io/docs/reference/access-authn-authz/rbac/) and [Configure Service Accounts for Pods](https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/).

## Config

You can configure Kyuubi the old-fashioned way by placing `kyuubi-defaults.conf` inside the image. Kyuubi does not recommend using this way on Kubernetes.

Kyuubi provide `${KYUUBI_HOME}/docker/kyuubi-configmap.yaml` to build ConfigMap for Kyuubi.

You can find out how to use it in the comments inside the above file.

If you want to know Kyuubi engine on Kubernetes configurations, you can refer to [Deploy Kyuubi engines on Kubernetes]($Deploy-Kyuubi-Engines-On-Kubernetes)

## Connect

If you do not use Service or HostNetwork to get the IP address of the node where Kyuubi deployed.
You should connect like:

```shell
kubectl exec -it kyuubi-example -- /bin/bash
${KYUUBI_HOME}/bin/beeline -u 'jdbc:kyuubi://localhost:10009'
```

Or you can submit tasks directly through local beeline:

```shell
${KYUUBI_HOME}/bin/beeline -u 'jdbc:kyuubi://${hostname}:${port}'
```

As using service nodePort, port means nodePort and hostname means any hostname of kubernetes node.

As using HostNetwork, port means kyuubi containerPort and hostname means hostname of node where Kyuubi deployed.

## TODO

Kyuubi will provide other connection methods in the future, like `Ingress`, `Load Balance`.
