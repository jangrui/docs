---
title: IPv4 转发已禁用
icon: ip
date: '2020-11-30T17:42:39.000Z'
categories:
  - 容器
tags:
  - Docker
---

# IPv4转发已禁用

## 问题

Docker 容器启动报`WARNING: IPv4 forwarding is disabled. Networking will not work`

```text
docker run -d -p 9100:9100 -v "/proc:/host/proc:ro" -v "/sys:/host/sys:ro" -v "/:/rootfs:ro" prom/node-exporter
WARNING: IPv4 forwarding is disabled. Networking will not work.
86c35154262b332d1f2f3425fde25840f43fdc3a1cef66a2010608af4b6ce736
```

## 解决

添加`net.ipv4.ip_forward=1`重启网络即可

```text
sudo sed -i '/net.ipv4.ip_forward/d' /etc/sysctl.conf
sudo echo "net.ipv4.ip_forward=1" >> /etc/sysctl.conf
sudo sysctl -p
```

