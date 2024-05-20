[TOC]

> We recommend that you back up database and configuration files before upgrading. Generally, we guarantee that the upgrade does not affect the existing data.

> To back up data means that you have the option to roll back even if the upgrade fails, or you do not want the advanced version.

> Docker Compose

If you use docker-compose to install answer, it is very easy to upgrade.

```bash
docker-compose pull
docker-compose down
docker-compose up -d
```

> Docker

If you are using docker to install answer, the upgrade steps are as follows.

```bash
docker pull apache/answer:latest
docker stop answer
docker rm answer
docker run -d -p 9080:80 -v answer-data:/data --name answer apache/answer:latest
```

> Binary

If you are using a binary installation of answer, the upgrade steps are as follows.

1. Download the [latest binary version](https://github.com/apache/incubator-answer/releases) for your system.
2. Stop old version
3. Execute the upgrade command `./answer upgrade -C ./answer-data/`
4. Run the latest version `./answer run -C ./answer-data/`

> When there are other unexpected cases such as upgrade exceptions, we provide a command to manually force the upgrade of Answer. `answer upgrade -f v1.1.0` Executing this command will force upgrade from the specified version, even if your Answer is already up to date. If you encounter an upgrade exception, you can try to execute this command or pull the latest docker image again and execute this command inside the container.
