## 限定查询

1. 关系运算 

   ```
   > < >= <= != <> =
   ```

2. 范围判断

   ```
   BETWEEN AND

   ```

3. 判断是否为空

   ```
   IS NULL
   IS NOT NULL

   ```

4. 指定范围的判断

   ```
   IN
   NOT IN
   ```

5. 模糊查询

   ```
   LIKE
   NOT LIKE
   匹配单个字符：_ 
   匹配任意多个字符：%
   ```

```
SELECT * 
FROM 表名称 [别名]
WHERE 条件
```

## 排序

order by  ASC默认升序 DESC降序

查询出所有的雇员信息，按照工资由高到低排序，如果工资相同，则按照雇佣日期由早到晚排序,此时肯定需要两个字段排序：工资（DESC），雇佣日期（ASC）

````
SELECT * 
FROM emp 
ORDER BY sal DESC, hiredate ASC
````



## 使用函数查询

upper, lower replace 替换 

```
SELECT lower(ename)
FROM  emp

SELECT REPLACE(ename, 's', '*') FROM emp
```

substr

````
SUBSTR(字符串 | 列，开始点, 长度)
SELECT ename,SUBSTR(ename,-2) FROM emp
````

## 多表查询

等值连接

```
SELECT *
FORM 表1,表2
WHERE 表1.列名=表2.列名;

SELECT *
FORM 表1 [INNER] JION 表2 
		ON 表1.列名=表2.列名;
```

左外连接

```
SELECT * 
FROM 表1 LEFT OUTER JION 表2
ON(表1.列名= 表2.列名)|
USING(列名(同名同类型))
```

右外连接 RIGHT OUTER JION

全外连接  FULL OUTER JOIN

自连接 SELF JOIN

```
SELECT e.ENAME,e.MGR,e.EMPNO,m.ENAME
FROM EMP e,EMP m
WHERE e.MGR = m.EMPNO
```

## 分组统计查询

统计: sum count max min avg

```
SELECT [DISTINCT] *|分组字段1 [别名] [,分组字段2 [别名] ,…] | 统计函数

FROM 表名称 [别名], [表名称 [别名] ,…]

[WHERE 条件(s)]

[GROUP BY 分组字段1 [,分组字段2 ,…]]

[ORDER BY 排序字段 ASC | DESC [,排序字段 ASC | DESC]];
```

按照部门编号分组，求出每个部门的人数，平均工资

````
SELECT deptno, COUNT(empno), AVG(sal)
FROM emp
GROUP BY deptno
````

mysql四种搜索引擎

```
MySQL常用的四种引擎的介绍
（1）：MyISAM存储引擎：不支持事务、也不支持外键，优势是访问速度快，对事务完整性没有 要求或者以select，insert为主的应用基本上可以用这个引擎来创建表
支持3种不同的存储格式，分别是：静态表；动态表；压缩表
静态表：表中的字段都是非变长字段，这样每个记录都是固定长度的，优点存储非常迅速，容易缓存，出现故障容易恢复；缺点是占用的空间通常比动态表多（因为存储时会按照列的宽度定义补足空格）ps：在取数据的时候，默认会把字段后面的空格去掉，如果不注意会把数据本身带的空格也会忽略。
动态表：记录不是固定长度的，这样存储的优点是占用的空间相对较少；缺点：频繁的更新、删除数据容易产生碎片，需要定期执行OPTIMIZE TABLE或者myisamchk-r命令来改善性能
压缩表：因为每个记录是被单独压缩的，所以只有非常小的访问开支

（2）InnoDB存储引擎*
该存储引擎提供了具有提交、回滚和崩溃恢复能力的事务安全。但是对比MyISAM引擎，写的处理效率会差一些，并且会占用更多的磁盘空间以保留数据和索引。 
InnoDB存储引擎的特点：支持自动增长列，支持外键约束

(3)：MEMORY存储引擎
Memory存储引擎使用存在于内存中的内容来创建表。每个memory表只实际对应一个磁盘文件，格式是.frm。memory类型的表访问非常的快，因为它的数据是放在内存中的，并且默认使用HASH索引，但是一旦服务关闭，表中的数据就会丢失掉。 
MEMORY存储引擎的表可以选择使用BTREE索引或者HASH索引，两种不同类型的索引有其不同的使用范围
Hash索引优点： 
Hash 索引结构的特殊性，其检索效率非常高，索引的检索可以一次定位，不像B-Tree 索引需要从根节点到枝节点，最后才能访问到页节点这样多次的IO访问，所以 Hash 索引的查询效率要远高于 B-Tree 索引。 
Hash索引缺点： 那么不精确查找呢，也很明显，因为hash算法是基于等值计算的，所以对于“like”等范围查找hash索引无效，不支持；
Memory类型的存储引擎主要用于哪些内容变化不频繁的代码表，或者作为统计操作的中间结果表，便于高效地对中间结果进行分析并得到最终的统计结果，。对存储引擎为memory的表进行更新操作要谨慎，因为数据并没有实际写入到磁盘中，所以一定要对下次重新启动服务后如何获得这些修改后的数据有所考虑。

（4）MERGE存储引擎
Merge存储引擎是一组MyISAM表的组合，这些MyISAM表必须结构完全相同，merge表本身并没有数据，对merge类型的表可以进行查询，更新，删除操作，这些操作实际上是对内部的MyISAM表进行的。
```

