#### Partitioning by hash of key

根据键的散列分区
应对热点和偏斜问题(risk of skew and hot spots)，散列函数可以将偏斜的数据(skewed data)均匀分布。
缺点：会降低范围查询的效率
解决方法，用复合主键
