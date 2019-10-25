# redis

## redis特性
 
1. 速度快
 - 机器配置
 - c语言编写，离操作系统近
 - 内存读写
 - 单线程，多路复用机制
2. 键值对得数据结构服务器
3. 丰富的功能
4. 简单稳定
5. 持久化
6. 主从复制
7. 高可用和分布式转移
8. 客户端语言多

## 使用场景
1. 缓存数据库
2. 排行榜
3. 计数器应用
4. 社交网络
5. 消息队列

## 5种数据结构
### 集合（set）
Redis 的 Set 是 String 类型的无序集合。集合成员是唯一的，这就意味着集合中不能出现重复的数据。
Redis 中集合是通过哈希表实现的，所以添加，删除，查找的复杂度都是 O(1)。
集合中最大的成员数为 232 - 1 (4294967295, 每个集合可存储40多亿个成员)。

1. 向集合添加一个或多个成员

		SADD key member1 [member2] 
2. 获取集合的成员数

		SCARD key 
3. 返回给定所有集合的差集

		SDIFF key1 [key2] 
4. 返回给定所有集合的差集并存储在 destination 中

		SDIFFSTORE destination key1 [key2] 
5. 返回给定所有集合的交集

		SINTER key1 [key2] 
6. 返回给定所有集合的交集并存储在 destination 中

		SINTERSTORE destination key1 [key2] 
7. 判断 member 元素是否是集合 key 的成员

		SISMEMBER key member 
8. 返回集合中的所有成员

		SMEMBERS key 
9. 返回所有给定集合的并集

		SUNION key1 [key2]
10. 所有给定集合的并集存储在 destination 集合中

		SUNIONSTORE destination key1 [key2] 
11. 移除集合中一个或多个成员
	
		SREM key member1 [member2] 
### 有序集合(sorted set)
Redis 有序集合和集合一样也是string类型元素的集合,且不允许重复的成员。
不同的是每个元素都会关联一个double类型的分数。redis正是通过分数来为集合中的成员进行从小到大的排序。
有序集合的成员是唯一的,但分数(score)却可以重复。
集合是通过哈希表实现的，所以添加，删除，查找的复杂度都是O(1)。 集合中最大的成员数为 232 - 1 (4294967295, 每个集合可存储40多亿个成员)。

1. 向有序集合添加一个或多个成员、或更新已存在成员的分数

		ZADD key score1 member1 [score2 member2]
2. 有序集合中对指定成员的分数加上增量 increment（ZINCRBY key increment member）

		ZINCRBY key increment member
3. 返回有序集合的成员，按分数值递增(从小到大)，正序

		ZRANGE key start stop [WITHSCORES]，start：开始索引，stop：结束索引，都是以0开始，-1表示最后一个成员
	获取key的所有成员:

		ZRANGE key 0 -1
4. 返回有序集合的成员，按分数值递减（从大到小）,逆序

		ZREVRANGE key start stop [WITHSCORES]
	<br>获取key的所有成员:

		ZREVRANGE key 0 -1

5. 返回有序集中，成员的分数值

		ZSCORE key member
6. 计算一个或多个有序集的交集，将结果放在新的有序集合key中

		ZUNIONSTORE destination numkeys key [key ...] 
7. 计算给定的一个或多个有序集的并集，并存储在新的 key 中

		ZUNIONSTORE destination numkeys key [key ...] 

8. 返回有序集合中指定成员的索引
	
	- 按分值，正序
		
			ZRANK key member
	- 按分值，倒序
	
			ZREVRANK key member
9. 