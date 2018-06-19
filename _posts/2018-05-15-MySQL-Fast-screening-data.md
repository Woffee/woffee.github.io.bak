---
layout: post
title:  "开发笔记 - MySQL 快速筛选出未关联的数据"
date:   2018-05-15 11:29:00 +0800
categories: mysql
---

### 方法一（写法较简单）

出于性能考虑，如果SQL语句过于复杂，我们要把它拆分成多个简单的语句。

比如：

1.先查出id范围（ids）

2.然后再这样写：

	select * from `table` where id in ( ids ) 

如果要筛选出“未关联”的数据，可以写成：

	select * from `table` where id not in ( ids )



### 方法二（效率较高）

但是这种写法遇到 ids 很多，上万条的时候，速度就很慢了。针对这种情况，可以使用 not exists :

	select * from `table` where not exists (
		select 1 from `otherTable` where `table`.id = `otherTable`.table_id
		)



### 方法三（效率最高，需要额外字段）

还有一种方法，在`table`表中建立一个字段“isRelated”，0代表未在`otherTable`关联，1代表有关联。然后就可以直接这样写：

	select * from `table` where `isRelated` = 0

这种方法需要在修改 `otherTable` 表的时候同步更新 isRelated 值。
