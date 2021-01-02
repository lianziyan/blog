---
title: 超实用的SQL语句之嵌套查询
tags:
  - MySQL
  - MyBatis
  - SQL技巧
categories:
  - 博客园博文
  - mybatis
top_img: 'https://cdn.jsdelivr.net/gh/glassy-sky-lisong/StaticFile1@master/top-img/1.jpg'
cover: >-
  https://cdn.jsdelivr.net/gh/glassy-sky-lisong/StaticFile1@master/post-cover/2.png
abbrlink: f3908263
date: 2020-08-31 19:40:33
---

<h2>嵌套查询</h2>
<h3>什么是嵌套查询</h3>.
 　　嵌套查询的意思是，一个查询语句(select-from-where)查询语句块可以嵌套在另外一个查询块的where子句中，称为嵌套查询。其中外层查询也称为父查询，主查询。内层查询也称子查询，从查询。
<h3>嵌套查询的工作方式</h3>
 　　先处理内查询，由内向外处理，外层查询利用内层查询的结果嵌套查询不仅仅可以用于父查询select语句使用。还可以用于insert、update、delete语句或其他子查询中。

<h2>子查询的组成</h2>
 1、包含标准选择列表组件的标准select查询。

 2、包含一个或多个表或者视图名称的标准from子句。

 3、可选的where子句。

 4、可选的group by子句。

 5、可选的having子句。
<h2>子查询的语法规则</h2>
 1、子查询的select查询总是使用圆括号括起来。

 2、不能包括compute或for.browse子句。

 3、如果同时指定top子句，则可能只包括order by子句。

 4、子查询最多可以嵌套到32层。个别查询可能会不支持32层嵌套。

 5、任何可以使用表达式的地方都可以使用子查询，只要它返回的是单个值。

 6、如果某个表只出现在子查询中二不出现在外部查询中，那么该表的列就无法包含在输出中。
<h2>简单子查询</h2>
<strong>示例：</strong>

    
    select name,age from person 
    where age > 
        (
            select age from person 
            where name = '孙权'
        )
    
<strong>输出结果为：</strong>
<img src="https://cdn.jsdelivr.net/gh/glassy-sky-lisong/StaticFile1@master/post/4.jpg" alt="1">
<h2>in嵌套查询</h2>
 　　in关键字用于where子句中用来判断查询的表达式是否在多个值的列表中。返回满足in列表中的满足条件的记录。

<strong>示例：</strong>

    select name from person 
    where countryid in 
    (
    select countryid from country
    where countryname = '魏国'
    )

<strong>输出结果为：</strong>

<img src="https://cdn.jsdelivr.net/gh/glassy-sky-lisong/StaticFile1@master/post/3.jpg" alt="2">
<h2>some嵌套查询</h2>
<h3>语法</h3>
 　　some在sql中的逻辑运算符号，如果在一系列比较中，有些值为True，那么结果就为True。some的语法是：

    <表达式>{ =|<>|!=|>|>=|!>|<|<=|!<}some(子查询)

<strong>示例：</strong>

    select name from person 
    where countryid = some 　　　　　　--用等号和以下查询到的值比较，如果与其中一个相等，就返回
    (
    select countryid from country
    where countryname = '魏国'
    )

<strong>输出结果为：</strong>
<img src="https://cdn.jsdelivr.net/gh/glassy-sky-lisong/StaticFile1@master/post/2.jpg" alt="3">
<h2>all嵌套查询</h2>
 　　all是sql中的逻辑运算符好，如果一系列的比较都为true，那么结果才能为true。
<h3>语法</h3>

    <表达式>{ =|<>|!=|>|>=|!>|<|<=|!<}all(子查询)

<strong>示例：</strong>

    select name from person 
    where countryid > all　　 --当countryid大于以下返回的所有id，此结果才为True，此结果才返回
    (
    select countryid from country
    where countryname = '魏国'
    )

<strong>输出结果为：</strong>
<img src="https://cdn.jsdelivr.net/gh/glassy-sky-lisong/StaticFile1@master/post/1.jpg" alt="4">
<h2>exists嵌套查询</h2>
<h3>语法</h3>
 　　exists是sql中的逻辑运算符号。如果子查询有结果集返回，那么就为True。exists代表“存在”的意义，它只查找满足条件的那些记录。<span style="color:red">一旦找到第一个匹配的记录后，就马上停止查找。</span>

    exists　子查询

 　　其中子查询是一个首先的select语句，不允许有compute子句和into关键字。
exists 的意思是，子查询是否有结果集返回。
<strong>例如：</strong>

    SELECT * FROM Person
    WHERE exists
    (
    SELECT 1      --SELECT 0  SELECT NULL 返回结果都一样，因为这三个子查询都有结果集返回，因此总是True  SELECT * FROM Person照常执行
    )

 　　但是如果子查询中因为加了条件而没有结果集返回，则主语句就不执行了：

    SELECT * FROM Person
    WHERE exists
    (
    SELECT * FROM Person 
    WHERE Person_Id = 100    --如果不存在Person_Id的记录，则子查询没有结果集返回，主语句不执行
    )

最后感谢<a href="https://www.cnblogs.com/kissdodog/archive/2013/06/03/3116284.html">不玩博客了！</a>同学的分享，么么哒！
