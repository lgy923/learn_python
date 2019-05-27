## String

1.  string是redis最基本的类型
2.  最大能存储512MB数据
3.  string类型是二进制最安全,即可以为任何数据,比如数字,图片,序列化对象等

#### 设置键值
-   设置键值: **SET key value**
-   设置键值及过期时间,以秒为单位: **SETEX key seconds value**
-   设置多个键值: **MSET key1 value2 key2 value2** 

#### 获取值
-   根据键获取值: **GET key**
-   根据多个键获取多个值: **MGET key1 key2**

#### 运算
-   将key对应的value加1(要求value是数字): **INCR key**
-   将key对应的value加**整数**: **INCRBY key increment**

-   将key对应的value减一: **DECR key**
-   将key对应的value减一个**整数**: **DECRBY key decrement**

#### 其他
-   追加值: **APPEND key value**
-   获取值长度: **SERLEN key**



## Hash

1.  hash用于存储对象,对象的格式为键值对

#### 设置对象属性值
-   设置单个属性: **HSET key field value**
-   设置多个属性: **HMSET key field1 value1 field2 value2**

#### 获取对象属性值
-   获取一个属性的值: **HGET key field**
-   获取多个属性的值: **HMGET key field1 field2**
-   获取所有的属性: **HKEYS key**
-   返回包含属性的个数: **HLEN key**
-   获取所有(属性)的值: **HVALS key**

#### 其他
-   判断对象是否存在某个属性: **HEXISTS key field**
-   删除对象的某个属性: **HDEL key field1 field2**
-   返回对象某个属性的值的字符串长度: **HSTRLEN key field**



## list

1.  list的元素类型为string
2.  按照插入顺序排序
3.  在列表的头部或者尾部添加元素

#### 设置list值
-   在头部插入数据(一次可以插入多个数据): **LPUSH key value1 value2 value3**
-   在尾部插入数据: **RPUSH key value1 value2 value3**
-   在一个元素(pivot)的前后插入新元素(value): **LINSERT key BEFORE|AFTER pivot value**
-   设置指定索引(index)的元素值(索引是基于0的下标): **LSTE key index value** 

#### 获取值
-   移除并返回key对应的list的第一个元素: **LPOP key**
-   移除并返回key对应的list的最后一个元素: **RPOP key**
-   返回存储在key中的list的指定范围内的元素(切片): **LRANGE key start stop**
-   返回存储在key中的list对应索引(index)的值: **LINDEX key index**

#### 其它
-   裁剪列表改为原集合的一个子集: **LTRIM key start stop**
-   返回存储在key中的list的长度: **LLEN key**



## Set

1.  无序集合
2.  元素为string类型
3.  元素具有唯一性,不重复

#### 添加元素
-   添加多个元素: **SADD key member1 member2**

#### 获取
-   返回key集合中所有的元素: **SMEMBERS key**
-   返回key集合中元素个数: **SCARD key**

#### 其它
-   求多个集合的交集: **SINTER key1 key2**
-   求多个集合的差集(集合顺序分前后): **SDIFF key1 key2**
-   求多个集合的并集: **SUNION key1 key2**
-   判断元素(member)是否在key集合中: **SISMEMBER key member**



## Zset

1.  sorted set,有序集合
2.  元素为string类型
3.  元素具有唯一性,不重复
4.  每个元素都会关联一个double类型的score,表示权重,通过权重将元素从小到大排序
5.  元素的score可以相同

#### 设置值
-   添加元素: **ZADD key score1 member1 score2 member2** 

#### 获取值
-   返回指定索引范围内的元素(可同时获取权重): **ZRANGE key start stop [WITHSCORE]**
-   返回元素个数: **ZCARD key**
-   返回有序集合key中,score值在min和max之间的元素个数: **ZCOUNT key min max**
-   返回有序集合key中,元素member的权重score值: **ZSCORE key member**



## 键命令

-   查找键,参数支持正则表达式: **KEYS pattern**
-   判断键是否存在,可同时判断多个key,返回已存在的key的数量: **EXISTS key1 key2**
-   查看键对应的value的类型: **TYPE key**
-   删除(一个或多个)键及对应的值: **DEL key1 key2**
-   设置过期时间,以秒为单位,创建时没有设置过期时间则一直存在,直到使用DEL删除: **EXPIRE key seconds**
-   查看键key的有效时间,以秒为单位(永久存在则返回-1,过期则返回-2): **TTL key**

### 其他操作
-   选择数据库: **select [0-15]**
-   查看所有键: <b>keys *</b>
-   删除所有键: **redis-cli keys "*" | xargs redis-cli del**



