# PHP基础

标签（空格分隔）： PHP

---

### 基本语法：PHP 脚本可以放在文档中的任何位置,PHP 脚本以 <?php 开始，以 ?> 结束：

```
<?php
// PHP 代码
?>

```
- 输出“helloWorld”：

```
<!DOCTYPE html> 
<html> 
<body> 

<h1>My first PHP page</h1> 

<?php 
echo "Hello World!"; 
?> 

</body> 
</html>

```

### PHP 中的注释

```
<?php
    // 这是 PHP 单行注释
    
    /*
    这是 
    PHP 多行
    注释
    */
?>
```

### PHP变量

```
<?php
    $x=5;
    $y=6;
    $z=$x+$y;
    echo $z;
?>
```
**PHP变量规则：**

变量以 $ 符号开始，后面跟着变量的名称；

变量名必须以字母或者下划线字符开始；

变量名只能包含字母数字字符以及下划线（A-z、0-9 和 _ ）；

变量名不能包含空格；

变量名是区分大小写的（$y 和 $Y 是两个不同的变量）；

### 创建（声明）PHP 变量
PHP 没有声明变量的命令。
变量在您第一次赋值给它的时候被创建。

### PHP 变量作用域
变量的作用域是脚本中变量可被引用/使用的部分。
PHP 有四种不同的变量作用域：
- local
- global
- static
- parameter

### 局部和全局作用域
在所有函数外部定义的变量，拥有全局作用域。除了函数外，全局变量可以被脚本中的任何部分访问，要在一个函数中访问一个全局变量，需要使用 global 关键字。
在 PHP 函数内部声明的变量是局部变量，仅能在函数内部访问：

```
<?php 
    $x=5; // 全局变量 
    
    function myTest(){ 
        $y=10; // 局部变量 
        echo "<p>测试函数内变量:<p>"; 
        echo "变量 x 为: $x";   // x:
        echo "<br>"; 
        echo "变量 y 为: $y";   // y:10
    }  
    
    myTest(); 
    
    echo "<p>测试函数外变量:<p>"; 
    echo "变量 x 为: $x";   // x:5
    echo "<br>"; 
    echo "变量 y 为: $y";   // y:
?>
```
### PHP global 关键字
global 关键字用于函数内访问全局变量。
在函数内调用函数外定义的全局变量，我们需要在函数中的变量前加上 global 关键字：

### PHP中双引号和单引号有什么区别呢？

【重要知识点】PHP面试题中，高概率面试题（建议背诵并实验三遍以上）

- 1.双引号解析变量，但是单引号不解析变量。

- 2.在双引号里面插入变量，变量后面如果有英文或中文字符，它会把这个字符和变量拼接起来，视为一整个变量。一定要在变          量后面接上特殊字符，例如空格等分开。

- 3.如果在双引号里面插变量的时候，后面不想有空格，可以拿大括号将变量包起来。

- 4.双引号解析转义字符，单引号不解析转义字符。但，单引号能解析\' 和\

- 5.单引号效率高于双引号，尽可能使用单引号

- 6.双号和单引号可以互插！！！双引号当中插入单引号，单引号当中插入变量，这个变量会被解析。

- 7.神奇的字符串拼接胶水——（.）点，用来拼接字符串。

- 8.我们将定界符声明字符串视为双引号一样的功能来看待。

### dump函数
```
// var_dump();
$fl = 0.8873;
var_dump($fl);     //float(0.8873)
是一个函数。向括号()中间插入变量。这个函数，会打印出来数据类型，还会对应显示变量的长度和值。
```
### null
php中主要有以下三空情况会产生空（null）类型：

- 1.通过变量赋值明确指定为变量的值为NULL；

- 2.一个变量没有给任何值；

- 3.使用函数unset()将变量销毁掉；

empty()可以向括号中间传入一个变量。这个变量的值如果为false或者为null的话，返回true。

```
//声明变量为null
$n = null;
var_dump($n); // NULL; 
if( $n ){
    echo 'null为true';
}else{
    echo 'null为false'; //执行这里的代码
}

```
isset()可以向括号中间传入一个或者多个变量，变量与变量间用逗号分开。只要有有一个变量为null，则返回false。否则，则返回true。

```
$jia = false;
$kong = null;

$result = isset($jia);
var_dump($result);  // 输出bool(false)

$result2 = isset($kong);
var_dump($result2);  // 输出bool(false)

```
unset()这个函数的功能是销毁变量。unset(变量)括号中间插入想要毁掉的变量名，这个变量就会被销毁。
```
$jia = null;

unset($jia);

var_dump($jia);     // 输出NULL

```
### 判断数据类型

我们使用is_* 系列函数。 is_types这一系列的函数，来进行判断某个东西是不是某个类型。如果是这个类型返回真，不是这个类型返回假。
```
is_int      是否为整型
is_bool     是否为布尔
is_float    是否是浮点
is_string   是否是字符串
is_array    是否是数组
is_object   是否是对象
is_null     是否为空
is_resource     是否为资源
is_scalar       是否为标量
is_numeric      是否为数值类型
is_callable     是否为函数
```

### php数据类型之自动转换和强制转换

**自动类型转换**，就是数据类型在某些情况下，自动会变为其他的类型参与运算。自动类型转换的发生时机是：运算和判断的时候某些值会自动进行转换。

下面的情况是布尔值判断时的自动类型转换：

- 1，整型的0为假，其他整型值全为真

