#### Navigator

```js
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script>
        /* 
            BOM
                浏览器对象模型
                BOM可以使我们通过JS来操作浏览器
                在BOM中为我们提供了一组对象，用来完成对浏览器的操作
                BOM对象
                    Window
                        代表的是整个浏览器的窗口，同时window也是网页的中的全局对象
                    Navigator
                        代表的是当前浏览器的信息，通过该对象可以来识别不同的浏览器
                    Location
                        代表当前浏览器的地址栏信息，通过location可以获取地址栏信息或者操作浏览器跳转页面
                    History
                        代表浏览器的历史记录，可以通过该对象来操作浏览器的历史记录
                        由于隐私原因，该对象不能获取到具体的历史纪录，只能操作浏览器的向前或向后翻页
                        而且该操作只在当次访问时有效
                    Screen
                        代表用户的屏幕的信息，通过该对象可以获取到用户的显示器的相关的信息


            这些BOM对象在浏览器中都是作为window对象的属性保存的
                可以通过window对象来使用，也可以直接使用
        */
        //返回浏览器名称
        /* 
            由于历史原因，navigator大部分属性不能用了
            但是userAgent可以用来判断浏览器的信息
                userAgent是一个字符串，这个字符串中包含有用来描述浏览器信息的内容
                不同的浏览器会有不同的userAgent
                userAgent不能用来判断IE11
        */
        //alert(navigator.userAgent);//Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/84.0.4147.89 Safari/537.36 SLBrowser/7.0.0.12151 SLBChan/8
        var ua = navigator.userAgent;
        if(/firefox/i.test(ua)){
            alert("你是火狐");
        }else if(/chrome/i.test(ua)){
            alert("你是chrome");
        }else if(/msie/i.test(ua)){
            alert("你是IE浏览器");
        }else if("ActiveXObject" in window){
            alert("你是IE");
        }
    </script>
</head>
<body>
    
</body>
</html>
```

#### History

```js
<script>
        /* 
            History
            对象可以用来操作浏览器向前或向后翻页
        */
       window.onload = function(){
           var btn = document.getElementById("btn");
           btn.onclick = function(){
                /* 
                    length
                        属性，可以获取到当前访问的链接数量
                */
                //alert(history.length);
                //history.back();//back()可以用来回退到上一个页面，作用和浏览器的回退按钮一样
                //history.forward();//可以跳转到下一个页面，和浏览器前进按钮一样

                /* 
                    go()
                        它可以用来跳转到指定的页面
                        他需要一个整数作为参数
                            1.表示向前跳转一个页面
                            2.向前跳转两个
                            -1.向后跳转一个
                            -2.向后跳转两个
                */
               history.go(-2);
           }
       }
    </script>
</head>
<body>
    <button id="btn">点我一下</button>
    <h1>History</h1>
</body>
```

#### Location

```js
<script>
        /* 
            Location
                该对象封装了浏览器的地址栏信息
        */
        window.onload = function(){
            var btn = document.getElementById("btn");
            btn.onclick = function(){
                //如果直接打印location，则可以获取到地址栏的信息(当前页面的完整路径)
                //alert(location);
                
                //如果直接将location属性修改为一个完整的路径，或者相对路径，则我们页面会自动跳转到该路径
                //并且会生成相应的历史记录
                // location = "http://www.baidu.com";

                /* 
                    assign()
                        用来跳转到其他页面，作用和直接修改location一样
                */
               //location.assign("http://www.baidu.com");

               /* 
                    reload()
                        用于重新加载当前页面，作用和刷新按钮一样
               */
              location.reload();

              /* 
                    replace()
                        可以使用一个新的页面替换当前页面，调用完毕也会跳转页面
                        不会生成历史记录，不能使用回退按钮回退
              */
             location.replace()
            };
        };
    </script>
</head>
<body>
    <button id="btn">点我一下</button>
    <h1>Location</h1>
    <input type="text">
</body>
```

#### 定时器简介

