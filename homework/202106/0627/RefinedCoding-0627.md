# ZooKeeper
- P10 - P14
- https://blog.csdn.net/qq_27639777/article/details/102535176

## 4 ZooKeeper的实现
- 写请求，先原子广播，然后再提交数据库
- 读请求，从本地数据库读取
- 每个节点复制整个数据树，存放在内存
- 每个znode最多1MB，但可配置
- 先以日志形式存入磁盘，然后再提交数据库
- 定期做快照，用快照和日志恢复节点

### 4.1 请求处理
- 消息传递符合原子性？
- 对于写请求，领导者对比较请求的版本号和需要更新znode的版本号
- 如果匹配生成setDataTXN，否则errorTXN

### 4.2 原子广播
- 对读请求，节点转发给领导者，领导者广播给所有，使用Zab协议，默认多数仲裁
- 流水线操作，TCP传输，事务符合幂等性

### 4.3 副本数据库
- 模糊快照，，深度优先扫描数据树，恢复时也发送状态修改？

### 4.4 服务器客户端交互
- 读请求被标记zxid
- 客户端发送心跳，超时会关闭会话？

## 5 评估

### 5.1吞吐量

### 5.2 请求延迟

### 5.3 故障性能

## 6 相关工作

## 7 结论