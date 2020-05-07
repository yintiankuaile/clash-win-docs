## 自定义节点排序

### 版本要求

0.9.10版本更新后，支持自定义客户端字体

### 配置文件

在 ``config.yaml``（General中点击Text Mode Edit）中添加以下字段: 

```yaml
cfw-proxies-order: default 
```

可选参数：

- default：按配置文件定义节点顺序
- latency：按节点延迟升序排列
- alphabet：按节点名称字母表排列