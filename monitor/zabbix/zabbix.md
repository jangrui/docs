---
icon: monitor
time: 2019-1-12
categories:
  - Monitor
tags:
  - Zabbix
copyrightText: >-
  本教程采用<a href="https://creativecommons.org/licenses/by-sa/3.0/deed.zh">知识共享
  署名-相同方式共享 3.0协议</a>
---

# Zabbix 是什么

Zabbix 由 Alexei Vladishev 创建，目前由其成立的公司—— Zabbix SIA 积极的持续开发更新维护， 并为用户提供技术支持服务

## 企业级分布式开源监控解决方案

Zabbix 是一个基于WEB界面的提供分布式系统监视以及网络监视功能的企业级的开源解决方案。

* agent端：主机通过安装agent方式采集数据。
* server端：通过收集agent发送的数据，写入数据库（MySQL，ORACLE等），再通过php+apache在web前端展示.

## 监控功能

1. 主机的性能监控、网络设备性能监控、数据库性能监控、多种告警方式、详细的报表图表绘制
2. 监控主机zabbix有专用的agent，可以监控Linux，Windows，FreeBSD等 。
3. 监控网络设备zabbix通过SNMP，ssh\(不多用\)
4. 可监控对象：
   * 设备：服务器，路由器，交换机
   * 软件：OS，网络，应用程序
   * 主机性能指标监控
   * 故障监控： 宕机，服务不可用，主机不可达

## 工作原理

Zabbix Agent 需要安装到被监控的主机上，它负责定期收集各项数据，并发送到 Zabbix Server端，Zabbix Server 将数据存储到数据库中，Zabbix Agent 根据数据在前端进行展现和绘图。

这里 Agent 收集数据分为主动和被动两种模式：

* 主动：Agent 请求 Server 获取主动的监控项列表，并主动将监控项内需要检测的数据提交给 Server/Proxy
* 被动：Server 向 Agent 请求获取监控项的数据，Agent 返回数据。

## Zabbix 的组件

1. Zabbix Web GUI：提供Web界面
2. Zabbix Database：提供数据存储功能，专用于存储配置信息，以及采集到的数据
3. Zabbix Server：接收Agent采集数据的核心组件。
4. Zabbix Agent：部署在被监控主机上，用于采集本地数据。
5. Zabbix Proxy：当被监控节点较多时，用于减轻Server压力的组件，也用于分布式监控系统。由Proxy接收数据后统一发送至Server。

## Zabbix 监控环境中基本概念

1. 主机（host）：要监控的网络设备，可由IP或DNS名称指定；
2. 主机组（host group）：主机的逻辑容器，可以包含主机和模板，但同一个组织内的主机和模板不能互相链接；主机组通常在给用户或用户组指派监控权限时使用；
3. 监控项（item）：一个特定监控指标的相关的数据；这些数据来自于被监控对象；item是zabbix进行数据收集的核心，相对某个监控对象，每个item都由"key"标识；
4. 触发器（trigger）：一个表达式，用于评估某监控对象的特定item内接收到的数据是否在合理范围内，也就是阈值；接收的数据量大于阈值时，触发器状态将从"OK"转变为"Problem"，当数据再次恢复到合理范围，又转变为"OK"；
5. 事件（event）：触发一个值得关注的事情，比如触发器状态转变，新的agent或重新上线的agent的自动注册等；
6. 动作（action）：指对于特定事件事先定义的处理方法，如发送通知，何时执行操作；
7. 报警升级（escalation）：发送警报或者执行远程命令的自定义方案，如每隔5分钟发送一次警报，共发送5次等；
8. 媒介（media）：发送通知的手段或者通道，如Email、Jabber或者SMS等；
9. 通知（notification）：通过选定的媒介向用户发送的有关某事件的信息；
10. 远程命令（remote command）：预定义的命令，可在被监控主机处于某特定条件下时自动执行；
11. 模板（template）：用于快速定义被监控主机的预设条目集合，通常包含了item、trigger、graph、screen、application以及low-level discovery rule；模板可以直接链接至某个主机；
12. 应用（application）：一组item的集合；
13. web场景（web scennario）：用于检测web站点可用性的一个活多个HTTP请求；
14. 前端（frontend）：Zabbix的web接口；

## Zabbix 报警级别

* 未分类
* 信息
* 警告
* 一般严重
* 严重
* 灾难

