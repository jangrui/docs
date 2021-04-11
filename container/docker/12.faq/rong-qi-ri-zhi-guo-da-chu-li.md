---
title: 容器日志过大处理
icon: logs
date: '2020-11-26T15:18:28.000Z'
categories:
  - 容器
tags:
  - docker
---

# 容器日志过大处理

## 1.临时解决（治标）

* 脚本内容如下：

```text
#!/bin/sh 
# chmod +x dk_log_clean.sh
# ./dk_log_clean.sh
echo -e "\033[44;37m 本机docker容器日志大小如下 \033[0m"

logs=$(find /var/lib/docker/containers/ -name *-json.log*)

for log in $logs
        do
            ls -sh $log
        done

echo -e "\033[44;37m 开始清理docker容器日志 \033[0m"

for log in $logs
        do
                cat /dev/null > $log
        done

echo -e "\033[44;37m 清理完毕 \033[0m"  

for log in $logs
        do
            ls -sh $log
        done
```

![&#x811A;&#x672C;&#x6267;&#x884C;&#x6548;&#x679C;](https://cdn.jsdelivr.net/gh/summerking1/image@main/84.png)

## 2.根本解决（治本）

找时间系统空闲时，删除容器重新创建

docker stop 【容器】 docker rm 【容器】

创建docker容器时的参数加上：

`--log-opt max-size=10m --log-opt max-file=3`