```js
<script>
        window.onload = function(){
            //获取count
            var count = document.getElementById("count");
            //使count内容自动切换
            /* 
                定时调用使一段程序每隔一段时间执行一次
            */
            /* for(var i=0;i<10;i++){
                count.innerHTML = i ;
            } */
            /* 
                setInterval()
                    定时调用
                    可以将一个函数每隔一段时间执行一次
                    参数：
                        1.回调函数
                        2.每次调用间隔时间，单位是毫秒


                    返回值：
                        返回一个Number类型的数据
                        这个数字用来作为定时器的唯一标识
            */
           var num = 1;
            /* setInterval(function(){
                count.innerHTML = num++;
            },1000); */

            var timer = setInterval(function(){
                count.innerHTML = num++;
                if(num == 11){
                    //关闭定时器
                    clearInterval(timer);
                }
            },1000);
            //console.log(timer);

            /* 
                clearInterval()可以用来关闭一个定时器
                方法中需要一个定时器的标识作为参数，这样将关闭标识对应的定时器
            */
            // clearInterval(timer);
        };
    </script>
</head>
<body>
    <h1 id="count"></h1>
</body>
```

#### 练习

```js
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script>
        window.onload = function(){
            /* 
                使图片自动切换
            */
           var img1 = document.getElementById("img1");
           //创建一个数组来保存图片的路径
           var imgArr = ["./img/1.jpg","./img/2.jpg","./img/3.jpg","./img/4.jpg","./img/5.jpg"];

           var btn01 = document.getElementById("btn01");
           var btn02 = document.getElementById("btn02");
           var timer ;
           btn01.onclick= function(){
            /* 
                在开启定时器之前，需要将当前元素的上一个定时器关闭
            */
           clearInterval(timer);

                //创建一个变量，用来保存当前图片的索引
           var index = 0;
           /* 
                开启一个定时器，来自动切换图片
           */
          timer = setInterval(function(){
              //使索引自增
              index++;
            
              /* if(index >= imgArr.length){
                  index = 0;
              } */
              index = index % imgArr.length;
              //修改img1的src属性
              img1.src = imgArr[index];
          },1000)
           }
           btn02.onclick = function(){
               /* 
                    clearInterval()
                        可以接受任意参数
                        如果参数是有效的定时器的标识，则停止对应的定时器
                        如果不是有效的标识，则什么也不做
               */
               clearInterval(timer);
           }
           
           
        }
    </script>
</head>
<body>

    <img id="img1" src="./img/1.jpg" alt="">
    <br>
    <br>
    <button id="btn01">开始</button>
    <button id="btn02">停</button>
</body>
</html>
```

#### 延时调用

```js
 <script>
        var num = 1;
        /* 
            延时调用
                一个函数不马上执行，而是隔一段时间后执行,而且只执行一次
            
        */
       var timer = setTimeout(function(){

       },3000)
       clearTimeout(timer);
    </script>
```

#### 定时器

```js
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        *{
            margin: 0;
            padding: 0;
        }
        #box1{
            width: 100px;
            height: 100px;
            background-color: red;
            position: absolute;
            left: 0;
        }
    </style>
    <script>
        /* 
            定义一个函数，用来获取指定元素的样式
            参数：
                obj 需要获取样式的元素
                name 需要获取的样式名
        */
       function getStyle(obj,name){
           if(window.getComputedStyle){
               return getComputedStyle(obj,null)[name];
           }else{
               return obj.currentStyle[name];
           }
       }
        window.onload = function(){
            var box1 = document.getElementById("box1");
            var btn01 = document.getElementById("btn01");
            var timer;
            btn01.onclick = function(){
                clearInterval(timer);
                timer = setInterval(function(){
                    var oldValue = parseInt(getStyle(box1,"left"));
                    var newValue = oldValue + 1;
                    if(newValue >= 800){
                        newValue = 800;
                    }
                    box1.style.left = newValue + "px";
                    if(newValue == 800){
                        //达到目标，关闭定时器
                        clearInterval(timer);
                    }
                },30)
            }
        }
    </script>
</head>
<body>
    <button id="btn01">点击按钮以后box1向右移动</button>
    <br>
    <br>
    <div id="box1"></div>
    <div id="box2" style="width: 0; height: 1000px; border-left: 1px black solid; position: absolute; left: 800px; top: 0;"></div>
</body>
</html>
```

