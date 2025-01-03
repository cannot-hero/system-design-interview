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
   [https://www.fengstatic.com/archives/3980]
   在数据库中，热点问题通常指的是同一行或同一数据区域在高并发场景下频繁被修改，导致数据库锁冲突、性能下降，甚至出现系统瓶颈

    解决方法：

    1. 异步队列 or 缓存（保留目前分区，只是让这个区变得不再 hot）
       比如可以先将增量缓存起来，然后定时写入更新，或者用 kafka 消息队列异步处理
       缺点： 数据更新会不及时
    2. 数据分片或分区（拆掉 hotspot）
       对于频繁修改的数据，可以考虑通过水平分片或逻辑分区的方式，将数据分散存储
    3. 通过锁来控制并发
