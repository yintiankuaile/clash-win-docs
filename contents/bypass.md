## 绕过系统代理

Clash for Windows在v 0.4.5 版本后可以自定义系统代理需要绕过的域名或IP

部分应用检测到系统代理会拒绝响应（例如网易云音乐uwp），此功能用于解决此类问题

### 设置方式

#### config.yaml
```yaml
port: 8888
socks-port: 8889
redir-port: 0
allow-lan: true
mode: Rule
log-level: info
external-controller: '0.0.0.0:6170'
secret: ''
Proxy:
  ...
Proxy Group:
  ...
Rule:
  ...
cfw-bypass:
  ... # 原有字段不用删除
  - 'music.163.com' # 网易云域名1
  - '*.music.126.net' # 网易云域名2
```


cfw-bypass类型为数组，item为需要绕过的域名或节点，支持通配符*

{% hint style='info' %}
最后一行对应系统中“请勿将代理服务器用于本地(Intranet)地址”选项，请确保此项在最底部
{% endhint %}