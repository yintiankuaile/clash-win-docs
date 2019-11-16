## TAP模式

对于不遵循系统代理的软件，TAP模式可以接管其流量并交由CFW处理

### 安装TAP网卡
点击``General``中``TAP Device``将会安装TAP网卡，此网卡用于接管系统流量，安装完成可在系统网络连接中看到名为``cfw-tap``的网卡

### 启动TAP模式

使用的Profile中包含fake-ip设置：
```yaml
dns:
   enable: true
   enhanced-mode: fake-ip
   listen: 127.0.0.1:53
   nameserver:
      - 223.5.5.5
```

### 工作原理

为避免循环，CFW只会将Fake IP段的请求发往TAP，所以必须要在配置文件中指定``enhanced-mode: fake-ip``

CFW会将系统DNS修改为Clash本地DNS服务器，获取到Fake IP的请求再发送至TAP网卡，这可以让大部分软件正常工作，但如果请求直接使用IP地址而非域名，则不会被发往TAP，例如Telegram

{% hint style='info' %}
目前TAP模式暂不支持UDP
{% endhint %}