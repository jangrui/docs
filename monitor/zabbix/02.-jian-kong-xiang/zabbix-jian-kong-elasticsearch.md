---
icon: elasticsearch
date: '2020-10-14T13:52:29.000Z'
categories:
  - Monitor
tags:
  - Zabbix
---

# Zabbix 监控 Elasticsearch

1. 创建es服务触发器

![&#x521B;&#x5EFA;es&#x670D;&#x52A1;&#x89E6;&#x53D1;&#x5668;](https://cdn.jsdelivr.net/gh/summerking1/image@main/31.png)

> 作用：diff\(\)函数主要是用来对比监控项前后两个值是否发生了变化，如果发生变化就会触发告警,返回值为1表示最近的值与之前的值不同，0为其他情况

1. 创建动作并添加条件 ![&#x521B;&#x5EFA;&#x52A8;&#x4F5C;&#x5E76;&#x6DFB;&#x52A0;&#x6761;&#x4EF6;](https://cdn.jsdelivr.net/gh/summerking1/image@main/32.png)
2. 添加操作细节 ![&#x6DFB;&#x52A0;&#x64CD;&#x4F5C;&#x7EC6;&#x8282;](https://cdn.jsdelivr.net/gh/summerking1/image@main/33.png)