```js
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        *{
            margin: 0;
            padding: 0;
        }
        #box1{
            width: 100px;
            height: 100px;
            background-color: red;
            position: absolute;
            left: 0;
        }
    </style>
    <script>
        /* 
            定义一个函数，用来获取指定元素的样式
            参数：
                obj 需要获取样式的元素
                name 需要获取的样式名
        */
       function getStyle(obj,name){
           if(window.getComputedStyle){
               return getComputedStyle(obj,null)[name];
           }else{
               return obj.currentStyle[name];
           }
       }
       var timer;
       /* 
            创建一个执行动画的函数
       */
       function move(obj,target,speed){
                //关闭上一个定时器
                clearInterval(timer);

                //获取元素目前的位置
                var current = parseInt(getStyle(obj,"left"));

                //判断速度的正负值
                if(current > target){
                    speed = -speed;
                }
                timer = setInterval(function(){
                    var oldValue = parseInt(getStyle(obj,"left"));
                    var newValue = oldValue + speed;

                    //向左移动时判断，需要判断newValue是否小于target
                    //向右移动时判断，newValue是否大于target
                    if((speed < 0 && newValue < target) || (speed > 0 && newValue > target)){
                        newValue = target;
                    }
                    obj.style.left = newValue + "px";
                    if(newValue == target){
                        //达到目标，关闭定时器
                        clearInterval(timer);
                    }
                },30)
       }
        window.onload = function(){
            var box1 = document.getElementById("box1");
            var btn01 = document.getElementById("btn01");
            var btn02 = document.getElementById("btn02");
            btn01.onclick = function(){
                move(box1,800,10);
            }
            btn02.onclick = function(){
                move(box1,0,10);
            }

        }
    </script>
</head>
<body>
    <button id="btn01">点击按钮以后box1向右移动</button>
    <button id="btn02">点击按钮以后box1向左移动</button>
    <br>
    <br>
    <div id="box1"></div>
    <div id="box2" style="width: 0; height: 1000px; border-left: 1px black solid; position: absolute; left: 800px; top: 0;"></div>
</body>
</html>
```

```js
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        *{
            margin: 0;
            padding: 0;
        }
        #box1{
            width: 100px;
            height: 100px;
            background-color: red;
            position: absolute;
            left: 0;
        }
        #box2{
            width: 100px;
            height: 100px;
            background-color: yellow;
            position: absolute;
            left: 0;
            top: 200px;
        }
    </style>
    <script src="./js/tools.js"></script>
    <script>
        window.onload = function(){
            var box1 = document.getElementById("box1");
            var box2 = document.getElementById("box2");
            var btn01 = document.getElementById("btn01");
            var btn02 = document.getElementById("btn02");
            var btn03 = document.getElementById("btn03");
            var btn04 = document.getElementById("btn04");
            btn01.onclick = function(){
                move(box1,"left",800,10);
            }
            btn02.onclick = function(){
                move(box1,"left",0,10);
            }
            btn03.onclick = function(){
                move(box2,"left",800,10);
            }
            btn04.onclick = function(){
                move(box2,"width",800,10,function(){
                    move(box2,"height",400,10,function(){

                    })
                });
            }
        }
    </script>
</head>
<body>
    <button id="btn01">点击按钮以后box1向右移动</button>
    <button id="btn02">点击按钮以后box1向左移动</button>
    <button id="btn03">点击按钮以后box2向右移动</button>
    <button id="btn04">测试</button>
    <br>
    <br>
    <div id="box1"></div>
    <div id="box2"></div>
    <div id="box2" style="width: 0; height: 1000px; border-left: 1px black solid; position: absolute; left: 800px; top: 0;"></div>
</body>
</html>
```

