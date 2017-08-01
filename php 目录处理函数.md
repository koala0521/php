# php 目录处理函数
标签（空格分隔）： php目录处理

--- 

之前我们处理的全都是文件，那目录和文件夹怎么处理呢?

我们就来学习目录或者称为文件夹的处理相关函数。

处理文件夹的基本思想如下：

    1.读取某个路径的时候判断是否是文件夹

    2.是文件夹的话，打开指定文件夹，返回文件目录的资源变量

    3.使用readdir读取一次目录中的文件，目录指针向后偏移一次

    4.使用readdir读取到最后，没有可读的文件返回false

    5.关闭文件目录

我们来学习一比常用函数：

|函数名	|功能
|--|--|
|opendir	|打开文件夹，返回操作资源
|readdir	|读取文件夹资源
|is_dir	|判断是否是文件夹
|closedir	|关闭文件夹操作资源
|filetype	|显示是文件夹还是文件，文件显示file，文件夹显示dir


```
<?php
//设置打开的目录是D盘
$dir = "d:/";

//判断是否是文件夹，是文件夹
if (is_dir($dir)) {
   if ($dh = opendir($dir)) {


      //读取到最后返回false，停止循环
      while (($file = readdir($dh)) !== false) {
           echo "文件名为: $file : 文件的类型是: " . filetype($dir . $file) . "<br />";
       }

       closedir($dh);
   }
}
?>
```
### php文件路径函数

我们把常用的路径处理函数为大家做了标注，大家对着这个路径处理函数进行处理即可：

|函数名	|功能
|--|--||
|pathinfo	|返回文件的各个组成部份
|basename	|返回文件名
|dirname	|文件目录部份
|parse_url	|网址拆解成各部份
|http_build_query	|生成url 中的query字符串
|http_build_url	|生成一个url

pathinfo

    array pathinfo ( string $路径)
    功能：传入文件路径返回文件的各个组成部份

```
<?php
    $path_parts = pathinfo('d:/www/index.inc.php');
    
    echo '文件目录名：'.$path_parts['dirname']."<br />";
    echo '文件全名：'.$path_parts['basename']."<br />";
    echo '文件扩展名：'.$path_parts['extension']."<br />";
    echo '不包含扩展的文件名：'.$path_parts['filename']."<br />"; 

//结果如下：
    //文件目录名：d:/www
    //文件全名：lib.inc.php
    //文件扩展名：php
    //不包含扩展的文件名：lib.inc
?>

```
#### dirname
```
dirname(string $路径) 
功能：返回文件路径的文件目录部份
<?php 
dirname(__FILE__); 
?>
```
#### parse_url

```
mixed parse_url ( string $路径 )
功能：将网址拆解成各个部份

<?php
$url = 'http://username:password@hostname:9090/path?arg=value#anchor';

var_dump(parse_url($url));

//结果
array(8) {
    ["scheme"]=> string(4) "http"
    ["host"]=> string(8) "hostname"
    ["port"]=> int(9090)
    ["user"]=> string(8) "username"
    ["pass"]=> string(8) "password"
    ["path"]=> string(5) "/path"
    ["query"]=> string(9) "arg=value"
    ["fragment"]=> string(6) "anchor"
}

?>

```

#### http_build_query

    string http_build_query ( mixed $需要处理的数据)
    功能：生成url 中的query字符串        

```
<?php
//定义一个关联数组
$data = [
       'username'=>'php',
       'area'=>'hubei'
        ];

//生成query内容
echo http_build_query($data);

// username=php&area=hubei

?>
```

http_build_url() 
功能： 生成一个url

注：
PHP_EOL 常量
在 windows平台相当于 echo "\r\n";
在unix\linux平台相当于 echo "\n";
在mac平台相当于 echo "\r";
