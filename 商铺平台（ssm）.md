# 开发环境

- eclipse 、jdk1.8 、maven、ssm、redis 、tomcat  

  ## maven项目搭建
- 添加maven依赖工具------maven-compiler-plugin,添加配置指明jdk版本和编码   

- 修改dynamic web moudle 修改，修改.sitting文件  ，同时修改web.xml

  ## 模块设计

- 前端展示（头条，类别，店铺信息，商品信息）
- 店铺和商品都需要支持查找和列表显示
- 店家系统（账号维护、店铺信息维护、权限认证、商品维护）
- 管理员系统（头条信息、权限认证、店铺管理、用户管理）
  ##  实体类
- 区域、用户信息（微信账号、本地账号）、头条、店铺类别、店铺、商品、商品类别
- 区域：id、权重、创建时间、修改时间、名称（datetime范围大于timestamp，timestamp能够自适应时区）
- 用户：id、姓名、头像、邮箱、性别、状态、身份标示、创建时间、修改时间
- 微信账号：id、用户id、创建时间、openid
- 本地账号：id、用户id、用户名、密码、创建时间、修改时间
- 头条：id、权重、状态、名称、链接、图片、创建时间、修改时间
- 店铺类别：id、权重、 上级id、名称、描述、图片、创建时间、修改时间
- 店铺：id、权重、门面照、店名、描述、联系方式、地址、区域id、类别id、用户id、状态、创建时间、修改时间、建议
- 商品类别：类别id、店铺id、名称、权重、创建时间
- 商品图片：图片id、地址、描述、权重、创建时间、商品id
- 商品：id、类别id、名称、描述、缩略图、原价、折扣价、店铺id、状态、修改时间、创建时间、权重
  ## ssm配置
- jdbc.properties
- mybatis：开启useGeneratedKeys、useColumnLable、mapUnderScoreToCamelCase(驼峰命名转换)
- spring-dao：配置数据的properties的属性、数据库连接池、sqlsessionfactory(注入数据库连接池，加载mybatis配置文件)、扫描dao接口包
- spring-service:扫描service包下注解的类型、配置事务管理器、申明基于注解的事务
- spring-mvc:开启注解、配置静态资源、定义视图解析器、扫描web相关的bean（controller）
- web.xml:配置org.springframework.web.servlet.DispatcherServlet(定义初始化参数contextConfiguration)、配置dispatcherservlet的mapping
  ## DispatcherServlet
- 拦截前端的不同请求
  ## logback

  ## dao增加店铺
  ## thumbnails图片处理
  ## SUI MOBLIE 轻量级UI库
  ## kaptcha实现验证码
  ## mysql主从库
- master将数据操作记录到二进制日志文件（binary log），slave读取binary log
  事件，写入到relay log中，slave 重新执行事件
- abstractroutingdatasource中的determinecurrentlookupkey方法