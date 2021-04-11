---
icon: docker
date: '2020-10-14T11:23:54.000Z'
categories:
  - Monitor
tags:
  - Zabbix
---

# Zabbix 基于 Docker 安装

## 1.启动 MySQL

```text
docker run --name mysql-server -t \
-v /etc/localtime:/etc/localtime:ro \
-e MYSQL_DATABASE="zabbix" \
-e MYSQL_USER="zabbix" \
-e MYSQL_PASSWORD="hadoop" \
-e MYSQL_ROOT_PASSWORD="hadoop" \
-d mysql:5.7 \
--character-set-server=utf8 --collation-server=utf8_bin
```

## 2.启动 Java Agent

```text
docker run --name zabbix-java-gateway -t \
-v /etc/localtime:/etc/localtime:ro \
-d zabbix/zabbix-java-gateway:latest
```

## 3.启动 Zabbix Server

```text
docker run --name zabbix-server-mysql -t \
  -e DB_SERVER_HOST="mysql-server" \
  -e MYSQL_DATABASE="zabbix" \
  -e MYSQL_USER="zabbix" \
  -e MYSQL_PASSWORD="hadoop" \
  -e MYSQL_ROOT_PASSWORD="hadoop" \
  -e ZBX_JAVAGATEWAY="zabbix-java-gateway" \
  --link mysql-server:mysql \
  --link zabbix-java-gateway:zabbix-java-gateway \
  -p 10051:10051 \
  -v /etc/localtime:/etc/localtime:ro \
  -d zabbix/zabbix-server-mysql:latest
```

## 4.安装 Nginx

```text
docker run --name zabbix-web-nginx-mysql -t \
-e DB_SERVER_HOST="mysql-server" \
-e MYSQL_DATABASE="zabbix" \
-e MYSQL_USER="zabbix" \
-e MYSQL_PASSWORD="hadoop" \
-e MYSQL_ROOT_PASSWORD="hadoop" \
--link mysql-server:mysql \
--link zabbix-server-mysql:zabbix-server \
-p 80:8080 \
-v /etc/localtime:/etc/localtime:ro \
-d zabbix/zabbix-web-nginx-mysql:latest
```

> 这时候访问IP：80应该能打开 Zabbix 的登录页面，账号密码分别是 Admin:zabbix

