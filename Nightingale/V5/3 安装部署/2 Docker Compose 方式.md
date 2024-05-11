[TOC]

使用Docker Compose一键启动夜莺，快速尝试。更多Docker Compose相关知识请参考[Docker官网](https://docs.docker.com/compose/) [操作演示](http://download.flashcat.cloud/n9e-compose.gif)

```
$ git clone https://gitlink.org.cn/ccfos/nightingale.git
$ cd nightingale/docker
# docker compose V2版本执行 docker compose up -d (https://docs.docker.com/compose/#compose-v2-and-the-new-docker-compose-command)
$ docker-compose up -d
Creating network "docker_nightingale" with driver "bridge"
Creating mysql      ... done
Creating redis      ... done
Creating prometheus ... done
Creating ibex       ... done
Creating agentd     ... done
Creating nwebapi    ... done
Creating nserver    ... done
Creating telegraf   ... done
# docker compose V2版本执行 docker compose ps (https://docs.docker.com/compose/#compose-v2-and-the-new-docker-compose-command)
$ docker-compose ps
   Name                 Command               State                                   Ports
----------------------------------------------------------------------------------------------------------------------------
agentd       /app/ibex agentd                 Up      10090/tcp, 20090/tcp
ibex         /app/ibex server                 Up      0.0.0.0:10090->10090/tcp, 0.0.0.0:20090->20090/tcp
mysql        docker-entrypoint.sh mysqld      Up      0.0.0.0:3306->3306/tcp, 33060/tcp
nserver      /app/n9e server                  Up      18000/tcp, 0.0.0.0:19000->19000/tcp
nwebapi      /app/n9e webapi                  Up      0.0.0.0:18000->18000/tcp, 19000/tcp
prometheus   /bin/prometheus --config.f ...   Up      0.0.0.0:9090->9090/tcp
redis        docker-entrypoint.sh redis ...   Up      0.0.0.0:6379->6379/tcp
telegraf     /entrypoint.sh telegraf          Up      0.0.0.0:8092->8092/udp, 0.0.0.0:8094->8094/tcp, 0.0.0.0:8125->8125/udp
```

> 💡启动成功之后，建议把 initsql 目录下的内容挪走，这样下次重启的时候，DB 就不会重新初始化了。否则下次启动 mysql 还是会自动执行 initsql 下面的 sql 文件导致 DB 重新初始化，页面上创建的规则、大盘等都会丢失。Docker Compose 这种部署方式，只是用于简单测试，不推荐在生产环境使用，当然了，如果您是 Docker Compose 专家，另当别论"

服务启动之后，浏览器访问nwebapi的端口，即18000，默认用户是`root`，密码是`root.2020`
