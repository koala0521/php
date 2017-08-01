# php 创建和修改文件内容

标签（空格分隔）： php php创建文件 php修改文件

---

### file_put_contents写入文件
我们先来学习第一种写入文件的方式：

    int file_put_contents ( string $文件路径, string $写入数据])

功能：向指定的文件当中写入一个字符串（会清空原有的内容），如果文件不存在则创建文件。返回的是写入的字节长度

```
<?php
   $data = "在PHP中文网学好PHP，妹子票子不再话下！";

   $numbytes = file_put_contents('binggege.txt', $data); //如果文件不存在创建文件，并写入内容

   if($numbytes){

       echo '写入成功，我们读取看看结果试试：';

       echo file_get_contents('binggege.txt');

   }else{
       echo '写入失败或者没有权限，注意检查';
   }
?>
```

### fwrite配合fopen进行写入操作

    int fwrite ( resource $文件资源变量, string $写入的字符串 [, int 长度])


```
<?php
   $filename = 'test.txt';
   $fp= fopen($filename, "w");  //w是写入模式，文件不存在则创建文件写入。
   $len = fwrite($fp, '我是一只来自北方的狼，却在南方冻成了狗');
   fclose($fp);
   print $len .'字节被写入了\n';
?>

```
总结：
1.不论有没有新建都会打开文件重新写入
2.原有的文件内容会被覆盖掉
3.文件不存在会创建

那我们来对比一下以下几个模式的不同：

|模式	|说明
|--|--|
|r	|只能读不能使用fwrite写
|r+	|可操作读、写
|w	|只可以写功能
|w+	|即可读又可以写

### a模式和w模式的不同

同样是下面的这段代码，我们改为a模式。
```
<?php
   $filename = 'test.txt';
   $fp= fopen($filename, "a");
   $len = fwrite($fp,'读大学迷茫了，PHP中文网学PHP给你希望');
   echo  $len .'字节被写入了\n';
?>
```

打开网页执行这段代码，你会发现：**每刷新一次，文件中就会多一段**
：读大学迷茫了，PHP中文网学PHP给你希望。

总结：

|模式	|总结
|--|--|
|x	|每次写入会干掉原有文件的内容，文件不存在都会创建
|a	|每次写入都会向文件的尾端追加内容

### x模式和w模式的不同
这段代码我们再实验一次，改为x模式：
```
<?php
   $filename = 'test.txt';
   $fp= fopen($filename, "x");
   $len = fwrite($fp,'读大学迷茫了，PHP中文网学PHP给你希望');
   echo  $len .'字节被写入了\n';
?>
```
我们会发现：

    1.文件存在的时候会报错

    2.如果把$filename 改成其他的文件名,就可以了。但是，再次刷新的时候又报错了

    3.x+ 是增强的x模式。读取时也可以使用。
    
### php 创建临时文件

我们来学习一下这个函数：

    resource tmpfile ( )
功能：创建一个临时文件，返回资源类型。关闭文件即被删除。

### php移动、拷贝和删除文件    

重命名文件

    bool rename($旧名,$新名);
    
这个函数返回一个bool值，将旧的名字改为新的名字。    

```
<?php
 //旧文件名
$filename = 'test.txt';

//新文件名
$filename2 = 'reName.txt.';

//修改名称
rename($filename, $filename2);
?>

```
复制文件

复制文件，就相当于是克隆技术，将一个原来的东西再克隆成一个新的东西。两个长得一模一样。

    bool copy(源文件,目标文件)

功能：将指定路径的源文件，复制一份到目标文件的位置。

```
<?php

    //旧文件名
    $filename = 'copy.txt';
    
    //新文件名
    $filename2 = 'copy2.txt';
    
    //修改名字。
    copy($filename, $filename2);

?>
```
注：
    1·复制的文件名不能和源文件同名，否则无法复制；
    2.复制文件名如果已经存在的话，会把源文件的内容copy一份替换复制文件的内容。
    
