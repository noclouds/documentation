
### 0.5.0
- loadtimeout根据ts文件时长自适应调整

### 0.5.1
- 改进loadtimeout自适应算法

### 0.5.2
- 修复重新初始化Hls实例时会自动切换到默认信令的bug 

### 0.5.3
- 修复下载超时情况下阻塞p2p的bug
- mobile设备可单独设置最大缓存大小

### 0.5.4
- 第三方播放器上报

### 0.6.0
- 修复播放卡顿的问题
- 加入新字段`live`

### 0.7.0
- 新增[切片校验功能](https://docs.cdnbye.com/#/API?id=how-to-check-segment-validity)

### 0.8.0
- 通过强制前几个ts采用HTTP下载来缓存足够的buffer，可以在p2pConfig配置
- p2p策略优化
- 可以在p2pConfig中监听下载信息

### 0.8.1
- 节点过期时重启P2P
- 增加视频缓存

### 0.9.0
- 优化算法，提升P2P效果
- 解决直播中的卡顿问题

### 0.9.1
- 解决数据上报bug
- 优化预加载策略

### 0.9.2
- 参数优化
- 修复clappr-plugin的bug