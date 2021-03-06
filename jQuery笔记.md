

### 一、简介

1. 

​	jQuery是一个轻量级，快速简洁的javascript库，

2. jQuery产生的对象是jQuery独有的，只能自己调用

3. 书写规则

   支持链式操作

   在变量前加 “  ( var  $variable = jQuery 对象);



### 二、寻找元素

1. 选择器

   基本选择器，层级选择器，属性选择器，与CSS类似

2. 基本选择器

   ```javascript
   $('li:first')		//第一个元素
   $('li:last')		//最后一个元素
   
   $("tr:even")		//索引为偶数的元素，从0开始
   $("tr:odd")			//索引为奇数的元素，从0开始
   
   $("tr:eq(1)")		//给定索引的元素
   $("tr:gt(0)")		//大于给定索引值的元素
   $("tr:lt(2)")		//小于给定索引值的元素
   
   $(":focus")			//当前获取焦点的元素
   $(":animated")		//正在执行动画效果的元素
   ```

3. 内容选择器 

   ```javascript
   $("div:contains('nick')")		//包含nick文本的元素
   $("td:empty")					//不包含子元素或者文本的空元素
   $("div:has(p)")					//含有选择器所匹配的元素
   $("td:parent")					//含有子元素或者文本的元素
   ```

4. 表单选择器

   ```javascript
   $(":input")		//匹配所有input，textarea，select，button元素
   $(":text")		//所有所有的单行文本框
   $(":password")	//匹配所有密码框
   $(":radio")		//匹配所有单选按钮
   $(":checkbox")	//匹配所有复选按钮
   $(":submit")	//匹配所有提交按钮
   $(":reset")		//匹配所有重置按钮
   $(":button")	//匹配所有button按钮
   $(":file")		//匹配所有文件域
   
   $("input:checked")		//匹配所有选中的元素
   $("select option:selected")		//select中所有选中的option元素
   ```



### 三、筛选器

1. 过滤

   ```javascript
   $("p").eq(N)		//p下的第N个jQuery对象，类似索引
   $('li').first()		//li下的第一个元素
   $('li').last()		//li下的最后一个元素
   $(this).hasClass("test")	//元素是否含有某个特定的类，返回布尔值
   $('li').has('ul')	//包含特定后代的元素
   ```

2. 查找

   ```javascript
   $("div").children()			//div中的每个子元素，第一层
   $("div").find("span")		//div中的包含的所有span元素，子子孙孙
   
   $("p").next()				//紧邻p元素后的一个同辈元素
   $("p").nextAll()			//p元素之后所有的同辈元素
   $("#test").nextUntil("#test2")		//id为“#test”元素之后到id为“#test2”之间所有的同辈元素，掐头去尾
   
   $("p").prev()				//紧邻p元素前的一个同辈元素
   $("p").prevAll()			//p元素之前的所有同辈元素
   $("#test").parentUntil("#test2")	//id为“#test”元素到id为“#test2“之间所有的同辈元素，掐头去尾
   
   $("p").parent()				//每个p元素的父元素
   $("p").parents()			//每个p元素的所有祖先元素,body,html
   $("#test").parentUntil("#test3")	//id为“#test”元素到id为“#test2”之间所有的父级元素，掐头去尾
   
   $("div").siblings			//所有的同辈元素，不包括自己
   ```



### 三、属性操作

1. 基本属性操作

   ```javascript
   $("img").attr("src")				//返回文档所有图像的src属性值
   $("img").attr("src","test.png")		//设置所有图片的src属性	
   $("img").removeAttr("src")			//将文档中图像的src属性删除
   $("img").removeProp("src")			//删除img的src属性
   
   $("input[type='checkbox']").prop("checked",true)	//选中复选框
   ```

2. CSS类

   ```javascript
   $("p").addClass("selected");		//为p元素加上‘selected’类
   $("p").removeClass("selected")		//为p元素删除'selected'类
   $("p").toggleClass("selected")		//如果p元素存在‘selected’属性就删除，没有就添加
   ```

3. HTML代码／文本／值

   ```javascript
   $('p').html();    　　　　　　　　　　 //返回p元素的html内容
   $("p").html("Hello <b>nick</b>!");  //设置p元素的html内容
   $('p').text();    　　　　　　　　　　 //返回p元素的文本内容
   $("p").text("nick");    　　　　　　　//设置p元素的文本内容
   $("input").val();    　　　　　　　　 //获取文本框中的值
   $("input").val("nick");     　　　　 //设置文本框中的内容
   ```



### 四、CSS操作



1. 样式

   ```javascript
   $("p").css("color");          //访问查看p元素的color属性
   $("p").css("color","red");    //设置p元素的color属性为red
   $("p").css({ "color": "red", "background": "yellow" });    //设置p元素的color为red，background属性为yellow（设置多个属性要用{}字典形式）
   ```

