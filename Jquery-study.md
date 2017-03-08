使用 Google 的 CDN
<head>
<script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs
/jquery/1.4.0/jquery.min.js"></script>
</head>
使用 Microsoft 的 CDN
<head>
<script type="text/javascript" src="http://ajax.microsoft.com/ajax/jquery
/jquery-1.4.min.js"></script>
</head>


$(document).ready(function(){

--- jQuery functions go here ----

});






鼠标事件，若用$ele.mouse事件( [eventData ], handler(eventObject) )传递数据的话，数据只传递一次。
mouseenter相当于在封装的时候对mouseover进行阻止冒泡

hover()这个方法里头封装的是mouseenter(), mouseleave()两个方法, 可以阻止冒泡问题. 这个方法可以用来改变样式, 比如鼠标移入div变色, 移出回到以前的颜色. 相当于css中的div:hover, 但是:hover很多的浏览器对a:hover支持还不错, 对div:hover, ul:hover支持有点差, 特别是ie6,ie7这些较低的版本. 用jquery可以解决兼容性,代码量比js要少很多, 可以专注在逻辑业务上.

focus与blur事件：不支持冒泡，focusin与focusout支持冒泡

on最大的用处，事件代理
可以利用冒泡，在指定元素内的元素绑定事件，取代之前的live方法
on的委托机制
.on( events ,[ selector ] ,[ data ], handler(eventObject) )可阻止冒泡（多个事件引号里用空格隔开）
$("elem").off()所有时间全部销毁




event.type：获取事件的类型

触发元素的事件类型

$("a").click(function(event) {
  alert(event.type); // "click"事件
});
event.pageX 和 event.pageY：获取鼠标当前相对于页面的坐标

通过这2个属性，可以确定元素在当前页面的坐标值，鼠标相对于文档的左边缘的位置（左边）与 （顶边）的距离，简单来说是从页面左上角开始,即是以页面为参考点,不随滑动条移动而变化

event.preventDefault() 方法：阻止默认行为

这个用的特别多，在执行这个方法后，如果点击一个链接（a标签），浏览器不会跳转到新的 URL 去了。我们可以用 event.isDefaultPrevented() 来确定这个方法是否(在那个事件对象上)被调用过了

event.stopPropagation() 方法：阻止事件冒泡

事件是可以冒泡的，为防止事件冒泡到DOM树上，也就是不触发的任何前辈元素上的事件处理函数

event.which：获取在鼠标单击时，单击的是鼠标的哪个键

event.which 将 event.keyCode 和 event.charCode 标准化了。event.which也将正常化的按钮按下(mousedown 和 mouseupevents)，左键报告1，中间键报告2，右键报告3

event.currentTarget : 在事件冒泡过程中的当前DOM元素

冒泡前的当前触发事件的DOM对象, 等同于this.

this和event.target的区别：

js中事件是会冒泡的，所以this是可以变化的，但event.target不会变化，它永远是直接接受事件的目标DOM元素；

.this和event.target都是dom对象

如果要使用jquey中的方法可以将他们转换为jquery对象。比如this和$(this)的使用、event.target和$(event.target)的使用；


mousedown、click、keydown等等这类型的事件都是浏览器提供的，通俗叫原生事件


triggerHandler与trigger的用法是一样的，重点看不同之处：
triggerHandler不会触发浏览器的默认行为，.triggerHandler( "submit" )将不会调用表单上的.submit()
.trigger() 会影响所有与 jQuery 对象相匹配的元素，而 .triggerHandler() 仅影响第一个匹配到的元素
使用 .triggerHandler() 触发的事件，并不会在 DOM 树中向上冒泡。 如果它们不是由目标元素直接触发的，那么它就不会进行任何处理
与普通的方法返回 jQuery 对象(这样就能够使用链式用法)相反，.triggerHandler() 返回最后一个处理的事件的返回值。如果没有触发任何事件，会返回 undefined





动画：
$('ele').hide().show()
toggle切换
slidedown slideup slideToggle 下卷上卷上下切换
fadeout fadein fadeToggle 淡出淡入出入切换
fadeTo .fadeTo( duration, opacity ,callback) 指定停止时透明度

