## 配置文件预处理

### 版本要求

0.10.1版本更新后，支持使用JavaScript对下载后的配置文件进行预处理

### 配置文件

如果需要对下载地址为``https://example.com/profile.yaml``的配置文件进行预处理，则需要在config.yaml文件中添加如下配置：

```yaml
cfw-profile-parsers:
  - url: https://example.com/profile.yaml
  - code: |
      module.exports.parse = async (raw, { axios, yaml, notify }) => {
        const obj = yaml.parse(raw)
        return yaml.stringify(obj)
      }
```

当配置文件触发刷新（包括自动更新）时，CFW会调用此方法对下载的配置文件内容进行处理，再写入本地文件中

当然，parsers也支持使用路径引入代码：

```yaml
cfw-profile-parsers:
  - url: https://example.com/profile.yaml
    path: 'C:/Users/cfw/parser.js'
```


#### 参数说明

CFW调用用户定义的``parse``方法时，会传入2个参数，分别是**配置文件文本内容**以及**工具类对象/方法**

##### 配置文件文本内容
raw是一个字符串，一般需要用yaml库解析成JavaScript对象

##### 工具类对象/方法

包括：
1. axios：网络请求框架，[GitHub](https://github.com/axios/axios)
2. yaml：yaml框架，[GitHub](https://github.com/eemeli/yaml)
3. notify：发出系统通知方法，签名为``function notify(title:string, message:string, silent:bool)``

#### 返回说明

``parse``方法需要返回一个字符串，CFW会将返回的字符串存入对应的配置文件中
