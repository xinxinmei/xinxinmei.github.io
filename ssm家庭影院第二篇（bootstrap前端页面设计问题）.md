## 前端页面在布局上碰到的问题
### 简单的理解一下bootstrap
* 使用bootStrap过程
   最重要的是bootstrap网格系统，这主要来定义页面的主题框架结构。
 	**核心是row和column**一行里面由12个单位组成，列是定义在行里，在设置列所占的单位时，只要满足和为12即可，一般4：4：4，8：4等等。通过网格系统可以简单的构建出一个一般的结构，至于结构优化，可以通过bootstrap的css属性来定义。

* 所使用的css属性
	class="container-fluid"	//使容器全屏
    
    ```css
    一般用来定义背景
    style=" background-image: url(b1.jpg)  ;
    background-repeat: no-repeat;
    background-position: center 0;
    background-attachment: fixed;
    background-size: cover;"
	```
	```css
	一般用来第一底部居中
	style="position:absolute;
	bottom:0;
	left:50%;
	margin-left:-150px;
	
	```

### 总结
对于前端页面的设计不熟练，主要是在于css样式的不熟，通过这一次简单的设计，对于css的简单运用有了一定理解。例如，div与div之间位置的设计，背景的设置。
	
   
