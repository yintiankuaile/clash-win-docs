## 自定义状态栏图标

### 版本要求

0.8.9版本后，增加``cfw-tray-icon``字段用于自定义状态栏图标

### 配置

```yaml
cfw-tray-icon: 
  default: C:\Users\abc\custom.ico           # 默认图标
  system-proxy-on: C:\Users\abc\custom.ico   # 开启系统代理后图标
```

### ICO文件大小

建议64x64，如果不清晰可以尝试32x32，纯白[custom.ico](../assets/custom.ico)