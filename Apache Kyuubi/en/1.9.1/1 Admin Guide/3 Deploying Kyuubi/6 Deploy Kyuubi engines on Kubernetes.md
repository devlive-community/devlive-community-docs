[TOC]


## Requirements

When you want to run Kyuubi's Spark SQL engine on Kubernetes, you'd better have cognition upon the following things.

* Read about [Running Spark on Kubernetes](https://spark.apache.org/docs/latest/running-on-kubernetes.html)
* An active Kubernetes cluster
* [kubectl](https://kubernetes.io/docs/reference/kubectl/overview/)
* [kubeconfig](https://kubernetes.io/docs/concepts/configuration/organize-cluster-access-kubeconfig/) of the target cluster

## Configurations

### Master

Spark on Kubernetes configures `spark.master` by using a special format.

`spark.master=k8s://https://<k8s-apiserver-host>:<k8s-apiserver-port>`

You can use cmd `kubectl cluster-info` to get api-server host and port.

### Deploy Mode

One of the main advantages of the Kyuubi server compared to other interactive Spark clients is that it supports cluster deploy mode.
It means that the Spark driver runs in an independent Pod which is isolated to Kyuubi server's pod.
It is highly recommended to run Spark on K8s in cluster mode.

The minimum required configurations are:

* spark.submit.deployMode cluster
* spark.kubernetes.file.upload.path (path on S3 or HDFS)
* spark.kubernetes.authenticate.driver.serviceAccountName ([viz ServiceAccount](#serviceaccount))

### Docker Image

Spark ships a `./bin/docker-image-tool.sh` script to build and publish the Docker images for running Spark applications on Kubernetes.

When deploying Kyuubi engines against a Kubernetes cluster, we need to set up the docker images in the Docker registry first.

Example usage is:

```shell
./bin/docker-image-tool.sh -r <repo> -t <tag> build
./bin/docker-image-tool.sh -r <repo> -t <tag> push
# To build docker image with specify openJdk 
./bin/docker-image-tool.sh -r <repo> -t <tag> -b java_image_tag=<openjdk:${java_image_tag}> build
# To build additional PySpark docker image
./bin/docker-image-tool.sh -r <repo> -t <tag> -p ./kubernetes/dockerfiles/spark/bindings/python/Dockerfile build
# To build additional SparkR docker image
./bin/docker-image-tool.sh -r <repo> -t <tag> -R ./kubernetes/dockerfiles/spark/bindings/R/Dockerfile build
```

### Test Cluster

You can use the shell code to test your cluster whether it is normal or not.

```shell
$SPARK_HOME/bin/spark-submit \
 --master k8s://https://<k8s-apiserver-host>:<k8s-apiserver-port> \
 --class org.apache.spark.examples.SparkPi \
 --conf spark.executor.instances=5 \
 --conf spark.dynamicAllocation.enabled=false \
 --conf spark.shuffle.service.enabled=false \
 --conf spark.kubernetes.container.image=<spark-image> \
 local://<path_to_examples.jar>
```

When running shell, you can use cmd `kubectl describe pod <podName>` to check if the information meets expectations.

### ServiceAccount

When use client mode to submit application, Spark driver uses the [kubeconfig](https://kubernetes.io/docs/concepts/configuration/organize-cluster-access-kubeconfig/) to access Kubernetes API server to create and watch executor pods.

When use cluster mode to submit application, Spark driver pod uses [ServiceAccount](https://kubernetes.io/docs/concepts/security/service-accounts/) to access Kubernetes API server to create and watch executor pods.

In both cases, you need to figure out whether you have the permissions under the corresponding namespace. You can use following commands to create ServiceAccount.

```shell
# create ServiceAccount
kubectl create serviceaccount spark -n <namespace>
# binding role
kubectl create clusterrolebinding spark-role --clusterrole=edit --serviceaccount=<namespace>:spark --namespace=<namespace>
```

### Volumes

As it known to us all, Kubernetes can use configurations to mount volumes into driver and executor pods.

* hostPath: mounts a file or directory from the host node’s filesystem into a pod.
* emptyDir: an initially empty volume created when a pod is assigned to a node.
* nfs: mounts an existing NFS(Network File System) into a pod.
* persistentVolumeClaim: mounts a PersistentVolume into a pod.

Note: Please
see [the Security section](https://spark.apache.org/docs/latest/running-on-kubernetes.html#security) for security issues related to volume mounts.

```
spark.kubernetes.driver.volumes.<type>.<name>.options.path=<dist_path>
spark.kubernetes.driver.volumes.<type>.<name>.mount.path=<container_path>

spark.kubernetes.executor.volumes.<type>.<name>.options.path=<dist_path>
spark.kubernetes.executor.volumes.<type>.<name>.mount.path=<container_path>
```

Read [Using Kubernetes Volumes](https://spark.apache.org/docs/latest/running-on-kubernetes.html#using-kubernetes-volumes) for more about volumes.

### PodTemplateFile

Kubernetes allows defining pods from template files. Spark users can similarly use template files to define the driver or executor pod configurations that Spark configurations do not support.

To do so, specify the Spark properties `spark.kubernetes.driver.podTemplateFile` and `spark.kubernetes.executor.podTemplateFile` to point to local files accessible to the `spark-submit` process.

### Other

You can read Spark's official documentation for [Running on Kubernetes](https://spark.apache.org/docs/latest/running-on-kubernetes.html) for more information.

