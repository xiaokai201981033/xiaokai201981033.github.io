什么是DOM?

DOM,全称Document Object Model文档对象模型

JS中通过DOM来对HTML文档进行操作。只要理解了DOM就可以随心所欲的操作WEB页面。

文档：

​	文档表示的就是整个的HTML网页文档

对象：

​	对象表示将网页中的每一个部分都转换为了一个对象

模型：

​	使用模型来表示对象之间的关系，这样方便我们获取对象。





节点

节点Node，是构成我们网页的最基本的组成部分，网页中的每一个部分都可以称为是一个节点。

节点：Node---构成HTML文档最基本的单元。

常用节点分为四类：

​	文档节点：整个HTML文档

​	元素节点：HTML文档中的HTML标签

​	属性节点：元素的属性

​	文本节点：HTML标签中的文本内容

### 节点的属性

|          | nodeName  | nodeType | nodeValue    |
| -------- | --------- | -------- | ------------ |
| 文档节点 | #document | 9        | null         |
| 元素节点 | 标签名    | 1        | null         |
| 属性节点 | 属性名    | 2        | 属性值       |
| 文本节点 | #text     | 3        | ==文本内容== |

事件

事件，就是文档或浏览器窗口中发生的一些特定的交互瞬间

JavaScript与HTML之间的交互是通过事件实现的。

对于Web应用来说，有下面这些代表性的事件：点击某个元素、将鼠标移动至某个元素上方、按下键盘上某个键，等等。

#### 文档的加载

```js
<!-- 
        浏览器加载 页面时，是按照自上向下的顺序加载的
        读取到一行就运行一行，如果将script标签写在页面的上边
        在代码执行时，页面还没有加载

        将js代码编写到页面的下部就是为了可以在页面加载完毕后再执行js代码


        onload事件会在整个页面加载完成之后才触发
        为window绑定一个onload事件
            该事件对应的响应函数将会在页面加载完成之后执行
            这样可以确保我们的代码执行时所有的DOM对象已经加载完毕了

     -->
     <script>
         window.onload = function(){
                var btn = document.getElementById("btn");
                btn.onclick = function(){
                    alert("hello");
                }
         };

     </script>
```

#### dom查询

```js
<script>
        window.onload = function(){
            //为id=btn01的按钮绑定一个单击响应函数
            var btn01 = document.getElementById("btn01");
            btn01.onclick = function(){
                //查找#bj的节点
                var bj = document.getAElementById("bj");
                //打印bj
                //innerHTML  通过这个属性可以获取到元素内部的html代码
                alert(bj.innerHTML);
            };

            //为id=btn02的按钮绑定一个单击响应函数
            var btn02 = document.getElementById("btn02");
            btn02.onclick = function(){
                //查找所有li节点
                //getElementsByTagName()可以根据标签名来获取一组元素节点对象
                //这个方法会给我们返回一个类数组对象，所有查询到的元素都会封装到对象中
                //即使查询到的元素只有一个，也会封装到类数组中返回
                var lis = document.getElementsByTagName("li");
                //打印lis
                //遍历lis
                for(var i = 0; i <lis.length ; i++){
                    alert(lis[i].innerHTML);
                }
            };
            //为id=btn02的按钮绑定一个单击响应函数
            var btn03 = document.getElementById("btn03");
            btn03.onclick = function(){
                //查找name=gender的所有节点
                var inputs = document.getElementsByName("gender");
                for(var i = 0; i <inputs.length ; i++){
                    /* 
                        innerHTML用户获取元素内部的HTML代码的
                        对于自结束标签，这个属性没有意义                    */
                    //alert(inputs[i].innerHTML);//这个不能用，没用

                    /* 
                        如果需要读取元素节点属性，直接使用元素.属性名
                            例子：元素.id  元素.name  元素.value
                            注意：class属性不能使用这种方式
                                读取class属性时需要使用   元素.className
                    */
                }
            };

        }
    </script>
```

#### 获取元素节点

通过document对象调用

1、getElementById()    通过id属性获取一个元素节点的对象

2、getElementsByTagName()    通过标签名获取一组元素节点对象

3、getElementsByName()      通过name属性获取一组元素节点对象



#### 获取元素节点的子节点

通过具体的元素节点调用

1、getElementByTagName()     方法，返回当前节点的指定标签名后代节点

2、childNodes      属性，表示当前节点的所有子节点

3、firstChild       属性，表示当前节点的第一个子节点

4、lastChild      属性，表示当前节点的最后一个子节点



#### 获取父节点和兄弟节点

通过具体的节点调用

1、parentNode    属性，表示当前节点的父节点

2、previousSibling   属性，表示当前节点的前一个兄弟节点

3、nextSibling    属性，表示当前节点的后一个兄弟节点

#### DOM查询的两个练习

