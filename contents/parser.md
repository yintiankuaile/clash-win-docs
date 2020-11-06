## 配置文件预处理

### 版本要求

0.10.1版本更新后，支持使用JavaScript对下载后的配置文件进行预处理

0.11.10版本更新后，支持使用YAML对下载后配置文件进行简单预处理

### 简便方法（YAML）
如果需要对下载地址为``https://example.com/profile.yaml``的配置文件进行预处理，操作如下：

1. 进入Settings界面
2. 滚动至Profiles栏
3. 点击Parsers右边Edit打开编辑器，填入：
    ```yaml
    parsers:
      - url: https://example.com/profile.yaml
        yaml: 
          prepend-rules:
            - DOMAIN,test.com,DIRECT # rules最前面增加一个规则
          append-proxies: 
            - name: test   # proxies最后面增加一个服务
              type: http
              server: 123.123.123.123
              port: 456
    ```
4. 点击编辑器右下角保存按钮

当配置文件触发刷新（包括自动更新）时，CFW会读取``yaml``字段定义的值，将对应值插入/合并到原配置文件中

#### 参数说明

键|值类型|操作
-|-|-
append-rules|数组|数组合并至原配置``rules``数组**后**
prepend-rules|数组|数组合并至原配置``rules``数组**前**
append-proxies|数组|数组合并至原配置``proxies``数组**后**
prepend-proxies|数组|数组合并至原配置``proxies``数组**前**
append-proxy-groups|数组|数组合并至原配置``proxiy-groups``数组**后**
prepend-proxy-groups|数组|数组合并至原配置``proxiy-groups``数组**前**
mix-proxy-providers|对象|对象合并至原配置``proxy-providers``中
mix-rule-providers|对象|对象合并至原配置``rule-providers``中
mix-object|对象|对象合并至原配置最外层中


### 进阶方法（JavaScript）

如果需要对下载地址为``https://example.com/profile.yaml``的配置文件进行预处理，操作如下：

1. 进入Settings界面
2. 滚动至Profiles栏
3. 点击Parsers右边Edit打开编辑器，填入：
    ```yaml
    parsers:
      - url: https://example.com/profile.yaml
        code: |
          module.exports.parse = async (raw, { axios, yaml, notify, console }, { name, url, interval, selected }) => {
            const obj = yaml.parse(raw)
            return yaml.stringify(obj)
          }
    ```
4. 点击编辑器右下角保存按钮

当配置文件触发刷新（包括自动更新）时，CFW会调用此方法对下载的配置文件内容进行处理，再写入本地文件中

当然，parsers也支持使用路径引入代码：

```yaml
parsers:
  - url: https://example.com/profile.yaml
    file: 'C:/Users/cfw/parser.js'
```


#### 参数说明

CFW调用用户定义的``parse``方法时，会传入3个参数，分别是**配置文件文本内容**，**工具类对象/方法**以及**配置文件元数据**

##### 配置文件文本内容
raw是一个字符串，一般需要用yaml库解析成JavaScript对象

##### 工具类对象/方法

包括：
- axios：网络请求框架，[GitHub](https://github.com/axios/axios)
- yaml：yaml框架，[GitHub](https://github.com/eemeli/yaml)
- notify：发出系统通知方法，签名为``function notify(title:string, message:string, silent:bool)``
- console：日志输出至文件，方便调试，在Settings界面中Parser设置下方打开

##### 配置文件元数据
元数据为JavaScript对象，包括：
- name：名称
- url：下载地址
- interval：更新周期
- selected：策略组选择缓存，数组
- mode：模式缓存

**元数据在配置文件首次下载时为空对象**

#### 返回说明

``parse``方法需要返回一个字符串，CFW会将返回的字符串存入对应的配置文件中

### 多处理器及正则匹配

#### 正则匹配
上面例子中，使用``url``匹配配置文件地址，如果一个处理器需要处理多个配置文件，也可以使用正则表达式进行匹配，使用关键字``reg``设置

```yaml
parsers:
  - reg: https://test.com.+$  # 正则匹配域名
    yaml: 
      prepend-rules:
        - DOMAIN,test.com,DIRECT
```

#### 多处理器

parser定义的数组支持多个处理器从上至下按顺序执行，例如：

```yaml
parsers:
  - reg: https://test.com.+$   # 第一个执行的parser
    file: 'C:/Users/cfw/parser.yaml'
  - url: https://example.com/profile.yaml  # 对上一个parser执行的结果进行处理
    file: 'C:/Users/cfw/parser.js'
```


{% hint style='info' %}
file同时支持yaml及js格式的文件
{% endhint %}