## 绕过系统代理

Clash for Windows在v 0.4.5 版本后可以自定义系统代理需要绕过的域名或IP

### 设置方式

1. 进入Settings页面
2. 点击System proxy Bypass右边Edit小字打开编辑界面
3. 若要增加绕过``example.com``域名，只需在修改编辑界面内容为：
    ```yaml
    bypass:
      - "example.com"  # 下面字段可不删除
      - 127.0.0.1  
      - ...
    ```
4. 点击编辑器右下角保存

bypass类型为数组，item为需要绕过的域名或节点，支持通配符*

{% hint style='info' %}
最后一行对应系统中“请勿将代理服务器用于本地(Intranet)地址”选项，请确保此项在最底部
{% endhint %}