```js
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <link rel="stylesheet" href="./04.domchaxun.css">
    <script>

        /* 
            定义一个函数，专门用来为指定元素绑定单击响应函数
            参数：
                idStr  要绑定单击响应函数的对象的id属性值
                fun   事件的回调函数，当单击元素时，该函数将会被触发
        */
       function myClick(idStr,fun){
           var btn = document.getElementById(idStr);
           btn.onclick = fun;
       }
        window.onload = function(){
            //为id=btn01的按钮绑定一个单击响应函数
            var btn01 = document.getElementById("btn01");
            btn01.onclick = function(){
                //查找#bj的节点
                var bj = document.getAElementById("bj");
                //打印bj
                //innerHTML  通过这个属性可以获取到元素内部的html代码
                alert(bj.innerHTML);
            };

            //为id=btn02的按钮绑定一个单击响应函数
            var btn02 = document.getElementById("btn02");
            btn02.onclick = function(){
                //查找所有li节点
                //getElementsByTagName()可以根据标签名来获取一组元素节点对象
                //这个方法会给我们返回一个类数组对象，所有查询到的元素都会封装到对象中
                //即使查询到的元素只有一个，也会封装到类数组中返回
                var lis = document.getElementsByTagName("li");
                //打印lis
                //遍历lis
                for(var i = 0; i <lis.length ; i++){
                    alert(lis[i].innerHTML);
                }
            };
            //为id=btn02的按钮绑定一个单击响应函数
            var btn03 = document.getElementById("btn03");
            btn03.onclick = function(){
                //查找name=gender的所有节点
                var inputs = document.getElementsByName("gender");
                for(var i = 0; i <inputs.length ; i++){
                    /* 
                        innerHTML用户获取元素内部的HTML代码的
                        对于自结束标签，这个属性没有意义                    */
                    //alert(inputs[i].innerHTML);//这个不能用，没用
                    alert(inputs[i].value);
                    /* 
                        如果需要读取元素节点属性，直接使用元素.属性名
                            例子：元素.id  元素.name  元素.value
                            注意：class属性不能使用这种方式
                                读取class属性时需要使用   元素.className
                    */
                }
            };

            //为id为btn04的按钮绑定一个单击响应函数
            var btn04 = document.getElementById("btn04");
            btn04.onclick = function(){
                //获取id为city的元素
                var city = document.getElementById("city");

                //查找#city下所有li节点
                var lis = city.getElementsByTagName("li");
                alert(lis.length);//4
                for(var i = 0;i < lis.length ; i++){
                    alert(lis[i].innerHTML);
                }
            };

            //为id为btn05的按钮绑定一个单击响应函数
            var btn05 = document.getElementById("btn05");
            btn05.onclick = function(){
                //获取id为city的节点
                var city = document.getElementById("city");
                //返回#city的所有子节点
                /* 
                    childNodes属性会获取包括文本节点在内的所有子节点
                    根据DOM标签，标签间的空白也会当成文本节点
                    注意：在IE8及以下的浏览器中，不会将空白文本当成子节点，
                        所以该属性在IE8中会返回4个子元素而其他浏览器是9个
                */
                var cns = city.childNodes;
                alert(cns.length);
                /* 
                    children属性可以获取当前元素的所有子元素，即标签
                */
                var cns2 = city.children;
                alert(cns2.length);
            };


            //为id为btn06的按钮绑定一个单击响应函数
            var btn06 = document.getElementById("btn06");
            btn06.onclick = function(){
                //获取id为phone的元素
                var phone = document.getElementById("phone");
                //返回#phone的第一个子节点
                //firstChild可以获取到当前元素的第一个子节点，包括文本节点
                var fir = phone.firstChild;
                alert(fir);//[object Text]
                //firstElementChild获取当前元素的第一个子元素，但是不支持IE8及以下的浏览器
                fir = phone.firstElementChild;
                alert(fir);
            }

            //为id为btn07的按钮绑定一个单击响应函数
            myClick("btn07",function(){
                //获取id为bj的节点
                var bj = document.getElementById("bj");

                //返回#bj的父节点
                var pn = bj.parentNode;
                alert(pn);//[object HTMLUListElement]
                alert(pn.innerHTML);
                                    /* <li id="bj">北京</li>
                                    <li>上海</li>
                                    <li>东京</li>
                                    <li>首尔</li> */

                /* 
                    innerText
                        该属性可以获取到元素内部的文本内容
                        他和innerHTML类似，不同的是它会自动将HTML删除
                */
               alert(pn.innerText);/*北京
                                    上海
                                    东京
                                    首尔*/
            });
            //为id为btn08的按钮绑定一个单击响应函数
            myClick("btn08",function(){
                //返回id为android的元素
                var and = document.getElementById("android");

                //返回#android的前一个兄弟节点(也可能获取到空白的文本)
                var ps = and.previousSibling;  //[object Text]
                //previousElementSibling  获取前一个兄弟元素，IE8以下不支持
                var pe = and.previousElementSibling;//[object HTMLLIElement]
                alert(ps);
                alert(pe);
            });
            //读取#username的value属性值
            myClick("btn09",function(){
                //获取id为username的元素
                var um = document.getElementById("username");

                //读取um的value属性值
                //文本框的value属性值，就是文本框中填写的内容
                alert(um.value);
            });
            //设置#username的value属性值
            myClick("btn10",function(){
                //获取id为username的元素
                var um = document.getElementById("username");

                um.value = "今天天气真不错~";
            });

            //返回#bj的文本值
            myClick("btn11",function(){
                //获取id为bj的元素
                var bj = document.getElementById("bj");

                alert(bj.innerHTML);
                alert(bj.innerText);

                //获取bj中的文本节点
                var fc = bj.firstChild;
                alert(fc.nodeValue);
                alert(bj.firstChild.nodeValue);
            })
        }
    </script>

</head>
<body>
    <div id="total">
        <div class="inner">
            <p>
                你喜欢哪个城市？
            </p>
            <ul id="city">
                <li id="bj">北京</li>
                <li>上海</li>
                <li>东京</li>
                <li>首尔</li>
            </ul>
            <br>
            <br>

            <p>
                你喜欢哪款单击游戏？
            </p>

            <ul id="game">
                <li id="rl">红警</li>
                <li>实况</li>
                <li>极品飞车</li>
                <li>魔兽</li>
            </ul>
            <br />
            <br />

            <p>
                你手机的操作系统是?
            </p>
            <ul id="phone">
                <li>IOS</li>
                <li id="android">Android</li>
                <li>Windows Phone</li>
            </ul>
        </div>
        <div class="inner">
            gender:
            <input type="radio" name="gender" value="male"/>
            Male
            <input type="radio" name="gender" value="female"/>
            Female
            <br>
            <br>
            name:
            <input type="text" name="name" id="username" value="abcde"/>
        </div>
    </div>
    <div id="btnList">
        <div><button id="btn01">查找#bj节点</button></div>
        <div><button id="btn02">查找所有li节点</button></div>
        <div><button id="btn03">查找name=gender的所有节点</button></div>
        <div><button id="btn04">查找#city下所有li节点</button></div>
        <div><button id="btn05">返回#city的所有子节点</button></div>
        <div><button id="btn06">返回#phone的第一个子节点</button></div>
        <div><button id="btn07">返回#bj的父节点</button></div>
        <div><button id="btn08">返回#android的前一个兄弟节点</button></div>
        <div><button id="btn09">返回#username的value属性值</button></div>
        <div><button id="btn10">设置#username的value属性值</button></div>
        <div><button id="btn11">返回#bj的文本值</button></div>

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
    <script>
        function myClick(idStr,fun){
            var btn = document.getElementById(idStr);
            btn.onclick=fun;
        }
        window.onload = function(){
            /* 
                全选按钮
                    点击按钮以后，四个多选框全都被选中
            */
           //为id为checkedAllBtn的按钮绑定一个单击响应函数
           myClick("checkedAllBtn",function(){
               //获取四个多选框items
               var items = document.getElementsByName("items");
               checkedAllBox.checked=true;

               //遍历items
               for(var i=0 ; i < items.length ; i++){
                   items[i].checked=true;
               }
           });
           myClick("checkedNoBtn",function(){
               //获取四个多选框items
               var items = document.getElementsByName("items");
               checkedAllBox.checked=false;

               //遍历items
               for(var i=0 ; i < items.length ; i++){
                   items[i].checked=false;
               }
           });
           myClick("checkedRevBtn",function(){
               //获取四个多选框items
               var items = document.getElementsByName("items");
               checkedAllBox.checked = true;
               //遍历items
               for(var i=0 ; i < items.length ; i++){
                   items[i].checked = !items[i].checked;
                   if(!items[i].checked){
                                checkedAllBox.checked = false;
                                
                            }

               }
               
               
            
           });
           myClick("sendBtn",function(){
               //获取四个多选框items
               var items = document.getElementsByName("items");

               //遍历items
               for(var i=0 ; i < items.length ; i++){
                   if(items[i].checked){
                       alert(items[i].value);
                   }
               }
           });
           myClick("checkedAllBox",function(){
               //获取四个多选框items
               var items = document.getElementsByName("items");

               //遍历items
               for(var i=0 ; i < items.length ; i++){
                   /* 
                        在事件响应函数中，响应函数是给谁绑定的this就是谁
                   */
                    if(this.checked){
                        items[i].checked=true;
                    }
                    else{
                        items[i].checked=false;
                    }
                }
            });



            var items = document.getElementsByName("items");
                for(var i =0;i < items.length ; i++){
                    items[i].onclick = function(){
                        //当点击一个时将所有的设置为选中
                        checkedAllBox.checked = true;
                        for(var j =0;j < items.length; j++){
                            //判断四个多选框是否全选
                            if(!items[j].checked){
                                checkedAllBox.checked = false;
                                break;
                            }
                        }
                    }
                
            }
            

    }
    </script>
</head>
<body>
    <form method="post" action="">
		你爱好的运动是？<input type="checkbox" id="checkedAllBox" />全选/全不选 
		
		<br />
		<input type="checkbox" name="items" value="足球" />足球
		<input type="checkbox" name="items" value="篮球" />篮球
		<input type="checkbox" name="items" value="羽毛球" />羽毛球
		<input type="checkbox" name="items" value="乒乓球" />乒乓球
		<br />
		<input type="button" id="checkedAllBtn" value="全　选" />
		<input type="button" id="checkedNoBtn" value="全不选" />
		<input type="button" id="checkedRevBtn" value="反　选" />
		<input type="button" id="sendBtn" value="提　交" />
</body>
</html>
```

