### Mybatis理解
  + **JDBC**
    > JDBC（Java DataBase Connectivity,java数据库连接）<br>
      是一种用于执行SQL语句的Java API<br>
      可以为多种关系数据库提供统一访问<br>
      它由一组用Java语言编写的类和接口组成
    + JAVA中连接数据库，处理SQL语句的基本API为JDBC
      > JDBC 的基本处理流程为:
        ![image1](https://github.com/flysafely/JAVA/blob/master/Pictures/mybatis-1.jpg)
    >> ODBC(Open Database Connectivity)开放的数据库连接<br>
       由微软开发出来的一套公共的连接数据库的接口(标准)
  + **Hibernate**
    > 一个全自动的ORM框架(object relational mapping)<br>
      全自动：<br>
        1.使用者不用编写SQL语句<br>
        2.返回结果自动封装成事先指定的类<br>
      缺点：<br>
        1.如果需要定制SQL语句来提高增删改查效率，只能使用其指定的HQL语言来实现
        2.因为其HQL也是需要写在JAVA源码中的，所以具有高耦合性
  + [**Mybatis**](https://mybatis.org/mybatis-3/zh/index.html)
    > 一个半自动的ORM框架<br>
      将**编写SQL**这个环节独立出来称为**配置文件**<br>
      半自动:<br>
        1.可以手动在SQL的XML配置文件中指定返回结果封装类<br>
        2.可以手动在SQL的XML配置文件中配置SQL语句<br>
        3.SQL查询语句和返回结果的封装类指定是写在XML文件中的，跟JAVA源程序不耦合<br>
