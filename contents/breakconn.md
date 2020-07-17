## 打断连接

默认情况下，CFW不会在任何时候主动打断正在进行的连接（Connections），连接会被保持到主动断开。

如果在特定情况下，需要在切换节点后或切换配置文件前先打断连接，操作：

1. 进入Settings页面
2. 点击滚动至Proxies设置
3. 根据需求进行选择或开关

### 选项说明

#### Break When Proxy Change
  - None：默认值，不进行打断
  - Chain：打断所有chains中包含此策略组的连接
  - All：打断所有连接

#### Break When Profile Change
  - 开：切换配置前先打断所有连接
  - 关：不打断

#### Break When Mode Change
  - 开：切换代理模式时断开所有连接
  - 关：不打断