- 2, 浮点的0.0，布尔值的假。小数点后只要有一个非零的数值即为真。

- 3，空字符串为假，只要里面有一个空格都算真。

- 4，字符串的0，也将其看作是假。其他的都为真

- 5，空数组也将其视为假，只要里面有一个值，就为真。

- 6，空也为假

- 7, 未声明成功的资源也为假

**强制类型转换**

强制类型转换有三种方式：

- 1.用后面的三个函数可以完成类型转换，intval()、floatval()、strval() **[不改变原来变量的类型，返回一个转换后的值]**

- 2.变量前加上()里面写上类型，将它转换后赋值给其他变量 **[不改变原来变量的类型，返回一个转换后的值]**

- 3.settype(变量，类型) 直接改变量本身 **[改变了原来变量的类型]**


**intval()、floatval()、strval()转换**

```
    $float = 1.23;
    $result = intval($float);
    //看看结果是不是变了？
    var_dump($result);  // int(1)
    //鸭脖子为整型的5
    $yabozi = 5;
    $re = floatval($yabozi);
    var_dump($re);  // float(5)
    //定义整型的变量
    $yabozi = 23;
    $bian = strval($yabozi);
    //强制变成字符串试试
    var_dump($bian); // string(2) "23" 
```
**变量前加上()里面写上类型，将它转换后赋值给其他变量**
```
   $transfer = 12.8;
   //把浮点变为整型
    $jieguo = (int)$transfer;
    var_dump($jieguo);  // int(12)
    echo '<br>';
   //把浮点变为布尔
   $jieguo = (bool) $transfer;
   var_dump($jieguo);   //bool(true) 
    echo '<br>';
   //把布尔变整型
   $bool = true;
   $jieguo = (int)$bool;
   var_dump($jieguo);   //int(1)
    echo '<br>';
    //把浮点变数组
   $fo = 250;
   $jieguo = (array)$fo;
   var_dump($jieguo);   // array(1) { [0]=> int(250) }
    echo '<br>';
   //把数字变字符串
    $n = 250;
    $jieguo = (string)$fo;
   var_dump($jieguo);  // string(3) "250"
```
**settype(变量，类型) 直接改变量本身**
```
    //定义浮点变为整型
    $fo = 250.18;
   //settype第二个参数是int，你实验的时候要记得第二个参数要为字符串类型
    settype($fo,'int');
    //输出看看结果
    var_dump($fo); //int(250)
```
### php常量和变量

常量在代码中的定义、书写方式：
    define(常量名，常量值)

注：

    1.常量值只能为上一章中我们讲到的标量。

    2.常量名可以小写，但是通常大写

    3.常量名可以不加引号，但是通常加上引号。

    4.在字符串中调用常量的时候，必须在引号外面

    5.常量名建议只用字母和下划线
```
    <?php
    
    define('MY_NAME','PHP中文网');
    
    echo MY_NAME;   // PHP中文网
    
    //下面是错误的调用方式
    echo '我的名字是MY_NAME';   // 我的名字是MY_NAME
    
    //正确的调用方式该这么写
    echo '我的名字是' . MY_NAME;    // 我的名字是PHP中文网
    ?>
```
<table>
    <tr>
        <th>常量名</th>
        <th>说明</th>
    </tr>
    <tr>
       <td>LINE</td> 
       <td>	当前所在的行</td> 
    </tr> 
        <tr>
       <td>FILE</td> 
       <td>	当前文件在服务器的路径</td> 
    </tr> 
    </tr> 
        <tr>
       <td>FUNCTIOIN</td> 
       <td>	当前函数名</td> 
    </tr>   
    </tr> 
        <tr>
       <td>CLASS</td> 
       <td>	当前类名</td> 
    </tr> 
    </tr> 
        <tr>
       <td>METHOD</td> 
       <td>	当前成员方法名</td> 
    </tr>
     </tr> 
        <tr>
       <td>DIR</td> 
       <td>	文件所在的目录</td> 
    </tr>   
    </tr> 
        <tr>
       <td>PHP_OS</td> 
       <td>	PHP运行的操作系统</td> 
    </tr> 
     </tr> 
        <tr>
       <td>PHP_VERSION</td> 
       <td>	PHP运行的操作系统</td> 
    </tr>    
      </tr> 
        <tr>
       <td>TRAIT</td> 
       <td>	Trait 的名字,php5.4新加</td> 
    </tr>   
       </tr>    
      </tr> 
        <tr>
       <td>NAMESPACE</td> 
       <td>	当前命名空间的名称（区分大小写）</td> 
    </tr>   
</table>

**php常量和变量之可变变量**
可变变量其实就是--——--已声明的变量前，再上变量符。
```
<?php
   //定义了一个变量叫作 $shu 将$shu这个变量的值设为字符串的biao
   $shu = 'biao';
   //定义了一个【变量】$biao。将他的值设置为鼠标
   $biao = '鼠标';

   //$$shu 就是可变变量：在已声明的变量$shu前又加上了一个变量符
   echo $$shu;  //鼠标
?>
```
**php常量和变量之外部变量**

**\$_GET**
我们的第一个外部变量： \$_GET。
$_GET 的主要作用是将得到get传值的数据

