# 数据库

### redis

* key-value存储系统
* Redis运行在内存中但是可以持久化到磁盘
* 五种数据类型：string（字符串），hash（哈希），list（列表），set（集合）及zset\(sorted set：有序集合\)
* [list做大数据分页](https://www.cnblogs.com/rjzheng/p/9096228.html)
* [使用注意事项](https://www.infoq.cn/article/K7dB5AFKI9mr5Ugbs_px)

### SQL

1. 防注入
   * 输入验证\(类型和长度\)
   * 加密处理\(用户输入的数据不再对数据库有任何特殊的意义\)
2. 索引优化
   * 主键索引，它是一种特殊的唯一索引，不允许有空值。
   * 不要写SELECT \*的语句
3. 语句优化
   * 不要写SELECT \*的语句
   * 不要写没有WHERE的SQL语句
   * 使用join代替子查询
   * 联合查询快，数据量少情况下；数据量大一般就会很慢
   * 单表查询慢一些，但是在数据量大情况下易于解耦，易于优化
   * update 批量更新用update table set field = case id when 1 then 10 case id when 2 then 20 end where id in \(1,2\) 比一条条更新快5-10倍
4. 全表扫描语句\(慎用\)
   * 左模糊查询'%...'
   * 使用了不等操作符！=
   * Or使用不当，or两边都必须有索引才行
   * In 、not in
   * Where子句对字段进行表达式操作
5. 数据转换
   * CAST\(Col as int\)
   * CAST\(Col as char\)
6. 数据库[读写分离](https://cnodejs.org/topic/57e4c290bf6e60030ebceed2)

### 原子性,原子性操作

* A想要从自己的帐户中转1000块钱到B的帐户里。那个从A开始转帐，到转帐结束的这一个过程，称之为一个事务。在这个事务里，要做如下操作：
  1. 从A的帐户中减去1000块钱。如果A的帐户原来有3000块钱，现在就变成2000块钱了。
  2. 在B的帐户里加1000块钱。如果B的帐户如果原来有2000块钱，现在则变成3000块钱了。
* 如果在A的帐户已经减去了1000块钱的时候，忽然发生了意外，比如停电什么的，导致转帐事务意外终止了，而此时B的帐户里还没有增加1000块钱。那么，我们称这个操作失败了，要进行回滚。回滚就是回到事务开始之前的状态，也就是回到A的帐户还没减1000块的状态，B的帐户的原来的状态。此时A的帐户仍然有3000块，B的帐户仍然有2000块
* 我们把这种要么一起成功（A帐户成功减少1000，同时B帐户成功增加1000），要么一起失败（A帐户回到原来状态，B帐户也回到原来状态）的操作叫原子性操作。 如果把一个事务可看作是一个程序,它要么完整的被执行,要么完全不执行。这种特性就叫原子性。

### graphql

* [graphql](http://graphql.cn/learn/queries/)

### Database loop in sync

```text
function dataBaseLoop() {
    var returnMsg = '';
    db.serialize(function() {
        db.run('BEGIN TRANSACTION;');
        var length = 10;
        for(var i = 0; i < length; i++) {
            var sql; //sentence
            var k = 0;
            db.run(sql, function(err, rows) {
                if(!err) {
                    k++;
                    //当所有的回调都执行完成时，返回错误
                    if(k == length) {
                        if(returnMsg) {
                            console.log('errMessage:',returnMsg);
                        } else {
                            console.log('成功！');
                        };

                    };
                } else {
                    returnMsg += '[数据：' + data.vals[k] + '新增失败，' + err + ']';
                    k++;
                    if(k == length) {     
                        if(returnMsg) {
                            console.log('errMessage:',returnMsg);
                        } else {
                            console.log('成功！');
                        };
                    };
                };    
            });
        };       
        db.run('COMMIT TRANSACTION;');
    });  
};
```

