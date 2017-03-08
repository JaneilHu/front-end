Asynchronous JavaScript and XML
异步的 JS 和 XML
ajax是一种方法，实现不用刷新页面也可以更新页面上的信息，改变了互联网网页的开发，像百度地图，谷歌地图等都在用。由于XML已经过时，现在大多数都用json。ajax+json极大的简化了开发过程。


Ajax三步骤：  
Asynchronous Javascript And XML
1、运用HTML和CSS实现页面，表达信息；
2、运用XMLHttpRequest和web服务器进行数据的异步交换；
3、运用JavaScript操作DOM，实现动态局部刷新；

1.同步：就是用户填写完信息之后，全部提交给服务器，等待服务器的回应，是一次性全部的。
2.异步：当用户填写完一条信息之后，这条信息会自动向服务器提交，然后服务器响应客户端，在此过程中，用户依然在填写表格的信息，即向服务器请求多次，节省了用户的时间，提高了用户的体验。
3.XMLhttpRequest对象来实现这一功能，也需要javascript来操作DOM实现局部的信息更新。

var request = new XMLHttpRequest();//IE6不支持
var request;
if(window.XMLHttpRequest{
    request=new XMLHttpRequest();
)else
    request=new ActiveXObject("Microsoft.XMLHTTP");//可以兼容IE6、IE5版本

HTTP 是一种无状态协议，请求和响应是没有记忆的
HTTP请求的完整过程：（HTTP1.1起默认长连接）
1，建立 TCP 连接（三次握手）
2，Web 浏览器向 web 服务器发送请求（包括头信息和数据）
3，Web 服务器做出应答（包括应答头信息和数据）
4，服务器关闭 TCP 连接（如果步骤2发送的头信息里包含keep-alive，那么这是一个长连接，服务器不会立马断开 TCP 连接）

步骤2发送的请求：
1.请求的方法：①get：使用 URL传递参数，可以重复的交互，可缓存有历史可被搜索引擎收录，幂等（取数据，跳页面
			②post：一般用于修改服务器上的资源，不可重复的操作，不能被缓存（创建修改一个条目
2.URL：
3.头信息：控制信息
4.请求正文
请求头和请求体之间有个空行，表示头信息结束

HTTP 状态码：
1XX：信息
2XX：成功
3XX：重定向
4XX：客户端请求错误
found：请求中引用的文档不存在
5XX：服务器错误


XMLHttpRequest发送请求

open(method,url,async)
method：规定HTTP发送请求的方式是get还是post,不区分大小写，一般来说用大写
url：请求地址(相对地址或绝对地址)
async:同步/异步(false/true)，默认是异步也就是true，可以不用填写

send(string):讲请求发送到服务器（该参数可以填或者不填-----get方法不填或填null，post:一般要填）

eg：
request.open("GET","get.php",true);
request.send();

request.open("POST","create.php",true);
request.setRequestHeader("Content-type","application/x-www-form-urlencoded ")//设置HTTP头信息--一定要写在open()和send()之间
request.send("name=xxxx&set=xxx");


XMLHttpRequest取得响应

responseText:获得字符串形式的响应数据
responseXML：获得XML形式的响应数据（比较少）
status和statusText:以数字和文本形式返回HTTP状态码 
getAllResponseHeader()：获取所有的响应报头
getResponseHeader()：查询响应中的某个字段的值

readyState属性的变化代表服务器响应的变化
0：请求未初始化，open还没有调用
1：服务器连接已建立，open已经调用了
2：请求已接收，也就是接收到头信息了
3：请求处理中，也就是接收到了响应主体
4：请求已完成，且响应已就绪，也就是响应完成了

eg:
var request = new XMLHttpRequest() //建立XHR对象
request.open("GET","get.php",true); //用get方法异步打开get.php
request.send(); //发送请求头信息
request.onreadystatechange=function(){//通过onreadystatechange事件，对readyState属性进行监听即对服务器的响应进行监听
	if(request.readState===4&&request.status===200){//readyState==4响应完成；status==200请求成功
		request.responseText;//做一些事情，获取服务器响应内容
	}
}
建立异步请求的过程4个步骤：
a:new一个XHR对象
b:调用open方法
c:send一些数据
d:对过程进行监听，来知道服务器是不是正确地做出了响应，接着可以做一些事情
（监听readyState,响应成功可以做一些事情，比如获取服务器响应的内容在页面上做一些呈现）



POST请求传递头信息的时候一定要记得单独设置Content-Type
request.setRequestHeader("Content-Type","application/x-www-form-urlencoded");