#### DOM查询的剩余方法

```js
<script>
        window.onload = function(){
            //获取body标签
            // var body = document.getElementsByTagName("body")[0];

            /* 
                在document中有一个属性body，它保存的是body的引用
            */
           var body = document.body;
           /* 
                document.documentElement保存的是html根标签
           */
          var html = document.documentElement;
        //   console.log(html);
          /* 
            document.all表示页面中所有的元素
          */
         var all = document.all;
         for(var i=0;i < all.length ; i++){
            //  console.log(all[i]);
         }
         all = document.getElementsByTagName("*");//也表示获取所有元素


         /* 
                根据元素的class属性值查询一组元素节点对象
                getElementsByClassName()可以根据class属性值获取一组元素节点对象
                但是该方法不支持IE8及以下浏览器
         */
        var box1 = document.getElementsByClassName("box1");
        // console.log(box1.length);

        //获取页面中的所有div
        // var divs = document.getElementsByTagName("div");
            // console.log(divs.length);

         //获取class的为box1中的所有div
         /* 
            document.querySelector()
                需要一个选择器的字符串作为参数，可以根据一个CSS选择器来查询一个元素节点对象
                虽然IE8中没有document.getElementsByTagName，但是可以根据querySelector查询

                使用该方法总会返回唯一的一个元素，如果满足条件的元素有多个，那么会返回第一个元素
         */
        var div = document.querySelector(".box1 div");
        console.log(div.innerHTML);//我是box1中的div

        /* 
            document.querySelectorAll()
                该方法与上面方法类似，不同的是它将符合条件的元素封装到类数组中返回，
                即使符合条件的元素只有一个，也会返回成类数组
        */
        }
    </script>
</head>
<body>
    <div class="box1">
        <div>我是box1中的div</div>
    </div>
    <div class="box2"></div>
</body>
</html>
```

#### DOM增删改练习

```js
<script type="text/javascript">
	
	function delA(){
		//点击超链接后需要删除超链接所在的那一行
			//这里我们点击的超链接就是this
			//获取当前的tr
			var tr = this.parentNode.parentNode;
			//获取要删除员工的名字
			var name = tr.getElementsByTagName("td")[0].innerHTML;
			var name = tr.children[0].innerHTML;
			//删除之前弹出提示框
			/* 
				confirm()用于弹出一个带有确认和取消按钮的提示框
				需要一个字符串作为参数，该字符串将会作为提示文字显示出来
				点击确定返回true，取消返回false
			*/
			if(confirm("确认删除"+name+"吗？")){
			//删除tr
			tr.parentNode.removeChild(tr);
			}
			/* 
				点击超链接后，超链接会跳转页面，这个是超链接的默认行为，
				但是此时我们不希望出现默认行为，可以通过在响应函数的最后return false来取消默认行为
			*/
			return false;
	}
	window.onload = function(){
		/* 
			点击超链接以后，删除一个员工的信息
		*/
		//获取所有的超链接
		var allA= document.getElementsByTagName("a");

		//为每个超链接都绑定一个单击响应函数
		for(var i = 0; i < allA.length ; i++){
			allA[i].onclick = delA;
		}

		//获取提交按钮
		var submit = document.getElementById("addEmpButton")
		submit.onclick = function(){
			//获取员工信息
			var name = document.getElementById("empName").value;
			var email = document.getElementById("email").value;
			var salary = document.getElementById("salary").value;

			// 创建一个tr
			var tr = document.createElement("tr");

			// 设置tr中的内容
			tr.innerHTML ="<td>"+name+"</td>"+
			"<td>"+email+"</td>"+
			"<td>"+salary+"</td>"+
			"<td><a href='javascript:;'>Delete</a></td>";
			//获取刚刚添加的a元素，并为其绑定单击响应函数
			var a = tr.getElementsByTagName("a")[0];
            /* 
				for循环会在页面加载完成之后立即执行，
				而响应函数会在超链接被点击时才执行
				当响应函数执行时，for循环早以执行完毕
			*/
			a.onclick = delA;//这条语句执行时，i已经是allA.length的值了

			// 获取table
			var employeeTable = document.getElementById("employeeTable");

			// 获取employeeTable中的tbody
			var tbody = employeeTable.getElementsByTagName("tbody")[0];
			// 将tr添加到tbody中
			tbody.appendChild(tr);
		}
	};

	
</script>
</head>
<body>

	<table id="employeeTable">
		<tr>
			<th>Name</th>
			<th>Email</th>
			<th>Salary</th>
			<th>&nbsp;</th>
		</tr>
		<tr>
			<td>Tom</td>
			<td>tom@tom.com</td>
			<td>5000</td>
			<td><a href="javascript:;">Delete</a></td>
		</tr>
		<tr>
			<td>Jerry</td>
			<td>jerry@sohu.com</td>
			<td>8000</td>
			<td><a href="deleteEmp?id=002">Delete</a></td>
		</tr>
		<tr>
			<td>Bob</td>
			<td>bob@tom.com</td>
			<td>10000</td>
			<td><a href="deleteEmp?id=003">Delete</a></td>
		</tr>
	</table>

	<div id="formDiv">
	
		<h4>添加新员工</h4>

		<table>
			<tr>
				<td class="word">name: </td>
				<td class="inp">
					<input type="text" name="empName" id="empName" />
				</td>
			</tr>
			<tr>
				<td class="word">email: </td>
				<td class="inp">
					<input type="text" name="email" id="email" />
				</td>
			</tr>
			<tr>
				<td class="word">salary: </td>
				<td class="inp">
					<input type="text" name="salary" id="salary" />
				</td>
			</tr>
			<tr>
				<td colspan="2" align="center">
					<button id="addEmpButton" value="abc">
						Submit
					</button>
				</td>
			</tr>
		</table>

	</div>

</body>
```