2. 位置

   ```javascript
   $('p').offset()     //元素在当前视口的相对偏移,Object {top: 122, left: 260}
   $('p').offset().top
   $('p').offset().left
   $("p").position()   //元素相对父元素的偏移,对可见元素有效，Object {top: 117, left: 250}
   
   $(window).scrollTop()    //获取滚轮滑的高度
   $(window).scrollLeft()   //获取滚轮滑的宽度
   $(window).scrollTop('100')    //设置滚轮滑的高度为100
   ```

3. 尺寸

   ```javascript
   $("p").height();    //获取p元素的高度
   $("p").width();     //获取p元素的宽度
   
   $("p:first").innerHeight()    //获取第一个匹配元素内部区域高度(包括补白、不包括边框)
   $("p:first").innerWidth()     //获取第一个匹配元素内部区域宽度(包括补白、不包括边框)
   
   $("p:first").outerHeight()    //匹配元素外部高度(默认包括补白和边框)
   $("p:first").outerWidth()     //匹配元素外部宽度(默认包括补白和边框)
   $("p:first").outerHeight(true)    //为true时包括边距
   ```

###五、文档处理

1. 内部插入

   ```javascript
   $("p").append("<b>nick</b>");    //每个p元素内后面追加内容
   $("p").appendTo("div");    　　　 //p元素追加到div内后
   $("p").prepend("<b>Hello</b>");  //每个p元素内前面追加内容
   $("p").prependTo("div");    　   //p元素追加到div内前
   ```

2. 外部插入

   ```javascript
   $("p").after("<b>nick</b>");     //每个p元素同级之后插入内容
   $("p").before("<b>nick</b>");    //在每个p元素同级之前插入内容
   $("p").insertAfter("#test");     //所有p元素插入到id为test元素的后面
   $("p").insertBefore("#test");    //所有p元素插入到id为test元素的前面
   ```

3. 替换

   ```javascript
   $("p").replaceWith("<b>Paragraph. </b>");    //将所有匹配的元素替换成指定的HTML或DOM元素
   $("<b>Paragraph. </b>").replaceAll("p");     //用匹配的元素替换掉所有 selector匹配到的元素
   ```

4. 删除

   ```javascript
   $("p").empty();     //删除匹配的元素集合中所有的子节点，不包括本身
   $("p").remove();    //删除所有匹配的元素,包括本身
   $("p").detach();    //删除所有匹配的元素(和remove()不同的是:所有绑定的事件、附加的数据会保留下来)
   ```

5. 复制

   ```javascript
   $("p").clone()    　　//克隆元素并选中克隆的副本
   $("p").clone(true)   //布尔值指事件处理函数是否会被复制
   ```



### 六、事件

1. 页面插入，当页面插入成功后再运行的函数事件

   ```javascript
   $(document).ready(function(){
     do something...
   });
   
   //简写
   $(function($) {
     do something...
   });
   ```

2. 页面处理

   ```javascript
   //bind 为每个匹配元素绑定事件处理函数，绑定多个用{}。
   $("p").bind("click", function(){
     alert( $(this).text() );
   });
   $(menuF).bind({
       "mouseover":function () {
        $(menuS).parent().removeClass("hide");
        },"mouseout":function () {
        $(menuS).parent().addClass("hide");
   }
   });         
   
   
   $("p").one( "click", fun...)    //one 绑定一个一次性的事件处理函数
   $("p").unbind( "click" )        //解绑一个事件
   ```

3. 页面委派

   ```javascript
   // 与bind 不同的是当时间发生时才去临时绑定。
   $("p").delegate("click",function(){
     do something...
   });
   
   $("p").undelegate();    　　　//p元素删除由 delegate() 方法添加的所有事件
   $("p").undelegate("click")   //从p元素删除由 delegate() 方法添加的所有click事件
   ```

4. 事件

   ```javascript
   $("p").click();    　　//单击事件
   $("p").dblclick();    //双击事件
   $("input[type=text]").focus()  //元素获得焦点时,触发 focus 事件
   $("input[type=text]").blur()   //元素失去焦点时,触发 blur事件
   $("button").mousedown()//当按下鼠标时触发事件
   $("button").mouseup()  //元素上放松鼠标按钮时触发事件
   $("p").mousemove()     //当鼠标指针在指定的元素中移动时触发事件
   $("p").mouseover()     //当鼠标指针位于元素上方时触发事件
   $("p").mouseout()    　//当鼠标指针从元素上移开时触发事件
   $(window).keydown()    //当键盘或按钮被按下时触发事件
   $(window).keypress()   //当键盘或按钮被按下时触发事件,每输入一个字符都触发一次
   $("input").keyup()     //当按钮被松开时触发事件
   $(window).scroll()     //当用户滚动时触发事件
   $(window).resize()     //当调整浏览器窗口的大小时触发事件
   $("input[type='text']").change()    //当元素的值发生改变时触发事件
   $("input").select()    //当input 元素中的文本被选择时触发事件
   $("form").submit()     //当提交表单时触发事件
   $(window).unload()     //用户离开页面时
   ```

