---
icon: container
date: '2020-10-14T11:53:30.000Z'
categories:
  - Monitor
tags:
  - Zabbix
---

# Zabbix 监控容器

> 实现效果:

![&#x5B9E;&#x73B0;&#x6548;&#x679C;](https://cdn.jsdelivr.net/gh/summerking1/image@main/21.png)

1. 编辑 conf 配置键值

```text
[root@elx summer]# cd /etc/zabbix/zabbix_agentd.d
[root@elx zabbix_agentd.d]# ll
total 8
-rwxr-xr-x 1 zabbix zabbix  118 Sep 28 01:02 userparameter_find_container.conf
-rwxr-xr-x 1 zabbix zabbix 1081 Sep 27 19:51 userparameter_mysql.conf
[root@elx zabbix_agentd.d]# cat userparameter_find_container.conf 
UserParameter=docker.discovery,/home/summer/docker.py
UserParameter=docker.[*],/home/summer/docker.py $1 $2
```

> 注意执行权限和所属用户组，注意重启 Agent

1. 导入模板后创建监控项
2. 键值：docker.\[eureka,ping\]

![&#x5BFC;&#x5165;&#x6A21;&#x677F;&#x540E;&#x521B;&#x5EFA;&#x76D1;&#x63A7;&#x9879;](https://cdn.jsdelivr.net/gh/summerking1/image@main/22.png)

zabbix\_docker模板.xml：

```markup
<?xml version="1.0" encoding="UTF-8"?>
<zabbix_export>
    <version>3.2</version>
    <date>2018-06-04T04:12:36Z</date>
    <groups>
        <group>
            <name>Templates</name>
        </group>
    </groups>
    <templates>
        <template>
            <template>docker-status</template>
            <name>docker-status</name>
            <description/>
            <groups>
                <group>
                    <name>Templates</name>
                </group>
            </groups>
            <applications>
                <application>
                    <name>docker_test</name>
                </application>
            </applications>
            <items/>
            <discovery_rules>
                <discovery_rule>
                    <name>docker.discovery</name>
                    <type>0</type>
                    <snmp_community/>
                    <snmp_oid/>
                    <key>docker.discovery</key>
                    <delay>60</delay>
                    <status>0</status>
                    <allowed_hosts/>
                    <snmpv3_contextname/>
                    <snmpv3_securityname/>
                    <snmpv3_securitylevel>0</snmpv3_securitylevel>
                    <snmpv3_authprotocol>0</snmpv3_authprotocol>
                    <snmpv3_authpassphrase/>
                    <snmpv3_privprotocol>0</snmpv3_privprotocol>
                    <snmpv3_privpassphrase/>
                    <delay_flex/>
                    <params/>
                    <ipmi_sensor/>
                    <authtype>0</authtype>
                    <username/>
                    <password/>
                    <publickey/>
                    <privatekey/>
                    <port/>
                    <filter>
                        <evaltype>0</evaltype>
                        <formula/>
                        <conditions>
                            <condition>
                                <macro>{#CONTAINERNAME}</macro>
                                <value>@ CONTAINER NAME</value>
                                <operator>8</operator>
                                <formulaid>A</formulaid>
                            </condition>
                        </conditions>
                    </filter>
                    <lifetime>30</lifetime>
                    <description/>
                    <item_prototypes>
                        <item_prototype>
                            <name>Container {#CONTAINERNAME} Diskio usage:</name>
                            <type>0</type>
                            <snmp_community/>
                            <multiplier>0</multiplier>
                            <snmp_oid/>
                            <key>docker.[{#CONTAINERNAME} ,BlockIO]</key>
                            <delay>60</delay>
                            <history>90</history>
                            <trends>0</trends>
                            <status>0</status>
                            <value_type>1</value_type>
                            <allowed_hosts/>
                            <units/>
                            <delta>0</delta>
                            <snmpv3_contextname/>
                            <snmpv3_securityname/>
                            <snmpv3_securitylevel>0</snmpv3_securitylevel>
                            <snmpv3_authprotocol>0</snmpv3_authprotocol>
                            <snmpv3_authpassphrase/>
                            <snmpv3_privprotocol>0</snmpv3_privprotocol>
                            <snmpv3_privpassphrase/>
                            <formula>1</formula>
                            <delay_flex/>
                            <params/>
                            <ipmi_sensor/>
                            <data_type>0</data_type>
                            <authtype>0</authtype>
                            <username/>
                            <password/>
                            <publickey/>
                            <privatekey/>
                            <port/>
                            <description/>
                            <inventory_link>0</inventory_link>
                            <applications>
                                <application>
                                    <name>docker_test</name>
                                </application>
                            </applications>
                            <valuemap/>
                            <logtimefmt/>
                            <application_prototypes/>
                        </item_prototype>
                        <item_prototype>
                            <name>Container{#CONTAINERNAME} CPU usage:</name>
                            <type>0</type>
                            <snmp_community/>
                            <multiplier>0</multiplier>
                            <snmp_oid/>
                            <key>docker.[{#CONTAINERNAME},CPUPerc]</key>
                            <delay>60</delay>
                            <history>90</history>
                            <trends>365</trends>
                            <status>0</status>
                            <value_type>0</value_type>
                            <allowed_hosts/>
                            <units>%</units>
                            <delta>0</delta>
                            <snmpv3_contextname/>
                            <snmpv3_securityname/>
                            <snmpv3_securitylevel>0</snmpv3_securitylevel>
                            <snmpv3_authprotocol>0</snmpv3_authprotocol>
                            <snmpv3_authpassphrase/>
                            <snmpv3_privprotocol>0</snmpv3_privprotocol>
                            <snmpv3_privpassphrase/>
                            <formula>1</formula>
                            <delay_flex/>
                            <params/>
                            <ipmi_sensor/>
                            <data_type>0</data_type>
                            <authtype>0</authtype>
                            <username/>
                            <password/>
                            <publickey/>
                            <privatekey/>
                            <port/>
                            <description/>
                            <inventory_link>0</inventory_link>
                            <applications>
                                <application>
                                    <name>docker_test</name>
                                </application>
                            </applications>
                            <valuemap/>
                            <logtimefmt/>
                            <application_prototypes/>
                        </item_prototype>
                        <item_prototype>
                            <name>Container {#CONTAINERNAME} mem usage:</name>
                            <type>0</type>
                            <snmp_community/>
                            <multiplier>0</multiplier>
                            <snmp_oid/>
                            <key>docker.[{#CONTAINERNAME},MemPerc]</key>
                            <delay>60</delay>
                            <history>90</history>
                            <trends>365</trends>
                            <status>0</status>
                            <value_type>0</value_type>
                            <allowed_hosts/>
                            <units>%</units>
                            <delta>0</delta>
                            <snmpv3_contextname/>
                            <snmpv3_securityname/>
                            <snmpv3_securitylevel>0</snmpv3_securitylevel>
                            <snmpv3_authprotocol>0</snmpv3_authprotocol>
                            <snmpv3_authpassphrase/>
                            <snmpv3_privprotocol>0</snmpv3_privprotocol>
                            <snmpv3_privpassphrase/>
                            <formula>1</formula>
                            <delay_flex/>
                            <params/>
                            <ipmi_sensor/>
                            <data_type>0</data_type>
                            <authtype>0</authtype>
                            <username/>
                            <password/>
                            <publickey/>
                            <privatekey/>
                            <port/>
                            <description/>
                            <inventory_link>0</inventory_link>
                            <applications>
                                <application>
                                    <name>docker_test</name>
                                </application>
                            </applications>
                            <valuemap/>
                            <logtimefmt/>
                            <application_prototypes/>
                        </item_prototype>
                        <item_prototype>
                            <name>Container {#CONTAINERNAME}  NETio usage:</name>
                            <type>0</type>
                            <snmp_community/>
                            <multiplier>0</multiplier>
                            <snmp_oid/>
                            <key>docker.[{#CONTAINERNAME},NetIO]</key>
                            <delay>60</delay>
                            <history>90</history>
                            <trends>0</trends>
                            <status>0</status>
                            <value_type>1</value_type>
                            <allowed_hosts/>
                            <units/>
                            <delta>0</delta>
                            <snmpv3_contextname/>
                            <snmpv3_securityname/>
                            <snmpv3_securitylevel>0</snmpv3_securitylevel>
                            <snmpv3_authprotocol>0</snmpv3_authprotocol>
                            <snmpv3_authpassphrase/>
                            <snmpv3_privprotocol>0</snmpv3_privprotocol>
                            <snmpv3_privpassphrase/>
                            <formula>1</formula>
                            <delay_flex/>
                            <params/>
                            <ipmi_sensor/>
                            <data_type>0</data_type>
                            <authtype>0</authtype>
                            <username/>
                            <password/>
                            <publickey/>
                            <privatekey/>
                            <port/>
                            <description/>
                            <inventory_link>0</inventory_link>
                            <applications>
                                <application>
                                    <name>docker_test</name>
                                </application>
                            </applications>
                            <valuemap/>
                            <logtimefmt/>
                            <application_prototypes/>
                        </item_prototype>
                        <item_prototype>
                            <name>Container{#CONTAINERNAME} is_run :</name>
                            <type>0</type>
                            <snmp_community/>
                            <multiplier>0</multiplier>
                            <snmp_oid/>
                            <key>docker.[{#CONTAINERNAME} ,ping]</key>
                            <delay>30</delay>
                            <history>90</history>
                            <trends>365</trends>
                            <status>0</status>
                            <value_type>3</value_type>
                            <allowed_hosts/>
                            <units/>
                            <delta>0</delta>
                            <snmpv3_contextname/>
                            <snmpv3_securityname/>
                            <snmpv3_securitylevel>0</snmpv3_securitylevel>
                            <snmpv3_authprotocol>0</snmpv3_authprotocol>
                            <snmpv3_authpassphrase/>
                            <snmpv3_privprotocol>0</snmpv3_privprotocol>
                            <snmpv3_privpassphrase/>
                            <formula>1</formula>
                            <delay_flex/>
                            <params/>
                            <ipmi_sensor/>
                            <data_type>0</data_type>
                            <authtype>0</authtype>
                            <username/>
                            <password/>
                            <publickey/>
                            <privatekey/>
                            <port/>
                            <description/>
                            <inventory_link>0</inventory_link>
                            <applications>
                                <application>
                                    <name>docker_test</name>
                                </application>
                            </applications>
                            <valuemap/>
                            <logtimefmt/>
                            <application_prototypes/>
                        </item_prototype>
                    </item_prototypes>
                    <trigger_prototypes>
                        <trigger_prototype>
                            <expression>{docker-status:docker.[{#CONTAINERNAME} ,ping].last()}=0</expression>
                            <recovery_mode>0</recovery_mode>
                            <recovery_expression/>
                            <name>docker_{#CONTAINERNAME}_down</name>
                            <correlation_mode>0</correlation_mode>
                            <correlation_tag/>
                            <url/>
                            <status>0</status>
                            <priority>5</priority>
                            <description/>
                            <type>0</type>
                            <manual_close>0</manual_close>
                            <dependencies/>
                            <tags/>
                        </trigger_prototype>
                    </trigger_prototypes>
                    <graph_prototypes/>
                    <host_prototypes/>
                </discovery_rule>
            </discovery_rules>
            <httptests/>
            <macros/>
            <templates/>
            <screens/>
        </template>
    </templates>
</zabbix_export>
```

docker.py

```text
#!/usr/bin/python
import sys
import os
import json

def discover():
    d = {}
    d['data'] = []
    with os.popen("docker ps -a --format {{.Names}}") as pipe:
        for line in pipe:
            info = {}
            info['{#CONTAINERNAME}'] = line.replace("\n","")
            d['data'].append(info)

    print json.dumps(d)

def status(name,action):
    if action == "ping":
        cmd = 'docker inspect --format="{{.State.Running}}" %s' %name
        result = os.popen(cmd).read().replace("\n","")
        if result == "true":
            print 1
        else:
            print 0
    else:
        cmd = 'docker stats %s --no-stream --format "{{.%s}}"' % (name,action)
        result = os.popen(cmd).read().replace("\n","")
        if "%" in result:
            print float(result.replace("%",""))
        else:
            print result

if __name__ == '__main__':
        try:
                name, action = sys.argv[1], sys.argv[2]
                status(name,action)
        except IndexError:
                discover()
```

