## 规则编辑

![Edit Rules](/assets/ui-profiles-rules1.png)

此界面用于增加和删减配置文件中的规则，目前Clash支持的规则类型如下：

- DOMAIN-SUFFIX：域名后缀匹配
- DOMAIN：域名匹配
- DOMAIN-KEYWORD：域名关键字匹配
- IP-CIDR：IP段匹配
- SRC-IP-CIDR：源IP段匹配
- GEOIP：GEOIP数据库（国家代码）匹配
- DST-PORT：目标端口匹配
- SRC-PORT：源端口匹配
- PROCESS-NAME：源进程名匹配
- RULE-SET：Rule Provider规则匹配
- MATCH：全匹配

{% hint style='info' %}

1. 使用``PROCESS-NAME``需要 Clash for Windows v0.11.5 及以上版本；规则需要匹配完整的进程名（包括可执行文件后缀）方可生效；该规则不适用于TAP流量

2. 用户界面暂不支持添加``RULE-SET``规则，请手动编辑配置文件

3. ``MATCH``需要位于规则列表末尾

{% endhint %}
