## Mixin

### 版本要求

0.9.5版本更新后，支持向所有配置文件中注入公共属性设置

### 配置文件

例如：在配置文件中统一添加``dns``字段，操作如下：

在 ``config.yaml``中添加以下字段: 
```yaml
cfw-profile-mixin: 
  dns:
    enable: true
    listen: :53
    nameserver:
      - 8.8.8.8   
```

在启动或切换配置时，上面内容将会替换到原有配置文件中进行覆盖


{% hint style='info' %}
配置文件内容不会被修改，混合行为只会发生在内存中
{% endhint %}

{% hint style='info' %}
可以通过任务栏图标菜单开关这个行为
{% endhint %}