#### 使用DOM操作CSS

```js
<style>
        #box1{
            width: 300px;
            height: 300px;
            background-color: #bfa;
        }
    </style>
    <script>
        window.onload = function(){
        	var box1 = document.getElementById("box1");
            var btn01 = document.getElementById("btn01");
            btn01.onclick= function(){

                /* 
                    通过JS修改元素的样式
                    语法：
                        元素.style.样式名 = 样式值;

                    注意：如果CSS的样式名有-,
                    这种名称在JS中是不合法的，需要修改为驼峰命名法

                    我们通过style属性设置的样式都是内联样式，而内联样式有较高的优先级，所以通过JS修改的样式往往会立即显示

                    但是如果在样式中写了!important,则此时即使通过JS修改样式，也不会生效
                */
                box1.style.width = "400px";
                box1.style.height = "400px";
                box1.style.backgroundColor="red";
            }


            var btn02 = document.getElementById("btn02");
            btn02.onclick= function(){
                /* 
                    读取box1的样式
                    语法：
                        元素.style.样式名;

                    通过style属性设置和读取的都是内联样式
                        无法读取样式表中的样式
                */
               alert(box1.style.height);
            }
        }
    </script>
</head>
<body>
    <button id="btn01">点我一下</button>
    <button id="btn02">点我一下</button>
    <br>
    <br>
    <div id="box1"></div>
</body>
```

#### 读取元素的样式

```js
<style>
        #box1{
            width: 300px;
            height: 300px;
            background-color: #bfa;
        }
    </style>
    <script>
        window.onload = function(){
            var box1 = document.getElementById("box1");
            var btn01 = document.getElementById("btn01");
            btn01.onclick = function(){
                /* 
                    获取元素的当前显示的样式
                    语法：
                        元素.currentStyle.样式名
                    它可以用来读取当前元素正在显示的样式，如果当前元素没有设置该样式，则获取它的默认值
                    currentStyle只有IE浏览器支持
                */
                // alert(box1.currentStyle.width);


                /* 
                    在其他浏览器中可以使用：
                        getComputedStyle()这个方法来获取当前元素的样式
                        这个方法是window的方法可以直接使用
                    需要两个参数：
                        第一个：要获取样式的元素
                        第二个：可以传递一个伪元素，一般都传null

                    该方法会返回一个对象，对象中封装了当前元素的样式

                    如果获取的样式没有设置，则会获取真实的值，而不是默认值
                    比如：没有设置width，他不会获取到auto，而是一个长度

                    该方法不支持IE8及以下浏览器
                */
               /* 
                    上面两个读取到的样式都是只读的，不能修改，如果要修改必须通过style属性
               */
            //    var obj = getComputedStyle(box1,null);
               //alert(obj);//[object CSSStyleDeclaration]
            //    alert(obj.width);

            // alert(getStyle(box1,"width"));

            var w = getStyle(box1,"width");
            alert(w);
            
            }

        }
                /* 
                    定义一个函数，用来获取指定元素的当前的样式
                    参数：
                        obj   要获取样式的元素
                        name   要获取的样式名
               */
               function  getStyle(obj,name){
                   if(window.getComputedStyle){//这里如果不加window它是一个变量，要在全局作用域中去寻找，没找到就会报错，加了window，变成对象的属性，属性没找到返回undefined
                    return getComputedStyle(obj,null)[name];
                   }else{
                    return obj.currentStyle[name];
                   }

                //正常浏览器的方式
                //return getComputedStyle(obj,null)[name];//这个中括号意思为  [变量]  直接获取为变量值的属性


                //IE8的方式
                //   return obj.currentStyle[name];
            }   
    </script>
</head>
<body>
    <button id="btn01">点我一下</button>
    <br><br>
    <div id="box1"></div>
</body>
```

#### DOM其他样式操作属性