```
<html>
   <head>
   </head>

   <body>
       <form action="reg.php" method="get">
           <input type="text" name="username" />
           <input type="password" name="pwd" />
           <input type="submit" value="提交" />
       </form>
   </body>
</html>

<?php
//$_GET后面加上中括号，将username作为字符串放在中括号里面，就得到了表单里面的<input type="text" name="username" /> 的值
$u = $_GET['username'];
echo $u.'<br />';

//$_GET['pwd'] 得到表单<input type="text" name="username" /> 的值
$passwd = $_GET['pwd'];
echo $passwd.'<br />';
?>

```
你可以输出值看一下结果。通过上面的实验我们知道了，通过$_GET这个外部变量，可以得到从表单输入的值。

**$_POST**
```
<?php
//$_POST后面加上中括号，将username作为字符串放在中括号里面，就得到了表单里面的<input type="text" name="username" /> 的值
$u = $_POST['username'];
echo $u.'<br />';

//$_POST['pwd'] 得到表单<input type="text" name="username" /> 的值
$passwd = $_POST['pwd'];
echo $passwd.'<br />';
?>
```
$_POST是通过我们看不见的浏览器的请求头文件传递的数据。所以在URL（网址）栏不可见。

除此之外，我们还有**$_REQUEST**来接收数据。现在我们这样处理：
```
<?php
$u = $_REQUEST['username'];
echo $u.'<br />';

$passwd = $_REQUEST['pwd'];
echo $passwd.'<br />';
?>
```

$_REQUEST既可以接收get传值也可以接收post传值。

**外部变量**
另外，我们总结一些外部变量，要求知识点的学习级别：了解含义，默写这个单词的写法和作用。


|全局变量名|功能说明
-|-|-
|\$_COOKIE | 得到会话控制中cookie传值
|\$_SESSION | 得到会话控制中session的值
|\$_FILES | 得到文件上传的结果
|\$_GET |	得到get传值的结果
|\$_POST | 得到post传值的结果
|\$_REQUEST | 即能得到get的传值结果，也能得到Post传值的结果

注：
1.我们认为从用户输入过来的所有数据都不是可信的。本书的下半部份会专门讲解限制和过滤

2.在提交数据的时候，我们常用的方法有get和post。可以这样理解，get传值在url中可见，而post传值在url中不可见。

而post传值在url中不可见，是通过浏览器的header头部份将数据发送给指定服务器的。需要通过专门的工具才能看到Post发送的值为什么


----------


**PHP常量和变量之环境变量**

环境变量我们主要用的有\$_SERVER 和 $_ENV两个环境变量。

不过，$_ENV逐渐被PHP的新版本给废弃了。
查看环境变量:
```
<?php

phpinfo();

?>
```
一些常用的环境变量的键名和值对应的意思：

键名 |含义
-|-|-
|\$_SERVER ["REQUEST_METHOD"]	|请求当前PHP页面的方法
|\$_SERVER ["REQUEST_URI"]	|请求的URI
|\$_SERVER ["SERVER_SOFTWARE"]|	用的是哪一种服务器
|\$_SERVER ["REMOTE_ADDR"]	|客户的IP地址
|\$_SERVER ["SERVER_ADDR"]	|当前服务器的IP地址
|\$_SERVER ["SCRIPT_FILENAME"]|	主前请求文件的路径
|\$_SERVER ["HTTP_USER_AGENT"]	|当前访问这个网址的电脑和浏览器的情况
|\$_SERVER ["HTTP_REFERER"]	|上级来源（用户从哪个地址进入当前网页的）
|\$_SERVER ["REQUEST_TIME"]	|当前的时间


URI 和URL都是网址，但是URL带有了主机地址部份，而URI不带主机地址部份，例如：
http://www.php.cn/abc.php?username=php 上面是一个**URL**（统一资源定位符），而**URI**是不带主机和"(http://)"

**php常量和变量之-----变量引用**
代码一：
```
<?php

$fo = 5;
//$fo的值为5，将5赋值
$bar = $fo;
//$bar的值原来为5，现在将值改为6
$bar = 6;
//$bar的结果为6
echo $bar.'<br />';     //6
//$fo的结果为5
echo $fo.'<br />';      //5

```

?>

代码二：

```
<?php

$fo = 5;
//注意，加上了一个&符哟
$bar = &$fo;

$bar = 6;
//$bar的结果为6
echo $bar.'<br />';     //6
//$fo的结果为6
echo $fo.'<br />';      //6

?>

```
通常情况下，一个变量名，对应了一个数据值。如下图：
![此处输入图片的描述][1]


而加上&（and 符后），把变量指向同一个存值空间了，如下图：  
![此处输入图片的描述][2]


  这时候，不论\$fo或\$bar的值如何发生变化，\$fo变\$bar也变，\$bar发生变化，\$fo也会发生变化。
  
**php基础语法之算术运算**  
  
|符号|说明|举例
|--|--|
|+	|加号	|\$x + \$y
|-	|减号	|\$x - \$y
|*	|乘号,乘以	|\$x * \$y
|/	|除号,除以	|\$x / \$y
|%	|取余也叫取模、求模 |\$x % \$y

与我们数学所学一样，也有优先级：先乘除，后加减。如果你想更明确的改变优先级，那就用()【小括号】，将想要优先的值给括起来。

**php基础语法之赋值运算**
```
<?php

$x = 5;

$x = true;

$x = '爱你';

$x = 12.888;

echo $x;
?>
```

那么PHP的赋值运算符还有几个：

|符号	|举例	|等价式
|--|--|
|+＝	|\$x +＝ \$y	|\$x ＝ \$x + \$y
|-＝	|\$x -＝ \$y	|\$x ＝ \$x - \$y
|*＝	|\$x *＝ \$y	|\$x ＝ \$x * \$y
|/＝	|\$x /＝ \$y	|\$x ＝ \$x / \$y
|%＝	|\$x %＝ \$y	|\$x ＝ \$x % \$y
|.＝	|\$x .＝ \$y	|\$x ＝ \$x . \$y

