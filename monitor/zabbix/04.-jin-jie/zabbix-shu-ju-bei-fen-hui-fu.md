---
icon: backup
date: '2020-10-14T14:21:01.000Z'
categories:
  - Monitor
tags:
  - Zabbix
---

# Zabbix 数据备份恢复

## 基于容器

### 1.进入docker容器

```text
./mysqldump -uroot -pXXXXX zabbix  > zabbix.sql
```

### 2.复制出来

```text
docker cp 80a55ac6456d:/usr/bin/zabbix.sql /home/
```

### 3.恢复

```text
docker cp zabbix.sql 671f0f909ab6:/etc/
root@671f0f909ab6:/etc# mysql -uroot -pXXXX zabbix <zabbix.sql
```

