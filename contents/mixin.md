## Mixin

### 版本要求

0.9.5版本更新后，支持向所有配置文件中注入公共属性设置

### 配置文件

例如：在配置文件中统一添加``dns``字段，操作如下：

1. 进入Settings页面
2. 滚动至Profile Mixin栏
2. 点击YAML右边Edit小字打开编辑界面
3. 在修改编辑界面内容为：
    ```yaml
    mixin: 
      dns:
        enable: true
        listen: :53
        nameserver:
          - 8.8.8.8   
    ```
4. 点击编辑器右下角保存


在启动或切换配置时，上面内容将会替换到原有配置文件中进行覆盖


{% hint style='info' %}
配置文件内容不会被修改，混合行为只会发生在内存中
{% endhint %}

{% hint style='info' %}
可以通过任务栏图标菜单开关这个行为
{% endhint %}

### JavaScript

0.10.1版本更新后，支持使用JavaScript进行mixin配置，需要传入一个字符串（yaml多行字符串使用``｜``）

具体步骤如上，只需要将代码填入JavaScript栏中，并将Type设置成JavaScript即可：

```js
module.exports.parse = async ({ content, name, url }, { axios, yaml, notify }) => {
  const extra = {
    dns: {
      enable: true,
      listen: ':53',
      nameserver: ['8.8.8.8']
    }
  }
  return { ...content, ...extra }
}
```


#### 参数说明

CFW调用用户定义的``parse``方法时，会传入2个参数，分别是**配置文件元数据**以及**工具类对象/方法**

##### 配置文件元数据

包括：
1. content：yaml格式化后的JavaScript对象
2. name：配置文件文件名
3. url：配置文件下载地址

##### 工具类对象/方法

包括：
1. axios：网络请求框架，[GitHub](https://github.com/axios/axios)
2. yaml：yaml框架，[GitHub](https://github.com/eemeli/yaml)
3. notify：发出系统通知方法，签名为``function notify(title:string, message:string, silent:bool)``

#### 返回说明

``parse``方法需要返回一个对象，CFW会将返回的对象序列化后直接载入