**php基础语法之自加自减**

|符号	|说明
|--|--|
|\$x++	|先赋值后加
|\$x--	|先赋值后减
|++\$x	|先加后赋值
|--\$x	|先减后赋值


**php基础语法之比较运算符**
比较语法类似于js语法比较
只需要注意一点 == 和 === ，两个等号只比较值是否相同，三个等号会比较类型是否相同。

**php基础语法之逻辑运算**


|举例	|说明	|详细说明
-|-|-
|\$x and \$y	|逻辑与（并且关系）	|\$x 和\$y 为真则返回真
|\$x && \$y	|同上	|同上
|\$x or \$y	|逻辑或	|\$x,\$y均为false时为假，其他情况全为真
|\$a\|\|\$b	|同上	|同上
|!$x	|逻辑非	|取反，即true变为false，false变为true
|\$x xor \$y	|逻辑异或	|相同取false，相异为true

逻辑与的特性是：两边为true即为true，其他情况均为假。
逻辑或的特性是：两边为假均为假，其他情况全为真。

短路应用:
```            
<?php
//如果为defined('AUTH')存在AUTH常量则为true，不访问后面的exit了。如果为false则执行exit
defined('AUTH') or exit('存在安全因素不准访问');
?>
```
exit 的意思是指在此处停止运行，退出。后面的PHP代码不再执行了。它有两种用法：
1,直接exit; 就是直接退出
2,exit(‘提示内容’)，退出的时候还给出一段提示内容

**PHP基础语法之 三元运算符和其它运算符**

|符号	|说明
|-|-
|$x? 真代码段 : 假代码段	|判断是否为真假 ? 真情况 : 假情况;
|``（反引号）	|反引号中间插代命令，执行系统命令，等价于shell_exec函数
|@	|单行抑制错误，把这一行的错误不让它显示出来了，效率低不建议使用
|=>	|数组下标访问符
|->	|对象访问符
|instanceof	|判断某个对象是否来自某个类，如果是的返回true，如果不是返回false


### PHP流程控制之if语句：
```
if（判断语句1）{
    执行语句体1
}elseif(判断语句2){
    执行语句体2
}else if(判断语句n){
        执行语句体n
}else{
        最后的else语句可选
}

//定义一个随机变量，抵达时间,随机0点至23点
$dida = rand(0,23);

if($dida > 6 && $dida < 10){
    echo '我爱泡澡';
}else if($dida >10 && $dida < 14){
    echo '吃神户牛肉';
}else if($dida >=19 && $dida < 22){
    echo '找一个朋友聊聊内心的寂寞';
}elseif($dida > 22 && $dida <= 23){
    echo '泡澡';

}elseif($dida >= 1 && $dida <3){
     echo '泡澡';
}else{
    echo '睡觉或者工作';
}

//if...else...多重钱套

if(判断1){
    if(判断2){
            代码段 1    
    }else{
            代码段2
        }
}else{
    if(判断3){
            代码段3
        }else{
            代码段4
        }
}

//PHP流程控制之分支结构switch语句的使用


switch(变量){    //字符串，整型

       case 具体值:
               执行代码;
               break;

       case 具体值2：

               执行代码2;
               break;

       case 具体值3：

               执行代码3;
               break;

       default:

}
```

### php流程控制 之循环语句的使用

```

//定义需要往返的次数，老外喜欢从0开始计数，我们也从0开始计
$count = 0;

//while后面接布尔值判断，为真执行，为假停止
//$count 小于100的时候执行，也就是$count为0至99的时候执行
//如果$count不小于100了，循环停止执行后续的代码

//循环开始处
while($count < 100){

   echo '我是王思总，我是第' . $count .'次出差<br />';
   //每次执行让$count+1，这样的话，就不会产生$count永远小于100的情况了
   $count++;

//循环结束
}

echo '后续代码';
?>

```
while的代码逻辑图：
![此处输入图片的描述][3]


  [1]: http://img.php.cn//upload/image/620/601/608/1479090182488980.png
  [2]: http://img.php.cn//upload/image/989/947/567/1479090195337097.png
  [3]: http://img.php.cn//upload/image/630/721/901/1476683702132927.png
  
那我们现在要用while循环写一个0-99的隔行变色的表格该怎么写呢？
```
<?php
$i=0;
echo '<table width="800" border="1">';

while($i<100){
    //0 - 9 为一行
        //10 -19 为一行
        //因此，每一行都能够被10求默，如为为10的时候，应该显示行开始的标签
    if($i%10 == 0){
                //为了隔行变色，每20，40，60每行的颜色不同的，因此我们又可以再进行一次取余运算
        if($i%20==0){
            echo '<tr>';
        }else{
            echo '<tr bgcolor="pink">';
        }
    }

    echo '<td>'.$i.'</td>';

    $i++;
        //同理，每一行结束是不是应该有一个</tr>结束标签呢？
    if($i%10==0){
        echo '</tr>';
    }
}
echo '</table>';
?>

```

do...while与while的语法结构基本一样，也是一个布尔型循环，功能也基本一样。

