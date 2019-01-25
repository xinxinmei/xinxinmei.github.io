# js实现父窗口和子窗口传递数据

1.test.html
	
```html(type)
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>父窗口</title>
<script>
function son(){//打开子窗口
	s=window.open("son.html")
}
function close_son(){//关闭子窗口
	if(s){
		s.close();
		s=null;
	}
}
</script>
</head>
<body>
<textarea id="text"></textarea><br>
<input type="button" value="打开子窗口"  onclick="son()"><br>
<input type="button" value="关闭子窗口" onclick="close_son()">
</body>
</html>
```

2.son.html
```swift
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>子窗口</title>
<script>
function request(){
	 var t=document.getElementById('input1').value;//获取id为input1的值
	 window.opener.document.getElementById('text').innerHTML=t;//使父窗口里id为text的区域显示t的值
}
</script>
</head>
<body>
<input type="text" id="input1"><br>
<input type="button" value="提交数据" onclick="request()"><br>
</body>
</html>
```
## 创建子窗口的方法
* 直接内嵌于标签内（不通过js实现）
``<input type="text" id="" value="" onclick="new=open("son.html","sm","")">``
## 关闭子窗口的方法

``<input type="text" onclick="new.close()">``

### 关于js中一些方法的理解
  * document.getElementById("id")的到是一个object（对象），需要得到值还需要使用.value,相关的方法请学习[W3C](http://www.w3school.com.cn/html/index.asp)
  
初学如有错误希望指出
