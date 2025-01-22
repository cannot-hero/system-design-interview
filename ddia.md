#### Partitioning by hash of key

根据键的散列分区
应对热点和偏斜问题(risk of skew and hot spots)，散列函数可以将偏斜的数据(skewed data)均匀分布。
缺点：会降低范围查询的效率
解决方法，用复合主键

Skewed Workloads and Relieving Hot Spots
哈希分区只能减少热点，不能完全避免，比如所有读写都是针对同一键的情况，这种情况下需要手动处理。比如给 hot spot 的主键加随机数(eg: 0-100)，从而存储在不同的分区中。代价是读取需要额外的合并工作。同时需要一套方法来跟踪哪些键需要呗分割。
