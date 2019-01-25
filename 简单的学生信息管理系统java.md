# 简单的学生信息管理系统java



## 简单的构思

1.首先需要的是数据库的操作（MySQL）和简单的逻辑实现比如查找、删除、更新、插入。对于这些逻辑可以进行细分例如如何查找和查找的方式，本人此次主要的是想熟悉数据库的操作所以对与逻辑这一部分只是进行 了简单的实现。

2.数据库操作的必备知识点和相关类的使用，首先需要添加相应的驱动程序，需要自行下载添加。

3.涉及相关的语法：

* jdbc的连接url： jdbc:mysql://localhost:3306/数据名
* Class.forName("com.mysql.cj.jdbc.Driver")
* PreparedStatement、DriverManager、Connection类的使用(不懂的可以查阅jdk文档)

## 实际操作

* 建立好数据库的操作类





```java
package student;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
public class Connect{
	private Connection con=null;	//创建Connection对象
	PreparedStatement statement=null;//创建PreparedStatement对象
	public Connection getCon() {
		return this.con;
	}
	public void connectData(){//建立连接
		
		try{
			Class.forName("com.mysql.cj.jdbc.Driver");//加载jdbc驱动程序
		}catch(ClassNotFoundException e){
			System.out.println("操作失败！");
			e.printStackTrace();
		}
		try{
			con=DriverManager.getConnection("jdbc:mysql://localhost:3306/winter?&serverTimezone=GMT","root","111");//建立数据库连接
		}catch(SQLException e){
			System.out.println("操作失败！");
			e.printStackTrace();
		}
		
	}
	public void insertData(String sql) {//插入数据
		try {
			statement = con.prepareStatement(sql);
			statement.executeUpdate();
		}catch(SQLException e) {
			System.out.println("操作失败！");
			e.printStackTrace();
		}
		
	}
	public void updateData(String sql) {//更新数据
		try {
			statement = con.prepareStatement(sql);
			statement.executeUpdate();
		}catch(SQLException e) {
			System.out.println("操作失败！");
			e.printStackTrace();
		}
		
	}
	public void deleteData(String sql) {//删除数据
		try {
			statement = con.prepareStatement(sql);
			statement.executeUpdate();
		}catch(SQLException e) {
			System.out.println("操作失败！");
			e.printStackTrace();
		}	
		
	}
	public void selectData(String sql) {查询数据
		try {
			statement = con.prepareStatement(sql);
			ResultSet rs=statement.executeQuery(sql);
			while(rs.next()) {
				System.out.println("姓名："+rs.getString("name")+"\n学号："+rs.getString("num")+"\n专业"+rs.getString("major")+"\n班级："+rs.getString("grade")+"\n年龄："+rs.getString("age"));
			}
		}catch(SQLException e) {
			System.out.println("操作失败！");
			e.printStackTrace();
		}
	}
	
}
```

理解prepareStatement()和executeUpdate()、executeQuery()



* 建立简单的逻辑类

``````java
package student;

import java.sql.SQLException;
import java.util.Scanner;

public class Menu {
	Connect con = new Connect();		//建立连接对象
	
	public static void main(String[] args) {
		Menu m = new Menu();
		boolean flag=true;
		int select = 0;
		
		while(flag) {
			m.menu();
			Scanner s = new Scanner(System.in);
			select = s.nextInt();
			switch(select) {
				case 1 :
					m.select();
					break;
				case 2 :
					m.insert();
					break;
				case 3 :
					m.update();
					break;
				case 4 :
					m.delete();
					break;
				case 5 :
					System.exit(0);
					break;
				default:
					System.out.println("命令错误！");
					break;
			
			}
			
		}
		
	}
	public void menu() {
		System.out.println("1.查询");
		System.out.println("2.插入");
		System.out.println("3.更新");
		System.out.println("4.删除");
		System.out.println("5.退出");
	}
	public void select() {			//简单的查找
		//System.out.println("select");
		System.out.println("请输入学号：");
		Scanner s = new Scanner(System.in);
		String n=s.nextLine();
		String sql="select * from student where num="+n;
		con.connectData();
		con.selectData(sql);
		try {
			con.getCon().close();
		}catch(SQLException e) {
			e.printStackTrace();
		}
	}
	public void insert() {			//简单的插入
		//System.out.println("insert");
		System.out.println("输入姓名、学号、专业、班级、年龄：");
		Scanner s = new Scanner(System.in);
		String n = s.nextLine();
		String[] a = n.split(" ");
		String sql="insert into student values("+"'"+a[0]+"'"+","+"'"+a[1]+"'"+","+"'"+a[2]+"'"+","+"'"+a[3]+"'"+","+"'"+a[4]+"'"+")";
		con.connectData();
		con.insertData(sql);
		try {
			con.getCon().close();
		}catch(SQLException e) {
			e.printStackTrace();
		}
	}
	public void update() {			//简单更新
		//System.out.println("update");
		System.out.println("输入修改的学号");
		Scanner s = new Scanner(System.in);
		String n = s.nextLine();
		System.out.println("输入修改后的姓名：");
		Scanner s1 = new Scanner(System.in);
		String  n1 = s1.nextLine();
		String sql="update student set name="+"'"+n1+"'"+"where num="+"'"+n+"'";

		con.connectData();
		con.insertData(sql);
		try {
			con.getCon().close();
		}catch(SQLException e) {
			e.printStackTrace();
		}
	}
	public void delete() {			//简单删除
		//System.out.println("delete");
		System.out.println("输入删除的学号：");
		Scanner s = new Scanner(System.in);
		String n = s.nextLine();
		String sql="delete from student where num="+"'"+n+"'";
		con.connectData();
		con.deleteData(sql);
		try {
			con.getCon().close();
		}catch(SQLException e) {
			e.printStackTrace();
		}
	}
	
	                                    
}

``````

在逻辑上我只是实现了简单的操作，可以更加详细话



### 小结

* 在进行一些操作时要注意异常处理（查看jdk文档）
* 结束操作后记得关闭连接
* **注意sql字符串的组成**



*文章如有错误欢迎指出，技术有限，如有带来困扰，敬请谅解！谢谢*