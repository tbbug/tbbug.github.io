---
layout: post
title: mysql存储过程重置所有表自增ID
categories: [数据库, mysql,储存过程,truncate]
tags: [sql, mysql,db, truncate,储存过程,自增ID]
status: publish
type: post
published: true
author: blackfox
permalink: /2018/09/07/mysql-truncatereset.html
keyword: sql, mysql,db, truncate,储存过程,自增ID
desc: mysql存储过程重置所有表自增ID，循环执行，清空表数据并重置id。
---
# 利用存储过程清空表数据并重置自增id

#### truncate table table_name;

注意：truncate 一次性地从表中删除所有的数据并不把单独的删除操作记录记入日志保存，删除行是不能恢复的。并且在删除的过程中不会激活与表有关的删除触发器。执行速度快。

##### 是DLL语言，无法回滚；当表被TRUNCATE 后，这个表和索引所占用的空间会恢复到初始大小。

```
select table_name from information_schema.tables where table_schema='mydb' and table_type='base table';
truncate table tpall_wx_fan;

use mydb;#视情况保留
DROP PROCEDURE IF EXISTS FountTable;
delimiter $$
create procedure FountTable()
begin
    declare TableName varchar(64);   
     
    DECLARE cur_FountTable CURSOR FOR SELECT TABLE_NAME FROM information_schema.TABLES WHERE table_schema='mydb' and table_type='base table';
    DECLARE EXIT HANDLER FOR not found CLOSE cur_FountTable;
    #打开游标
    OPEN cur_FountTable;
    REPEAT
     FETCH cur_FountTable INTO TableName;
		 #可执行循环SQL语句
		 SET @SQLSTR1 = CONCAT('truncate table ',TableName);
		 
     PREPARE STMT1 FROM @SQLSTR1;
     EXECUTE STMT1;
      
     DEALLOCATE PREPARE STMT1;    
       
     UNTIL 0 END REPEAT;
  #关闭游标
  CLOSE cur_FountTable;
  
END $$
DELIMITER ;
  
call FountTable();
```

