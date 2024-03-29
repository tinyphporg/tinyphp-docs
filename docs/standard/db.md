MYSQL操作规范
====

包括数据库操作规范，包括查询优化，库和表和设计，MYSQL参数配置等

查询语句
-----
-----


### 查询语句规范   

`【规则1-1.1】` 所有SQL关键字，全部使用大写，比如SELECT INSERT UPDATE WHERE 等. 例：

```sql  
  SELECT id FROM t WHERE id = 1
```
  
`【规则1-1.2】`非必须情况，禁止使用SQL自身函数。
`【规则1-1.3】` 取一行数据时，SQL语句后面，必须加 LIMIT 1语句。  
`【规则1-1.4】` 任何查询语句，都必须考虑LIMIT 分页，禁止不带 LIMIT 。
  

### 查询优化建议

`【规则1-2.0】` 避免使用全表扫描,尽量利用索引
`【规则1-2.1】` 避免在 WHERE 子句中使用!=或<>操作符。

```sql
 SELECT id FROM t WHERE name != ''
```
  
`【规则1-2.2】` 避免在WHERE字句里判断''或者 NULL ，可以设置默认值为0，判断是否=0。

```sql
  避免
  SELECT id FROM t WHERE name IS NULL
  可用以下语句替代：
  SELECT id FROM t WHERE uid = 0 
```

`【规则1-2.3】` 避免在 WHERE 子句中使用 OR 来连接条件。

```sql
  SELECT id FROM t WHERE uid=10 or uid=20
  替代
  SELECT id FROM t WHERE uid=10
  UNION ALL
  SELECT id FROM t WHERE uid=20
```
  
`【规则1-2.4】` 避免在 WHERE 字句中使用 LIKE %小明%。
注意： `LIKE 小明%` 可利用到索引。
  
```sql
  全表扫描和没有利用索引的情况：
  SELECT id FROM t WHERE name LIKE '%c%'
  或
  SELECT id FROM t WHERE name LIKE '%小明'
  利用到索引的情况：
  SELECT id FROM t WHERE name LIKE '小明%'
```
  
`【规则1-2.5】`IN 和 NOT IN 慎用,连续值可用BETWEN, 或者用EXISTS代替 如：

```sql
    SELECT id from t WHERE uid in(1,2,3)
    对于连续的数值，尽量用 BETWEEN 替代 IN ：
    SELECT id FROM t WHERE num BETWEEN 1 AND 3
    可用EXISTS代替IN
    SELETC num FROM a WHERE num EXISTS(SELECT 1 FROM b WHERE num=a.num)
```

 `【规则1-2.6】`  SQL语句中避免使用SQL局部变量等,将无法用到查询优化器。
 
 ```sql
   SELECT id FROM t WHERE name=@NAME
   ```
   
 `【规则1-2.7】` 可强制使用索引。
 
 ```sql
 SELECT id FROM t WITH(index索引名称) WHERE name ="小明"
 ```
 
`【1-2.8】` 禁止在SQL语句中 进行表达式操作。

```sql
  SELECT name FROM t WHERE uid/2 = 10
```

`【1-2.9】` 禁止在WHERE 字句的=号 左边进行参数操作。

```sql
SELECT id FROM t WHERE SUBSTRING(name, 1, 3) = ’abc’
```

`【1-2.10】` 使用复合索引时，WHERE 子句的条件，必须用到复合索引的第一个字段，才能利用到该索引。  

`【1-2.11】` 一个表的索引，原则上不超过6个，因为会降低INSERT UPDATE等写入语句的效率。  

`【1-2.12】` 当一个字段的数据大量重复时，一般情况不需要建立索引，可用ENMU类型代替。  

`【1-2.13】` 尽量使用数字型字段，查询时，可将文本字段映射为数字字段，增加查询效率，如uid->username   

`【1-2.14】` 使用变长字段代替定长字段，如varchar 替代 var，但是当一个表里面的所有非定长字段全部为定长字段时，查询效率更快。   

`【1-2.15】` 任何时候，禁止使用SELECT * FROM t 的*，必须只取需要的字段。   

`【1-2.16】` 禁止频繁创建和删除临时表，可采用查询在程序内部处理数据的方法。    

`【1-2.17】` 避免查询返回大数据。    

`【1-2.18】` 避免大的事务操作，提高性能。    

`【1-2.19】` 禁止滥用GROUP BY 比如导出全表数据的查询，或者该字段涉及大量非重复值.   

`【1-2.20】` 多看慢查询日志。   

`【1-2.21】` JOIN时，小表联大表。     

`【1-2.22】` 对于关键性查询语句，善用explain关键词进行索引和性能分析进行优化。     
   
 
库和表的规范  
-----
-----

### 库   

