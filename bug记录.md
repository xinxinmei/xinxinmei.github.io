# bug记录

```
Error querying database.  Cause: org.springframework.jdbc.CannotGetJdbcConnectionException: Failed to obtain JDBC Connection; nested exception is java.sql.SQLException: An attempt by a client to checkout a Connection has timed out.
```

- 1.db.properties 配置参数出了问题	2.mysql的jar版本问题

```Invalid bound statement (not found):
org.apache.ibatis.binding.BindingException: Invalid bound statement (not found): com.css.mapper.OrderMapper.findOrder
```

- 1.controller层无法注入service：原因在使用注解@Service时指定了bean的名称@Service（"xxximpl"）名称错误所以@Autowired 无法注入。

- 2.解释：就是说，你的Mapper接口，被Spring注入后，却无法正常的使用mapper.xml的sql；

  ​       这里的Spring注入后的意思是，你的接口已经成功的被扫描到，但是当Spring尝试注入一个代理（MyBatista实现）的实现类后，却无法正常使用。这里的可能发生的情况有如下几种；

  1. 接口已经被扫描到，但是代理对象没有找到，即使尝试注入，也是注入一个错误的对象（可能就是null）
  2. 接口已经被扫描到，代理对象找到了，也注入到接口上了，但是调用某个具体方法时，却无法使用（可能别的方法是正常的）

- 忘记配置<property name="mapperLocations" value="classpath:mapper/*.xml" />

- 解决

  >mapper.xml和对应的java文件我放在了同一个包com.css.mapper下面，在@test中可以调用service层方法可以使用。
  >
  >但是在运行过程中则报上述错误。
  >
  >核心在于没有找到mapper.xml文件
  >
  >个人推测 测试中可以找到，运行则不行。说明两者查找的文件的方式不同
  >
  >随后百度   	mybatis的mapper.xml扫描方法			
  >
  >随后直接 将mapper.xml提出来，放到resources文件下，配置
  >
  ><property name="mapperLocations" value="classpath:mapper/*.xml" />
  >
  >成功解决问题

  

- 思考

  研究spring项目加载文件的过程

   

```
Tests in error: 
  initializationError(user.BaseTest): No runnable methods
```

- 勾选skip test





