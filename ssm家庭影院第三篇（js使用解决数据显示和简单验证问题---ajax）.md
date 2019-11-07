## 验证问题
* 这里注意的是表单提交的问题，1.在form设置属性onsubmit=“return check（）”
	2 .在js代码中调用form.submit()
	**js完成的只是简单的验证，当数据传入后端时还是需要进行细化的验证。**
```javascript
function checkUname(){
    var unameInput=document.getElementById("inputEmail3");
    var span=unameInput.nextElementSibling;
	
    var inputEmail3=unameInput.value;
	if(!unameInput.value.length<1){
	if(!unameInput.validity.valid){
          span.innerHTML="邮箱格式不正确";
          span.className="msg-error";
      }else{
          span.innerHTML="邮箱格式正确";
          span.className="msg-success";
		  /*$.ajax({
            url:'../user/checkUname.do',
            type:'get',
            data:'uname='+uname,
            success:function(result) {
                if(result=='no'){
                    span.innerHTML="该用户名已被占用";
                    span.className="msg-error";
                }else{
                    span.innerHTML="合法的用户名";
                    span.className='msg-success';
                }
            }
        });*/
      }
	  }
  }

  function checkUpwd(){
      var upwdInput1=document.getElementById("inputPassword3");
	  var upwdInput2=document.getElementById("inputPassword4");
      var span=upwdInput2.nextElementSibling;
      var upwd1=upwdInput1.value;
	  var upwd2= upwdInput2.value ;
      if(!upwd1.length<1){
	  if(upwd1!=upwd2){
          span.innerHTML="两次密码不一致";
          span.className="msg-error";
      }else{
          span.innerHTML="密码格式正确";
          span.className="msg-success";
      }
	  }
  }
  function regist(){
    var spans=document.getElementsByClassName("msg-success");
    console.log(spans.length);
    if(spans.length<2){
      alert("注册资料不完整，请填写完整！");
	  return false ;
    }else{
		return true ;
      //alert("ok");
    }
```
## ajax数据请求数据问题
```javascript
$(
	function(){
		$.ajax({
			url:"1.json",
			type:"get",
			data:{
				pageCurrent:pageCurrent ,
			}
			dataType:"json",
			success:function(data){
				alert(data);
			},
		error:function(xhr){
			alert("错误提示： " + xhr.status + " " + xhr.statusText);
		},
		}
			
		)
	}
	);
```
## 数据显示问题，js生成页面
* 主要的使字符串的拼接问题
```javascript
function page() {
	html='<div class="col-sm-6 col-md-6 col-lg-3" >\
                      <div class="text-center">\
                        <a href=""><img style="" src="m.jpg" /></a>\
                          <div class="movie-name">\
                            <span class="movie-name-text"><a href="">肖申克的救赎</a></span>\
                            <div>\
                              <span>1994 / 美国 / 犯罪 / 剧情</span>\
                            </div>\
                            <div class="movie-rating">\
                              <span class="rating_num">9.7</span>\
                            </div>\
                          </div>\
                      </div>\
                    </div>';
	document.getElementById("result").innerHTML=html;
}
```
## 分页显示问题
* 主要问题使解决分页区域，相应的页码变化，和如何触发相应的事件
```javascript
<dl class="test_001">
         <p style="float:right;">每页9条记录  总共<span id="mlen"></span>条记录
         <a href="javascript:page(0)">首页</a>
         <a href="javascript:page(pageIndex-1)">上一页</a>
         <a href="javascript:page(pageIndex+1)">下一页</a>
         <a href="javascript:page(datar.llength-1)">尾页</a>
         </p>
 </dl>
```
