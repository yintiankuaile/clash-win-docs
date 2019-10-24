## URL Scheme

CFW支持使用URL Scheme快速导入配置文件：

```
clash://install-config?url=<encoded URI>
```

### 自定义名称

在CFW中使用URL导入后显示的配置文件名称识别逻辑如下：
1. 响应体头部中是否存在``content-disposition``字段，如果存在则使用里面``filename``对应的值
2. 使用URL最后一部分作为配置文件名