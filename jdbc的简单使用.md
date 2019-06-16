## jdbc的简单使用
### Connection 、PreparedStatement、ResultSet类的使用
```java
Class.forName("Oracle.jdbc.OracleDriver");
Connection con = DriverManager.getConnection("jdbc:oracle:thin:@localhost:1521:ex","system","123456");
PreparedStatement pre = con.prepareStatment(SQL);
ResultSet rs = pre.executeQuery();
```
connection类：建立连接
preparedstatement类：预编译sql语句
resultset类：获取执行结果集

### .properties文件的使用
   为了不重复输入driver，url等相关参数
```java
Properties p = new  Properies();
BufferedReader buff = new BufferedReader(new FileReader(path));
p.load(buff);
p.getProperty(name);
```

### dbcp连接池

```java
DataSource ds = new BasicDataSource();
		ds.setUrl("jdbc:oracle:thin:@localhost:1521:xe");
		ds.setDriverClassName("oracle.jdbc.OracleDriver");
		ds.setUsername("system");
		ds.setPassword("123456");
		ds.setInitialSize(10);
		ds.setMaxActive(8);
		Connection con=ds.getConnection()
```