#### 轮播图

```js
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        *{
            margin: 0;
            padding: 0;
        }
        #outer{
            width: 520px;
            height: 333px;
            margin: 50px auto;
            background-color: yellowgreen;
            padding: 10px 0;

            /* 开启相对定位 */
            position: relative;

            overflow: hidden;
        }
        #imgList{
            list-style: none;

            /* width: 2600px; */

            /* 开启绝对定位 */
            position: absolute;
            left: 0px;
        }
        #navDiv{
            position: absolute;
            bottom: 15px;
            /* 
                设置left
                outer宽度520
                navDiv宽度 25*5=125
                520-125=395
                395/2=197.5
            */
            /* left: 197px; 不好，不建议采用*/
        }
        #navDiv a{
            float: left;
            width: 15px;
            height: 15px;
            background-color: red;
            margin: 0 5px;

            /* 设置透明 */
            opacity: 0.5;

            /* 兼容IE8透明 */
            filter: alpha(opacity=50);
        }
        #navDiv a:hover{
            background-color: black;
        }
        #imgList li{
            float: left;
            margin: 0 10px;
        }
    </style>
    <!-- 引入tools文件 -->
    <script src="./js/tools.js"></script>
    <script>
        window.onload = function(){
            //获取imgList
            var imgList = document.getElementById("imgList");

            //获取页面中所有的img标签
            var imgArr = document.getElementsByTagName("img");

            //设置imgList的宽度
            imgList.style.width = 520*imgArr.length + "px";

            // 设置导航按钮居中
            var navDiv = document.getElementById("navDiv");
            var outer = document.getElementById("outer");
            navDiv.style.left = (outer.offsetWidth - navDiv.offsetWidth)/2 + "px";


            //设置默认显示图片的索引
            var index = 0;
            //获取所有的a
            var allA = document.getElementsByTagName("a");
            //设置默认选中的效果
            allA[index].style.backgroundColor = "black";

            /* 
                点击超链接切换到指定的图片
            */
           for(var i=0 ; i < allA.length ; i++){
               //为每一个超链接都添加一个num属性
                allA[i].num = i;

               allA[i].onclick = function(){
                   //获取点击超链接的索引，并将其设置为index
                    index = this.num;

                    // 切换图片
                    // imgList.style.left = -520 * index + "px";
                    // 使用move函数来切换图片
                    move(imgList,"left", -520*index,50,function(){

                    });


                    // 设置选中的a
                    setA();

               }
           }
        //    创建一个方法用来设置选中的a
        function setA(){
            //遍历所有的a并将背景颜色设置为红色
            for(var i=0 ; i < allA.length ; i++){
                allA[i].style.backgroundColor="";//这里内联样式里的背景颜色设置为空串是为了让伪类hover起作用
            }
            allA[index].style.backgroundColor = "black";
        }

        }
    </script>
</head>
<body>
    <div id="outer">
        <ul id="imgList">
            <li>
                <img src="./img/1.jpg" alt="">
            </li>
            <li>
                <img src="./img/2.jpg" alt="">
            </li>
            <li>
                <img src="./img/3.jpg" alt="">
            </li>
            <li>
                <img src="./img/4.jpg" alt="">
            </li>
            <li>
                <img src="./img/5.jpg" alt="">
            </li>
        </ul>
        <div id="navDiv">
            <a href="javascript:;"></a>
            <a href="javascript:;"></a>
            <a href="javascript:;"></a>
            <a href="javascript:;"></a>
            <a href="javascript:;"></a>
        </div>
    </div>
</body>
</html>
```

