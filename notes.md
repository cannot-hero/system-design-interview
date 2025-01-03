### chapter 26 Real-time Gaming Leaderboard

场景： heavy write + effectively sorting items

#### 首选解决方案

redis + mysql
DAU 较小时可以选择单个 redis 服务器
替代方案
nosql

#### 知识点

1. 排序集比关系数据库性能更高，因为数据始终保持排序，代价是 O（logN） add and find 操作
2. 当 dau 大了之后需要分区(partition, shard)，如何选择分区依据很重要，如选择时间做分区依据会导致热点分区(hotspot partition)

#### 困惑

1. 热点分区会带来什么问题？