```js
<style>
        #box1{
            width: 100px;
            height: 100px;
            background-color: red;
            padding: 10px;
            border: 10px solid yellow;
        }
        #box2{
            padding: 100px;
            background-color: #bfa;
        }
        #box4{
            width: 200px;
            height: 300px;
            background-color: #bfa;
            overflow: auto;
        }
        #box5{
            width: 450px;
            height: 600px;
            background-color: yellow;
        }
    </style>
    <script>
        window.onload = function(){
            var box1 = document.getElementById("box1");
            var btn01 = document.getElementById("btn01");
            var box4 = document.getElementById("box4");
            btn01.onclick= function(){
                /* 
                    clientHeight;
                    clientWidth;
                        这两个属性可以获取元素的可见宽度和高度
                        这些属性都是不带px的，返回的都是一个数字，可以直接进行计算
                        包括内容区和内边距
                        这些属性都是只读的，不能修改
                */
                //alert(box1.clientHeight);//120 返回值不带px


                /* 
                    offsetWidth
                    offsetHeight
                        获取元素的整个宽度和高度，包括内容区和内边距和边框
                */
                // alert(box1.offsetWidth);

                /* 
                    offsetParent
                        可以用来获取当前元素的定位父元素
                        会获取到离当前元素最近的开启了定位的祖先元素
                        如果所有祖先元素都没有开启定位，则返回body
                */
                var op = box1.offsetParent;
                //alert(op.id);//box2


                /* 
                    offsetLeft
                        当前元素相对于其定位父元素的水平偏移量
                    offsetTop
                        当前元素相对于其定位父元素的垂直偏移量
                */
               //alert(box1.offsetLeft);//100


               //alert(box4.clientHeight);//300

               /* 
                    scrollHeight
                    scrollWidth
                        可以获取元素整个滚动区域的高度
               */
               //alert(box4.scrollHeight);//600
               //alert(box4.scrollWidth);//450

               /* 
                    scrollLeft
                    scrollTop
                        获取滚动条水平和垂直滚动的距离
               */
               //alert(box4.scrollLeft);



               //alert(box4.clientHeight);//283

               //当满足.scrollHeight - .scrollTop == clientHeight时，说明垂直滚动条滚动到底了
               //当满足.scrollWidth - .scrollLeft == clientWidth时，说明水平滚动条滚动到底了
                alert(box4.scrollHeight - box4.scrollTop);//整个滚动区域高度 - 滚动条垂直方向上滚动的距离
            };
        };
    </script>

</head>
<body>
    <button id="btn01">点我一下</button>
    <br><br>
    <div id="box4">
        <div id="box5"></div>
    </div>
    <br><br>
    <div id="box3" style="position:relative;">
        <div id="box2" style="position:relative;">
            <div id="box1"></div>
        </div>
    </div>
</body>
```

#### 滚动条滚动到底练习

```js
<style>
        #info{
            width: 400px;
            height: 500px;
            background-color: #bfa;
            overflow: auto;
        }
    </style>
    <script>
        window.onload = function(){
            /* 
                当滚动条滚动到底时使表单可用
                onscroll
                    该事件会在元素的滚动条滚动时触发
            */
           //获取id为info的p元素
           var info = document.getElementById("info");
           //获取两个表单项
           var inputs = document.getElementsByTagName("input");
           //为info绑定一个滚动条滚动的事件
           info.onscroll = function(){
            //    检查滚动条是否滚动到底
                if(info.scrollHeight - parseInt(info.scrollTop) < info.clientHeight+1){
                    // alert("我已经滚到底了");


                    //滚动条滚动到底使表单项可用
                    /* 
                        disabled属性可以设置一个元素是否禁用
                        如果设置为true，表示元素禁用
                        设置为false，表示元素可以使用
                    */
                    inputs[0].disabled = false;//disabled可以使用
                    inputs[1].disabled = false;
                }
           };
        };
    </script>
</head>
<body>
    <h3>欢迎注册</h3>
    <p id="info">
        请认为你真阅读请认为你真阅读请认为你真阅读
        请认为你真阅读请认为你真阅读请认为你真阅读
        请认为你真阅读请认为你真阅读请认为你真阅读
        请认为你真阅读请认为你真阅读请认为你真阅读
        请认为你真阅读请认为你真阅读请认为你真阅读
        请认为你真阅读请认为你真阅读请认为你真阅读
        请认为你真阅读请认为你真阅读请认为你真阅读
        请认为你真阅读请认为你真阅读请认为你真阅读
        请认为你真阅读请认为你真阅读请认为你真阅读
        请认为你真阅读请认为你真阅读请认为你真阅读
        请认为你真阅读请认为你真阅读请认为你真阅读
        请认为你真阅读请认为你真阅读请认为你真阅读
        请认为你真阅读请认为你真阅读请认为你真阅读
        请认为你真阅读请认为你真阅读请认为你真阅读
        请认为你真阅读请认为你真阅读请认为你真阅读
        请认为你真阅读请认为你真阅读请认为你真阅读
        请认为你真阅读请认为你真阅读请认为你真阅读
        请认为你真阅读请认为你真阅读请认为你真阅读
        请认为你真阅读请认为你真阅读请认为你真阅读
        请认为你真阅读请认为你真阅读请认为你真阅读
        请认为你真阅读请认为你真阅读请认为你真阅读
        请认为你真阅读请认为你真阅读请认为你真阅读
        请认为你真阅读请认为你真阅读请认为你真阅读
        请认为你真阅读请认为你真阅读请认为你真阅读
        请认为你真阅读请认为你真阅读请认为你真阅读
        请认为你真阅读请认为你真阅读请认为你真阅读
        请认为你真阅读请认为你真阅读请认为你真阅读
        请认为你真阅读请认为你真阅读请认为你真阅读
        请认为你真阅读请认为你真阅读请认为你真阅读
        请认为你真阅读请认为你真阅读请认为你真阅读
        请认为你真阅读请认为你真阅读请认为你真阅读
        请认为你真阅读请认为你真阅读请认为你真阅读
        请认为你真阅读请认为你真阅读请认为你真阅读
        请认为你真阅读请认为你真阅读请认为你真阅读
        请认为你真阅读请认为你真阅读请认为你真阅读
        请认为你真阅读请认为你真阅读请认为你真阅读
        请认为你真阅读请认为你真阅读请认为你真阅读
        请认为你真阅读请认为你真阅读请认为你真阅读
        请认为你真阅读请认为你真阅读请认为你真阅读
        请认为你真阅读请认为你真阅读请认为你真阅读
        请认为你真阅读请认为你真阅读请认为你真阅读
        请认为你真阅读请认为你真阅读请认为你真阅读
    </p>
    <!-- 如果为表单项添加 disabled="disabled"，则表单项将变成不可用状态 -->
    <input type="checkbox" disabled="disabled" />我已经仔细阅读协议
    <input type="submit" value="注册" disabled="disabled" />
</body>
```

#### 事件对象