toggle、sildeToggle以及fadeToggle的区别：
toggle：切换显示与隐藏效果
sildeToggle：切换上下拉卷滚效果
fadeToggle：切换淡入淡出效果

toggle与slideToggle细节区别：
toggle：动态效果为从右至左。横向动作，toggle通过display来判断切换所有匹配元素的可见性
slideToggle：动态效果从下至上。竖向动作，slideToggle 通过高度变化来切换所有匹配元素的可见性

fadeToggle方法：
fadeToggle() 方法在 fadeIn() 和 fadeOut() 方法之间切换。
元素是淡出显示的，fadeToggle() 会使用淡入效果显示它们。
元素是淡入显示的，fadeToggle() 会使用淡出效果显示它们。
注释：隐藏的元素不会被完全显示（不再影响页面的布局）



animate:
.animate( properties ,[ duration ], [ easing ], [ complete ] )

properties：一个或多个css属性的键值对所构成的Object对象。 用于动画的属性值必须是数字。（border、margin、padding、width、height、font、left、top、right、bottom、wordSpacing）
注意：CSS 样式使用 DOM 名称（比如 "fontSize"）来设置，而非 CSS 名称（比如 "font-size"）。
duration时间：动画执行的时间，持续时间是以毫秒为单位的；值越大表示动画执行的越慢，不是越快。还可以提供'fast' 和 'slow'字符串，分别表示持续时间为200 和 600毫秒。
easing动画运动的算法：jQuery库中默认调用 swing。如果需要其他的动画算法，请查找相关的插件。
complete回调：动画完成时执行的函数，这个可以保证当前动画确定完成后发会触发。

.animate( properties, options )


stop()：只会停止第一个动画，第二个第三个继续
stop(true)：停止第一个、第二个和第三个动画
stop(true ture)：停止动画，直接跳到第一个动画的最终状态

jQuery.inArray()函数用于在数组中搜索指定的值，并返回其索引值。如果数组中不存在该值，则返回 -1。

trim()去空格：
移除字符串开始和结尾处的所有换行符，空格(包括连续的空格)和制表符（tab）
如果这些空白字符在字符串中间时，它们将被保留，不会被移除

.get( [index ] )
get方法是获取的dom对象，也就是通过document.getElementById获取的对象
get方法是从0开始索引，负值从-1开始

.index()
.index( document.getElementById("test5") )
.index( $("#test6") )
如果不传递任何参数给 .index() 方法，则返回值就是jQuery对象中第一个元素相对于它同辈元素的位置
如果在一组元素上调用 .index() ，并且参数是一个DOM元素或jQuery对象， .index() 返回值就是传入的元素相对于原先集合的位置
如果参数是一个选择器， .index() 返回值就是原先元素相对于选择器匹配元素的位置。如果找不到匹配的元素，则 .index() 返回 -1




jQuery表单验证插件：https;//plugins.jquery.com/tag/validate/
jQuery Validation插件是最常用的插件之一:http://jqueryvalidation.org/
validate校验的是表单的name属性，而不是 id