```js
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        *{
            margin: 0;
            padding: 0;
        }
        #outer{
            width: 520px;
            height: 333px;
            margin: 50px auto;
            background-color: yellowgreen;
            padding: 10px 0;

            /* 开启相对定位 */
            position: relative;

            overflow: hidden;
        }
        #imgList{
            list-style: none;

            /* width: 2600px; */

            /* 开启绝对定位 */
            position: absolute;
            left: 0px;
        }
        #navDiv{
            position: absolute;
            bottom: 15px;
            /* 
                设置left
                outer宽度520
                navDiv宽度 25*5=125
                520-125=395
                395/2=197.5
            */
            /* left: 197px; 不好，不建议采用*/
        }
        #navDiv a{
            float: left;
            width: 15px;
            height: 15px;
            background-color: red;
            margin: 0 5px;

            /* 设置透明 */
            opacity: 0.5;

            /* 兼容IE8透明 */
            filter: alpha(opacity=50);
        }
        #navDiv a:hover{
            background-color: black;
        }
        #imgList li{
            float: left;
            margin: 0 10px;
        }
    </style>
    <!-- 引入tools文件 -->
    <script src="./js/tools.js"></script>
    <script>
        window.onload = function(){
            //获取imgList
            var imgList = document.getElementById("imgList");

            //获取页面中所有的img标签
            var imgArr = document.getElementsByTagName("img");

            //设置imgList的宽度
            imgList.style.width = 520*imgArr.length + "px";

            // 设置导航按钮居中
            var navDiv = document.getElementById("navDiv");
            var outer = document.getElementById("outer");
            navDiv.style.left = (outer.offsetWidth - navDiv.offsetWidth)/2 + "px";


            //设置默认显示图片的索引
            var index = 0;
            //获取所有的a
            var allA = document.getElementsByTagName("a");
            //设置默认选中的效果
            allA[index].style.backgroundColor = "black";

            /* 
                点击超链接切换到指定的图片
            */
           for(var i=0 ; i < allA.length ; i++){
               //为每一个超链接都添加一个num属性
                allA[i].num = i;

               allA[i].onclick = function(){
                   //关闭自动切换定时器
                   clearInterval(timer);
                   //获取点击超链接的索引，并将其设置为index
                    index = this.num;

                    
                    // 设置选中的a
                    setA();


                    // 切换图片
                    // imgList.style.left = -520 * index + "px";
                    // 使用move函数来切换图片
                    move(imgList,"left", -520*index,50,function(){
                        //动画执行完毕，开启自动切换
                        autoChange();
                    });


                    

               }
           }

           //开启自动切换图片
           autoChange();

        //    创建一个方法用来设置选中的a
        function setA(){
            //判断当前索引是否为最后一张图片
            if(index >= imgArr.length - 1){
                index = 0;

                //此时显示的最后一张图片，和第一张一样的
                //通过CSS将最后一张切换成第一张
                imgList.style.left = 0;
            }


            //遍历所有的a并将背景颜色设置为红色
            for(var i=0 ; i < allA.length ; i++){
                allA[i].style.backgroundColor="";//这里内联样式里的背景颜色设置为空串是为了让伪类hover起作用
            }
            allA[index].style.backgroundColor = "black";
        }
        var timer;
        //创建一个函数，用来自动切换图片
        function autoChange(){

            // 开启一个定时器，定时去切换图片
            timer = setInterval(function(){
                index++;
                index %= imgArr.length;
                move(imgList,"left",-520*index,20,function(){
                    //修改导航按钮
                    setA();
                });
            },2000)
        }

        }
    </script>
</head>
<body>
    <div id="outer">
        <ul id="imgList">
            <li>
                <img src="./img/1.jpg" alt="">
            </li>
            <li>
                <img src="./img/2.jpg" alt="">
            </li>
            <li>
                <img src="./img/3.jpg" alt="">
            </li>
            <li>
                <img src="./img/4.jpg" alt="">
            </li>
            <li>
                <img src="./img/5.jpg" alt="">
            </li>
            <li>
                <img src="./img/1.jpg" alt="">
            </li>
        </ul>
        <div id="navDiv">
            <a href="javascript:;"></a>
            <a href="javascript:;"></a>
            <a href="javascript:;"></a>
            <a href="javascript:;"></a>
            <a href="javascript:;"></a>
        </div>
    </div>
</body>
</html>
```

#### 类的操作