do-while **不论while判断是否成立，先执行一次代码代码块循环语句**，保证会执行一次（表达式的真值在每次循环结束后检查）。
然而我们之前的while循环会检查布尔判断区域，成立则执行。不成立则不执行。
```
<?php
$i = 0;
do {
   echo $i;
} while ($i > 0);
?>
```
### PHP流程控制之for循环控制语句

for ( 表达示1; 表达示2; 表达示3 ){
        需要执行的代码段
}

- 表达式1 是初始化赋值，可以同时赋值多个代码。
- 表达示2 在每次循环开始前求值。如果值为 - TRUE，则继续循环，执行嵌套的循环语句。如果值为 FALSE，则终止循环。
- 表达示3 在每次循环之后被求值。

```
<?php
    for ($i = 1; $i <= 10; $i++) {
        echo '分手后第'.$i.'年，我全都忘了你的样子<br />';
    }
?>
```
### 循环控制break,exit和continue

|语句	|作用
-|-|-
|exit	|exit之前我们讲过了，从当前处停止后续执行
|break	|之前遇到过，跳出循环或者跳出结构体执行后续代码
|continue	|跳出此次循环，下次循环继续

### PHP流程控制之goto语法
```
<?php
for($i=0; $i<100; $i++) {
    echo '第'. $i .'周往返北京大连<br />';
    if($i == 17){
            goto end; 
     }
}

end:
echo '集团公司要求停止此项';
?>
```

注：
goto 操作符可以用来跳转到程序中的另一位置。
该目标位置可以用目标名称加上冒号来标记，而跳转指令是 goto 之后接上目标位置的标记。
PHP 中的 goto 有一定限制，目标位置只能位于同一个文件和作用域，也就是说无法跳出一个函数或类方法，也无法跳入到另一个函数。也无法跳入到任何循环或者 switch 结构中。可以跳出循环或者 switch，通常的用法是用 goto 代替多层的 break。

### php函数基本语法之自定义函数

1.函数以function开始

2.function后面接空格，空格后接函数名

3.函数名与变量命名规则基本一样，但是不同的是：**函数名不区分大小写**
4.所谓参数其实就是变量**，函数体的参数若是定义了，未传参数并且没有设置默认值，代码会报错**

5.函数名后接括号，括号内跟参数，参数全都有[]（中括号）括起来了，代表参数可填可不填

6.**如果有参数的话，参数后可以接（＝）等号，等号接默认值**。参数值也是用[]（中括号）括起来的，代表选填

7.函数后的参数变量，主要功能是把函数体外的变量值，传入函数体内来使用，函数体的变量和函数体外的变量通常是两个不         同的变量。

8.函数中的具体功能（功能体）用大括号括起来，代表这是一个函数的功能区间

9.函数可以有返回值也可以没有返回值，用[]（中括号）括起来的，代表选填。

10.return后接空格，空格后接返回值，若有return,return后的代码均不执行。

11.函数的执行没有顺序关系，可以在定义处之前的位置调用

12.函数不能被定义两次，即函数不能被重载

### php自定义函数之内部函数
内部函数，是指在函数内部又声明了一个函数。
注意事项：

    1.内部函数名，不能是已存在的函数名

    2.假设在函数a里面定义了一个内部函数，不能定用两次函数a。
```
<?php
function foo(){
   echo '我是函数foo哟，调一下我才会执行定义函数bar的过程<br />';
     function bar(){
          echo '在foo函数内部有个函数叫bar函数<br />';
     }
}
// 1.foo()调用两次会报错
// 2.如果不调foo()函数无法执行bar函数，因为bar是在foo的内部
```

### php自定义函数之变量作用域

我们通过前面的章节函数定义部份的学习我们知道了几个不同的规矩：

函数定义时后括号里面接的变量是形式上的参数（形参），与函数体外的变量没有任何关系。仅仅是在函数内部执行

函数内声明的变量也与函数外的变量没关系。

但是，我们实际的处理情况中会遇到这样的一个情况：

我想在函数体内定义的变量在函数体外用

我想把函数体外的变量拿到函数体内来使用

**1.通过$GLOBLAS来读取外部变量**
```
<?php

$one = 10;

function demo(){
   $two = 100;

   $result = $two + $GLOBALS['one'];

   return $result;

}
//你会发现结果变成了110
echo demo();

?>
```
**2.通过$GLOBLAS，在函数内修改外部变量**
```
<?php

$hongniu = '我是一个兵，来自老百姓';

function test(){

   echo '执行了函数test哟<br />';
   //调用test()函数，将通过$GLOBALS['hongniu'],把$hongniu的值改变掉

   $GLOBALS['hongniu'] = '帮助别人很快乐';
}

test();
//发现是不是输出的值变了呀？
echo $hongniu;

?>
```

**3.通过$GLOBLAS，在函数内创建全局变量**

```
<?php

function hello(){

   $GLOBALS['que'] = '提神喝茶更好哟';

   echo '你调了一下函数hello<br />';
}

hello();

echo $que;  // 提神喝茶更好哟

?>

```

**global $变量1[,变量2,....变量n]**

```
<?php
$a = 10;
$b = 100;
function test(){
   global $a , $b;
   echo $a + $b;
}
//结果是不是显示出来了？
test();  // 110
?>

```
注意：
不可在global 后写 $变量 = 值。

php自定义函数之参数的引用

```
<?php

$foo = 100;

//注意：在$n前面加上了&符(引用符)
function demo(&$n){

       $n = 10;

       return $n + $n;

}

echo  demo($foo).'<br />';

//你会发生$foo的值变为了10
echo $foo;

?>
```
通过上例，我们发现实参为\$foo，在调用demo的时候，**让\$foo和\$n指向到了同一个存储区域，当\$n的值发生变化的时候。那么$foo的值也发生变化。**