删除文件

删除文件就是将指定路径的一个文件删除，不过这个删除是直接删除。使用的是windows电脑，你在回收站看不到这个文件。

你只会发现，这个文件消失了。

    bool unlink(指定路径的文件)
    
```
<?php
   $filename = 'test.txt';

   if (unlink($filename)) {
       echo  "删除文件成功 $filename!\n";
   } else {
       echo "删除 $filename 失败!\n";
   }
?>
```
### php检测文件属性函数

    bool file_exists ( $指定文件名或者文件路径)
    功能：文件是否存在。

    bool is_readable ( $指定文件名或者文件路径)
    功能：文件是否可读

    bool is_writeable ( $指定文件名或者文件路径)
    功能：文件是否可写

    bool is_executable ( $指定文件名或者文件路径)
    功能：文件是否可执行

    bool is_file ( $指定文件名或者文件路径)
    功能：是否是文件

    bool is_dir ( $指定文件名或者文件路径)
    功能：是否是目录

    void clearstatcache ( void )
    功能：清楚文件的状态缓存

我们来讲第一个例子，文件锁。如果已经安装了，存在安装锁就提示已安装，否则就继续安装。

我们假设安装界面的网址是：install.php,安装的锁文件是install.lock。我们就可以检测install.lock文件是否存在。
```
<?php

if(file_exists('install.lock')){

   echo '已安装，请不要再次进行安装';
   exit;

}
?>
```

### php 文件常用函数和常量


|平台	|分割符
|--|--|
|windows	|\
|类unix	|/


我们会使用到一个常量：
    
    DIRECTORY_SEPARATOR //代表反斜杠
    
**由于FILE是PHP的预定义常量，所以没办法改变，如果需要让FILE也自适应操作系统。
那么就是不要用FILE,可以用自定义的常量，并且把FILE处理一下，如下：**    

```
<?php
//获取文件路劲，然后用DIRECTORY_SEPARATOR替换路劲中的'/'、'\\'；
$_current_file = str_replace(array('/', '\\'), DIRECTORY_SEPARATOR, __FILE__);

//重新字定义常量,输出格式化后的文件路劲
define('__CUR_FILE__', $_current_file);

echo __CUR_FILE__;      // D:\myphp\test\inidex.php

?>
```

文件指针操作函数
    
    rewind ( resource handle)
    功能：指针回到开始处

    fseek ( resource handle, int offset [, int from_where])
    功能：文件指针向后移动指定字符

```
<?php

> demo2.txt
    >     aaaaa
    >     bbbbb
    >     11111
    >     22222

$fp = fopen('demo2.txt', 'r+');
//读取10个字符， //读取前十个字节（空格算一个，换行算两个字节）
echo fread($fp,10);

//指针设置回到开始处    
rewind($fp);    // aaaaa bbb
//再读取10次看看输出的是什么
echo '<br>';
echo fread($fp,10);     // aaaaa bbb
echo '<br>';
//文件指针向后移动10个字符，（当前指针在最开始的位置）
echo fseek($fp,10);     // fseek的返回值为0
echo '<br>';
//再看看文件中输出的是什么
echo fread($fp,10);     // bb 11111 
echo '<br>';
fclose($fp);
?>

```

#### filesize 检测文件的大小

```
<?php


$filename = 'demo.txt';
echo $filename . '文件大小为: ' . filesize($filename) . ' bytes';

?>
```
其它操作文件的函数

其实还有一些其他操作文件的函数，读取文件

|函数名	|功能
|--|--|
|file	|把整个文件读入一个数组中
|fgets	|从文件指针中读取一行,读到最后返回false
|fgetc	|从文件指针中读取一个字符，读到最后返回false
|ftruncate	|将文件截断到给定的长度

