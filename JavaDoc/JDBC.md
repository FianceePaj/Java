# JDBC

> JDBC是什么？JDBC英文名为：Java Data Base Connectivity(Java数据库连接)，官方解释它是Java编程语言和广泛的数据库之间独立于数据库的连接标准的Java API，根本上说JDBC是一种规范，它提供的接口，一套完整的，允许便捷式访问底层数据库。可以用JAVA来写不同类型的可执行文件：JAVA应用程序、JAVA Applets、Java Servlet、JSP等，不同的可执行文件都能通过JDBC访问数据库，又兼备存储的优势。简单说它就是JAVA与数据库的连接的桥梁或者插件，用JAVA代码就能操作数据库的增删改查、存储过程、事务等。

![img](https://images2015.cnblogs.com/blog/1066658/201702/1066658-20170203195903651-1572602039.png)

## 1.加载驱动&连接建立

加载数据库驱动

```java
//mysql
Class.forName('com.mysql.jdbc.Driver');
//sqlserver
Class.forName('com.microsoft.jdbc.sqlserver.SQLServerDriver');
```

数据库URL

```java
//URL写法
//Oracle：jdbc:oracle:thin:@localhost:1521:database_name
//SqlServer：jdbc:microsoft:sqlserver://localhost:1433; DatabaseName=database_name
//MySql：jdbc:mysql://localhost:3306/database_name
```

连接建立

```java
Connection conn = DriverManager.getConnection(url,userName,password); 
```

## 2.SQL语句执行

### 1.Statement

```java
Statement statement = conn.createStatement();
String sql = "select id,name,password,email from users";
statement = conn.executeQuery(sql);

//executeQuery(String sql) 
//executeUpdate(String sql)
//execute(String sql)  
//addBatch(String sql) 将多条语句放入批处理
//executeBatch()       执行批处理
```

### 2.PreparedStatement

```java
PreparedStatment statement = null;
String sql = "select * from users where id=? and password=?";
//预编译sql
statement = conn.preparedStatement(sql);
statement.setString(1,"zlf");
statement.setString(2,"12345");
statement.executeQuery();
```

可以防止SQL注入的问题。

## 3.结果获取

ResultSet代表了Sql的执行结果

### 1.获取行和列

```java
ResultSet resultSet = statement.executeQuery(sql);
while(resultSet.next()){
    String id = resultSet.getString("id");
    String name = resultSet.getString("name");
}
```

## 4.释放资源

```java
if(resultSet!=null){
    try{
        resultSet.close();
    } catch(Exception e){
        e.printStackTrace();
    }
}
if(statement!=null){
    try{
        statement.close();
    } catch(Exception e){
        e.printStackTrace();
    }
}
if(conn!=null){
    try{
        conn.close();
    } catch(Exception e){
        e.printStackTrace();
    }
}
```

