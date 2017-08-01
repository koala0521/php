# php 读取文件

标签（空格分隔）： php读取文件 php文件 

---

### readfile读取文件

那如何读取一个文件呢？我们先学一个函数。

    int readfile ( string $文件名)

```
<?php
   //linux类的读了方式
   readfile("/home/paul/test.txt");
   //windows类的读取方式
   readfile("c:\\boot.ini");
?>
```

file_get_contents打开文件

上面的是单纯打文件就直接输出了，有没有打开文件后，能够赋值给一个变量的操作方式呢。

PHP当然会提供这种方式。这个方式就是PHP打开文件并返回内容的方式之一，我们来看看函数：

    string file_get_contents ( string filename)

功能：传入一个文件或文件路径，打开这个文件返回文件的内容。文件的内容是一个字符串。
```
<?php

   $filename = 'NoAlike.txt';

   $filestring = file_get_contents($filename);
   echo $filestring;
?>
```

### fopen、fread、fclose操作读取文件

    resource fopen ( string $文件名, string 模式)

    string fread ( resource $操作资源, int 读取长度)

    bool fclose ( resource $操作资源 )
    
通过上面的函数我们来讲解资源类型的通常操作方式：
    
    1.打开资源

    2.使用相关函数进行操作

    3.关闭资源

fopen函数 fopen函数的功能是打开文件，参数主要有两个：

    1.文件打开的路径

    2.打开文件的模式
返回类型是一个资源类型，我们第一次遇到了之前基础类型的时候讲到的资源类型。
资源类型需要其他的函数来操作这个资源。所有的资源有打开就要有关闭。

fread函数 函数的功能的功能是读取打开的文件资源。读取指定长度的文件资源，读取一部份向后移动一部份。至到文件结尾。

fclose函数 fclose函数的功能是关闭资源。资源有打开就有关闭。

open函数的模式到底是什么，fopen的模式有下面几个，我们来讲一下fopen的模式：

|模式	|说明
|--|--|
|r	|只读方式打开，将文件指针指向文件头。
|r+	|读写方式打开，将文件指针指向文件头。
|w	|写入方式打开，将文件指针指向文件头并将文件大小截为零。如果文件不存在则尝试创建
|w+	|读写方式打开，将文件指针指向文件头并将文件大小截为零。如果文件不存在则尝试创建
|a	|写入方式打开，将文件指针指向文件末尾。如果文件不存在则尝试创建
|a+	|读写方式打开，将文件指针指向文件末尾。如果文件不存在则尝试创建之
|x	|创建并以写入方式打开，将文件指针指向文件头。如果文件已存在，则 fopen() 调用失败并返回 FALSE，并生成一条 E_WARNING 级别的错误信息。如果文件不存在则尝试创建
|x+	|创建并以读写方式打开，将文件指针指向文件头。如果文件已存在，则 fopen() 调用失败并返回 FALSE，并生成一条 E_WARNING 级别的错误信息。如果文件不存在则尝试创建

#### 打开文件、读取文件、关闭文件
```
//打开文件
$fp = fopen( 'C:\\readme.txt' , "r");
var_dump($fp);

//打开一个文件类型后，读取长度
$contents = fread($fp, 1024);
var_dump($contents);

//关闭文件
fclose($fp);
echo $contents;
```