### php自定义函数之静态变量

静态变量的特点是：声明一个静态变量，第二次调用函数的时候，静态变量不会再初始化变量，会在原值的基础上读取执行。
```
<?php
function demo()
{
   $a = 0;
   echo $a;
   $a++;
}


// static声明静态变量；
function test()
{
   static $a = 0;
   echo $a.'<br />';
   $a++;
}

demo(); // 0
demo(); // 0
demo(); // 0

for($i = 0 ;$i < 3 ; $i++){
  test();   // 分别打印1、2、3
}

?>

```
### php 文件包含函数

在PHP中， 有require、require_once、include、include- once四种方法包含（加载）一个文件。

|函数	|包含失败	|特点
-|-|-
|Inlcude	|返回一条警告	|文件继续向下执行。通常用于动态包含
|Require	|一个致命的错	|代码就不会继续向下执行。通常包含极为重要的文件，整个代码甭想执行
|Include_once	|返回一条警告	|除了原有include的功能以外，它还会做once检测，如果文件曾经已经被被包含过，不再包含
|Require_once	|一个致命的错	|除了原的功能一外，会做一次once检测，防止反复被包含

### php 数学常用函数

php获取时期时间信息函数

设置时区的函数为：
1). date_default_timezone_get()
2).date_default_timezone_set()

- 1. 设置时区
用于所有日期时间函数的默认时区设置
注：中国只能设置上海
```
<?php

//定义一下时区常量，以后你可以放到配置文件里
define('TIME_ZONE','Asia/shanghai');

//执行函数
date_default_timezone_set(TIME_ZONE);

echo date('Y-m-d H:i:s');

?>

```
- 2.time()获取当前的unix时间戳
从Unix纪元（1970 年 1月1日零时）开始到某个时间经过的秒数
```
<?php
   $time=time();
   print_r( $time);
?>

```
- 3. “亚麻跌”是PHP学习时间处理的关键

Y 英文是 year，为年份代表年 ——亚

m 英文代表month，为月份代表——麻

d 英文代表day，为日期 代表——跌
```
<?php

echo date('Y年m月d日');     //2017年07月27日
?>
```

后面还有几个参数：

H:m:s 代表的是：时分秒

h 的英文为：hour 代表小时

i的英文为：minute 代表分钟

s的英文为：second 代表秒
完整的写法
```
<?php

//就可以显示出来当前的时间了哟。
echo date('Y-m-d H:i:s');   // 2017-07-27 10:06:51
?>
```

date函数用于将一个时间进行格式化输出，以方便时间的显示或存储。其语法格式如下：
string date ( string \$forrnat [, int $tirnestamp] )
在参数列表中:

$timestamp是一个时间戳，函数将这个时间戳按\$format规定的格式输出。

如果$timestamp没有输入值，则默认为当前的时间。


**3. getdate获取当前系统时间**

getdate用来获取当前系统的时间，或者获得一个时间戳的具体含义。时间戳是一个长整数，表示getdate的语法格式如下所示。
```
array getdate ([ int $timestamp = time() ] );

\\ 返回值 Array
(
    [seconds] => 1            //秒
    [minutes] => 10            //分钟
    [hours] => 17            //小时
    [mday] => 18            //日
    [wday] => 0            //星期中的第几天
    [mon] => 1            //月
    [year] => 2015            //年
    [yday] => 17            //年中的第几天
    [weekday] => Sunday        //星期
    [month] => January        //月份
    [0] => 1421597401        //时间戳
)

```
函数的返回值是一个根据timestamp得到的包含有时间信息的数组。如果没有参数，则会返回当前的时间。getdate返回的数组，键名包括时间和日期的完整信息。

下面的代码就是用getdate函数取得时间信息，调用返回时间数组的值输出时间信息。
```
<?php 
$mytime = getdate();
echo "年 :".$mytime['year']."\n";
echo "月 :".$mytime['mon']."\n";
echo "日 :".$mytime['mday']."\n";
echo "时 :".$mytime['hours']."\n";
echo "分 :".$mytime['minutes']."\n";
echo "秒 :".$mytime['seconds']."\n";
echo "一个小时中的第几钟 :".$mytime['minutes']."\n";
echo "这是一分钟的第几秒 :".$mytime['seconds']."\n";
echo "星期名称 :".$mytime['weekday']."\n";
echo "月份名称 :".$mytime['month']."\n";
echo "时间戳   :".$mytime[0]."\n";
?>

```
### php日期验证函数
checkdate可以判断一个输出的日期是否有效。

在实际的工作中，我们需要经常用于检测常用于用户提交表单的数据验证。

例如：验证用户输入的时间是否正确。

函数的语法格式如下：
```
bool checkdate ( int $month , int $day , int $year );
```
如果是有效的时间就返回真，如果不是有效的时间就返回假。

下例中，我们就可以用一个代码来进行实验，写出一段真实的例子。试试2011年有没有2月29日。
```
<?php
var_dump(checkdate(12, 31, 2018));  // boolean true

var_dump(checkdate(2, 29, 2011));   // boolean false
?>
```
### php获取本地化时间戳函数