**fgetc**
```
//以增加的r模式打开
$fp = fopen('demo2.txt','r+');

//你会发现每次只读一个字符
echo  fgetc($fp) .'<br />'; //只读取一个字符

//我要全部读取可以,读取一次将结果赋值一次给$string
while($string = fgetc($fp)){

    echo $string;
    //读取不到返回false
}
```
**fgets**
```

//以增加的r模式打开
$fp = fopen('demo.txt','r+');

//你会发现每次读取一次打开一行
echo  fgets($fp);
echo  fgets($fp);
echo  fgets($fp);
echo  fgets($fp);   //读取不到返回false
```

**ftruncate**返回值为1 int
    
    ftruncate（$file , len）;截取的长度大于文件内容长度，会用空字符填补
    
```

//打开我们上面的demo.txt文件
$file = fopen("demo.txt", "a+");

//你可以数数20个字有多长，看看是不是达到效果了
echo ftruncate($file,20);
fclose($file);
```

### 文件的时间函数

|函数	|功能说明
|--|-|
|filectime	|文件创建时间
|filemtime	|文件修改时间
|fileatime	|文件上次访问时间

```
<?php

$filename = 'demo.txt';

    if (file_exists($filename)) {
       echo '$filename文件的上次访问时间是:'  . date("Y-m-d H:i:s", fileatime($filename));
       echo '$filename文件的创建时间是: ' . date("Y-m-d H:i:s", filectime($filename));
        echo '$filename文件的修改时间是: ' . date("Y-m-d H:i:s", filemtime($filename));}
        
?>    
```

### php 文件锁处机制

文件锁的用途：

若一个人在写入一个文件，另外一个人同时也打个了这个文件进行写入文件。
这情况下，如果遇到一定的碰撞概率的话，不知道到底谁的操作为准。
因此，这个时候我们引入锁机制。
若用户A在写入或者读取这个文件的时候，将文件加上共享所。我可以读，其他人也可以读。
但是，我如果这与的时候。我使用独占锁。这个文件归我了，你们都别动，除非我将文件锁进行释放。

注意：加上了文件锁后要注意释放。

php 文件锁处机制
文件锁机制一般在单一打开文件的时候根本看不到效果。这一块的学习有一点点抽象。

大家不要去思考怎么实现的呀？

为什么看不到效果呀？
答：因为电脑的操作太快了，基本上是毫秒级的。所以这个实验其实是看不到效果的。

这一章了解文件锁的基本概念即可，熟悉文件锁函数和锁机制。

文件锁的用途：

若一个人在写入一个文件，另外一个人同时也打个了这个文件进行写入文件。
这情况下，如果遇到一定的碰撞概率的话，不知道到底谁的操作为准。
因此，这个时候我们引入锁机制。
若用户A在写入或者读取这个文件的时候，将文件加上共享所。我可以读，其他人也可以读。
但是，我如果这与的时候。我使用独占锁。这个文件归我了，你们都别动，除非我将文件锁进行释放。

注意：不论加上了文件锁后要注意释放。

我们来看看这个函数：

    bool flock ( resource $handleFile , int $operation)

我们来看看锁类型：

|锁类型	|说明
|--|--|
|LOCK_SH	|取得共享锁定（读取的程序）
|LOCK_EX	|取得独占锁定（写入的程序）
|LOCK_UN	|释放锁定（无论共享或独占）   

我们接下来把demo2.txt加上一个独占锁，进行写入操作。
```
    $fp = fopen("demo2.txt", "r+");
    
    // 进行排它型锁定
    if (flock($fp, LOCK_EX)) {
    
        echo '1';
    
        fwrite($fp, "文件这个时候被我独占了哟\n");
    
        // 释放锁定
        flock($fp, LOCK_UN);
    } else {
        echo "锁失败，可能有人在操作，这个时候不能将文件上锁";
    }
    
    fclose($fp);
```
说明：

1.上例中我为了写入文件，把文件加上了独占锁。

2.如果我操作完成，写入完成后，解除掉了独占锁。

3.如果是在读取文件的时候，大家可加按照同样的处理思路加上共享锁。