`【规则2-1.1】` 库的创建原则，根据项目和模块划分，尽量保持相同垂直业务模块的表位于同一库。
  
`【规则2-1.2】`  库的默认引擎统一为`InnoDB` 语言编码统一为`utf8_general_ci`

`【规则2-1.3】` 库的命名规则: 库名的字符范围为`[a-z0-9]`，统一为小写字母，按下划线`_`分割，需简介明了，按项目字母简写_模块名规则排列，长度不超过30个字符， ， 比如项目为bx,用户模块为user 则用户数据库的命名为bx_user。
  
`【规则2-1.4】`  数据库的设计，应该是做到冷热数据分离。

### 数据表

`【规则2-2.1】` 数据表的创建原则，根据模块划分，尽量保持单一业务模块为一个数据表系列。

`【规则2-2.2】` 数据表的命名，字符范围为`[a-z09]`,统一为小写字母，按下划线分割。每个表必须有自增主键，表与表的相关联字段，必须尽可能保持相同，前缀必须带上项目简写。
例：
项目bx，用户数据表，便为bx_user, bx_user_info, bx_user_extend等。

`【规则2-2.3】` 表字段的创建原则，在InnoDB引擎下，用尽量少的存储空间在存储字段数据，减少内存占用，比如 int varchar等，必须指定长度，能用smallint tinyint 的 就不要用int,能用int(8)的，就不要用int(10)；每个字段尽可能保持NO NULL 和默认值，增加查询和索引效率。

`【规则2-2.4】` 数据表的索引创建原则，命名简洁明了，尽量与字段名产生关联，bx_user的username字段建立索引的名称，需为bx_user_username_index，也可简写为bxu_username。

`【规则2-2.5】` 每个表必须有主键索引，索引应该合理，并每个表不超过6个索引，慎用复合索引。


### 数据库

`【范式2-3.1】` 字段名必须具备原子性，即不可能产生下一个子字段，比如name。

`【范式2-3.2】` 每个表必须有主键和主键索引。

`【范式2-3.3】` 一个表，非考虑扩展性情况下，不能有冗余字段，即尽量保持精简和减少无意义字段，`但在为了减少join查询，可适当在不同表添加相同字段`。

`【范式2-3.4】` 垂直切分表数据时，冷热数据可以拆分到不同表中，更新频繁且数据量小的字段放到热表，数据量大更新频率低的字段放到冷表。


数据库设计原则
-----
------


### 核心原则

`【规则3-1.1】`数据库只做数据存储，不做业务逻辑和数据运算。
 
`【规则3-1.2】` cpu计算密集型的任务，必须移至程序的模型层处理。
 
`【规则3-1.3】` 控制字段表的列数，尽可能少于20。
 
`【规则3-1.4】` 效率优先，适当的冗余来提升效率。
 
`【规则3-1.5】` 严禁超长的SQL语句，严禁2个以上的联表查询，严禁大的事务处理，严禁大批量SQL的写入和更新，删除等操作，严禁大批量数据查询。
 
`【规则3-1.6】` 严禁在数据库负载较高的情况下，在大数据量的表上更改添加删除索引和字段等操作。
 
### 字段类原则

`【规则3-2.1】` 合适的字段，节省空间，提升查询效率。

`【规则3-2.2】` 能用数字字段的SQL语句，尽量避免用字符字段。

`【规则3-2.3】`  避免使用NULL字段。

`【规则3-2.4】` 尽量用varchar字段替代text。

### 索引类原则

`【规则3-3.1】` 合理使用索引，索引不是越多越好，在大数据量的情况下，除专业DBA外，禁止擅自创建索引。

`【规则3-3.2】` 常用查询的字符字段必须建立前缀索引。

`【规则3-3.3】` 不在索引字段做运算。

`【规则3-3.4】` innodb主键使用自增列。

`【规则3-3.5】` 禁止使用外键。

### SQL原则

`【规则3-4.1】` SQL语句尽可能简单，尽可能减少子句，在程序层面拆分多次查询(一条查询语句只能利用CPU的一个核心，一个SQL可以堵死整个服务)。

`【规则3-4.2】` 常规情况下禁止使用触发器，应该在程序层面进行数据同步写入，比如双写。

`【规则3-4.3】` 禁止使用 SELECT *


数据库的配置优化
-----
-----

`【规则4.1】`优化MYSQL性能的最佳办法，就是尽量不用数据库，多利用内存缓存。   

`【规则4.2】` 复杂的文本字段搜索，尽量利用MYSQL以外的全文搜索引擎。   

`【规则4.3】` 分库分表和冷热数据分离时，对承载数据库的硬件也要根据冷热数据原则进行定制。   

`【规则4.4】` 内部的核心网络交换设备和网卡也是影响数据库数据交换的关键硬件。   
 