5.  (event object) 对象。所有的事件函数都可以传入event参数方便处理事件

   ```javascript
   $("p").click(function(event){  
    alert(event.type); //"click"  
   }); 
   
   (evnet object)属性方法：
   event.pageX 　 //事件发生时，鼠标距离网页左上角的水平距离
   event.pageY 　 //事件发生时，鼠标距离网页左上角的垂直距离
   event.type 　　//事件的类型
   event.which 　 //按下了哪一个键
   event.data 　　//在事件对象上绑定数据，然后传入事件处理函数
   event.target 　//事件针对的网页元素
   event.preventDefault() 　//阻止事件的默认行为(比如点击链接，会自动打开新页面)
   event.stopPropagation()  //停止事件向上层元素冒泡
   ```

### 七、效果

1. 基本

   ```javascript
   $("p").show()    　　　　//显示隐藏的匹配元素
   $("p").show("slow");    //参数表示速度,("slow","normal","fast"),也可为900毫秒
   $("p").hide()    　　　　//隐藏显示的元素
   $("p").toggle();   　　 //切换 显示/隐藏
   ```

2. 滑动

   ```javascript
   $("p").slideDown("900");    //用900毫秒时间将段落滑下
   $("p").slideUp("900");    　//用900毫秒时间将段落滑上
   $("p").slideToggle("900");  //用900毫秒时间将段落滑上，滑下
   ```

3. 淡入淡出

   ```javascript
   $("p").fadeIn("900");    　　  //用900毫秒时间将段落淡入
   $("p").fadeOut("900");    　　 //用900毫秒时间将段落淡出
   $("p").fadeToggle("900");    　//用900毫秒时间将段落淡入,淡出
   $("p").fadeTo("slow", 0.6);    //用900毫秒时间将段落的透明度调整到0.6
   ```



### 八、对象访问



```javascript
$.trim() 　　//去除字符串两端的空格
$.each() 　　//遍历一个数组或对象，for循环
$.inArray() //返回一个值在数组中的索引位置，不存在返回-1  
$.grep() 　 //返回数组中符合某种标准的元素
$.extend()  //将多个对象，合并到第一个对象
$.makeArray() //将对象转化为数组
$.type()    //判断对象的类别（函数对象、日期对象、数组对象、正则对象等等
$.isArray() //判断某个参数是否为数组
$.isEmptyObject() //判断某个对象是否为空(不含有任何属性)
$.isFunction()    //判断某个参数是否为函数
$.isPlainObject() //判断某个参数是否为用"{}"或"new Object"建立的对象
$.support()       //判断浏览器是否支持某个特性
```



模拟each()内部实现机制

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>

    <script src="../../jquery-1.12.4.js"></script>
    <script>
        li = [11,22,33];
        $.each(li,function (k,v) {
            console.log(this);
            console.log(k,v);
            if (k == 1){
                return false;
            }
        })
    </script>


    <script>
        function myEach(obj,func) {
            for (var i=0;i<obj.length;i++){
                var current = obj[i];
                var ret = func(i,current);
                if (ret == false){
                    break;
                }
            }
        }

        var li = [10,20,30];
        myEach(li,function (k,v) {
            console.log(k,v);
            return false;
        })
    </script>
</body>
</html>
```



### 九、插件拓展机制



```javascript
//方式一
jQuery.fn.extend({
  check: function() {
    return this.each(function() { this.checked = true; });
  },
  uncheck: function() {
    return this.each(function() { this.checked = false; });
  }
});

$("input[type=checkbox]").check();
$("input[type=radio]").uncheck();
```



```javascript
//方式二
jQuery.extend({
  min: function(a, b) { return a < b ? a : b; },    //三元运算
  max: function(a, b) { return a > b ? a : b; }
});

jQuery.min(2,3);     //2
jQuery.max(4,5);    //5
```



```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <div class="title">111</div>
    <div class="title">222</div>

    <script src="../../jquery-1.12.4.js"></script>
    <script>
        jQuery.fn.extend({
            show1: function () {
                var val = this.text();
                val = val + "sb";
                return val;
            },
            show2: function () {

            }
        });
        var ret = $(".title").show1();
        console.log(ret);


        jQuery.extend({
            s1: function (arg) {
                var val = $(arg).text();
                return val + "sb";
            },
            s2: function () {

            }
        });
        var ret2 = $.s1(".title");
        console.log(ret2);
    </script>
</body>
</html>
```