$("#form").valid()?"correct":"error";        //valid()方法检查表单或元素是否有效，返回true,false
$("username").rules();                       //获取表单元素（表单里的某个元素，而不是表单）的校验规则
$("username").rules("add",{min:2,max:10};    //添加规则
$("username").rules("remove","min max");     //删除规则

validate 方法返回 validator对象，对象的用法：
var validator={$("#demoForm").validate({...});}
validator.form()                        //整个表单是否有效  true/false
validator.element("username")           //验证元素有无校
validator.resetForm()                   //表单恢复到验证前状态
validator.showErrors({
	username:“用户名填错了！”})        //针对某个元素显示特定的错误信息
validator.numberOfInvalids()            //返回无效元素数量

Validator对象的静态方法：
1、jQuery.validator.addMethod(name,method[,message])：增加自定义的验证方法
2、jQuery.validator.format(template,argument,argumentN...)：格式化字符串，用参数代替模板中的{n}
如：var template=$.validator.format("{0}-{1}-{2}");
template("你","我","他")或template(["你","我","他"])则输出"你-我-他"，参数个数不够则会输出{n}来代替
3、jQuery.validator.setDefaults(options)：修改插件默认设置
如：$.validator.setDefaults({debug:true});表示给所有的表单都设置
4、jQuery.validator.addClassRules(name,rules)：为某些class属性值包含name的元素增加验证规则（批量设置规则，可减少重复代码）
如：$.validator.addClassRules({text:{required:true,minlength:5}});表示给class="text"的元素添加验证规则

validate()方法配置项（即 validator 对象属性）是validate插件的核心内容：
submitHandler:通过验证后运行的函数，可以加上表单提交方法
invalidHandler:无效表单提交后运行的函数
ignore:对某些元素不进行验证
rules:定义校验规则
messages:定义提示信息
groups:对一组元素的验证，用一个错误提示，用errorPlacement控制把出错信息放在那实例调用：
submitHandler:function(from){
//表单提交的方式
from:submit();//$(form).Ajax.submit();//$ajax等方式提交表单
}
invalidHandler:function(event,validator){ //event:无效验证触发的事件 //validator:对象
}也可以写一个事件来触发
$("选择器属性值").on("事件名",function(event,validator)){
	console.log("错误数："+validator.numberOfInvalids	());
});

onsubmit:是否在提交时验证，默认值为true
onfoucusout:是否在获取焦时验证
onkeyup:是否在敲击键盘时验证
onclick:是否在鼠标点击时验证，一般用于checkbox或者radio
focusInvalid:提交表单后，未通过验证的表单（第一个或提交之前获得焦点的未通过验证的 表单）是否会获得焦点
focusCleanup:当未通过验证的元素获得焦点时，是否移除错误提示
errorClass:指定错误提示的css类名，可以自定义错误提示的样式
validClass:指定验证通过的css类名
errorElement:使用什么标签标记错误
wrapper：使用什么标签把上边的errorElement包起来
errorLaberContainer:把错误信息统一放在一个容器里面
errorContainer:显示或者隐藏验证信息，可以自动实现有错误信息出现时把容器属性变为显示，无错误时隐藏。

1、showErrors：可以显示总共有多少个未通过验证的元素
如：showErrors:function(errorMap,errorList){
errorMap：元素信息和错误信息的键值对
errorList：元素信息、错误信息、验证方法等信息列表
this.defaultShowErrors();//使用默认的错误提示信息展示方式，需要这个否则错误信息不显示了
}
2、errorPlacement：自定义错误信息放在哪里，配合groups一起使用
3、success：要验证的元素通过验证后的动作
如：success:"right" 或 success:function(label){label.addClass("right")}
效果是给错误信息展示label元素的class属性值追加right值
4、highlight：可以给未通过验证的元素加效果
如：highlight:function(element,errorClass,validClass){
//element：绑定验证的元素
//errorClass：验证错误信息展示label的class属性值
//validClass：验证通过信息展示label的class属性值
}
5、unhighlight：去除未通过验证的元素的效果，一般和highlight同时使用，同上
注意：success主要针对label元素，highlight主要针对input元素
     highlight和unhighlight主要用在单项验证时


validate插件自带的选择器：
1、:blank   选择所有值为空的元素，会自动去除半角的空格，全角的空格则不为空
2、:filled  选择所有值不为空的元素 会自动去除半角的空格，全角的空格则不为空
3、:unchecked  选择所有没有被选中的元素



自定义验证方法
$.validator.addMethod(name,method，[message])
name:验证方法名称，
method:function(value(验证元素的值),element(被验证的元素),params(验证方法的值)方法逻辑
message:提示消息

eg:
$.validator.addMethod("postcode",function(value,ele,params){
	var postcode = /^[0-9]{6}$/;
	return this.optional(ele)||(postcode.test(value));
},"请填写正确的邮编！");
代码解释：
this.optional(element)：元素为空的话，返回 true，不为空才会接着验证postcode
postcode.test(value)：对元素的值进行正则表达式判断，符合正则表达式返回true


additional-methods.js包含了很多扩展验证方法。在写自定义方法时可以参考这个js库


所有表单数据最少要验证两次，一提交潜在客户端验证，二提交后在服务器端验证，保证数据合法性。
服务器端不要相信任何客户端的数据！