```js
<style>
        .b1{
            width: 100px;
            height: 100px;
            background-color: red;
        }
        .b2{
            width: 200px;
            height: 200px;
            background-color: yellow;
        }
    </style>

    <script>
        window.onload = function(){
            var box = document.getElementById("box");
            var btn01 = document.getElementById("btn01");
            btn01.onclick = function(){

                /* 
                    我们可以通过修改元素的class属性来间接的修改样式
                    这样一来，我们只需要修改一次，即可同时修改多个样式
                    浏览器只需要重新渲染页面一次，性能比较好
                    并且这种方式，可以使表现和行为分离
                */
                // box.className = "b2";

                //在b1的样式里面添加b2
                //box.className += " b2";//一定要加空格
                //addClass(box,"b2");//添加
                //removeClass(box,"b2");//删除
                toggleClass(box,"b2");
            }
        };
        /* 
            定义一个函数，用来向一个元素中添加指定的class属性值
            参数：
                obj 要添加class属性的元素
                cn  要添加的class值
        */
        function addClass(obj,cn){
            //检查obj中是否含有cn
            if(!hasClass(obj,cn)){
                obj.className += " " + cn;
            }
            
        }
        /* 
            判断一个元素中是否含有指定的class属性值

        */
        function hasClass(obj,cn){
            //判断obj中有没有cn class
            //创建一个正则表达式
            //var reg = /\bb2\b/;//单词边界
            var reg = new RegExp("\\b"+cn+"\\b");
            return reg.test(obj.className);
        }

        /* 
            删除一个元素中指定的class属性
        */
        function removeClass(obj,cn){
            //创建一个正则表达式
            var reg = new RegExp("\\b"+cn+"\\b");

            //删除class
            obj.className = obj.className.replace(reg,"");
        };

        /* 
            切换一个类
            如果元素中具有该类，则删除
            如果元素中没有该类，则添加
        */
       function toggleClass(obj,cn){
           if(hasClass(obj,cn)){
               removeClass(obj,cn);
           }else{
               addClass(obj,cn);
           }
       };
    </script>

</head>
<body>
    <button id="btn01">点击按钮修改box样式</button>
    <br>
    <br>
    <div id="box" class="b1"></div>
</body>
```

#### 二级菜单

```js
<!DOCTYPE html>
<html>

	<head>
		<meta charset="UTF-8">
		<title>二级菜单</title>
		<style type="text/css">
			* {
				margin: 0;
				padding: 0;
				list-style-type: none;
			}
			
			a,img {
				border: 0;
				text-decoration: none;
			}
			
			body {
				font: 12px/180% Arial, Helvetica, sans-serif, "新宋体";
			}
		</style>

		<link rel="stylesheet" type="text/css" href="./css/sdmenu.css" />
		
		<script type="text/javascript" src="./js/tools.js"></script>
		<script type="text/javascript">
			window.onload = function(){
				/* 
					每一个菜单都是一个div
						当DIV具有collapsed这个类时，div就是折叠状态
						当div没有这个类时，就是展开状态
				*/	
				/* 
					点击菜单，切换菜单的显示状态
				*/
				//获取span
				var menuSpan = document.querySelectorAll(".menuSpan");
				var openDiv = menuSpan[0];
				for(var i=0 ; i <menuSpan.length ; i++){
					menuSpan[i].onclick = function(){
						//this代表我当前点击的span
						//获取当前span的父元素
						var parentDiv = this.parentNode;

						toggleMenu(parentDiv);

						if(openDiv != parentDiv && !hasClass(openDiv,"collapsed")){
							//打开菜单以后，应该关闭之前打开的菜单
							// addClass(openDiv,"collapsed");
							//此处toggle不需要移除功能
							toggleMenu(openDiv);
							// toggleClass(openDiv,"collapsed");
						}


						//修改openDiv为当前打开的菜单
						openDiv = parentDiv;
					};
				}
			function toggleMenu(obj){
					//在切换类之前获取元素的高度
					var begin = obj.offsetHeight;

					//切换parentDiv
					toggleClass(obj,"collapsed");

					//切换之后获取一个高度
					var end = obj.offsetHeight;

					//动画效果就是将高度从begin向end过渡
					//将元素的高度重置为begin，这是内联样式
					obj.style.height = begin + "px";

					//执行动画,从begin向end过渡
					move(obj,"height",end,10,function(){
						//动画执行完毕，删除内联样式
						obj.style.height = "";
					});
			};
				
			};
			
			
		</script>
		
	</head>

	<body>

		<div id="my_menu" class="sdmenu">
			<div>
				<span class="menuSpan">在线工具</span>
				<a href="#">图像优化</a>
				<a href="#">收藏夹图标生成器</a>
				<a href="#">邮件</a>
				<a href="#">htaccess密码</a>
				<a href="#">梯度图像</a>
				<a href="#">按钮生成器</a>
			</div>
			<div class="collapsed">
				<span class="menuSpan">支持我们</span>
				<a href="#">推荐我们</a>
				<a href="#">链接我们</a>
				<a href="#">网络资源</a>
			</div>
			<div class="collapsed">
				<span class="menuSpan">合作伙伴</span>
				<a href="#">JavaScript工具包</a>
				<a href="#">CSS驱动</a>
				<a href="#">CodingForums</a>
				<a href="#">CSS例子</a>
			</div>
			<div class="collapsed">
				<span class="menuSpan">测试电流</span>
				<a href="#">Current or not</a>
				<a href="#">Current or not</a>
				<a href="#">Current or not</a>
				<a href="#">Current or not</a>
			</div>
		</div>
	</body>
</html>
```

