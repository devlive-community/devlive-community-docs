[TOC]

A guide on how to uninstall the self-hosted version of Coolify from your server.

To uninstall the self-hosted version of Coolify from your server, follow these steps:

1. Stop and Remove Containers:

Use the following command to stop the Coolify containers with a timeout of 0, ensuring they stop immediately, and then remove them:

```bash
sudo docker stop -t 0 coolify coolify-realtime coolify-db coolify-redis coolify-proxy
sudo docker rm coolify coolify-realtime coolify-db coolify-redis coolify-proxy
```

2. Remove Docker Volumes:

Execute the command below to remove the Docker volumes associated with Coolify:

```bash
sudo docker volume rm coolify-db coolify-redis
```

3. Remove Docker Network:

Remove the custom Docker network named “coolify”:

```bash
sudo docker network rm coolify
```

4. Delete Coolify Data Directory:

Delete the directory where Coolify data is stored:

```bash
sudo rm -rf /data/coolify
```

5. Remove Docker Images:

Use the following commands to remove the Docker images used by Coolify:

```bash
sudo docker rmi ghcr.io/coollabsio/coolify:latest
sudo docker rmi ghcr.io/coollabsio/coolify-helper:latest
sudo docker rmi quay.io/soketi/soketi:1.6-16-alpine
sudo docker rmi postgres:15-alpine
sudo docker rmi redis:alpine
sudo docker rmi traefik:v2.10
```

After completing these steps, Coolify will be uninstalled from your server.
