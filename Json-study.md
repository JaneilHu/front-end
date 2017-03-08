JSON基本概念：
JSON：javaScript对象表示法（JavaScript Object Notation）
JSON是存储和交换文本信息的语法，类似XML。它采用键值对的方式来组织，易于人们阅读和编写，同时也易于机器解析和生成
JSON是独立于语言的，也就是说不管什么语言，都可以解析json，只需要按照json的规则来就行

JSON和XML比较：
短小,读写的速度快,可以使用JavaScript内建的方法直接进行解析后转换成JavaScipt对象

JSON语法规则：
1.数据格式：
名称/值对
都用双引号括起来，中间冒号分割；例如："name":"郭靖"
2.值类型：
数字（整数和浮点数）
字符串（在双引号中）
逻辑值（true或false）
数组（在方括号中[]）
对象（在花括号中{}）
null

eg:
{
  "staff":[
     {"name":"洪七","age":"73"},
     {"name":"郭靖","age":"35"},
     {"name":"黄蓉","age":"30"}
  ]
}

JOSN解析的方法：
1.eval（eg:var jsondata=...;var jsonobj=eval('('+jsondata+')')）
2.JSON.parse（eg:var jsondata=...;var jsonobj=JSON.parse(jsondata)）
区别：eval方法不会检验join的格式是否正确，会把里面的一些JS方法也一并执行，而JSON.parse在解释JSON时会先检验JOIN的格式，如果格式不对，会报错，而且不会执行JSON里面的JS方法。一般用JSON.parse。jsonlint.com(一个在线检验JOSN语法是否正确的网站)

