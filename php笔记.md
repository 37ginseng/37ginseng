## 标记

标准标记:<?php?>

短标记:<??>

## 注释

单行注释: // 或#

多行注释: /*  */

## 输出

### echo

 php语句。可将紧跟其后的一个或多个字符串、表达式、变量、常量输入到页面中，多个数据间使用逗号分隔。

echo没有返回值

### print

php print()函数用于输出一个字符串，它其实不是一个函数，所以可以不用加`()`。它只能打印简单的数据类型（如：int ,string）。

当执行失败时返回false，返回整型数据，返回值总是1。

print(） 比 echo 稍慢。

**语法**

```
print（strings）
```



### print_r()

php的内置函数，它可以打印关于变量的易于理解的信息.返回值为bool型

**语法格式**

```
bool print_r ( mixed $expression [, bool $return ] )
```

- $expression: 要打印的变量，如果给出的是 string、integer 或 float 类型变量，将打印变量值本身。如果给出的是 array，将会按照一定格式显示键和元素。object 与数组类似。
- $return: 可选，如果为 true 则不输出结果，而是将结果赋值给一个变量，false 则直接输出结果。

### var_dump()

不仅可以打印一个或多个任意类型的数据，还可以获得数据的类型和元素个数。显示关于一个或多个表达式的结构信息，包括表达式的类型与值。数组将递归展开值，通过缩进显示其结构。

## 常量定义

define(name,value [,case_insensitive])  

 //case_insensitive 规定是否对大小写敏感  true 大小写不敏感 false 默认 大小写敏感

## 变量

变量相当于一个内存中的地址别名。简单来说，php中的变量与值是2个不同的概念，变量存于一个符号表中，并有作用域，而值则在php内部（zend引擎中），存于一个zval结构体当中。

### 组成

在PHP中，变量是由$符号和变量名组成的。变量名命名规则与标识符命名规则相同。

### 赋值

一种是默认的传递赋值，一种是引用赋值。

传递赋值：$a=$b

引用赋值：$a=&$b

## 数据类型

支持3种数据类型：标量数据类型、复合数据类型、特殊数据类型

<img src="D:\InformationSecurityLearning\web材料\PHP\php数据类型.png" style="zoom: 80%;" />

### PHP EOF(heredoc) 

定义一个字符串的方法。EOF会解析html格式内容,解析变量,双引号内的内容具有转义效果.除此之外的,即使是特殊字符,也按原样输出

**语法格式**

以 **<<<EOF** 开始标记开始，以 **EOF** 结束标记结束，结束标记必须顶头写，不能有缩进和空格，且在结束标记末尾要有分号 。开始标志和结束标志需相同(此处为EOF),常用大写的 **EOT、EOD、EOF** 来表示.

```
<?php
$name="变量会被解析";
$a=<<<EOF
$name<br><a>html格式会被解析</a><br/>双引号和Html格式外的其他内容都不会被解析
"双引号外所有被排列好的格式都会被保留"
"但是双引号内会保留转义符的转义效果,比如table:\t和换行：\n下一行"
EOF;
echo $a;
?>  
```

### nowdoc

newdoc很像heredoc,nowdoc不会进行解析变量,?不转义?。

语法格式与heredoc相同，标识符要用单引号包裹。

**示例**

```
<?php
$var = '123';
$content = <<<'FDIPZONE'
$var time();
<h1>hello</h1>;
FDIPZONE;
echo '<h1>"猪"</h1>'	;
echo $content; // $var time(); $var没有被替换
?>
```

### 双引号和单引号

双引号会解析变量,解析HTML格式代码

单引号不会解析变量,会解析HTML

单引号字符串只对`‘`和`\`进行转义；而双引号字符串支持多种转义字符。

{}分隔变量,防止误解变量名.

**示例**

```
<?php
$num=666;
echo "$num 会等于<h1>六六六</h1></br>";
echo '$num 不会等于<h1>六六六</h1>'

?>
```

### 数据类型检测

内置函数	`is_*()`

如果检测的值符合数据类型，返回true，否则返回false。

### 强制类型转换

在需要转换的数据或变量前加`（数据类型）`

## 运算符

进行四则运算时，遵守先乘除后加减的原则

进行取模运算时，正负号取决于被取模数，与模数无关。

### 字符串运算符

用于拼接字符串的运算符`.`

**示例**

```
$html = 'Welcome to ' . $str . ' PHP';
```

### 错误控制运算符

`@`把它放在PHP表达式前，将忽略任何错误信息。



## 流程控制语句

if...else结构语法

```
if(判断条件){

}
else{

}
```

选择结构-switch语句

```
switch(表达式){ //表达式不能为数组或对象
case 值1:代码段1;break;
case 值2:代码段2;break;
default: 代码段3;
}
```

while 循环

```
while(判断条件){

	循环体
}
```

do...while 循环

```
do{


}while();
```

for 循环

```
for(初始化表达式;循环表达式;操作表达式){
	
	循环体
}
```



## 函数

### 函数定义

函数的定义由4部分组成：关键字function、函数名、参数、函数体。

**语法格式**

```
function 函数名([参数1,参数2...])
{
	函数体...

}
```

### 参数设置

参数的不同设置,决定了函数的调用和使用方式.

无参函数适用于不需要提供任何数据即可完成指定功能的情况.

#### 按值传递和引用传递

PHP默认支持按值传递,若需要函数修改它的参数值,则需通过函数参数的引用传递.

引用传递只需在参数前添加'&'符号即可.

#### 参数默认值

当调用者未传递该参数时，使用默认参数。默认参数必须放在非默认参数的右侧，且默认参数必须是常量表达式。

#### 指定数据类型

**弱类型参数设置**：自定义函数可以指定参数的数据类型，传递的参数数据类型不符时会强制转换。

示例

```
function sum1(int $a, int $b)
{

}
```

**强类型参数**：当用户传递的参数不符合函数定义时，报错。

```

declare(strict_types = 1);//申明本页面函数参数使用强类型
function sum2(int $a, int $b)
{
    return $a + $b;
}
echo sum2(2.6, 3.8); // 输出结果：Fatal error: ...

```

 **设置函数返回值类型**：

示例

```
function returnIntValue(int $value): int
{
    return $value + 1.0;
}

```

### 变量的作用域

变量只有在其作用范围才能使用，这一作用范围称为变量的作用域。

在函数中定义的变量成为局部变量，在函数外定义的变量称为全局变量。

在默认情况下，函数中不能使用全局变量，局部变量的改变也不会对全局变量产生印象。

如果要在函数中使用全局变量，使用global关键字和超全局变量$GLOBALS

### 静态变量

 示例

```
function add()
{
	static $i=1,$j=1;
	print "i=$i,j=$j";
	$i++;
}
print(add());
print(add());
print(add());
print(add()); 
//i=1,j=1i=2,j=1i=3,j=1i=4,j=1
```

### 可变函数

pass

### 回调函数

pass

### 匿名函数

## 数组

**数组构成**：数组是由一个或多个数组元素组成的

**数组元素**：一每个数组元素由键（Key）和值（Value）构成

**键**：“键”为元素的识别名称，也被称为数组下标

**值**： “值”为元素的内容

**映射**： “键”和“值”之间存在一种对应关系，称之为映射

**类型划分**：根据键的数据类型，可以将数组划分为索引数组和关联数组

**多维数组**：当一个数组的值又是一个数组时，就可以形成多维数组。

**索引数组**：索引数组是指键名为整数的数组。默认情况下，索引数组的键名是从0开始，并依次递增。

**关联数组**：关联数组是指键名为字符串的数组。通常情况下，关联数组元素的“键”和“值”之间有一定的业务逻辑关系。

### 数组定义

#### array()方式

array() 语言结构中的数组元素使用’‘键=>值’‘的方式进行表示，各元素之间用逗号隔开。

**省略键名**

```
$fruits=array('apple','grape','pear');
```

**指定键名**

```
$sports=array(2=>'basketball',4=>'swimming');
```



数组的键名默认是从0开始，并依次递增1。当定义了更大的数字键名时，默认从最大数值开始递增。

在定义数组时，还可以定义没有任何元素的数组，以及既有索引表示方式、又有关联表示方式的数组元素。

**键名的数据类型**

1、键只能是整型或字符串型的数据，如果是其他类型，则会执行类型自动转换
2、合法整型的字符串会被转为整型，如“2”转为2，而“02”则不会被转换
3、浮点数会被舍去小数部分直接转换成整型，如“2.6”转为2
4、布尔类型的true会被转为1，false转为0
5、NULL类型会被转为空字符串
6、若数组中存在相同键名的元素时，后面的元素会覆盖前面元素的值

#### 赋值定义

使用赋值方式定义数组，实际上就是创建一个数组变量，然后使用赋值运算符直接给变量赋值。

示例

```
$arr[] = 123;	
```

赋值方式定义数组就是单独为数组元素赋值。需要注意的是，赋值方式不能定义一个空数组。

### 访问

数组定义完成后，若想要查看数组中某个具体的元素，则可以通过“数组名[键]”的方式获取。

用print_r()或var_dump()访问整个数组



### 遍历数组

格式1

```
foreach (数组名称 as 键 => 值) {
    // 处理语句
}
--------
示例
$info = ['id' => 1, 'usr' => 'Jacie', 'age' => 18];
// 使用方式一
foreach ($info as $k => $v) {//用$k遍历键名，变量$v遍历值
    echo $k . ': ' . $v . ' ';	// 输出的结果：id: 1 usr: Jacie age: 18
}

```

格式2

```
foreach (数组名称 as 值) {
    // 处理语句
}
---------
// 使用方式二
foreach ($info as $v) {
    echo $v . ' ';		// 输出的结果：1 Jacie 18
}

```

foreach()**的传值赋值**

foreach默认是传值赋值，foreach中的处理语句不会对数组的值产生影响。

如果需要**引用传递**,在变量前加'`&`'

用于遍历的变量是全局变量，可以用unset($v)销毁变量。

删除数组也用unset()



## 面向对象

**类定义**

```
class 类名  //命名采用大驼峰命名法
{
	//成员方法
	//成员属性
}
```

**实例化类**

```
$对象名=new 类名([参数列表])
```

**使用成员方法或成员变量**

```
对象名->成员方法/成员变量
```

无论是$this->还是'对象名->'格式,后面的变量是没有$符号的.

**类常量**

使用关键字const定义常量

```
const P=3.1415
```

常量和变量和输出是不一样的。常量不需要实例化对象，直接由“类名：：常量名”调用即可。

```
echo Employee::NAME
```

### 构造方法

构造方法是在生成对象时自动执行的成员方法，作用就是初始化对象。

构造方法可以没有参数，也可以有多个参数。

定义

```
void __construct([mixed args[,...]])
```

示例

```
<?php
//filename:class_employee.php
//-*-coding=utf-8-*-

//定义员工类型
class Employee{
	//定义成员常量
	const DNAME='天地设计';
	const COUNTRY='???';
	//定义成员变量
	public $name;
	public $age;
	public $sex;
	public $id;
	//定义方法
	public function __construct($name,$age,$sex,$id){	//构造方法
		$this->name=$name;
		$this->age=$age;
		$this->sex=$sex;
		$this->id=$id;
	}
	public function SetInformation($name,$age,$sex,$id){
		$this->name=$name;
		$this->age=$age;
		$this->sex=$sex;
		$this->id=$id;
	}
	public function GetInformation(){	
		echo "name is ",$this->name,'<br>';
		echo 'id is ',$this->id;
	}
}
$e=new Employee('秀吉',17,'秀吉','0803<br>'); //实例化
$e->GetInformation();

echo $e->name,'的部门是',Employee::DNAME,'<br>';//调用常量
//修改类属性
$e->SetInformation('秀吉',14,'男','0067<br>');
$e->GetInformation();
echo $e->name,'country is ',Employee::COUNTRY,'<hr>';
var_dump($e);
?>
```

运行结果

```
name is 秀吉
id is 0803
秀吉的部门是天地设计
name is 秀吉
id is 0067
秀吉country is ???
object(Employee)#1 (4) { ["name"]=> string(6) "秀吉" ["age"]=> int(14) ["sex"]=> string(3) "男" ["id"]=> string(8) "0067
" }
```

## 连接MySQL

1.连接数据库

```
mysql_connect(servername,username,password);
```

| 参数       | 描述                                                         |
| :--------- | :----------------------------------------------------------- |
| servername | 可选。规定要连接的服务器。默认是 "localhost:3306"。          |
| username   | 可选。规定登录所使用的用户名。默认值是拥有服务器进程的用户的名称。 |
| password   | 可选。规定登录所用的密码。默认是 ""。                        |

脚本一结束，就会关闭连接。如需提前关闭连接，请使用 mysql_close() 函数。

```
<?php
$con= new mysql("localhost","root","123","mydb")
//$con = mysql_connect("localhost","peter","abc123");
if (!$con)
  {
  die('Could not connect: ' . mysql_error());
  }
 mysql_close($con);
?>
```

2.创建

为了让 PHP 执行语句，我们必须使用 mysql_query() 函数。此函数用于向 MySQL 连接发送查询或命令。

```
mysql_query(query,connection)
```

返回值
mysql_query() 仅对 SELECT，SHOW，EXPLAIN 或 DESCRIBE 语句返回一个资源标识符，如果查询执行不正确则返回 FALSE。

| 参数       | 描述                                                         |
| :--------- | :----------------------------------------------------------- |
| query      | 必需。规定要发送的 SQL 查询。注释：查询字符串不应以分号结束。 |
| connection | 可选。规定 SQL 连接标识符。如果未规定，则使用上一个打开的连接。 |

选择数据库。通过 mysql_select_db() 函数选取数据库。

3.插入

```
<?php
$con = mysql_connect("localhost","peter","abc123");
if (!$con)
  {
  die('Could not connect: ' . mysql_error());
  }

mysql_select_db("my_db", $con);

mysql_query("INSERT INTO Persons (FirstName, LastName, Age) 
VALUES ('Peter', 'Griffin', '35')");

mysql_query("INSERT INTO Persons (FirstName, LastName, Age) 
VALUES ('Glenn', 'Quagmire', '33')");

mysql_close($con);
?>
```