我们的mktime()函数可以对一个日期和时间获得一个本地化时间戳。其语法格式如下所示：
    
    int mktime (int $hour [, int $minute [, int $second [, int $month [, int $day [. int$year [, int $.is_dstl.l } ] ] 31 );

函数的参数分别表示：时、分、秒、月、日、年、是否为夏令时。在使用这个函数时，需要注意所列的参数要与函数的参数含义相同。例如，下面的代码实现了用mktime构造一个时间戳的功能。
```
<?php
    echo  mktime (13 ,15 , 30, 8,18, 2008);
?>
```

php 程序执行时间检测
我们有的时经常需要做程序的执行时间执行效率判断。

**microtime()**这个函数，能够返回当前 Unix **时间戳和微秒数**

参数：
如果你传入true的话，将会返回一个浮点类型的时间，这样方便参与运算。

我们来模拟一个检测函数执行时间的例子，测试某个函数效率的快慢：
```
<?php
//开始时间
$time_start = microtime(true);

//循环一万次
for($i = 0 ; $i < 10000 ; $i++){


   //你可以用上，mktime() 生成一个昨天的时间

   //再用strtotime() 生成一个昨天的时间

   //对比两个函数认的效率高

}

//结整时间
$time_end = microtime(true);
//相减得到运行时间
$time = $time_end - $time_start;

echo "这个脚本执行的时间为 $time seconds\n";
?>

```

### php字符串常用函数

PHP字符串常用函数：
http://www.cnblogs.com/koala0521/p/7244924.html

### php数组
```
<?php

$kele = array('张三',10 => '李四', 'PHP中文网' , '去PHP中文网学PHP', 19 => '王二' , '小明');

//打印显示$kele
echo '<pre>';
var_dump($kele);
echo '</pre>';
?>
```

向索引数组中增加元素

1.向索引数组中增加元素用: **数组变量名[]**、**数组变量名[键值]**这两种方式来增加元素
**粗体文本**
2.键值的增长规则与之前的规则一样。都是最大值加1的原则。

```
<?php

$minren = array(
           '杨幂',
           '王珞丹',
           '刘亦菲',
           '黄圣依'
       );


//如何向这$minren这个数组中增加元素呢

//猜猜范冰冰的下标是多少？
$minren[] = '范冰冰';

$minren[100] = '范爷';

//它的下标又为几呢？
$minren[] = '李晨';

?>
```


向索引数组中删除元素
  1.使用unset删除变量的方式来删除数组里面的值。

2.删除了中间的值，并不会让后面的下标向前自动移动。而是原来的值为多少就为多少

3.删除掉其中的某个值，新加入的值不会替换掉原来的位置，依然遵循最大值加1的原则。
```
<?php

$minren = array(
           '杨幂',
           '王珞丹',
           '刘亦菲',
           '黄圣依',
           '范冰冰'
       );


//假设我不喜欢：黄圣依，如何将黄圣依给删掉掉呢？

//如果删除掉后范冰冰的下标为多少呢？

//如果在后面再追加一个元素，会填掉：“黄圣依”留下来的空吗？

unset($minren[3]);

$minren[] = '金星';


echo '<pre>';

var_dump($minren);

echo '</pre>';


?>
```
索引数组的其他声明方式

```
// 一、直接用之前未声明的变量，用变量名后面接中括号的方式声明数组。
<?php
    //直接写一个变量后面加上中括号，声明变量
    $qi[] = '可口可乐';
    $qi[10] ='百事可乐';
    echo '<pre>';
    var_dump($qi);
    echo '</pre>';
?>

//二、每次用array()写的太麻烦了，还可以不用写array哟，更简单。

<?php

$minren = [
           '杨幂',
           '王珞丹',
           100 => '刘亦菲',
           '黄圣依',
           '范冰冰'
       ];

echo '<pre>';

var_dump($minren);

echo '</pre>';

?>

```

关联数组

```
<?php

//声明一下关联数组
$rela = array(
       '帅' => '陈奕迅',
       '很帅' => '黄晓明',
       '灰常灰常帅' => '宁泽涛',
       '有男人味的大叔' => '吴秀波',
);




//再来玩玩简洁声明

$drink = [
        '美' => '凤姐',
        '很美' => '芙蓉姐姐',
        'verymei' => '杨幂',
        '心中滴女神呀' => '华妃',
        100 => '孙俪',
        '娘娘',
       ];


// 输出 $rela
echo '<pre>';

var_dump($rela);

echo '</pre>';


// 输出$drink

echo '<pre>';

var_dump($drink);

echo '</pre>';

?>

```

关联数组

```

//声明一下关联数组
$rela = array(
       '帅' => '陈奕迅',
       '很帅' => '黄晓明',
       '灰常灰常帅' => '宁泽涛',
       '有男人味的大叔' => '吴秀波',
);




//再来玩玩简洁声明

$drink = [
        '美' => '凤姐',
        '很美' => '芙蓉姐姐',
        'verymei' => '杨幂',
        '心中滴女神呀' => '华妃',
        100 => '孙俪',
        '娘娘',
       ];


// 输出 $rela
echo '<pre>';

var_dump($rela);

echo '</pre>';


// 输出$drink

echo '<pre>';

var_dump($drink);

echo '</pre>';

?>
```
我们通过实验知道：

    1.声明关联数组是 键名 => 值

    2.在关联数组可以有索引数组的元素

    3.关联数组中的索引数组的元素后再声明了无下标的元素，依然是最大值+1原则.

php 数组的计算

count函数的用法：

int count ( mixed $变量);
1.参数$变量 要求是一个数组或者一个可以被统计的对象

```
<?php
$a[0] = 1;
$a[1] = 3;
$a[2] = 5;
$result = count($a);
echo $result;   //3

$arr = [ 1,2,3 4];
echo $result;   //4

?>
```

php for循环遍历索引数组
```
<?php

//声明一个数组，值为1到10
$num = array(1,2,3,4,5,6,7,8,9,10);

//按照索引数组的特点，下标从0开始。所以1的下标为0，10的下标为9
echo $num[0].'<br />';
echo $num[9].'<br />';


//我们可以得到数组中元素的总个数,为10
echo count($num);

//遍历这个索引数组的话，我们就可以定义一个变量为$i
//$i 的值为0，从0开始
//可以设定一个循环条件为：$i 在下标的(9)最大值之内循环
for($i = 0 ; $i < count($num) ; $i++){

   echo $num[$i].'<br />';

}

?>

```

#### php ​foreach遍历关联数组

foreach( 要循环的数组变量 as [键变量 =>] 值变量){
//循环的结构体
}

```
<?php

$data = [
       'fj' => '凤姐',
       'fr' => '芙蓉',
   ];


foreach($data  as $key => $value){
       echo $key . '-------' . $value . '<br />';
}


//如果我们只想读取值的话，就可以把下面的$key => 给删除掉，读取的时候，就只读取值了。做完上面的实验，你可以打开下面的代码再实验几次。

/*
foreach($data  as  $value){
       echo  $value . '<br />';
}
*/
?>
```
#### php list、each函数遍历数组

list函数

我们先来讲list函数：

list ( mixed \$变量1 [, mixed \$变量n ] )

它的功能：将索引数组下标和变量一一对应，如果变量对应的数组项不存在返回null 并且弹出警告。
```
<?php

list($one , $two , $three) = array('张三' ,'李四' ,'王五');

//再次声明：单引号不结释变量，所以输出的是字符串$one
echo '$one----'.$one.'<br />';  //$one----张三
echo '$two----'.$two.'<br />';  //$two----李四
echo '$three----'.$three.'<br />';  //$three----王五
?>

list($one, $two, $three) = array(2 => '张三', '李四', '王五');

echo '$one----' . $one . '<br />';  //  $one----
echo '$two----' . $two . '<br />';  //  $two----
echo '$three----' . $three . '<br />';   //$three----张三   


```

### php 常用操作数组函数


下面的几个主要是移动数组指针和压入弹出数组元素的和个函数

|函数	|功能
|--|--|
|array_shift	|弹出数组中的第一个元素
|array_unshift	|在数组的开始处压入元素
|array_push	|向数组的末尾处压入元素
|array_pop	|弹出数组末尾的最后一个元素
|current	|读出指针当前位置的值
|key	|读出指针当前位置的键
|next	|指针向下移
|prev	|向上移
|reset	|指针到开始处
|end	|指针到结束处

**array_shift**
```
<?php
$mingren = array("邓超", "黄晓明", "宁泽涛", "钟汉良");
$dc = array_shift($mingren);

echo $dc .'<br />'; //邓超

print_r($mingren);  //Array ( [0] => 黄晓明 [1] => 宁泽涛 [2] => 钟汉良 )
?>
```
结论：

    1.将第一个数组元素弹出，改变了原数组的结果

    2.函数返回值为删除的数组元素
    

**array_unshift**    
功能：向指数组的开始处压入一个或多个元素，返回的是数组总的长度。

```
<?php
$mingren = array("邓超", "黄晓明");
$dc = array_unshift($mingren , "宁泽涛", "钟汉良");

echo $dc .'<br />';

print_r($mingren);
?>
```

**array_pop**

mixed array_pop ( array &$array )

功能：弹出数组末尾的一个元素

```
<?php
$mingren = array("邓超", "黄晓明", "宁泽涛", "钟汉良");
$dc = array_pop($mingren);

echo $dc .'<br />';     //钟汉良

print_r($mingren);  //Array ( [0] => 邓超 [1] => 黄晓明 [2] => 宁泽涛 )
?>
```

array_push

int array_push ( array &\$array , mixed \$value1 [, mixed $... ] )

功能：向指数组末尾处压入一个或多个元素，返回的是总个数。

```
<?php
$mingren = array("邓超", "黄晓明");
$dc = array_push($mingren , "宁泽涛", "钟汉良");

echo $dc .'<br />';

print_r($mingren);
?>
```

**current,key,prev,next,reset** 

```
<?php
$t=array(
    '01' =>'小明1号',
   '02'=>'小明2号',
   '03'=>'小明3号',
   '04'=>'小明4号'
   );


//读取数组的值
echo current($t).'<br />';  //小明1号
//读取数组的键
echo key($t).'<br />';      // 01

//向后移动一下
next($t);   

//再读值和键
echo current($t).'<br />';      // 小明2号

echo key($t).'<br />';      // 02


//向后移动一下
next($t);
echo current($t).'<br />';      // 小明3号

echo key($t).'<br />';      // 03


//向前移动一下
prev($t);
echo current($t).'<br />';      // 小明2号
echo key($t).'<br />';      // 02


//移到末尾
end($t);
echo current($t).'<br />';      // 小明4号
echo key($t).'<br />';      // 04

//移至开始处
reset($t);
echo current($t).'<br />';    //小明1号

echo key($t).'<br />';      // 01


//销毁数组
unset($t);
var_dump($t);   // NULL
?>
```

#### php数组常用函数
http://www.cnblogs.com/koala0521/p/7249464.html

