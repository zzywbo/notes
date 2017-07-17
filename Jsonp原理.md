# Jsonp原理
- 首先在客户端注册一个callback (如:'jsoncallback') 

- 然后把callback的名字(如:jsonp1236827957501)传给服务器。 此时，服务器先生成 json 数据。

- 然后以 javascript 语法的方式，生成一个function , function 名字就是传递上来的参数 'jsoncallback'的值 jsonp1236827957501 .

- 最后将 json 数据直接以入参的方式，放置到 function 中，这样就生成了一段 js 语法的文档，返回给客户端。

- 客户端浏览器，解析script标签，并执行返回的 javascript 文档，此时javascript文档数据,作为参数， 传入到了客户端预先定义好的 callback 函数。

## 注意： 
**jsonp回调函数，jsonpCallback必须为全局函数，因为jsonp返回的是在全局环境中执行函数的语句，即jsonpCallback(data)** 

- 如被封装在其他函数中，可以  

		function a(){
	     window.jsonpCallback=function(data){ 
    	 ...... 
    	 }
		}


## Eg： 
 

	<script type="text/javascript">
	    function jsonpCallback(result) {
	        alert(result.msg);
	    }
	</script>
	<script type="text/javascript" src="http://crossdomain.com/jsonServerResponse?jsonp=jsonpCallback"></script>  


其中 jsonCallback 是客户端注册的，获取跨域服务器上的json数据后，回调的函数。

	http://crossdomain.com/jsonServerResponse?jsonp=jsonpCallback 

这个 url 是跨域服务器取 json 数据的接口，参数为回调函数的名字，返回的格式为:

	jsonpCallback({ msg:'this  is  json  data'})  


## 在jquery 中的应用：  
  ```
	<!DOCTYPE html>
 	<html>
	<head>
	<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
	<title>Demo</title>
	<script type="text/javascript" src="jquery.js"></script>
	<script type="text/javascript">
	function do_jsonp() {
  	 $.getJSON("http://demo.hpyer.cn/php/jsonp.php?type=json&callback=?",
   	function(data) {
   	$('#result').val('data.Image.IDs: ' + data.Image.IDs);
   	});
	}
	</script>
	</head>
	<body>
	<a href="javascript:do_jsonp();">Click me</a><br />
	<textarea id="result" cols="50" rows="5"></textarea>
	</body>
	</html>
    ```