```js
<style type="text/css">

	#areaDiv {
		border: 1px solid black;
		width: 300px;
		height: 50px;
		margin-bottom: 10px;
	}
	
	#showMsg {
		border: 1px solid black;
		width: 300px;
		height: 20px;
	}

</style>
<script type="text/javascript">

	window.onload = function(){
		/* 
			当鼠标在areaDiv中移动时，在showMsg中来显示鼠标的坐标
		*/
		//获取两个Div
		var areaDiv = document.getElementById("areaDiv");
		var showMsg = document.getElementById("showMsg");

		/* 
			onmousemove
				该事件将会在鼠标在元素中移动时被触发
			事件对象
				当事件的响应函数被触发时，浏览器每次都会将一个事件对象作为实参传递进响应函数，
				在事件对象中封装了当时事件相关的一切信息，比如： 鼠标的坐标 键盘哪个按键被按下 鼠标滚轮滚动的方向。。。
		*/
		areaDiv.onmousemove = function(event){
			/* 
				在IE8中，响应函数被触发时，浏览器不会传递事件对象
				在IE8及以下的浏览器中，是将事件对象作为window对象的属性保存的，要变为
				var x = window.event.clientX;//火狐不行
			*/

			//解决事件对象兼容性问题
			if(!event){
				event=window.event;
			}

			event = event || window.event;//和上面一样的
			/* 
				clientX可以获取鼠标的水平坐标
				clientY可以获取鼠标的垂直坐标
			*/

			var x = event.clientX;
			var y = event.clientY;
			// alert("x = " + x + ", y = "+y);
			//在showMsg显示坐标
			showMsg.innerHTML = "x = " + x + ", y = "+y ;
		};
		
	};

</script>
</head>
<body>

	<div id="areaDiv"></div>
	<div id="showMsg"></div>

</body>
```

#### 事件对象练习

```js
<style>
        body{
            width: 2000px;
            height: 1000px;
        }
        #box1{
            width: 100px;
            height: 100px;
            background-color: red;
            /* 开启绝对定位 */
            position: absolute;
        }
    </style>
    <script>
        window.onload = function(){
            //获取box1
            var box1 = document.getElementById("box1");
            //绑定鼠标移动事件，给整个文档绑定
            document.onmousemove = function(event){
                //解决兼容性问题
                event = event || window.event;
                //获取滚动条的距离
                /* 
                    chrome认为浏览器的滚动条是body的，可以通过body.scrollTop来获取
                    火狐等浏览器认为浏览器的滚动条是HTML的，通过documentElement.scrollTop来获取
                */
            //    var st = document.body.scrollTop;
            //    var st = document.documentElement.scrollTop;

               //解决兼容
               var st = document.body.scrollTop || document.documentElement.scrollTop;
               var sl = document.body.scrollLeft || document.documentElement.scrollLeft;
            //    console.log(st);

                //获取鼠标坐标
                /* 
                    clientX和clientY是获取鼠标在当前可见窗口的坐标
                    Div的偏移量，是相对于整个页面的


                    pageX和pageY是获取鼠标相对于整个页面的坐标
                    但是这两个属性在IE8中不支持
                */
                /* var left = event.clientX;
                var top = event.clientY; */

                /* var left = event.pageX;
                var top = event.pageY; */

                var left = event.clientX;
                var top = event.clientY;
                //设置div的偏移量
                box1.style.left = left + sl + "px";//加上水平滚动条滚动距离
                box1.style.top = top + st + "px";//加上滚动条垂直方向滚动的距离
            };
            var box2 = document.getElementById("box2");
            box2.onmousemove = function(event){

                //取消冒泡
                event = event || window.event;
                event.cancelBubble = true;
            }
        };
    </script>
</head>
<body>
    <div id="box2" style="width:500px;height: 500px;background-color: #bfa;"></div>
    <div id="box1"></div>
</body>
```

#### 事件的冒泡

```js
<style>
        #box1{
            width: 200px;
            height: 200px;
            background-color: yellowgreen;
        }
        #s1{
            background-color: yellow;
        }
    </style>
    <script>
        window.onload = function(){

            /* 
                事件的冒泡(Bubble)
                所谓的冒泡指的就是事件的向上传导，当后代元素上的事件被触发时，其祖先元素的相同事件也会被触发
                大部分情况下冒泡都是有用的，如果不希望冒泡，可以通过对象取消
            */
            //为s1绑定单击响应函数
            var s1 = document.getElementById("s1");
            s1.onclick = function(event){
                event = event || window.event;
                alert("我是span单击响应函数");

                //取消冒泡
                //可以将事件对象的cancelBubble设置为true，即可取消冒泡
                event.cancelBubble = true;
            };

            //为box1绑定单击响应函数
            var box1 = document.getElementById("box1");
            box1.onclick = function(){
                alert("我是div的单击响应函数");
            };

            //为body绑定单击响应函数
            document.body.onclick = function(){
                alert("我是body的单击响应函数");
            };
        };
    </script>
</head>
<body>
    <div id="box1">
        我是box1
        <span id="s1">我是span</span>
    </div>
</body>
```

#### 事件的委派

```js
<script>
        window.onload = function(){
            var btn01 = document.getElementById("btn01");
            var ul = document.getElementById("ul");
            btn01.onclick = function(){
                //创建一个li
                var li = document.createElement("li");
                li.innerHTML = "<a href='javascript:;' class='link'>新链接</a>";
                //将li添加到ul中
                ul.appendChild(li);
            };


            //获取所有的a
            var allA = document.getElementsByTagName("a");
            //遍历

             
           /*      这里我们为每一个超链接都绑定了一个单击响应函数，但是这中操作只能为已有的超链接设置，新添加的超链接必须重新绑定
           
            for(var i=0;i<allA.length;i++){
                allA[i].onclick = function(){
                    alert("我是a的单击响应函数");
                };
            }; */

            /* 
                我们希望，只绑定一次事件，即可应用到多个元素上，即使元素是后添加的
                我们可以尝试将其绑定给元素的共同祖先元素

                事件的委派
                    指将事件统一绑定给元素共同的祖先元素，这样当后代元素上的事件触发时，会一直冒泡到祖先元素
                        从而通过祖先元素的响应函数来处理事件
                事件的委派是利用了冒泡，通过委派可以减少事件绑定的次数，提高程序的性能
            */
           //为ul绑定一个单击响应函数
           ul.onclick = function(event){
               event = event || window.event;
               /* 
                    target
                        event中的target表示的触发事件的对象
               */
                //alert(event.target);
               //如果触发事件的对象是我们期望的元素，则执行，否则不执行
               //alert("我是ul的单击响应函数");

               if(event.target.className == "link"){
                alert("我是ul的单击响应函数");
               }
           };


        };
    </script>
</head>
<body>
    <button id="btn01">添加超链接</button>
    <ul id="ul">
        <li>
            <p>我是p元素</p>
        </li>
        <li><a href="javascript:;" class="link">超链接一</a></li>
        <li><a href="javascript:;" class="link">超链接二</a></li>
        <li><a href="javascript:;" class="link">超链接三</a></li>
    </ul>
</body>
```

