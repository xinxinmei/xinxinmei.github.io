## 数据传输
* 	涉及传输的pojo，定义在common中，因为service和web都需要使用。  
	pojo需要实现serializable接口，实现序列化。

## debug
*	debug模式启动，需要加上源代码（debug configuration 设置resource----add-----javaproject选择相应的maven项目）  
	service注解是否存在———— scan扫描包———— ref名字是否错误———— web.xml是否加载配置文件

## 添加功能
*	弹框：返回一个div。两个div嵌套，外围设置灰色半天透明，内部为弹框内容，实现弹框效果  
	jquery绑定形式id或者class。   
	利用pojo接受表单，

## tree
* 	基于easyUi的tree（id,text,status--是否有子节点），数据库设置可以设计parent标志定义父节点。   
	根据parentid查询到直接子节点。  
  	controller中可以使用requestparam定name 和default值。

## 上传图片
* 	比起传统的单个项目，集群对于资源文件需要建立单独的资源服务器存储资源。  
	上传：用户----服务器------资源服务器  
  	访问：用户————资源服务器  
  	资源服务器fastDFS实现分布式，提供高可用可扩展。  
	responsebody注解，响应数据（注意浏览器兼容性问题）

## 富文本编辑器
* 	ueditor kindeditor ckeditor  
	页面引入相应的js和css—— 创建textarea控件（初始化控件）——  调用相应方法创建富文本编辑器（指定id）——  同步textarea内容提交   
	
## 	id
*	时间戳，redis
	价格可以使用分为单位，避免浮点运算

## 展示页面
*	配置mapping设置伪静态化，过滤规则**.html*

## solr
*	索引库添加的是变化性小的字段

