#  常用的数据类型

## date, time,datetime 和 timestamp

- date 表示的是日期，格式为: `YYYY-MM-DD`, 表示的时间范围是: `1000-01-01` - `9999-12-31`, 占 3 个字节
- time 表示的是时间，格式为: `00:00:00`, 表示的时间范围: `00:00:00` - `23:59:59`, 占 3 个字节
- datetime 表示的日期时间，格式为 `YYYY-MM-DD HH:mm:SS`, 表示的时间范围 `1000-01-01 00:00:00` - `9999-12-31 23:59:69` ，占 8 个字节。
- timestamp 表示的是一个时间戳。表示的是 1970-01-01 年以来经历的秒数, 占 4 个字节。

# UTF-8 & UTF8mb4

mysql 的 UTF-8 编码并不是真正意义上的 UTF-8。MySQL 的 UTF8 是一种“专属的编码”，它能够编码的 Unicode 字符并不多。

MySQL 在 2010 年发布了一个叫作 utf8mb4 的字符集，这个才是真正意义上的 UTF-8。所以，我们都应该改用 utf8mb4，永远都不要再使用 UTF8。

# char 和 varchar

- char 表示的是定长字符串
- varchar 表示的是变长字符串
- char(10) 表示可以存放 10 个字符，varchar(10) 表示最大可存放 10 个字符
- char 会去掉尾部的空格，而 varchar 不会
- varchar 会占用 1~2 个字节来存储字符串的长度，如果最大长度超过 255， 就需要两个字节，否则只需要一个字节

# Mysql 索引

## Mysql 索引为什么要使用 B+ 树

这个主要和数据库所需要提供的功能以及查询效率相关，数据库需要提供如下的几个功能：

- 等值查询
- 范围查询
- 结果排序

对于等值查询而言，采用 hash 索引是最快的，时间复杂度为 $O(1)$, 但是 hash 索引对于范围查询以及结果排序的支持不好。

数据库中的数据是存放在磁盘中的，数据查询的效率主要依赖于磁盘 IO 的次数，磁盘 IO 的次数越少，查询的速度就越快。

树有很多种：

- 二叉树
- 平衡二叉树
- B 树

如果使用二叉树，

B+树是对 B 树的改进：

- B+ 树的非叶子节点全部用于存放索引，因为一个数据页中存放的索引数量越多，对应的磁盘 IO 次数就会越少。
- B+ 树的叶子节点使用双向指针进行连接，形成一个顺序的双向链表，方便顺序查找和范围查找。
- B+ 树的查询效率稳定，因为每次都需要查询到树的叶子节点才能够查询到真实的数据

# 建立索引的原则

- 建立索引的字段应该是常用于查询和连接的字段。例如经常用于 where， join，和 order by 的字段

# 索引失效

- 模糊查询的前缀匹配
- 索引列参与表达式计算
- 没有满足联合索引的最左匹配原则