#### 事件的绑定

```js
<script>
        window.onload = function(){
            var btn01 = document.getElementById("btn01");

            /* 
                使用 对象.事件=函数 的形式绑定响应函数，
                它只能同时为一个元素的一个事件绑定一个响应函数，
                不能绑定多个，如果绑定多个，则后边的会覆盖前边的
            */
       /*  btn01.onclick = function(){
            alert(1);
        };
        btn01.onclick = function(){
            alert(2);
        }; */


        /* 
            addEventListener("click",function(){},false)
                通过该方法也可以为元素绑定响应函数
                参数：
                    1.事件的字符串  ，不要on
                    2.回调函数，当事件触发时该函数会被调用
                    3.是否在捕获阶段触发事件，需要一个布尔值，一般都传false
                里面的this是绑定事件的对象
            使用这种方式可以同时为一个元素的相同事件同时绑定多个响应函数，
            这样当事件被触发时，响应函数将会按照函数的绑定顺序执行

            IE8及以下不支持
        */
       /*  btn01.addEventListener("click",function(){
            alert(1);
        },false);
        btn01.addEventListener("click",function(){
            alert(2);
        },false); */

        /* 
            attachEvent()
                在IE8中可以使用attachEvent()来绑定事件
                参数：
                    1.事件的字符串  ，要on
                    2.回调函数
                里面的this是window
        使用这种方式可以同时为一个元素的相同事件同时绑定多个响应函数，
        不同的是，后绑定先执行
            
        */
       /* btn01.attachEvent("onclick",function(){
           alert(1);
       })
       btn01.attachEvent("onclick",function(){
           alert(2);
       }) */

       /* 
            定义一个函数，用来为指定元素绑定响应函数
            参数：
                obj要绑定事件的对象
                eventStr事件的字符串
                callback 回调函数
       */
      function bind(obj,eventStr,callback){
          if(obj.addEventListener){
              //大部分浏览器兼容的方式
              obj.addEventListener(eventStr,callback,false);
          }else{
              /* 
                    this是谁由调用方式决定
                    callback.call(obj)
              */
              //IE8以下
              //obj.attachEvent("on"+eventStr,callback);
              obj.attachEvent("on"+eventStr,function(){
                  //在匿名函数中调用回调函数，相当于用函数的方法调用回调函数，可以用call改变this
                  callback.call(obj);
              });
          }
      }
      bind(btn01,"click",function(){
          alert(1);
      })
      bind(btn01,"click",function(){
          alert(2);
      })
    };
        
    </script>
</head>
<body>
    <button id="btn01">点我以下</button>
</body>
```

#### 事件的传播

```js
<style>
        #box1{
            width: 300px;
            height: 300px;
            background-color: yellowgreen;
        }
        #box2{
            width: 200px;
            height: 200px;
            background-color: yellow;
        }
        #box3{
            width: 150px;
            height: 150px;
            background-color: skyblue;
        }
    </style>
    <script>
        window.onload = function(){
            var box1 = document.getElementById("box1");
            var box2 = document.getElementById("box2");
            var box3 = document.getElementById("box3");
            /* 
                事件的传播
                    关于事件的传播网景公司和微软公司有不同的理解
                    微软公司认为事件应该是由内向外传播，也就是说当事件触发时，应该先触发当前元素上的事件，
                        然后再向当前元素的祖先元素上传播，也就是说事件应该在冒泡阶段执行
                    网景公司认为事件应该是由外向内传播的，也就是当事件触发时，应该先触发当前元素的最外层的祖先元素的事件，
                        然后再向内传播给后代元素
                    w3c综合了两个公司方案，将事件分成了三个阶段
                        1.捕获阶段
                            在捕获阶段时从最外层的祖先元素，向目标元素进行事件的捕获，但是默认此时不会触发事件
                        2.目标阶段
                            事件捕获到目标元素，捕获结束开始在目标元素上触发事件
                        3.冒泡阶段
                            事件从目标元素向祖先元素传递，依次触发祖先元素上的事件
                如果想要在捕获阶段就触发事件，可以将addEventListener(eventStr,callback,true)中的第三个参数设置为true
                    一般情况下我们不会希望在捕获阶段触发事件，所以这个参数一般都是false
                IE8及以下的浏览器中没有捕获阶段
            */
        function bind(obj,eventStr,callback){
          if(obj.addEventListener){
              //大部分浏览器兼容的方式
              obj.addEventListener(eventStr,callback,false);
          }else{
              /* 
                    this是谁由调用方式决定
                    callback.call(obj)
              */
              //IE8以下
              //obj.attachEvent("on"+eventStr,callback);
              obj.attachEvent("on"+eventStr,function(){
                  //在匿名函数中调用回调函数，相当于用函数的方法调用回调函数，可以用call改变this
                  callback.call(obj);
              });
          }
        }
        bind(box1,"click",function(event){
            alert("我是box1的响应函数");
            //取消冒泡
            //event.cancelBubble = true;
        });

        bind(box2,"click",function(event){
            alert("我是box2的响应函数");
            //event.cancelBubble = true;
        });

        bind(box3,"click",function(){
            alert("我是box3的响应函数");
            //event.cancelBubble = true;

        });
        };
    </script>
</head>
<body>
    <div id="box1">
        <div id="box2">
            <div id="box3"></div>
        </div>
    </div>
</body>
```

#### 事件练习-拖拽

