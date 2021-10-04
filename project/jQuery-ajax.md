# Jquery的ajax

## 1.$.ajax()

jquery调用ajax方法：

格式：$.ajax({});

参数：

1. type：请求方式GET/POST
2. url：请求地址url
3. async：是否异步，默认是true表示异步
4. data：发送到服务器的数据
5. dataType：预期服务器返回的数据类型
6. contentType：设置请求头
7. success：请求成功时调用此函数
8. error：请求失败时调用此函数

get请求

```JavaScript
  $.ajax({    
    type:"get",    
    url:"../js/cuisine_area.json",    
    async:true,    
    success : function (msg) {      
      var str = msg;      
      console.log(str)      
      $('div').append("<ul></ul>");      
      for(var i=0; i<msg.prices.length;i++){        
        $('ul').append("<li></li>")         
        $('li').eq(i).text(msg.prices[i])      
      }    
    },    
    error : function (errMsg) {      
      console.log(errMsg);      
      $('div').html(errMsg.responseText)
    }  
  });   
```

post请求

```JavaScript
  $.ajax({    
    type:"post",    
    data:"name=tom",    
    url:"../js/cuisine_area.json",    
    contentType: "application/x-www-form-urlencoded",    
    async:true,    
    success : function (msg) {      
      var str = msg;      
      console.log(str)      
      $('div').append("<ul></ul>");      
      for(var i=0; i<msg.prices.length;i++){        
        $('ul').append("<li></li>")        
        $('li').eq(i).text(msg.prices[i])      
      }    
    },    
    error : function (errMsg) {      
      console.log(errMsg);      
      $('div').html(errMsg.responseText)    
    }  
  });
```

 

## 2.$.get()

这是一个简单的 GET 请求功能以取代复杂 $.ajax 。

  请求成功时可调用回调函数。如果需要在出错时执行函数，请使用 $.ajax。

1.请求json文件，忽略返回值  

```JavaScript
$.get('../js/cuisine_area.json');  
```

2.请求json文件，传递参数，忽略返回值     

```JavaScript
$.get('../js/cuisine_area.json',{name:"tom",age:100}); 
```

3.请求json文件,拿到返回值,请求成功后可拿到返回值  

```JavaScript
$.get('../js/cuisine_area.json',function(data){    
  console.log(data)  
});    
```

4.请求json文件,传递参数,拿到返回值   

```JavaScript
$.get('../js/cuisine_area.json',{name:"tom",age:100},function(data){    
  console.log(data)  
});   
```

## 3.$.post()

这是一个简单的 POST 请求功能以取代复杂 $.ajax 。

请求成功时可调用回调函数。如果需要在出错时执行函数，请使用 $.ajax。

  1.请求json文件，忽略返回值 

 $.post('../js/cuisine_area.json');          

```JavaScript
 $.post('../js/cuisine_area.json');
```

  2.请求json文件，传递参数，忽略返回值  

```JavaScript
$.post('../js/cuisine_area.json',{name:"tom",age:100});
```

  3.请求json文件,拿到返回值,请求成功后可拿到返回值 

```JavaScript
$.post('../js/cuisine_area.json',function(data){
  console.log(data)
});
```

  4.请求json文件,传递参数,拿到返回值  

```JavaScript
$.post('../js/cuisine_area.json',{name:"tom",age:100},function(data){    
  console.log(data)  
});  
```



## 4.$.getJSON()

表示请求返回的数据类型是JSON格式的ajax请求

 

## 5.jsonp

远程跨域时，如果有两个域名，从其中一个域名去访问另一个域名时，使用普通的ajax方法是获取不到数据的，那么就可以使用jsonp方式发送请求。

添加属性：

jsonp:‘callback’

dataType:‘jsonp’

```JavaScript
  $.ajax({    
    type:"post",    
    url:"http://iservice.itshsxt.com/restaurant/find",    
    dataType : 'jsonp',    
    jsonp:"callback",    
    success : function (msg,status) {      
      if(status == "success"){        
        var res = msg.result;        
        $('div').append("<ul></ul>");        
        for(var i=0; i<res.length;i++){         
          $('ul').append("<li></li>")           
          $('li').eq(i).text(res[i].name)         
        }      
      }else {        
        alert("请求失败,错误信息：" + msg);      
      }    
    },    
    error : function (errMsg,sta) {      
      console.log(errMsg.message)    
    }  
  });  
```