#### JSON

```js
<title>Document</title>
    <!-- 如果需要兼容IE7及以下的JSON操作，则可以通过引入一个外部的js文件来处理 -->
    <script src="./js/json2.js"></script>
    <script>
        /* 
            JSON    IE7及以下不兼容
                js中的对象只有js自己认识，其他语言都不认识
                JSON就是一个特殊格式的字符串，这个字符串可以被任意的语言识别，
                    并且可以转换为任意语言中的对象，JSON在开发中主要用来数据的交互
                JSON
                    JavaScript Object Notation JS对象表示法
                    JSON和JS对象的格式一样，只不过JSON字符串中的属性名必须加双引号
                        其他和JS语法一致
                    JSON分类
                        1.对象{}
                        2.数组[]
                    JSON中允许的值：
                        1.字符串
                        2.数值
                        3.布尔值
                        4.null
                        5.对象
                        6.数组
        */
       //创建一个对象
    //    var obj = '{"name":"孙悟空","age":18,"gender":"男"}';

    //    var arr = '[1,2,3,"helo",true]';

       /* 
            JSON字符串转换为JS中的对象
                在JS中，为我们提供了一个工具类，就叫JSON

            JSON.parse()
                可以将JSON字符串转换为js对象
                它需要一个JSON字符串作为参数，会将该字符串转换为js对象
       */
      /* var json = '{"name":"孙悟空","age":18,"gender":"男"}';
      var o = JSON.parse(json);
      console.log(o.gender);//男 */



      var obj3 = {name:"猪八戒",age:28,gender:"男"};
      /* 
            js对象转JSON
                JSON.stringify()
                    将js对象转为JSON字符串
      */
     var str = JSON.stringify(obj3);
     console.log(str);//{"name":"猪八戒","age":28,"gender":"男"}






     /* 
        eval()
            这个函数可以执行一段字符串形式的JS代码，并将执行结果返回
            如果使用eval()执行的字符串中含有{}，它会将{}当成是代码块
            如果不希望是将其当成代码块解析，则需要在字符串前后各加一个()
        在开发中尽量不要使用，首先执行性能比较差，然后它还具有安全隐患


        var str = '{"name":"孙悟空","age":18,"gender":"男"}';
        var obj = eval("(" + str + ")");
     */
    </script>
</head>
<body>
    
</body>
```