```js
<style>
        #box1{
            width: 100px;
            height: 100px;
            background-color: red;
            position: absolute;
        }
        #box2{
            width: 100px;
            height: 100px;
            background-color: aqua;
            position: absolute;
            top: 200px;
            left: 200px;
        }
    </style>
    <script>
        window.onload = function(){
            /* 
                拖拽box1元素
                拖拽流程
                    1.当鼠标在被拖拽元素上按下时，开始拖拽  onmousedown
                    2.当鼠标移动时被拖拽元素跟随鼠标移动   onmousemove
                    3.当鼠标松开时，被拖拽元素固定在当前位置   onmouseup
            */
           var box1 = document.getElementById("box1");
           var box2 = document.getElementById("box2");

           drag(box1);
           drag(box2);
        };
        //拖拽的函数
        function drag(obj){
                obj.onmousedown = function(event){
                event = event || window.event;
                //鼠标偏移量  鼠标.clientX - 元素.offsetLeft
                //           鼠标.clientY - 元素.offsetTop
                var ol = event.clientX - obj.offsetLeft;
                var ot = event.clientY - obj.offsetTop;

                //当鼠标移动时被拖拽元素跟随鼠标移动
                //为document绑定一个onmousemove 事件
                document.onmousemove = function(event){
                    event = event || window.event;
                    //当鼠标松开时，被拖拽元素固定在当前位置
                    //获取鼠标的坐标
                    var left = event.clientX - ol;
                    var top = event.clientY - ot;

                    //修改box1的位置
                    obj.style.left = left + "px";
                    obj.style.top = top + "px";
                };
                //为document绑定一个鼠标松开事件
                document.onmouseup = function(){
                    //当鼠标松开时，被拖拽元素固定在当前位置
                    //取消document的onmousemove事件
                    document.onmousemove = null;

                    //取消document的onmouseup事件
                    document.onmouseup = null;
                };

                /* 
                    当我们拖拽一个网页中的内容时，浏览器会默认去搜索引擎中搜索内容，
                    此时会导致拖拽功能的异常，这个是浏览器提供的默认行为，
                    如果不希望发生这个行为，可以通过return false 来取消默认行为
                    当时对IE8没用
                */
               return false;
           };
        }
    </script>
</head>
<body>
    我是一段文字
    <div id="box2"></div>
    <div id="box1"></div>
</body>
</html>

<!-- //设置box1捕获所有鼠标按下的事件
               box1.setCapture();//只有IE8支持
//当鼠标松开时，取消对事件的捕获
                box1.releaseCapture(); -->
```

#### 滚轮事件

```js
<style>
        #box1{
            width: 100px;
            height: 100px;
            background-color: red;
        }
    </style>
    <script>
        window.onload = function(){
            /* 
                当鼠标滚轮向下滚动时，box1变长
                当滚轮向上滚动时，box1变短
            */
           //获取id为box1的div
           var box1 = document.getElementById("box1");
           /* 
                onmousewheel鼠标滚轮事件
                火狐不支持该属性

                在火狐中需要使用DOMMouseScroll 来绑定滚动事件
                注意该事件需要通过addEventListener()函数来绑定
           */
          box1.onmousewheel = function(event){
              event = event || window.event;
              /* 
                    判断鼠标滚轮滚动的方向
                    event.wheelDelta  可以获取鼠标滚轮的方向
                    向上滚120，向下滚 -120
              */
             /* 
                    wheelDelta这个属性火狐中不支持
                    在火狐中使用event.detail来获取方向
                    向上滚-3  向下滚3
             */
            if(event.wheelDelta > 0 || event.detail < 0){
                //向上滚变短
                box1.style.height = box1.clientHeight - 10 + "px";
            }else{
                //向下滚变长
                box1.style.height = box1.clientHeight + 10 + "px";
            }
            /* 
                当滚轮滚动时，如果浏览器有滚动条，滚动条会随之滚动
                这是浏览器的默认行为，可以取消
            */
           return false;

           /* 
                使用addEventListener()方法绑定响应函数，取消默认行为时不能使用return false
                需要使用event来取消默认行为
                但是IE8不支持event.preventDefault();这个，如果直接调用会报错
           */
          event.preventDefault();
          };
          bind(box1,"DOMMouseScroll",box1.onmousewheel)
        };
        function bind(obj,eventStr,callback){
          if(obj.addEventListener){
              //大部分浏览器兼容的方式
              obj.addEventListener(eventStr,callback,false);
          }else{
              /* 
                    this是谁由调用方式决定
                    callback.call(obj)
              */
              //IE8以下
              //obj.attachEvent("on"+eventStr,callback);
              obj.attachEvent("on"+eventStr,function(){
                  //在匿名函数中调用回调函数，相当于用函数的方法调用回调函数，可以用call改变this
                  callback.call(obj);
              });
          }
      }
    </script>
</head>
<body style="height: 2000px;">
    <div id="box1"></div>
</body>
```

#### 键盘事件

```js
<script>
        window.onload = function(){
            /* 
                键盘事件：
                    onkeydown
                        按键按下
                        如果一直按着不放，事件会一直触发
                        当onkeydown连续触发时，第一次和第二次之间会间隔稍微长一点，其他的会非常快
                    onkeyup
                        按键松开

                键盘事件一般都会绑定给一些可以获取到焦点的对象或者是document
            */
           document.onkeydown = function(event){
               event = event || window.event;
                /* 
                    可以通过keycode来获取按键编码,用来判断哪个键被按下
                    除了keycode，事件对象中还提供了几个属性
                        altKey
                        ctrlKey
                        shiftKey
                            这三个用来判断alt ctrl shift 是否被按下
                            如果按下则返回true，否则返回false
                */
               //判断y是否被按下
               if(event.keyCode === 89){
                   alert("y被按下了");
               }
               //p判断ctrl 和 y 是否同时被按下
               if(event.keyCode === 89 && event.ctrlKey){
                   alert("同时被按下了");
               }
            //    console.log("按下");
           };
           document.onkeyup = function(){
            //    console.log("松开");
           };


           var input = document.getElementsByTagName("input")[0];
           input.onkeydown = function(event){
               event = event || window.event;
               //在文本框中输入内容，属于onkeydown默认行为
            //    如果取消默认行为，则内容不会出现在文本框中
            //使文本框中不能输入数字
            if(event.keyCode >= 48 && event.keyCode <=57){
                return false;//取消默认行为
            }
           };
        };
    </script>
</head>
<body>
    <input type="text">
</body>
```



#### 键盘事件练习

```js
<style>
        #box1{
            width: 100px;
            height: 100px;
            background-color: red;
            position:absolute;
        }
    </style>
    <script>
        window.onload = function(){
            var box1 = document.getElementById("box1");
            document.onkeydown = function(event){
                event = event || window.event;
                var speed= 10;
                if(event.ctrlKey){
                    speed = 500;
                }
                /* 
                    上  38
                    下  40
                    左  37
                    右  39
                */
                // console.log(event.keyCode);
                var left = box1.offsetLeft;//获取div在窗口里的位置
                var top = box1.offsetTop;
                switch(event.keyCode){
                    case 37:
                        box1.style.left = left - speed + "px";
                        break;
                    case 38:
                        box1.style.top = top - speed + "px";
                        break;
                    case 39:
                        box1.style.left = left + speed + "px";
                        break;
                    case 40:
                        box1.style.top = top + speed + "px";
                        break;
                }
                
            };
        };
    </script>
</head>
<body>
    <div id="box1"></div>
</body>
```

