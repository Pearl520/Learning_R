# Learning R笔记

笔记示例代码：https://cran.r-project.org/web/packages/learningr/

#  简介

R 支持混合型的编程范式，是S语言的开源版本。它的核心是一种命令式语言(写一个脚本来逐条执行计算命令)，但它也支持面向对象编程(数据和函数都绑定在类的内部)和函数式编程(函数是 第一类对象，你可以像对待其他任何变量一样对待它们，而且也可以递归调用它们)。**R有两种编程模式：命令式、面向对象和函数式。**

# 第一章 如何从R中获得帮助

## 1. 帮助

### 1.1 ？&？？

查找某函数信息：`?mean`=`help("mean")` 打开mean函数的帮助页面

​                               `?"+"`=`help("+")`

​                               `?"if"`=`help("if")`打开if的帮助页面，用于分支代码

​                               `??plotting`=`help.search("plotting")`搜索所有包含“plotting”的主题

​                               `??"regression model"`=`help.search("regression model")` 搜索所有与regression model相关的主题。

⚠️#符号表示注释。R忽略此行的其他部分。在R上搜索帮助的函数`help.search`，在互联网上用于搜索R相关帮助的函数`RSiteSearch`   。

### 1.2 apropos函数

`apropos`：匹配其输入的变量（重新记起）

举例：变量`vector`

用法：

```R
apropos（"vector")  # 会查找所有含有vector字符串的变量
apropos("z$")       # 寻找所有以z结尾的变量
apropos（"[4-9]"     # 寻找含有4到9之间数字的所有变量
```

### 1.3 其他函数

```R
example(plot)    # 查找函数范例（举例：plot）
demo（）          # 列出所有演示（较长的概念）
browseVignettes（） # 浏览机器上包含片段
vignette("Sweave", package="utils")              # 访问函数特定片段
RSiteSearch（"{Bayesian regression}")            # 在互联网上搜索R相关帮助，查找任何包
```

*vignettes：片段，指导如何使用这些包文件的短文档

## 2. 其他资源

>- R邮件：http://www.r-project.org/mail.html
>- Rseek：http://rseek.org
>- R-博客：http://www.r-bloggers.com

## 小结

- ？+函数名获取帮助
- ？？+字符串获取帮助
- apropos获取帮助

## 练习

```R
> sd(0:100)    # sd函数计算标准差
[1] 29.30017
> demo(plotmath)   # 观看数学符号演示
```





#  第二章 科学计算器

## 1. 冒号运算符 & c函数

**冒号运算符（：）**：创建一个从某个数值开始到另一个数值结束的序列；

**c函数**：把一系列的值拼接起来创建向量；

```R
> 1:5 + 6:10                       # "+"左右有无空格对结果不影响，
[1]  7  9 11 13 15
> c(1,3,6,10,15) + c(0,1,3,6,10)   # c函数是小写c
[1]  1  4  9 16 25
```

⚠️：R变量名不区分大小写。



## 2. 其他运算关系

```R
sum(1:5)  # 求和
median（1:5） # 求中位数
```

### 2.1 普通运算

减法：

```R
> c(1,3,6,7,8) - 2
[1] -1  1  4  5  6
```

乘法：

```R
> -2:2 * -2:2
[1] 4 1 0 1 4
```

```R
identical(2 ^ 3, 2 ** 3)    # ^和**都代表求幂
[1] TRUE
```

浮点数除法：

```R
> 1:10 / 3             # "/"
 [1] 0.3333333 0.6666667 1.0000000 1.3333333 1.6666667 2.0000000 2.3333333
 [8] 2.6666667 3.0000000 3.3333333
```

整数除法：

```R
> 1:10 %/% 3           # "%/%"
 [1] 0 0 1 1 1 2 2 2 3 3
```

求余数：

```R
> 1:10 %% 3             # "%%"
 [1] 1 2 0 1 2 0 1 2 0 1
```

⚠️：所有的函数都作用于向量，而不仅仅是单个值。



### 2.2 复杂运算

```R
> cos(c(0, pi/4, pi/2, pi))     # pi是内置常数
[1]  1.000000e+00  7.071068e-01  6.123234e-17 -1.000000e+00
```

==**欧拉公式**==

```R
> exp(pi * 1i) + 1
[1] 0+1.224647e-16i
```

阶乘：

```
> factorial(5)
[1] 120
```

```
> factorial(7) + factorial(1) - 71 ^ 2
[1] 0
```

chooose函数：

```R
> choose(5, 0:5)         # 逻辑斯蒂模型，排列组合C（n,k）
[1]  1  5 10 10  5  1
> choose(4, 2)
[1] 6
```

choose(a,b)：有a个元素，从a个元素中选出b个元素进行自由组合。



### 2.3 数值比较

⚠️：**要比较数值是否相等要用“==”，**而不是“=”；不等是“!="。

```R
> c(3, 4 -1 ,1 + 1 + 1) == 3
[1] TRUE TRUE TRUE
> 1:3 != 1:3
[1] FALSE FALSE FALSE
> 1:3 != 3:1                # "!="不等于
[1]  TRUE FALSE  TRUE
```

```R
> (1:5) ^ 2 >= 16
[1] FALSE FALSE FALSE  TRUE  TRUE
```



### 2.4 其他函数

log函数：略

exp函数略

### 2.5 舍入误差

> ```R
> > sqrt(2) ^ 2 == 2
> [1] FALSE
> > sqrt(2)^2-2
> [1] 4.440892e-16
> ```
>
> 两个数应该是相等的。

⚠️：用 `== `来比较<u>非整型变量</u>会带来问题，存在**“舍入误差”。**

```R
> all.equal(sqrt(2) ^ 2, 2)
[1] TRUE
```

```R
> all.equal(sqrt(2) ^ 2, 2)       # 提供一个容忍度吃，小于容忍度的舍入误差将被忽略
[1] TRUE
> all.equal(sqrt(2) ^ 3, 3)
[1] "Mean relative difference: 0.06066017"
> isTRUE(all.equal(sqrt(2) ^ 3, 3))
[1] FALSE
```

⚠️：**要检查两个数字是否一样，不要使用“`==`”，而使用`all.equal`函数。**

比较字符串：

```
> c("Can", "you", "a", "canner", "can") == "can"
[1] FALSE FALSE FALSE FALSE  TRUE
```

```
> c("a", "b", "c", "d") < "C"
[1]  TRUE  TRUE  TRUE FALSE
> c("A", "B","C","D") < "C"
[1]  TRUE  TRUE FALSE FALSE
```

⚠️：在帮助页面中*?Arithmetic*、*?Trig*、*?Special*和*?Comparison*有更多的例子，并提供边界情况下的大量处理细节。

> ```R
> > 0^0
> [1] 1
> ```
>



### 2.6 变量赋值

**2.6.1 变量赋值符号**

```R
> x <- 1                     # "<-"或则"="都可以为变量赋值，不需要声明他们
> y = 6                      # "<-"或则"="都可以为变量赋值
> x + 2 * y - 3              # 进行下一步计算
[1] 10
```

⚠️：变量名可包含字母、数字、点和下划线，但不能以一个数字或一个点后跟数字开头。系统的保留字也不允许，如`if`和`for`。

⚠️：命名规则可见：`?make.names`

⚠️：变量赋值运算符两边的空格不是必须的，但可以增加可读性。

✏️:**可以使用`<<-`对全局赋值。**

**2.6.2 assign函数**

不太常见的赋值方式，可读性降低（除了涉及环境变量的高级程序设计）。

```R
assign("my_local_variable", 9^3+10^3)                      # 本地赋值：变量名+值
assign("my_local_variable", 9^3+10^3, globalenv())         # 全局赋值还需要加上参数
> my_local_variable           # 打印变量（linux下使用需要print）
[1] 1729                                                    
```

另外两种打印变量的方式

```R
z <- rnorm(5) ; z                         # 方法一：用分号";"间隔
[1]  2.5857066 -0.2039312 -0.9920766  0.6220330  0.1152765
> (zz <- rlnorm(5))                       # 方法二：将赋值语句用括号括起来
[1] 0.6062625 0.8691764 0.7961486 1.2239356 2.7155873
```



### 2.7 特殊数字

R支持4种特殊值：**Inf**、**-Inf**、**NaN**、**NA**。这四个特殊值的含义依次是：正无穷、负无穷、"不是一个数（Not-a-number"、不可用（not available，缺失值）。

⚠️：如果计算涉及一个缺失值，结果也将丢失。

```R
> c(Inf + 1, Inf - 1, Inf - Inf)
[1] Inf Inf NaN
> c(sqrt(Inf), sin(Inf))
[1] Inf NaN
Warning message:
In sin(Inf) : NaNs produced
> c(NA+1, NA*5, NA+Inf)
[1] NA NA NA
```

⚠️：当算术中涉及NA和NaN时，得到的结果将为这两个值之一，取哪个值则取决于所使用的系统。

⚠️：NaN和NA既非有限值亦非无限值，NaN代表不是一个数，NA代表缺失值。

### 2.8 逻辑向量

许多编程语言都使用布尔逻辑（Boolean），其中的值为TRUE或FALSE。在R中，还可能有缺失值NA，拥有这三种状态的系统成为**troolean逻辑**。

⚠️变量T和F已被系统默认定义为TURE和FALSE，但由于不是保留字，用户可以重新定义它们。

在R中有三个向量化逻辑运算符：

> ! 代表非操作
>
> & 代表与操作
>
> ｜代表或操作

其他两个比较有用的处理逻辑向量的函数是**any**和**all**，如果输入向量中至少包含一个TRUE值或只包含TRUE值，它们将分别返回为TRUE：

```R
> none_true <- c(FALSE, FALSE, FALSE)
> some_true <- c(FALSE, TRUE, FALSE)
> all_true <- c(TRUE, TRUE, TRUE)
> any(none_true)
[1] FALSE
> any(some_true)
[1] TRUE
> any(all_true)
[1] TRUE
> all(none_true)
[1] FALSE
```

## 小结

- R使用troolean逻辑：TRUE\FALSE\NA

## 练习

1. 如何检查变量x是否等于pi。

```R
all.equal(x,pi)
>isTRUE(all.equal(x,pi))     # 更好的写法
[1] TRUE
```

2. 至少描述两种给变量赋值的方式。

> - <-
> - +=
> - +<<-
> - assign

3. (1)求1～1000所有整数的倒数的反正切。参考?Trig帮助页面找到反正切函数。

   (2)将变量x分配从1到1000的数字变量，计算x的倒数的反正切值，然后将其值分配给变量y。逆转此操作，计算y的切线的倒数，然后把值赋给变量z。

```R
atan(1/1:1000)
```

```R
x <- 1:100
y <-atan(1/x)
z <1/tan(y)
```

4. 使用==符号、indentical和all.equal函数，比较第3题中第2题的x和z变量。对于all.equal，尝试通过传入函数的第三个参数改变其容差值。如果容差值设为0，会发生什么?

```R
x == z     
identical(x, z)
all.equal(x, z)
all.equal(x, z, tolerance = 0)
```

5. ```R
   > true_and_missing <- c(TRUE, NA)
   > false_and_missing <- c(FALSE, NA)
   > mixed <- c(TRUE, FALSE, NA)
   > any(true_and_missing)
   [1] TRUE
   > any(false_and_missing)
   [1] NA
   > any(mixed)
   [1] TRUE
   > all(true_and_missing)
   [1] NA
   > all(false_and_missing)
   [1] FALSE
   > all(mixed)
   [1] FALSE
   > 
   ```

   

# 第三章 检查变量和工作区

## 1. 类

R的所有变量都有一个类，表明此变量属于什么类型。大部分的数字是numeric类，逻辑值是logical类。R没有标量类型（scalar type，所以更严格的说，**数字向量应该是numeric类，逻辑向量是logical类。**在R中，“最小的“的数据类型是**向量**。

- **numeric类**
- **logical类**

```R
> class(my_variable)      # 可以使用class函数来找出变量的类名
> class(c(TRUE, FALSE))   # 举例
[1] "logical"
```

⚠️：所有的变量除了类之外，还有一个内部存储类型（通过typeof访问）、一个模式（mode）、一个存储模式（storage.mode)。（一般不怎么使用这些，只需要使用对象的类。）

⚠️：下面将将类（class）和类型（type）等同。

### 1.1 不同类型的数字

R包括三种不同类别的数值变量：**浮点值numeric**、**整数integer**和**复数complex**。

```R
> class(sqrt(1:10))            
[1] "numeric"
> class(3+1i)   # "i"创建了复数的虚部
[1] "complex"
> class(1)      # 尽管只有一个数字，也是浮点值numeric
[1] "numeric"
> class(1L)     # 添加L后缀吧数字变成整型
[1] "integer"
> class(0.5:4.5)  # 冒号操作符返回值是numeric
[1] "numeric"
> class(1:5)      # 除非全部是整数
[1] "integer"
```

⚠️：即使是把R装在64位操作系统上，所有的浮点数仍然是32位（双精度），16位（单精度）的数字是不存的。

输入`.Machine`，将显示一些R的数字属性信息。

> R中最大的全精度浮点数是：1.8e308（日常够用，比无穷大小的多）
>
> 可以表示的最小正数是2.2e-308
>
> 最大的整数为2^31-1
>
> 此外，可以从`Rmpfr`包中得到更高精度的值，或者`brobdingnag`中得到非常大的数字（基本用不上）。
>
> ⚠️：ε是最小的正浮点数

### 1.2 其他通用类

除了numeric类和logical类，向量还有其他三个类：存储文本的字符**character**、存储类别数据的因子**factor**、罕见的存储二进制数据的原始值**raw**。

**1.2.1 character  & factor**

```R
> (gender <- factor(c("male","female","female","male","female"))) # 创建字符向量
[1] male   female female male   female
Levels: female male
> levels(gender)     # 因子（拥有标签的整数）
[1] "female" "male"  # 因子水平按字母顺序排序
> nlevels(gender)    # 查找因子的水平值
[1] 2
> as.integer(gender) # 在底层，因子的值被存储为整数，而非字符
[1] 2 1 1 2 1
```

⚠️：可以使用`obeject.size`返回每个对象的内存分配大小。32位和64位系统中变量所占用的内存数量是不一样的，所以在不同情况下`object.size`将返回不同的值。

当操作因子水平的内容时（如清理命名，把所有的男性统一位”male“，而非”Male“），最好先把因子转换成字符串后再处理，以便充分利用字符串操作函数。

**1.2.2 raw**

原始类raw存储向量的“原始‘字节。每个字节由一个两位的十六进制值表示。它们主要用于保存输入的二进制文件的内容。使用`as.raw`

函数可把0到255之间的整数转换为原始值，此范围之外的数字将全部视为0，分数和虚部也被丢弃。

```R
> as.raw(1:17)
 [1] 01 02 03 04 05 06 07 08 09 0a 0b 0c 0d 0e 0f 10 11
> as.raw(c(pi,1+1i,-1,256))
[1] 03 01 00 00
Warning messages:
1: imaginary parts discarded in coercion 
2: out-of-range values treated as 0 in coercion to raw 
```

⚠️：对字符串，`as.raw`则不起作用，而需要使用`charToRaw`函数：

```R
> (sushi <- charToRaw("Fish!"))   # charToRaw函数将字符串"Fish!"转换为raw
[1] 46 69 73 68 21
> class(sushi)
[1] "raw"
```

**1.2.3 其他类型变量**

数组包含多维数据，矩阵（通过matrix类）是特殊的二维数据。

⚠️：目前所有以上的变量类型都要包含相同类型的值，如character向量或数组里必须包含字符串。

⚠️：列表（list）则比较灵活，列表里的每一项都可以是不同的类型，甚至能包含其他列表

**1.2.4 检查更改类-is&as**

命令行提示符：直接键入类class的函数名来检查变量

脚本中测试对象：is函数或针对某个特定类写的特定函数

```R
> is.logical(FALSE)   
[1] TRUE
>ls(pattern="^is", baseenv())  # 查看在base包中所有的is函数；
```

> 改变一个对象的类型：**转型（casting）**
>
>  ⚠️：尽可能使用特定的`as*`函数，而非单纯的as函数。
>
> ```R
> > x <- "123.456"
> > as(x,"numeric")
> [1] 123.456
> > as.numeric(x)
> [1] 123.456
> # R能打印到小数点后第几位取决于R的设置。
> > options(digits=n) # n在1和22之间
> ```

一般情况下，特定类的变量的使用应始终优先于标准函数as。

```R
> y <- c(2,12,343,34997)
> as(y,"data.frame")
Error in as(y, "data.frame") : 
  no method or default for coercing “numeric” to “data.frame”
> as.data.frame(y)
      y
1     2
2    12
3   343
4 34997
```

## 2. 检查变量

大多数情况下，method和function是可以互换的。有时，R中的函数也被称为<u>面向对象中的方法</u>。不同类型的对象有不同版本的print函数，使得矩阵与向量的打印方法不同。

**打印输出- print**

对于内循环或函数来说，自动打印功能不起作用，需要<u>显式调用print</u>。

```R
> ulams_spiral <- c(1,8,23,46,77)
> for(i in ulams_spiral) i    # 自动打印不起作用
> for(i in ulams_spiral) print(i)  # 显式调用print
[1] 1
[1] 8
[1] 23
[1] 46
[1] 77
```

⚠️：大部分print函数的实现建立在调用底层的cat函数上；c和cat函数都是concatenate的缩写，但它们的作用完全不同。 

**查看对象汇总信息- summary**

```R
> num <- runif(30)   # runif函数生成30个均匀分布于0和1的随机数
> summary(num)
   Min. 1st Qu.  Median    Mean 3rd Qu.    Max. # 数值变量会被汇总统计出平均数、中位数，分位数
0.02874 0.20021 0.45683 0.43698 0.62428 0.82473 
```

类比变量和逻辑向量将根据每个值的计算进行汇总。

> ```R
> > fac <- factor(sample(letters[1:5],30,replace = TRUE))
> > summary(fac)
> a b c d e 
> 7 6 6 3 8 
> ```
>
>   注释：letters是内置常数，包含a～z的小写值，同理LETTERS是从A～Z；
>
> ​             letters[1:5]用索引将letters 的范围限制在a～e；
>
> ​             sample函数使用重复抽样replace随机抽样30次。
>
> ```R
> > bool <- sample(c(TRUE,FALSE,NA),30,replace = TRUE)
> > summary(bool)
>    Mode   FALSE    TRUE    NA's 
> logical       3      11      16 
> ```

**检查前几行-head**

```R
> dfr <- data.frame(num,fac,bool)  # 定义一个dfr数据框变量
> head(dfr)    # head函数只显示大量数据的前6行
        num fac bool
1 0.6263754   d TRUE
2 0.6089705   b TRUE
3 0.5228430   c TRUE
4 0.3860174   b TRUE
5 0.1967886   c   NA
6 0.3204016   e   NA
# 对数据库使用summary函数
> summary(dfr)
      num          fac      bool        
 Min.   :0.02874   a:7   Mode :logical  
 1st Qu.:0.20021   b:6   FALSE:3        
 Median :0.45683   c:6   TRUE :11       
 Mean   :0.43698   d:3   NA's :16       
 3rd Qu.:0.62428   e:8                  
 Max.   :0.82473  
```

**对象的结构-str**

str函数对数据框的嵌套列表非常有用：

```R
> str(num)
 num [1:30] 0.626 0.609 0.523 0.386 0.197 ...
> str(dfr)
'data.frame':	30 obs. of  3 variables:
 $ num : num  0.626 0.609 0.523 0.386 0.197 ...
 $ fac : Factor w/ 5 levels "a","b","c","d",..: 4 2 3 2 3 5 5 3 1 3 ...
 $ bool: logi  TRUE TRUE TRUE TRUE NA NA ...
```

⚠️：每个类都有自己的打印（print）方法，但有时这种打印模糊了其内部结构 或会忽略一些有用的信息。使用`unclass`函数可以避免这一点，显示变量是如何构建的。

**显示变量构建方法-unclass**

```R
> unclass(fac)   # 对因子调用unclass显示它仅是一个integer，拥有一个叫levels的属性
 [1] 4 2 3 2 3 5 5 3 1 3 1 1 2 1 5 3 2 5 5 5 4 4 2 2 1 5 1 5 1 3
attr(,"levels")       
[1] "a" "b" "c" "d" "e"
# attributes函数能显示当前对象的所有属性列表
> attributes(fac)
$levels
[1] "a" "b" "c" "d" "e"

$class
[1] "factor"
```

**可视化二维变量-View/edit/fix**

```R
View(dfr)   # 注意是大写“V“，不允许更改；
new_dfr <- edit(dfr) # 更改并保存于new_dfr
fix(dfr)  # 更改保存于dfr
```

> <img src="Learning R.assets/image-20211207154814661.png" alt="image-20211207154814661" style="zoom: 33%;" />

结合`View`和`head`来查看数据框的前几行：`View(head(dfr,50))`.

## 3. 工作区

**ls函数**

`ls`函数可以知道已经创建的变量及其内容，变量以`. `开头的是隐藏文件。

```R
> ls()
 [1] "bool"         "dfr"          "fac"          "i"            "new_dfr"      "num"         
 [7] "test_R.R"     "ulams_spiral" "x"            "y"           
> ls(all.names = TRUE)   # 传入all.names=TRUE参数查看隐藏文件
 [1] ".Random.seed" "bool"         "dfr"          "fac"          "i"            "new_dfr"     
 [7] "num"          "test_R.R"     "ulams_spiral" "x"            "y"           
> ls(pattern = "oo")     # 查看含有"_"的变量
[1] "bool"
```

**ls.str函数**

要了解更多工作区的信息，可以使用`ls.str`函数查看变量的结构，`browseEnv`提供类似的功能（以HTML输出）。

**rm函数**

```R
> rm(apple, pear, lemon) 
> rm(list = ls())    # 删除所有变量。小心使用！
```

## 小结

- 可通过`is`函数或特定类的变量来测试一个对象是否是某个类；
- 可使用`as`函数或特定类的变量来改变一个对象的类；
- 检视变量的函数：`summary`，`head`，`str`，`unclass`，`attributtes`，和`View`；
- `ls`能列出变量；`ls.str`连同名字及结构一起列出；
- `rm`删除变量；

R中最基本的数据类型：

> - Numeric类
> - Logical类
> - Character类
> - Factor类
> - Raw类

按对象类型来分：

> - 向量（vector）
>
> - 列表（list）
>
> - 矩阵（matrix）
> - 数组（array）
> - 因子（factor）
> - 数据框（data.frame)

<img src="https://www.runoob.com/wp-content/uploads/2020/07/52988954-D570-42FD-9CFC-90CD78D361C3.jpg" alt="img" style="zoom: 67%;" />

## 练习

数字的三个内置类：numeric、integer、complex

查找因子的水平和水平值所用函数：`levels()` 及`nlevels()`

如何把字符串“6.283185”转换为数字：`as.numeric("6.283185)`

**1. 查找以下值的类、类型、模式及存储模式：Inf、NA、NaN和" "。**

```R
> class(Inf)     # 类
[1] "numeric"
> class(NA)
[1] "logical"
> class(NaN)
[1] "numeric"
> class(" ")
[1] "character"
> typeof(Inf)     # 类型
[1] "double"
> typeof(NA)
[1] "logical"
> typeof(NaN)
[1] "double"
> typeof(" ")
[1] "character"
> mode(Inf)      # 模式
[1] "numeric"
> mode(NA)
[1] "logical"
> mode(NaN)
[1] "numeric"
> mode(" ")
[1] "character"
> storage.mode(Inf)   # 存储模式
[1] "double"
> storage.mode(NA)
[1] "logical"
> storage.mode(NaN)
[1] "double"
> storage.mode(" ")
[1] "character"
```

**2. 随机从“dog”、“cat”、“hamster”和“goldfish”中以相等的概率生成1000个宠物名，显示所得变量的前几个值，并计算每种宠物的数量**。

```R
# sample函数使用重复抽样replace 1000次
> pets <- factor(sample(c("dog","cat","hamster","goldfish"),1000,replace = TRUE))
> head(pets)
[1] goldfish cat      cat      hamster  dog      cat     
Levels: cat dog goldfish hamster
> summary(pets)   # summary查看对象汇总信息
     cat      dog goldfish  hamster 
     267      277      239      217 
```

**3. 创建一些以蔬菜命名的变量。列出用户工作区所有包含字母“a“的变量。**

```R
> ls(pattern="a")
```



# 第四章 向量、矩阵和数组

## 1. 向量

**回顾：**

创建从某个数到另一个数的数字序列：冒号运算符

拼接数值和向量：`c`函数

```R
> c(1,1:3,c(5,8),13)
[1]  1  1  2  3  5  8 13
```

**创建指定类型和长度的矢量-vector**

```R
> vector("numeric",5)
[1] 0 0 0 0 0
> vector("complex",5)
[1] 0+0i 0+0i 0+0i 0+0i 0+0i
> vector("logical",5)
[1] FALSE FALSE FALSE FALSE FALSE
> vector("character",5)
[1] "" "" "" "" ""
> vector("list",5)
[[1]]       # null是一个特殊的”空“值
NULL

[[2]]
NULL

[[3]]
NULL

[[4]]
NULL

[[5]]
NULL
```

用每个类型的包装函数（wrapper）来创建矢量以节省打字时间，下面命令与上面的命令等价：

```R
> numeric(5)
[1] 0 0 0 0 0
> complex(5)
[1] 0+0i 0+0i 0+0i 0+0i 0+0i
```

⚠️：list函数的工作方式与它们不同，`list(5)`创建的内容有所不同。

### 1.1 序列

seq函数可以以许多不同的方式指定序列，一般不需要调用它，有三个专门的序列函数，运行更快更便捷。

```R
# seq.int函数
> seq.int(3,12)   
 [1]  3  4  5  6  7  8  9 10 11 12
> seq.int(3,12,2)   # seq.int可以指定步长，比冒号实用
[1]  3  5  7  9 11
> seq.int(0.1,0.01,-0.01)
 [1] 0.10 0.09 0.08 0.07 0.06 0.05 0.04 0.03 0.02 0.01
> n <- 0
> 1:0
[1] 1 0
# seq_len函数
> seq_len(n) # 创建1：n向量
> seq_len(5)
[1] 1 2 3 4 5
> seq_len(0) # 输入值为0时，这个函数更有用
integer(0)
# seq_along函数
> pp <- c("Peter", "Piper", "picked","a","peck","of","pickled","peppers")
> for(i in seq_along(pp)) print(pp[i])
[1] "Peter"
[1] "Piper"
[1] "picked"
[1] "a"
[1] "peck"
[1] "of"
[1] "pickled"
[1] "peppers"
# 上面三个函数都可以用seq函数替换，但没有必要
```

### 1.2 长度

所有的向量都有一个长度，告诉我们向量包含多少个元素。长度是一个非负整数（可为0）。

```R
> length(1:5)
[1] 5
> length(c(TRUE,FALSE,NA))
[1] 3
```

⚠️：容易混淆的是字符向量，它们的长度为字符串的数目，而非每个字符串中字符的长度。

```R
> sn <- c("Sheena", "leads", "Sheila", "needs")
> length(sn)
[1] 4
> nchar(sn)   # 字符向量数目使用nchar函数
[1] 6 5 6 5
```

可以为向量重新分配长度。

```R
> poincare <- c(1,0,0,0,2,0,2,0)
> length(poincare) <- 3
> poincare
[1] 1 0 0     # 后面的值会删除
> length(poincare) <- 8
> poincare
[1]  1  0  0 NA NA NA NA NA # 缺失值会增加
```

### 1.3 命名

```R
> c(apple=1, banana=2, "kiwi fruit"=3)   # 可以用name=value的形式在创建向量时为其指定名称
     apple     banana kiwi fruit 
         1          2          3 
> x <- 1:4
> names(x) <- c("apple","bananas","kiwi fruit","") # 也可以使用names函数为元素添加名字
> x
     apple    bananas kiwi fruit            
         1          2          3          4
```

names函数也可以以用于去的向量的名称：

```R
> names(x)
[1] "apple"      "bananas"    "kiwi fruit" ""  
```

### 1.4 索引

通常，我们只要访问向量中的部分或个别元素，这就是所谓的**索引**，用方括号`[]`来实现。

⚠️：给向量传入正数，它会返回此位置上的向量元素切片。它的第一个位置是1，而不是想其他语言一样是0。

（其他索引方法略）

举例：

```R
> x<- (1:5)^2
> print(x)
[1]  1  4  9 16 25
> x[c(1,3,5)]  # 正整数的位置索引
[1]  1  9 25
> x[c(-2,-4)]  # 传入负值，返回一个向量切片，包含除了这些位置意外的所有元素
[1]  1  9 25
> x[c(TRUE,FALSE,TRUE,FALSE,TRUE)] # 传入逻辑向量，返回的向量切片里面只包含索引为TRUE的元素
[1]  1  9 25
```

如果给每个元素命名，以以下方法也将返回相同的值：

```R
> names(x) <- c("one","four","nine","sixteen","twenty five") # 元素名称
> x[c("one","nine","twenty five")]
        one        nine twenty five 
          1           9          25 
```

混合使用正负值是不允许的，会抛出一个错误：

```R
> x[c(1,-1)]  # 说不通
Error in x[c(1, -1)] : only 0's may be mixed with negative subscripts
```

⚠️：使用正数或逻辑值作为下标，那没缺失索引所对应的值同样也是缺失值。

⚠️：对于负的下标值来说，不允许存在缺失值，会产生错误。

⚠️：超过范围的下标值（超出矢量的长度）不会导致错误，而是返回缺失值NA。

⚠️：非整数下标会默认向零舍入。（R过于宽松）

```R
> x[1.9]
one 
  1 
```

⚠️不传递任何下标值将返回整个向量。

```R
> x[]
        one        four        nine     sixteen twenty five 
          1           4           9          16          25    # 没有传递索引值
```

⚠️：`which`函数将返回逻辑向量中为TRUE的位置。如果要将逻辑索引切换到整数引中，这个函数很有用。

```R
> which(x > 10)
    sixteen twenty five 
          4           5 
```

此外：

```R
> which.min(x)  # 最小的x，是which(min(x))的缩写
one 
  1 
> which.max(x)   # 最大的x，是which(max(x))的缩写
twenty five 
          5 
```

### 1.5 向量循环和重复

单独的数字与向量相加，向量的每个元素都会与该数字相加：

```R
> 1:5+1
[1] 2 3 4 5 
```

两个向量相加时，R将会循环较短向量中的元素以配合较长的那个：

```
> 1:5+1:15
 [1]  2  4  6  8 10  7  9 11 13 15 12 14 16 18 20
```

较优做法：明确创建同等长度的向量，然后对它们进行操作：

```R
> rep(1:5,3)
 [1] 1 2 3 4 5 1 2 3 4 5 1 2 3 4 5
> rep(1:5,each=3)
 [1] 1 1 1 2 2 2 3 3 3 4 4 4 5 5 5
> rep(1:5,times=1:5)
 [1] 1 2 2 3 3 3 4 4 4 4 5 5 5 5 5
> rep(1:5,length.out=7)
[1] 1 2 3 4 5 1 2
# rep有一个更为简单和快速的变体rep.int
> rep.int(1:5,3)
 [1] 1 2 3 4 5 1 2 3 4 5 1 2 3 4 5
> rep_len(1:5,13)
 [1] 1 2 3 4 5 1 2 3 4 5 1 2 3
```

## 2. 矩阵和数组

数组能存放多维矩形数据，矩阵事二维数组的特例。

### 2.1 创建

可以使用`array`函数创建一个数组，为它们传入两个向量（值和维度）作为参数，可以为每个维度命名。

**创建数组：**

```R
> (three_d_array <- array(   # array函数创建数组
+ 1:24,     # 含有1～12一共12个元素
+ dim=c(4,3,2),     # 维度dim参数
+ dimnames= list(   # 给每个维度命名
+ c("one","two","three","four"),  # 4
+ c("ein","zwei","drei"),         # 3
+ c("un","deux")                  # 2
+ )
+ ))
 # 输出数组
, , un                     

      ein zwei drei
one     1    5    9
two     2    6   10
three   3    7   11
four    4    8   12

, , deux

      ein zwei drei
one    13   17   21
two    14   18   22
three  15   19   23
four   16   20   24
```

**创建矩阵：**（与创建数组类似，使用`matrix`函数+`nrow`）

```R
> (a_matrix <- matrix(   # matrix函数创建矩阵
+ 1:12,
+ nrow=4,           # 只需要指定行数或列数； #ncol=3将为是同样的效果
+ dimnames=list(
+  c("one","two","three","four"),
+  c("ein","zwei","drei")
+ )
+ ))
      ein zwei drei    # 仔细看这里传入的值是按照列来填充矩阵的！
one     1    5    9
two     2    6   10
three   3    7   11
four    4    8   12
> class(a_matrix)        # 也可以使用array函数创建此矩阵，且具有矩阵类
[1] "matrix" "array"    
# 用array函数创建矩阵
> (two_a_array <- array(
+ 1:12,
+ dim=c(4,3),
+ dimnames=list(
+   c("one","two","three","four"),
+   c("ein","zwei","drei")
+ )
+ ))
      ein zwei drei
one     1    5    9
two     2    6   10
three   3    7   11
four    4    8   12
> class(two_a_array)
[1] "matrix" "array"   # 用array函数创建的matrix同时具有array类和matrix类
```

创建矩阵时，传入的值会按列填充矩阵。也可以指定参数`byrow=TRUE`来按行填充矩阵：

```R
> matrix(
+ 1:12,
+ nrow=4,
+ byrow=TRUE,   # 指定matrix按照行来填充
+ dimnames=list(
+   c("one","two","three","four"),
+   c("ein","zwei","drei")
+ )
+ )
      ein zwei drei  # nrow=4，按照row开始填充
one     1    2    3
two     4    5    6
three   7    8    9
four   10   11   12
```

### 2.2 行、列、维度

```R
# 对于矩阵和数组，dim函数可以返回其维度的整数值向量
> dim(three_d_array)
[1] 4 3 2
> dim(a_matrix)
[1] 4 3

# 对于矩阵，函数nrow和ncol将分别返回行数和列表
> nrow(a_matrix)
[1] 4
> ncol(a_matrix)
[1] 3
```

`length`函数也能用于矩阵和数组，将返回<u>所有维度的乘积</u>：

```R
> length(a_matrix)
[1] 12
```

我们还可以通过`dim`函数分配一个新的维度来**重塑矩阵**或数组。

⚠️：小心使用`dim`函数重塑功能，它会删除原维度的名称。

```R
> dim(a_matrix) <- c(6,2)  # 将原4*3矩阵改为6*2矩阵
> a_matrix
     [,1] [,2]     # 可以发现原来的dimnames都被删除了
[1,]    1    7
[2,]    2    8
[3,]    3    9
[4,]    4   10
[5,]    5   11
[6,]    6   12
```

⚠️：把`nrow`、`ncol`和`dim`用于向量时将返回**NULL**值。与`nrow`和`ncol`相对的函数是`NROW`和`NCOL`。他们把向量看作具有单个列的矩阵（列向量）。

```R
> recaman <- c(0,1,3,6,2,7,13,20)
> nrow(recaman)
NULL
> NROW(recaman)
[1] 8
> NCOL(recaman)
[1] 1
> dim(recaman)
NULL
```

### 2.3 行名、列名、维度名

矩阵的行和列也有行名rownames和列名colnames，维度名dimnames。

### 2.4 索引数组

索引数组与索引向量类似，只是现在要索引的维度多于一个。我们用方括号表示索引。有4种指定索引的方法（正整数、负整数、逻辑值、元素名称）。每个维度的下标用逗号分隔。

```R
# 复习利用matrix函数创建矩阵
> (a_matrix <- matrix(
+ 1:12,
+ nrow=4, 
+ dimnames=list(
+ c("one","two","three","four"),
+ c("ein","zwei","drei")
+ )
+ ))
      ein zwei drei
one     1    5    9
two     2    6   10
three   3    7   11
four    4    8   12
```

利用创建的a_matrix数组可以实现下面的操作：

```R
> a_matrix[1,c("zwei","drei")] # 提取第一行，第二列和第三列的元素
zwei drei 
   5    9 
# 要包括所有的维度，则只需要置空相应的下标：
> a_matrix[1, ]
 ein zwei drei 
   1    5    9 
> a_matrix[, ] # 输出略
```

### 2.5 合并矩阵

c函数能在拼接矩阵之前把它们转换成向量：

```R
> (another_matrix <- matrix(
+ seq.int(2,24,2), # 从2到24创建步长为2的向量
+ nrow=4,
+ dimnames=list(
+  c("five","six","seven","eight"),
+  c("vier","funf","sechs")
+ )
+ ))
      vier funf sechs
five     2   10    18
six      4   12    20
seven    6   14    22
eight    8   16    24
# 使用c函数将矩阵a_matrix和another_matrix拼接
> c(a_matrix,another_matrix)
 [1]  1  2  3  4  5  6  7  8  9 10 11 12  2  4  6  8 10 12 14 16 18 20 22 24
```

使用`cbind`函数和`rbind`函数按行和列来绑定两个矩阵：

```R
# 横向合并矩阵：按行绑定(行固定，列相连)
> cbind(a_matrix,another_matrix)
      ein zwei drei vier funf sechs
one     1    5    9    2   10    18
two     2    6   10    4   12    20
three   3    7   11    6   14    22
four    4    8   12    8   16    24
# 竖向合并矩阵：按列绑定（列固定，行相连
> rbind(a_matrix,another_matrix)
      ein zwei drei
one     1    5    9
two     2    6   10
three   3    7   11
four    4    8   12
five    2   10   18
six     4   12   20
seven   6   14   22
eight   8   16   24
```

### 2.6 数组算数

与向量中的运算一样，标准算术运算符（+、-、\*、/）可以以同样的方式按元素处理矩阵和数组：

```R
> a_matrix + another_matrix # 演示加法
> a_matrix * another_matrix # 演示乘法（哈达玛积，见后文）
```

⚠️：当对两个数组执行算术运算时，必须确保这两个数组的大小适当（是一致的）。

例如，两个数组在相加时大小必须相等，矩阵相乘时候第一个矩阵的行数必须和第二矩阵的列数相等。

```R
> a_matrix               # 4*3矩阵
      ein zwei drei
one     1    5    9
two     2    6   10
three   3    7   11
four    4    8   12
> another_matrix        # 4*3矩阵
      vier funf sechs
five     2   10    18
six      4   12    20
seven    6   14    22
eight    8   16    24
> a_matrix * another_matrix  # 两个矩阵相乘，一一对应
      ein zwei drei
one     2   50  162
two     8   72  200
three  18   98  242
four   32  128  288
```

**`t`函数**可以用来**转置矩阵**，但不能转置数组，举例：

```R
> t(a_matrix)   # 使用t函数将矩阵a_matrix的行列置换
     one two three four
ein    1   2     3    4
zwei   5   6     7    8
drei   9  10    11   12
```

矩阵内乘和外乘运算：特殊运算符**%*%**和**%o%**。如果维度的名称存在的话，都取自第一个输入。

> 还有一个特殊的运算符：**`%in%`**(判断元素是否在向量里面)

```R
# 矩阵乘法
> a_matrix %*% t(a_matrix)    # a_matrix的转置矩阵为a_matrix的同型矩阵
      one two three four
one   107 122   137  152
two   122 140   158  176
three 137 158   179  200
four  152 176   200  224

# 矩阵外乘
> 1:3 %o% 4:6
     [,1] [,2] [,3]
[1,]    4    5    6
[2,]    8   10   12
[3,]   12   15   18
> outer(1:3,4:6)      # outer函数与运算符"%o%"是等价的
      [,1] [,2] [,3]
[1,]    4    5    6
[2,]    8   10   12
[3,]   12   15   18
```

> 复习一下矩阵乘法计算：
>
> （上面案例中涉及3种乘法计算）
>
> **矩阵乘法Matrix Multiplication**
>
> <u>A和B必须是同型矩阵。</u>
>
> 
>
> 
>
> ![image-20211215190044441](Learning R.assets/image-20211215190044441.png)
>
> R中用**`%*%`**表示矩阵的内乘。
>
> 
>
> **矩阵外乘Outer Product of Arrays**
>
> 略
>
> R中用**`%o%`**表示矩阵的外乘，也可以用`outer`函数。
>
> 
>
> **哈达玛积（Hadamard Product）——A*B**
>
> 机器学习中称之为元素积。
>
> **输入：** 两个相同形状的矩阵。
>
> **输出：** 具有同样形状的、各个位置的元素等于两个输入矩阵相同位置元素的乘积的矩阵。
>
> ![Hadamard Product矩阵表示](https://www.maixj.net/pics/uploads/2018/11/hadamard_product_2.jpg)
>
> 在R语言中使用**`*`**来计算Hadamard积。

因为**幂运算符号`^`**也将作用于矩阵的每个元素，所以在<u>为矩阵求反</u>时不能简单地为矩阵使用一次负一次方运算，而应该使用`solve`函数。

```R
> (m <- matrix(c(1,0,5,-3,1,2,4,7),nrow=3))
     [,1] [,2] [,3]
[1,]    1   -3    4
[2,]    0    1    7
[3,]    5    2    1
Warning message:
In matrix(c(1, 0, 5, -3, 1, 2, 4, 7), nrow = 3) :
  data length [8] is not a sub-multiple or multiple of the number of rows [3]
> m^-1
     [,1]       [,2]      [,3]
[1,]  1.0 -0.3333333 0.2500000
[2,]  Inf  1.0000000 0.1428571
[3,]  0.2  0.5000000 1.0000000
# 使用solve函数求反
> (inverse_of_m <- solve(m))
            [,1]        [,2]         [,3]
[1,]  0.09420290 -0.07971014  0.181159420
[2,] -0.25362319  0.13768116  0.050724638
[3,]  0.03623188  0.12318841 -0.007246377
# 可以试着求一下单位矩阵
> m %*% inverse_of_m
              [,1]         [,2]          [,3]
[1,]  1.000000e+00 5.551115e-17 -3.469447e-17    # e是科学记数法
[2,] -6.938894e-18 1.000000e+00  3.469447e-18    
[3,] -4.857226e-17 1.387779e-17  1.000000e+00
# 3.4699447e-18表示3.4699447*（10的-18次方），认为是0 
# 出现这一情况的原因是因为R的浮点精度问题
```

**补充：如何去计算一个4阶矩阵的特征值与特征向量？**

```R
> a_matrix <- matrix(c(2, 2, 1, 0, 2, 0, 1, 3, 1, 1, 2, 2, 0, 3, 2, 4),
+ ncol=4,
+ nrow=4
+ )
> ev <- eigen(a_matrix)
> ev$val
[1]  7.0269811  2.5085189  0.8369291 -2.3724291
> ev$vec
           [,1]       [,2]       [,3]        [,4]
[1,] -0.2656231  0.8561408  0.2025162  0.39427718
[2,] -0.4505149  0.1586817  0.3263394 -0.81569542
[3,] -0.4342524  0.1180003 -0.8882194 -0.09255815
[4,] -0.7334204 -0.4774086  0.2521033  0.41306110
> ev
eigen() decomposition
$values
[1]  7.0269811  2.5085189  0.8369291 -2.3724291

$vectors
           [,1]       [,2]       [,3]        [,4]
[1,] -0.2656231  0.8561408  0.2025162  0.39427718
[2,] -0.4505149  0.1586817  0.3263394 -0.81569542
[3,] -0.4342524  0.1180003 -0.8882194 -0.09255815
[4,] -0.7334204 -0.4774086  0.2521033  0.4130611
```



## 小结

- 三个专门的序列函数：`seq.int`，`seq_lens`，`seq.along`。

  其中seq.along函数的用法较难，可以创建创建一个从[1]开始，长度为其输入值的序列。

- 向量的长度可以通过length函数指定。可以指定方括号的索引值来访问向量中的子向量。

- `rep`函数能创建重复的向量元素。

- `nrow`、`ncol`、`dim`函数提供了访问数组维度的方法。也可以用`rownames`、`colnames`和`dimnames`取得数组中维度的名称。

## 练习

**1. 如何创建一个包含值0、0.25、0.5、0.75和1的向量？**

```R
> Q_1 <- c(0, 0.25, 0.5, 0.75, 1)
> Q_1
[1] 0.00 0.25 0.50 0.75 1.00
> seq.int(0,1,0.25) # 观察数据特点
[1] 0.00 0.25 0.50 0.75 1.00
```

 **2. 两种命名向量元素的方式。**

```R
> # 方式一：name=value
> c(A=1, B=2, C=3)
A B C 
1 2 3 
> # 方式二：names()函数
> x<-1:3
> names(x)<-c("a","b","c")
> x
a b c 
1 2 3 
```

**3. 向量索引中的四种类型。**

答：正整数位置索引、负整数位置索引、逻辑值索引，元素名称。

**4. 一个3\*4\*5的数组的长度是多少？**

答：3\*4\*5=60。

**5. 求矩阵乘法用到的操作符。**

答：%*%。

**6. 第n个三角形数表示为n*（n+1）/2。创建一个包含前20个三角形的序列。用内置常数letters，使用前20个英文字母来给创建的向量命名。选择命名为元音的三角数。**

```R
> n <- seq_len(20)
> n <- seq_len(20)   # 创建序列，seq_len函数可以创建1:n向量
> triangular <- n*(n+1)/2    # 三角形数
> names(triangular) <- letters[seq_along(n)]# letters是内置常数，含有小写字母，names(x)命名；seq_along:规律序列
> triangular[c("a","e","i","o")]  # 根据索引[]提取向量元素 
  a   e   i   o 
  1  15  45 120 
```

**7.`diag`函数有几种用途，其中之一是以输入向量作为对角线来创建一个方阵。使用序列10到0到11（11，10，...，1，0，1，...，11）创建一个21*21的矩阵。**

```R
# 参考答案：
> diag(abs(seq.int(-11,11)))  # abs是能计算一个数的绝对值的函数
```

**8. 给diag函数传递两个额外的参数来指定输出的维度。1）创建一个主对角线元素都为1的20*21的矩阵。在此基础上加一行全零元素来创建21*21的方阵，原主对角线上的全1元素现在全体向下偏移一行。 2）创建另一个矩阵，使主对象线上的全1元素往上偏移一行。3）把这两个矩阵相加，然后和`diag(abs(seq.int(-10,10)))`相加。所得矩阵被称为wilkison矩阵。4）eigen函数计算矩阵的特征值和特征向量。**

```R
# 参考答案：
> identity_20_by_21 <- diag(rep.int(1,20),20,21)
> below_the_diagonal <- rbind(0,identity_20_by_21)
> identity_21_by_20 <- diag(rep.int(1,20),21,20)
> above_the_diagonal <-cbind(0,identity_21_by_20)
> on_the_diagonal <- diag(abs(seq.int(-10,10)))
> wilkinson_21 <- below_the_diagonal + above_the_diagonal + on_the_diagonal
> eigen(wilkinson_21)$value
```



# 第五章 列表和数据框

向量、矩阵、数组所包含的元素的类型都是相同的。列表和数据框能将不同类型的数据合并到单一变量。

## 1. 列表

### 1.1 创建列表

列表由`list`函数创建，用逗号分隔每个参数即可指定列表中的内容。列表中的元素变量的类型不限，可以是向量、矩阵、函数。

```R
> a_list <- list(      # 列表中的元素变量类型不限，与
+  c(1,1,2,5,14,42),   # 列表元素可以是向量
+  month.abb,          # month.abb是一个Built-in Constants，即内置常量同letters一样
+  matrix(c(3,-8,1,-3),nrow = 2),    # 列表元素可以是矩阵
+  asin                              # 列表元素可以是函数
+  )
> a_list
[[1]]
[1]  1  1  2  5 14 42

[[2]]
 [1] "Jan" "Feb" "Mar" "Apr" "May" "Jun" "Jul" "Aug" "Sep" "Oct" "Nov" "Dec"

[[3]]
     [,1] [,2]
[1,]    3    1
[2,]   -8   -3

[[4]]                                       
function (x)  .Primitive("asin")

# 与向量命名类似，可以在构造列表时就给元素命名，或者在构造列表之后使用names函数命名：
> names(a_list) <- c("catalan","months","involutary","arsin") # catalan：卡特兰数
> a_list
$catalan
[1]  1  1  2  5 14 42

$months  # month.abb 的命名
 [1] "Jan" "Feb" "Mar" "Apr" "May" "Jun" "Jul" "Aug" "Sep" "Oct" "Nov" "Dec"

$involutary
     [,1] [,2]
[1,]    3    1
[2,]   -8   -3

$arsin
function (x)  .Primitive("asin")
```

⚠️：在命名时最好使用有效的变量名！

这里列举一些R中的Built-in Constants：

> ```R
> LETTERS
> letters
> month.abb
> month.name
> pi
> ```

列表也可以作为一个列表的元素：

```R
> (main_list <- list(    # 事实上，过多的嵌套没有意义，且超过一定量（上千万层）会报错
+    middle_list =list(
+      elemet_in_middle_list = diag(3),      
+      inner_list            = list(
+         element_in_inner_list    = pi^1:4,   # 要注意的是在嵌套的时候注意代码行之间的对齐规律有助于增加可读性
+         another_element_in_inner_list = "a"
+      )
+   ),
+   element_in_main_list = log10(1:10)
+ ))
```

### 1.2 原子变量和递归变量

列表具有把其他列表包含在内的能力，因此列表被认为是**递归变量**。与之相对应矩阵和数组则是**原子变量**。

⚠️：**变量或是递归的，或是原子的，不可两者兼具。**

```R
> is.atom(list())
## [1] FALSE
> is.recursive(numeric())
## [1] FALSE
# 函数is.atom和is.recursive可以测试类型
```

### 1.3 列表的维度和算术运算

```R
# 列表也向向量一样有长度
> length(main_list)    # 不包含嵌套列表的长度
[1] 2
# 列表没有维度，会返回NULL
> dim(a_list)       
NULL
# ncol、NCOL及相应的行函数作用于列表时，与作用于矢量上的原理基本相同
> ncol(a_list)  
NULL
> NCOL(a_list)
[1] 1
> NROW(a_list)
[1] 4
> 
```

与向量不同的是，算术运算对列表不起作用。由于每个元素的类型可以不同，将两个列表相加或相乘没有任何意义。

⚠️：如果两个列表中的元素类型相同，则可以对它们进行算术运算，这种情况下，一般的算术运算都适用。

```R
> l1 <- list(1:5)
> l2 <- list(6:10)
> l1
[[1]]
[1] 1 2 3 4 5

> l2
[[1]]
[1]  6  7  8  9 10

> l1+l2           # 不能这样直接相加，会报错
Error in l1 + l2 : non-numeric argument to binary operator
> l1[[1]]+l2[[1]]
[1]  7  9 11 13 15
```

### 1.4 索引列表

与向量类似，我们可以通过方括号[]、正或负的下标数字、元素名称或逻辑索引这四种方法访问列表中的元素。

```R
> l <- list(
+   first = 1,
+   second = 2,
+    third =list(
+     alpha=3.1,
+     beta =3.2
+    )
+ )
> l[1:2]
$first
[1] 1
$second
[1] 2

> l[c("first","second")]
$first
[1] 1
$second
[1] 2

> l[c(TRUE,TRUE,FALSE)]
$first
[1] 1
$second
[1] 2
```

有时，我们要访问的是列表元素中的内容。在双方括号 `[[]]`传入正整数，它代表返回的索引下标，或指定该元素的名称字符串

```R
> l[[2]]
[1] 2
> l[["second"]]
[1] 2
```

如果输入的是一个列表，`is.list`函数将返回TRUE，否则将返回FALSE。(==这里暂不理解==)

```R
> is.list(l[1])    
[1] TRUE
> is.list(l[[1]])
[1] FALSE   
```

对于列表中的命名元素，也可以使用美元符号运算符`$`。

```R
> l$first
[1] 1
> l$f   # 部分匹配将“f”解释为“first”
[1] 1
```

可以通过嵌套方括号或传入向量来访问嵌套元素，后者不常用。

```R
> l[["third"]]["beta"]
$beta
[1] 3.2
```

⚠️：使用单方括号的索引，将返回只带一个NULL元素的列表（且名称为NA）。

```R
> l[c(4,2,5)]
$<NA>    # 不存在的元素
NULL

$second
[1] 2

$<NA>
NULL
```

如果名字错误，也会返回NULL。

```R
# 体会单双括号返回值的区别
> l[[3.1]]  # 输入的是列表元素内容，用is.list返回为FALSE
$alpha
[1] 3.1

$beta
[1] 3.2

> l[3.1]     # 输入的是一个列表，用is.list返回为TRUE
$third
$third$alpha
[1] 3.1

$third$beta
[1] 3.2
```

### 1.5 向量和列表之间的转换

向量可使用函数`as.list`函数转换成列表。所创建的可见列表与向量中元素的值一一对应：

```R
> busy_beaver <- c(1,6,21,107)
> as.list(busy_beaver)   # 使用as.list函数将向量转换为列表
```

如果列表中每个元素都是标量值，也可以使用`as.numeric`和`as.character`将其转换成向量。但如果包含非标量元素，这种方法将不起作用。

⚠️：列表可以存储不同类型的数据，也能存储相同类型的数据。

```R
> (prime_factors <- list( two=2,
+   three=3,
+   four=c(2,2),
+   five=5,
+   six=c(2,3),
+ ))
# 可以利用unlist函数将其转换为向量
> unlist(prime_factors)
  two three four1 four2  five  six1  six2 seven 
    2     3     2     2     5     2     3     7 
```

### 1.6 组合列表

c函数能用于拼接向量，也能够用于拼接列表。

```R
> c(list(a=1,b=2),list(3))  # 两个列表之间的拼接
$a
[1] 1

$b
[1] 2

[[3]]
[1] 3
# 如果用来拼接列表和向量，向量在拼接之前将被转换为列表（就好像调用了as.list函数）
> c(list(a=1,b=2),3)
$a
[1] 1

$b
[1] 2

[[3]]   # 与上例返回相同，因为向量在拼接之前被转换成了列表
[1] 3

```

也可以对列表使用`cbind`和`rbind`函数，但结果可能很奇怪。（避免使用，最好不使用！）

## 2. NULL

NULL是个特殊值，表示一个空的变量。常用于列表中，也会出现在数据框和函数参数中。

（在创建列表时，可能有元素它必须存在但没有赋值，就可以用到NULL。）

```R
> (uk_bank_holidays_2013 <- list(
+   Jan = "New Year's Day",
+   Feb = NULL,
+   Mar = "Good Friday",
+   Apr = "Easter Monday",
+   May = c("Early May Bank Holiday", "Spring Bank Holiday"),
+   Jun = NULL,
+   Jul = NULL
+ ))
$Jan
[1] "New Year's Day"

$Feb
NULL
# 省略部分返回值
```

 ⚠️：**NULL和NA是不同的，NA是一个标量值，而NULL不会占用任何空间，其长度为0。**

```R
> length(NULL)
[1] 0
> length(NA)
[1] 1
# 也可以用is.null测试变量是否为NULL值，缺失值不是NULL
> is.null(NA)
[1] FALSE
```

NULL也可用于删除列表中的元素。把元素设置为NULL（即使已经是NULL）则会删除它。

```R
# 利用NULL删除列表中元素
> (test_null_function <- list(
+   Aa = 1,
+   Bb = 2,
+   Cc = 3,
+   Dd = 4,
+   Ee = 5
+ ))
> test_null_function$Aa <- NULL  # 删除Aa=1
> test_null_function$Dd <- NULL  # 删除Dd=4
> test_null_function
$Bb
[1] 2

$Cc
[1] 3

$Ee
[1] 5
```

将现有元素设置为NULL值，不能直接分配为NULL，这样就会直接删除此元素。需要使用**`list(NULL)`**来设置。

```R
> (test_null_function <- list(
+   Aa = 1,
+   Bb = 2,
+   Cc = 3,
+   Dd = 4,
+   Ee = 5
+ ))
> test_null_function ["Cc"] <- list(NULL)
> test_null_function 
$Aa
[1] 1

$Bb
[1] 2

$Cc     #将现有的Cc元素设置为NULL
NULL

$Dd
[1] 4

$Ee
[1] 5
```

## 3. 成对列表

R有另一种形式的列表：成对列表（Pairlists）。成对列表只在内部使用，用于将参数传递到函数中（一般不会主动用到）。成对列表唯一有可能被显式调用是在使用`formals`时。该函数将返回一个函数参数的成对列表。

> **formals**: Access to and Manipulation of the Formal Arguments
>
> Get or set the formal arguments of a function.

```R
# 举例：标准差函数sd
> (arguments_of_sd <- formals(sd))
$x


$na.rm
[1] FALSE  # 默认值
> class(arguments_of_sd)
[1] "pairlist"
# 成对列表和列表的区别:
> pairlist()     # ⻓度为零的成对列表为NULL NULL
> list()         # ⻓度为零的列表为空列表 list()
```

## 4. 数据框

数据框用于存储类似电子表格的数据。它们可以被看作是每列可存储不同数据类型的矩阵或是非嵌套的列表。

### 4.1 创建数据框

使用 **`data.frame`** 函数创建数据框:

```R
> (a_data_free <- data.frame(    # data.frame创建数据框
+ x = letters[1:5],              # letters是build-in constant
+ y = rnorm(5),                  # the normal distribution 正态分布
+ z = runif(5) >0.5              # the uniform distribution 均匀分布
+ ))
x          y     z
1 a  1.6994261 FALSE
2 b  0.1527135 FALSE
3 c  1.4937160  TRUE
4 d  0.1671744 FALSE
5 e -0.7541439  TRUEna m.  
```

> 在上述例子中 **`rnorm`** 函数以及 **`runif`** 函数都是产生随机数的两个有用的函数。
> ` rnorm `函数用于生成n个平均值为0，方差为1的随机数;rrnorm(n, mean = 0, sd = 1)。
>
> ` runif` 函数用于生成n个从0到1区间范围内的随机数;runif(n, min = 0, max = 1)。

⚠️：数据框的每列的类型可与其他列不同，但在同一列表中的元素必须相同。

```R
# 在上例中，如果输入的任何向量有名称，那么行名称就取自第一个向量名称。例如y有命名，那么数据框中每行 的名字将以y列的向量命名。
> y <- rnorm(5)
> names(y) <- month.name[1:5]   # 对y进行提前命名
> data.frame(
+   x = letters[1:5],
+   y=y,
+   z = runif(5) > 0.5 
+)
 x          y     z
January  a -0.3426378  TRUE     # 每行的名字以y列的向量命名
February b  0.5431232 FALSE
March    c  2.9801914 FALSE
April    d -0.3783004 FALSE
May      e -1.1775872  TRUE
```

这种命名规则可以通过给data.frame函数传入参数 **`row.names = NULL`** 覆盖掉:

```R
> data.frame(
+   x = letters[1:5],
+   y=y,
+   z = runif(5) > 0.5,
+   row.names = NULL   # 覆盖了命名
  +)
```

数据框能和矩阵一样使用row.names，也可以使用colnames和dimnames来分别获取或置列和维度的名称。几乎 所用有用于矩阵的函数亦可用于数据框上。例如，nrow、ncol和dim函数的使用与矩阵一样。

> ⚠️：两个需要注意的地方
>
> - length将返回与ncol相同的值，而不是数据框元素的总数。
>
> -  names将返回与colnames相同的值。
>
>    (避免使用这两个函数)

可以使用不同⻓度的向量来创建数据库，只要⻓度较短的向量能刚好循环至总⻓度。从技术上讲，**所有向量⻓度的 最小公倍数必须与最⻓向量的⻓度相等。**

```R
> b_data_frame <- data.frame(
+     x = 1,      #循环4次
+     y = 2:3,    #循环2次
+     z = 4:7
+)
> b_data_frame
> b_data_frame
  x y z
1 1 2 4
2 1 3 5
3 1 2 6
4 1 3 7
```

⚠️：创建数据框的另一个要点:在默认情况下，**列名必须是唯一且有效的变量名称。**此功能可通过给data.frame 传入 **`check.names = FALSE`** 来关闭。

一般情况下使用非标准的列名并不好。复制列名更加糟糕，因为一旦使用了子集，会出现难以发生的错误。**一般情 况下，请不要关闭列名检查!**

### 4.2 索引数据框

有很多不同的方式可用于索引数据框。和矩阵索引一样，可以使用四种不同的向量索引(正整数、负整数、逻辑值
和字符)。

```R
> (a_data_frame <- data.frame(
+   x = letters[1:5],
+   y = rnorm(5),
+   z = runif(5) > 0.5
+ ))
  x           y     z
1 a  0.54428171  TRUE
2 b -0.09621382  TRUE
3 c -1.26901393 FALSE
4 d  0.89813360  TRUE
5 e -1.20816563  TRUE
# 示例
> a_data_frame[2:3, -3]   # 索引除了第3列（z列）的2～3行
  x           y
2 b -0.09621382
3 c -1.26901393
> a_data_frame[c(FALSE,TRUE,TRUE,FALSE,FALSE), c("x","y")] 
# TRUE为索引2，3行;与z的逻辑值无关
  x           y
2 b -0.09621382
3 c -1.26901393
```

如果只需要一个列，那么也可以使用列表样式的索引(带有正整数或名称的双方括号，或者带有名称的美元符号运
算符)

```R
> a_data_frame$x[2:3] # 一下3个命名都是选择a_data_frame中第一列中的第二个和第三个元素 
[1] "b" "c"
> a_data_frame[[1]][2:3]
[1] "b" "c"
> a_data_frame[["x"]][2:3]
[1] "b" "c"
```

**`subset`** 能得到一个数据框子集。`subset` 需要三个参数:数据框、一个行的条件逻辑向量、一个需要保留的名字 向量(如果该参数被忽略，将保留所有列。该函数是的提取数据框子集变的简单。

```R
> a_data_frame
  x           y     z
1 a  0.54428171  TRUE
2 b -0.09621382  TRUE
3 c -1.26901393 FALSE
4 d  0.89813360  TRUE
5 e -1.20816563  TRUE
> a_data_frame[a_data_frame$y > 0 | a_data_frame$z, "x"]  # 写法过于复杂
[1] "a" "b" "d" "e"
> subset(a_data_frame, y > 0 | z, x)     # 利用subset函数提取数据框中的数据框子集
  x
1 a
3 c 
4 d
```

### 4.3 基本数据框操作

像矩阵一样，数据框可使用t函数进行转置。在此过程中，所有的列将被转换为相同的类型，然后将变成一个矩 阵。如果两个数据框的大小一致，也可以使用 cbind 和 rbind 把它们进行连接。但要警惕，cbind不会对列名做重 复性检查，要小心使用。

```R
> (another_data_frame <- data.frame(
+  z = rlnorm(5),
+  y = sample(5),
+  x = letters[3:7]
+ ))
          z y x
1 0.9038900 1 c
2 2.9367889 5 d
3 0.2626604 2 e
4 0.6330025 4 f
5 0.7873532 3 g
> a_data_frame
  x           y     z
1 a  0.54428171  TRUE
2 b -0.09621382  TRUE
3 c -1.26901393 FALSE
4 d  0.89813360  TRUE
5 e -1.20816563  TRUE
> rbind(a_data_frame, another_data_frame)  # 用rbind将两个数据框不动连接起来
   x           y         z
1  a  0.54428171 1.0000000
2  b -0.09621382 1.0000000
3  c -1.26901393 0.0000000
4  d  0.89813360 1.0000000
5  e -1.20816563 1.0000000
6  c  1.00000000 0.9038900
7  d  5.00000000 2.9367889
8  e  2.00000000 0.2626604
9  f  4.00000000 0.6330025
10 g  3.00000000 0.7873532
> cbind(a_data_frame, another_data_frame)
# 用cbind将两个数据框不动连接起来，cbind不对列做重复性检查
  x           y     z         z y x
1 a  0.54428171  TRUE 0.9038900 1 c
2 b -0.09621382  TRUE 2.9367889 5 d
3 c -1.26901393 FALSE 0.2626604 2 e
4 d  0.89813360  TRUE 0.6330025 4 f
5 e -1.20816563  TRUE 0.7873532 3 g
# 当两个数据框有相同的列时，可以使用merge函数合并
> merge(a_data_frame, another_data_frame, by = "x")
  x        y.x   z.x       z.y y.y
1 c -1.2690139 FALSE 0.9038900   1
2 d  0.8981336  TRUE 2.9367889   5
3 e -1.2081656  TRUE 0.2626604   2
> merge(a_data_frame, another_data_frame, by = "x", all = TRUE)
  x         y.x   z.x       z.y y.y   # 指定x为我们所要包含的ID，其他merge后的列带上后缀
1 a  0.54428171  TRUE        NA  NA   # another_data_frame没有a、b行，因此NA
2 b -0.09621382  TRUE        NA  NA
3 c -1.26901393 FALSE 0.9038900   1
4 d  0.89813360  TRUE 2.9367889   5
5 e -1.20816563  TRUE 0.2626604   2
6 f          NA    NA 0.6330025   4   # a_data_frame没有f、g行，因此NA
7 g          NA    NA 0.7873532   3
# 能够合并的只有共同出现的c、d、e行
```

当merge两个数据框时，需要指定包含键值的列以作匹配。如果数据框中只包含数值，那么` colSums `和 `colMeans `函数可分别用于计算每列的总和和平均值。同样 `rowSums` 和 `rowMeans` 将计算每一行的总和及平均值。

```R
> colSums(a_data_frame[, 2:3]) # 第二个参数时维度值
        y         z 
-1.130978  4.000000 
> colMeans(a_data_frame[, 2:3])
         y          z 
-0.2261956  0.8000000 
```

## 小结

- 列表是递归变量，它可以包含其他列表
- 使用[ ]、[[ ]]以及$来索引列表
- NULL
- 数据框有类似矩阵和列表的属性，也能被索引
- merge函数能对数据框进行连接操作

## ==练习：没做==

1. 如何找到成对列表。
2. 创建数据框子集的方法。
3. 创建一个数据框，使列名既不是唯一也非有效。
4. 那个函数可以将数据框加到另一个后面。

# 第六章 环境和函数

## 1. 环境

所创建的所有变量都需要存储在某处——环境。环境本身也是另一种类型的变量，可以分配操作，并将其以参数的 形式传递到函数中。

环境和列表有相似性，大部分用于列表的语法也同样适用于环境，也能强制地把列表强制当作环境使用。一般情况下，不需要直接与环境变量打交道。

>  例如:在命令提示符下分配一个变量，它会自动进入全局环境(用户工作区)。

环境的创建不是使用 **`environment`** 函数(该函数将返回包含的特定函数的环境)，而是使用 **`new.env`** 函数。

```R
> an_environment <- new.env() # 创建环境
> an_environment[["pythag"]] <- c(12, 15, 20, 21) # 向环境中分配变量,可以使用双括号或美元符
```

如之前的 `assign` 函数有一个可选的环境参数，用于指定变量的存储位置。

```R
# 复习assign函数变量赋值
> assign(
+ "moonday",
+ weekdays(as.Date("1969/07/20")),
+ an_environment # 用于指定变量的存储位置 
+)
```

检索变量的方式：

```R
> an_environment[["pythag"]]
[1] 12 15 20 21
> an_environment$root
[1] 2+0i 3-0i
```

也可以使用`assign`的对立函数`get`来检索变量:

```R
> get("moonday",an_environment) 2 [1]"Sunday"
```

可以把环境参数传入 `ls` 和` ls.str` 函数中，列出它所有内容:

```R
> ls(envir = an_environment)
[1] "moonday" "pythag"  "root"
> ls.str(envir = an_environment)
moonday :  chr "Sunday"
pythag :  num [1:4] 12 15 20 21
root :  cplx [1:2] 2+0i 3-0i
```

可用 **`exists`** 函数测试变量是否存在环境中:

```R
> exists("pythag",an_environment) 
[1]TRUE
```

使用 `as.list` 和` as.environment` 函数能分别从环境到列表或者相反过程的转换。还可以使用**` list2env`** 函数， 它在创建环境时更为灵活。

```R
> a_list <- as.list(an_environment)   # 将环境转换为列表 
> as.environment(a_list)              # 将列表转换为环境 
<environment: 0x12a86de78>
# 效果一致
> list2env(a_list)                   # list to environment
<environment: 0x11d1faea0>
```

⚠️：所有的环境都是嵌套的，这意味着它们必须有一个父环境(除了位于顶端的特殊环境——空环境以外) 。默认情况下， **`exists`** 和 **`get`** 函数也将在父环境中寻找变量。通过给它们传入 **`inherits = FALSE`** 来改变这种行为，使它们仅在指定的环境中搜索。

```R
# 父环境(an_env)中创建nested_environmen环境
> nested_environmet <- new.env(parent = an_environment)
> exists("pythag", nested_environmet) # 测试变量"pythag"是否存在于当前环境中 (nested_env)
[1] TRUE # exists也会查找当前环境上一层的父环境即an_env，而an_en中存在变量，返回为TRUE > exists("pythag", nested_environmet, inherits = FALSE)# 改变在父环境中查找的行为
[1] FALSE
```

⚠️：在R中框“frame”这个词几乎可以与“环境”互换。

下列快捷键可以同时访问全局环境和基础环境：

> **全局环境**：从命令提示符中分配的变量的存储空间
>
> **基础环境**：R基础包中自带的基础函数和变量

```R
> non_stormers <<- c(3, 7, 8, 13, 17, 18, 21) # 对全局进行赋值
> get("non_stormers", envir=globalenv())
[1]  3  7  8 13 17 18 21
> head(ls(envir = baseenv()), 20)
 [1] "-"             "-.Date"        "-.POSIXt"      ":"             "::"            ":::"          
 [7] "!"             "!.hexmode"     "!.octmode"     "!="            "("             "["            
[13] "[.AsIs"        "[.data.frame"  "[.Date"        "[.difftime"    "[.Dlist"       "[.DLLInfoList"
[19] "[.factor"      "[.hexmode"    
```

调用函数时，函数所定义的所有变量都被存储在属于该函数的环境中。

> 函数及其环境称为**“闭包”**

## 2. 函数

### 2.1 创建和调用函数

首先来看一看函数的组成：

```R
> rt
function (n, df, ncp)   # rt函数需要3个参数
{
    if (missing(ncp))    # 如果ncp可选非中心参数被省略，将会调用C代码生成随机数并返回
        .Call(C_rt, n, df)
    else rnorm(n, ncp)/sqrt(rchisq(n, df)/df)   # 否则该函数将会调用rnorm、sqrt、rchisq函数并返回值
}
<bytecode: 0x12d5b8500>
<environment: namespace:stats>
```

在rt函数中，三个参数n、df和ncp是rt函数的**形式参数**（formal argument)。当你调用该函数并给它传递值时，这些值背称为**参数**。（差异不重要）

创建一个自己的函数，只需要向其他变量一样为它赋值。如，创建一个函数能够用计算直角三角形斜边的长度：

```R
> hypotenuse <- function(x,y)
+ { 
+   sqrt(x^2 + y^2)
+ }    # 这里函数体只有一行代码，可以省略大括号
> hypotenuse <- function(x,y) sqrt(x^2 + y^2) # 与上面相同
```

⚠️：R对空格符的使用很宽容。

调用上面创建的函数有多种方式，如：

```R
> hypotenuse(3,4)   # 不命名参数，一般R将按位置匹配它们
[1] 5
> hypotenuse(y=24, x=7)  
[1] 25
```

可以给函数提供默认值，如：

```R
> hypotenuse <- function(x = 5, y = 12)
+ { 
+   sqrt(x^2 + y^2)
+ } 
> hypotenuse <- function(x = 5, y = 12)
+ {
+   sqrt(x^2 + y^2)
+ }
> hypotenuse()
[1] 13
```

这里，复习一下`formals`函数：

> `formals`函数能取得函数的参数并返回一个成对列表，`args`函数也能做相同的事。
>
> `formalArgs`函数将返回参数名称的字符向量。
>
> ```R
> > formals(hypotenuse)
> $x
> [1] 5
> 
> $y
> [1] 12
> 
> > args(hypotenuse)
> function (x = 5, y = 12) 
> NULL
> > formalArgs(hypotenuse)
> [1] "x" "y"
> ```

`body`函数可用于返回函数体。如果，我们需要以文本的方式检查它们，比如查找一个调用了另一个函数的函数，可以使用`deparse`函数。

```R
> (body_of_hypotenuse <- body(hypotenuse))
{
    sqrt(x^2 + y^2)
}
> deparse(body_of_hypotenuse)
[1] "{"                   "    sqrt(x^2 + y^2)" "}"
```

函数形参的默认值不仅仅可以是常数，也可以是任何的R代码，甚至是其他形参。

```R
> normalize <- function(x, m = mean(x), s = sd(x))  # normalize函数将缩放一个向量
+ {
+   (x-m) / s
+ }
> normalized <- normalize(c(1, 3, 6, 10, 15))
> mean(normalized)
[1] 0
> sd(normalized)
[1] 1
# 如果normalize函数中有一些x没有给出，比如：
> normalize(c(1, 3, 6, 10, NA))
[1] NA NA NA NA NA     # 如果向量的所有元素都没有给出，在默认情况下，mean和sd都将返回NA
# 如果只有输入值是NA时，才返回NA，或许会更好，这里我们可以引入参数na.rm
```

`mean`和`sd`函数都有一个参数**`na.rm`**，能够让我们删除计算之前的任何缺失值。为了避免输入那些实际上没有被函数用到的参数名（na.rm只被传递到mean和sd中），R提供了一个特殊的参数**`...`**，它包含了所有不能被位置或名称匹配的参数。

```R
> normalize <- function(x, m=mean(x, ...), s=sd(x, ...), ...)
+ {
+   (x-m)/s
+ }
> normalize(c(1,3,6,10,NA))
[1] NA NA NA NA NA
> normalize(c(1,3,6,10,NA), na.rm=TRUE)
[1] -1.0215078 -0.5107539  0.2553770  1.2768848         NA
# 在normalize(c(1, 3, 6, 10, NA), na.rm=TRUE)中，na.rm不能匹配normalize的任何形参，因为它不是x、m、s。这意味na.rm被存储在normalize的参数...里。
```

### 2.2 向其他函数传递和接收函数

函数可以像其他变量类型一样地使用，可以将之作为其他函数的参数，并且从函数中返回。

**`do.call`**函数提供了一种调用其他函数的替代语法，可以像列表一样传递参数。`do.call`最常见的案例是与`rbind`混用，拼接多个数据框或矩阵。

```R
> do.call(hypotenuse, list(x=3, y=4))      # 和hypotenuse（3，4）一样
[1] 5
> dfr1 <- data.frame(x=1:5, y=rt(5,1))
> dfr2 <- data.frame(x=6:10, y=rf(5,1,1))
> dfr3 <- data.frame(x=11:15, y=rbeta(5,1,1))
> do.call(rbind, list(dfr1,dfr2,dfr3))     
```

把函数用作参数时，没必要一开始就为它们赋值。比如：

```R
> menage <- c(1,0,0,1,2,13,80)
> mean(menage)
[1] 13.85714
> mean(c(1,0,0,1,2,13,80))   # 简化为：
[1] 13.85714
```

我们还可以以*匿名方式*传递函数：

```R
> x_plus_y <- function(x,y) x+y
> do.call(x_plus_y, list(1:5, 5:1))
[1] 6 6 6 6 6
> # 与下面的相同
> do.call(function(x,y) x+y, list(1:5, 5:1))
[1] 6 6 6 6 6
```

返回值为函数的情况比较罕见，但是有效。

### 2.3 变量的作用域 

变量的作用域是指你在哪里可以看到此变量。

示例：

```R
> f <- function(x)
+ {
+   y <- 1
+   g <- function(x)   # g是f的子函数，f的环境是g的父环境
+   {
+     (x+y)/2
+    }
+   g(x)
+ }
> f(sqrt(5))
[1] 1.618034
# 如果g不再是f的子函数
> f <- function(x)
+ {
+   y <- 1
+   g(x)
+ }
> g <- function(x)   # g的父环境是全局环境，不包含y，因此y找不到
+ {
+   (x+y)/2
+ }
```

⚠️：变量作用域的工作方式与get和exists函数在其父环境和当前环境下搜索变量的工作方式完全相同。

```R
> h <- function(x)  # 在干净的用户工作区创建一个新函数h
+ {
+   x*y             # 只接受参数x
+ }
> h(9)
Error in h(9) : object 'y' not found   # y没有被定义，抛出报错
> y <- 16      # 把y定义在用户工作区（父环境）
> h(9)
[1] 144
# 该案例说明当R在h的环境中无法找到一个名为y的变量时，它会在h的父环境（定义了y的工作区（全局环境））搜索。
```

⚠️：**小心使用全局变量！**

```R
# 接上一案例
> h2 <- function(x)  # 再创建一个新函数h2
+ {
+    if(runif(1) > 0.5) y <- 12    # 在h2函数体内定义变量y
+    x*y
+ }
> replicate(10,h2(9))       # 使用replicate重复运行h2函数，h2和此时的“y”有一半的几率被定义为局部变量
 [1] 144 144 108 144 108 144 108 108 108 108  # 返回值随着y是局部变量还是全局变量完全随机而变化！
# 在本案例中runif函数产出的均匀分布的随机数（在0和1之间）比0.5要大时，局部变量y的值被赋值为12，否则将使用全局值16
```

### *2.4 R中常见的一些分布函数

|                 函数                 |         分布         |
| :----------------------------------: | :------------------: |
|     **`rnorm(n, mean=0, sd=1)`**     | **正态（高斯）分布** |
|           `rep(n, rate=1)`           |         指数         |
|     `rgamma(n, shape, scale=1)`      |        γ分布         |
|        **`rpois(n, lamba)`**         |   **Poisson分布**    |
|    `rweibull(n, shape, scale=1)`     |    *Weibull*分布     |
|  `rcauchy(n, location=0, scale=1)`   |     *Cauchy*分布     |
|      `rbeta(n, shape1, shape2)`      |        β分布         |
|           **`rt(n, df)`**            |      **t分布**       |
|        **`rf(n, df1, df2)`**         |      **F分布**       |
|         **`rchisq(n, df)`**          |     **卡方分布**     |
|     **`rbinom(n, size, prob)`**      |     **二项分布**     |
|           `rgeom(n, prob)`           |       几何分布       |
|        `rhyper(nn, m, n, k)`         |      超几何分布      |
| **`rlogis(n, location=0, scale=1)`** |   **logistic分布**   |
|   `rlnorm(n, meaning=0, sdlog=1)`    |       对数正态       |
|      `rnbinorm(n, size, prob)`       |      负二项分布      |
|     **`runif(n, min=0, max=1)`**     |     **均匀分布**     |

## 小结

- new.env函数能创建环境；环境能存储变量
- 空环境；父环境
- 函数由形参和函数体组成
- R将在当前环境及其父环境中寻找变量

## ==练习：没做==

1. 

# 第七章 字符串和因子

## 1. 字符串

因子用于存储类别数据，如性别（男或女），它提供有限的字符串选项。文本数据存储在字符向量中（或字符数组中）。字符向量中的每个元素都是字符串，而非单独的字符。（在R中字符串是非正式用语，实际上为“字符向量元素”）。文本的基本单位是字符向量，意味着大部分处理字符串处理函数也能用于字符串向量，与数学运算的向量化方式相同。

### 1.1 创建和打印字符串

- 可以使用单引号或双引号把字符串引用起来，只要引号之间匹配就好（双引号更加标准）。

- 字符向量可用`c`函数创建。

  ```R
  > c(
  +   "How are you?"
  + )
  [1] "How are you?"
  ```

`paste`函数能将不同的字符串组合起来。

```R
> paste(c("red", "yellow"), "lorry")
[1] "red lorry"    "yellow lorry"
> # 使用参数sep可以更改分隔符
> paste(c("red", "yellow"), "lorry", sep="-")
[1] "red-lorry"    "yellow-lorry"
> # 所有的字符串被组合后，可以使用collapse参数把结果收缩成一个包含所有元素的字符串
> paste(c("red", "yellow"), "lorry", collapse=",")
[1] "red lorry,yellow lorry"
> paste0(c("red", "yellow"), "lorry")
[1] "redlorry"    "yellowlorry"
```

`toString`函数是`paste`的变种，用于打印向量。`toString`使用逗号和空格分隔每个元素，可以限制打印的数量。

```R
> x <- (1:15)^2
> toString(x)
[1] "1, 4, 9, 16, 25, 36, 49, 64, 81, 100, 121, 144, 169, 196, 225"
> toString(x, width=40)   # width参数将输出限制为40个字符
[1] "1, 4, 9, 16, 25, 36, 49, 64, 81, 100...."    
```

`cat`函数使用的少：

```R
> cat(c("red", "yellow"), "lorry")
red yellow lorry
```

通常当字符串打印到控制台时，它们会以双引号括起来。如果对他们使用`noquote`函数，可以去掉这些引号。

```R
> x <- c(
+   "I", "saw", "a", "pig"
+ )
> y <- noquote(x)
> x
[1] "I"   "saw" "a"   "pig"
> y
[1] I   saw a   pig     # 去掉引号使得文本更具可读性
```

### 1.2 格式化数字

下面这些函数可用于数字的格式化：

`formatC`可让你使用C语言的格式化风格来指定使用固定型或科学型的格式、小数的位数以及输出的宽度。无论是哪个选项，输入都应该是`numeric`类型（包括数组），且输出的`character`字符向量或数组。

```R
> pow <- 1:3
> (powers_of_e <- exp(pow))
[1]  2.718282  7.389056 20.085537
> formatC(powers_of_e)
[1] "2.718" "7.389" "20.09"
> formatC(powers_of_e, digits=3)  # 指定三个数字
[1] "2.72" "7.39" "20.1"
> formatC(powers_of_e, digits=3, width=10) # 前面加一个空格
[1] "      2.72" "      7.39" "      20.1"
> formatC(powers_of_e, digits=3, format="e")  # 科学格式
[1] "2.718e+00" "7.389e+00" "2.009e+01"
> formatC(powers_of_e, digits=3, flag="+")
[1] "+2.72" "+7.39" "+20.1"
```

R还提供了更通用的C风格的格式化函数**`sprintf`**。

⚠️：R中大部分的数值是浮点值而非整数。`sprintf`的第一个参数指定了一个格式化字符串，其中包括其他值的占位符。

**%s**代表另一个字符串，**%f**和**%e**分别代表固定型格式和科学型格式的浮点数，**%d**表示整数。

```R
> sprintf("%s %d = %f", "Euler's constant to the power", pow, powers_of_e)
[1] "Euler's constant to the power 1 = 2.718282" 
[2] "Euler's constant to the power 2 = 7.389056" 
[3] "Euler's constant to the power 3 = 20.085537"
```

其他格式化数字的方法有`format`（和formatC类似）和`prettyNum`(适合非常大或非常小的数字）这两个函数

```R
> format(powers_of_e)
[1] " 2.718282" " 7.389056" "20.085537"
> format(powers_of_e, digits=3)
[1] " 2.72" " 7.39" "20.09"
> format(powers_of_e, digits=3, trim=TRUE)
[1] "2.72"  "7.39"  "20.09"
> format(powers_of_e,digits=3, scientific=TRUE)
[1] "2.72e+00" "7.39e+00" "2.01e+01"
```

```R
> prettyNum(
+  c(1e10, 1e-20), big.mark=",", small.mark=" ", preserve.width="individual", scientific= FALSE)
[1] "10,000,000,000"            "0.00000 00000 00000 00001"
```

### 1.3 特殊字符

**"\t"**

```R
> cat("foo\tbar", fill=TRUE)   # 用cat而不用print，是因为print会将\t执行为"\t"
foo	bar                        # cat的参数fill=TRUE使光标在一行结束后移动到下一行
```

**"\n"**

```R
> cat("foo\nbar", fill=TRUE)
foo
bar
```

"\0"在R内部用于终止字符串；打印反斜杠需要连续输入两个反斜杠（同perl。

字符串中使用双引号：

```R
> cat("foo\"bar", fill=TRUE)  # 要加反斜杠来转义
foo"bar
```

```R
> cat("foo'bar", fill=TRUE)
foo'bar
> cat('foo"bar', fill=TRUE)
foo"bar
```

此外：通过打印报警符\a 能让电脑发出beep（alarm函数也可以）。[可以用于分析任务结束后主动通知]

用法：

```R
cat("\a")
alarm()
```

### 1.4 更改大小写

`toupper`和`tolower`函数能把字符串中的字符全部转换为大写或小写：

```R
> toupper("I'm Shouting")
[1] "I'M SHOUTING"
> tolower("I'm Whispering")
[1] "i'm whispering
```

### 1.5 截取字符串

有两个函数可用于从字符串中截取子字符串：`substring`和`substr`。

> 区别：
>
> - substring：输出长度与最长输入一样；
> - substr：输出长度只和第一个输入相等；==# 不明白怎么截取的==

```R
> test <- c(
+   "AAA BBB CCC DDD EEE",        # AAA_BB
+   "FFF GGG HH F MMMM N",        #  FF_GG
+   "aa bbb c ddddd eeee ff",     #   _bbb
+   "1234 5678 90",               #    4_5
+   "cccCCCCCCcccccc"
+ )  
> substring(test, 1:5,6)
[1] "AAA BB" "FF GG"  " bbb"   "4 5"    "CC"    
> substr(test, 1:5, 6)
[1] "AAA BB" "FF GG"  " bbb"   "4 5"    "CC"   
```

### 1.6 分割字符串

与`paste`相反的是**`strsplit`**函数，可以将字符串切割。

```R
> woodchuck <- c(
+  "How much wood would a woodchuk chuck",
+  "If a woodchuck could chuck wood?",
+  "He would chuck, he would, as much as he could",
+  "And chuck as much wood as a woodchuck would",
+  "If a woodchuck could chuck wood."
+ )
> strsplit(woodchuck, " ", fixed=TRUE)
[[1]]
[1] "How"      "much"     "wood"     "would"    "a"        "woodchuk" "chuck"   

[[2]]
[1] "If"        "a"         "woodchuck" "could"     "chuck"     "wood?"    

[[3]]
 [1] "He"     "would"  "chuck," "he"     "would," "as"     "much"   "as"     "he"     "could" 

[[4]]
[1] "And"       "chuck"     "as"        "much"      "wood"      "as"        "a"        
[8] "woodchuck" "would"    

[[5]]
[1] "If"        "a"         "woodchuck" "could"     "chuck"     "wood." 
```

⚠️：`strplit`返回的是列表（而不是字符向量或矩阵），因为他的结果是由不同的字符向量组成。

某些词最后的逗号有些烦人，最好的方法是在空格分割符后加一个可选的逗号，使用正则表达式很容易搞定：

`strsplit(woodchuck, ",?")`

### 1.7 文件路径

**R有一个工作目录，默认为文件被读写的地方**，可以使用**`getwd`**查看它的位置，并使用**`setwed`**来改变它。

```
> getwd()
[1] "/Users/username" # 为了保持可移植性，在R中你可以始终对路径使用正斜杠
```

可以使用**`file.path`**来从各个目录中创建文件路径（会在目录名称之间插入正斜杠）。

```R
> file.path("Users", "username", "R", "R-devel", "test2022")
[1] "Users/username/R/R-devel/test2022"
```

`R.home()`显示R的安装目录：

```R
> R.home()
[1] "/Library/Frameworks/R.framework/Resources"
```

路径分绝对路径和相对目录。在相对目录中：

> 当前目录：`.`
>
> 夫目录：`..`
>
> 用户主目录：`~`

**`path.expand`**能将相对路径转换为绝对路径：

```R
> path.expand(".")
[1] "."
> path.expand("..")
[1] ".."
> path.expand("~")
[1] "/Users/liupeiyao"
```

**`basename`**只返回文件名，而不包括前面的目录位置；**`dirname`**只返回文件的目录：

```R
> file2022test <- "Users/username/R/R-devel/test2022"
> basename(file2022test)
[1] "test2022"
> dirname(file2022test)
[1] "Users/username/R/R-devel"
```



## 2. 因子

因子是一个用于存储类别变量的特殊的变量类型。

当你用一列文本数据创建数据框时，R将文本默认为类别数据并进行转换。

### 2.1 创建因子

```R
> (heights <- data.frame(
+   height_cm =c(153, 180, 181, 182, 185, 167, 156, 171, 172, 176),
+   gender =c("F", "M", "M", "M", "F", "M", "F", "M", "F", "M")
+ ))
   height_cm gender
1        153      F
2        180      M
3        181      M
4        182      M
5        185      F
6        167      M
7        156      F
8        171      M
9        172      F
10       176      M
> # 检查gender一列的类
> class(heights$gender)
[1] "character"    # 这里2013《learning R》教程中说应该是factor，问题不大可以使用as.函数更该类
# v4.0.0后data.frame的默认函数stringsAsFactors=TRUE变为FALSE产生了上面的问题
> (heights <- data.frame(
+   height_cm =c(153, 180, 181, 182, 185, 167, 156, 171, 172, 176),
+   gender =c("famale", "male", "male", "male", "male", "male", "male", "male", "male", "male"),
+   stringsAsFactors = TRUE)   # 将这个默认参数改为TRUE
+   )
> class(heights$gender)
[1] "factor"
```

因子中的每个值都是一个字符串，在上面的例子中，它们被限制为“famale“、”male“、或缺失值。如果把不同的字符串添加到genders中，约束就会变得很明显。

```R
> heights$gender[1] <- "Female"
Warning message:
In `[<-.factor`(`*tmp*`, 1, value = c(NA, 2L, 2L, 2L, 2L, 2L, 2L,  :
  invalid factor level, NA generated
> heights$gender
 [1] <NA> male male male male male male male male male
Levels: famale male
```

选项“female”和“male”被称为因子水平，它能用`levels`函数查询到，水平的级数可由`nlevel`函数查询到：

```R
> levels(heights$gender)
[1] "famale" "male"  
> nlevels(heights$gender)
[1] 2
```

除了使用数据框在内部自动创建因子之外，也可以使用**`factor`**函数创建它。`factor`函数的第一个参数 （唯一强制）是一个字符向量。

```R
> gender_char <- c(
+   "female", "male", "female", "male", "male",
+   "female", "female", "male", "male", "female"
+ )
> (gender_fac <- factor(gender_char))   
 [1] female male   female male   male   female female male   male   female
Levels: female male
```

### 2.2 更改因子水平

可以通过指定levels参数来更改因子被创建时水平的先后顺序：

```R
> factor(gender_char, levels = c("male", "female"))
 [1] female male   female male   male   female female male   male   female
Levels: male female
> # 如果想在因子创建之后再改变因子水平的顺序，就再次使用factor函数，这时它的参数是当前的因子（而不是字符向量）
> factor(gender_fac, levels = c("male", "female"))
 [1] female male   female male   male   female female male   male   female
Levels: male female
```

⚠️：不能使用levels函数直接改变因子的水平值。（往往更改数据的做法不是被提倡的）

例如：

```R
> levels(gender_fac) <- c("male", "female")
> gender_fac
 [1] male   female male   female female male   male   female female male    # 可以看见数据被直接更改了
Levels: male female
```

`relevel`函数是另一种改变因子水平顺序的方法。（用的少，使用`factor`函数设置水平值更方便）

`relevel(gender_fac, "male")`

### 2.3 去掉因子水平

在数据集清理的过程中，最终你可能需要去掉所有与因子水平对应的数据。

```R
> getting_to_work <- data.frame(
+  mode = c(
+    "bike", "car", "bus", "car", "walk",
+    "bike", "car", "bike", "car", "car"
+ ),
+   time_mins=c(25, 13, NA, 22, 65, 28, 15, 24, NA, 14)
+ ）
# 可以看到并非每次都有记录，需要去掉那些time_mins的NA行
> (getting_to_work <- subset(getting_to_work, !is.na(time_mins)))
   mode time_mins
1  bike        25
2   car        13
4   car        22
5  walk        65
6  bike        28
7   car        15
8  bike        24
10  car        14
> unique(getting_to_work$mode)
[1] "bike" "car"  "walk"  # 因子水平是four（这里没有像教材一样显示levels，原因可能是stringsAsFactor=TRUE
  # mode一列只有3个值，但因子水平是4
  # 要删除未使用的水平因子，我们可以使用droplevels函数（接受因子或数据框作参数）
  # 对于数据框来说，函数droplevels它会丢弃输入因子中所有未使用的水平
> getting_to_work$mode <- droplevels(getting_to_work$mode)
Error in UseMethod("droplevels") :    # 本来上下两个应该是等价的，这里可能是因为v.4.0.0中dataframe参数默认值发生版本更新的原因出现了报错
  no applicable method for 'droplevels' applied to an object of class "character"
> getting_to_work <- droplevels(getting_to_work
```

### 2.4 有序因子

有些因子的水平在语义上大于或小于其他水平。举例：

> 问题：你有多快乐？
>
> 回答包括："depressed"、"grumpy"、"so-so"、"cheery"、"ecstatic"。
>
> 结果是类别变量，因此可以创建一个拥有五个选项的因子。

```R
# 在此使用sample函数来产生10000个随机回复
> happy_choices <- c("depressed", "grumpy", "so-so", "cheery", "ecstatic") # 字符向量
> happy_value <- sample(      # 字符向量
+   happy_choices,
+   10000,
+   replace = TRUE)
> happy_fac <- factor(happy_value, happy_choices)   # factor函数的第一个参数是一个字符向量
> head(happy_fac)
[1] cheery    grumpy    grumpy    depressed so-so     cheery   
Levels: depressed grumpy so-so cheery ecstatic
# 在本例中，对于调查者来说，五个选项是有顺序的，最好把回复存储在一个按顺序排列的因子中：ordered函数
> happy_ord <- ordered(happy_value, happy_choices)
> head(happy_ord)
[1] cheery    grumpy    grumpy    depressed so-so     cheery   
Levels: depressed < grumpy < so-so < cheery < ecstatic
> # 也可以通过给factor传入order = TRUE实现这个功能
> # 有序的因子还是因子，一般的因子不一定有序
> is.factor(happy_ord)
[1] TRUE
> is.ordered(happy_fac)
[1] FALSE
```

有序因子在分析调查数据时，比较有用。

### 2.5 将连续变量转换为类别变量

一个汇总数值变量的方法是计算有多少个值落入不同的“组”中，**`cut`**函数能将数值变量切成不同的快，然后返回一个因子。它通常使用**`table`**函数得到每组数字的总和。（`hist`函数能画出直方图，也可以实现`table`的这一功能）

```R
> ages <- 16 + 50*rbeta(10000, 2, 3)    # 使用Beta分布随机生成10000名工人的年龄数据，从16到60; 
# 请注意：ages是一个数字变量
> class(ages)
[1] "numeric"
> grouped_ages <- cut(ages, seq.int(16, 66, 10))  # 将他们按10年分组
# group_ages是一个因子
> class(grouped_ages)
[1] "factor"
> head(grouped_ages)
[1] (16,26] (26,36] (26,36] (16,26] (36,46] (46,56]
Levels: (16,26] (26,36] (36,46] (46,56] (56,66
> table(grouped_ages)     # 利用table函数得到每组数字的总和
grouped_ages
(16,26] (26,36] (36,46] (46,56] (56,66] 
   1773    3430    2964    1548     285 # 大部分工人的年龄分布于26到46之间，符合Beta分布结果                      
```

### 2.6 将类别变量转换为连续变量

上一小节我们将连续变量转换为了类别变量，相反的可以将类别变量转换成为数值变量。（应用：清理脏数据）

举例：

```R
> dirty <- data.frame(x = c("1.23", "4..56", "7.89"))  # 想把x列转换为数字
> as.numeric(dirty$x)   # 调用as.numeric
[1] 1.23   NA 7.89
Warning message:
NAs introduced by coercion 
> # 因为一个数字中有两个小数点，产生了warning
> class(dirty$x)
[1] "character"   # 这里因为data.frame在R v.4.0.0后版本中默认参数stringAsFactor默认值改变，x列直接为字符向量，不再需要像《learning R（2013）》中将factor转换为character再进行as.numeric
```

### 2.7 生成因子水平

为了平衡数据，使到在每个水平上的数据点的数目相同，可用**`gl`**函数来生成因子。

形式：【要生成因子的水平数（整型参数），水平需要的重复次数】

为每个水平命名，可以通过`label`参数传入一个字符向量来实现。可以通过传入`length`参数创建更复杂的水平排序。

```R
> gl(3, 2)
[1] 1 1 2 2 3 3
Levels: 1 2 3
> gl(3, 2, labels =c("placebo", "drugA", "drugB"))
[1] placebo placebo drugA   drugA   drugB   drugB  
Levels: placebo drugA drugB
> gl(3, 1, 6, labels = c("placebo", "drugA", "drugB"))   # 传入length参数，产生交替
[1] placebo drugA   drugB   placebo drugA   drugB  
Levels: placebo drugA drugB
```

### 2.8 合并因子

如果有多个类别变量，有时需要把它们合并成一个单一的因子，其中<u>每个水平由每个变量之间的交叉合并组成</u>（**`interaction`**函数）。

```R
> treatment <- gl(3, 2, labels = c("placebl", "drug A", "drug B"))
> gender <- gl(2, 1, 6, labels = c("female", "male"))
> treatment
[1] placebl placebl drug A  drug A  drug B  drug B 
Levels: placebl drug A drug B
> gender
[1] female male   female male   female male  
Levels: female male
> interaction(treatment, gender) # 使用interaction函数将多个变量合并
[1] placebl.female placebl.male   drug A.female  drug A.male    drug B.female  drug B.male   
6 Levels: placebl.female drug A.female drug B.female placebl.male ... drug B.male
```

## 小结

- paste及其衍生函数能将字符串连接起来
- 类别数据被存储在因子或有序因子中
- 因子中每个可能的类别被称为一个level
- 连续变量可以被cut函数转换 成类别变量

## ==练习：没做==



# 第八章 流程控制和循环

⚠️：R具有矢量化的性质，循语句在R中的运用不如预期广泛。

## 1. 流程控制

执行代码——> 执行流程（满足哪些条件）

### 1.1 if 和else

if接受一个长度为1的逻辑向量作为参数，且当该值为TRUE时才会执行下一条语句：

```R
> if(TRUE)message("It was true!")
It was true!
> if(FALSE)message("It wasn't true!") # 只有逻辑值为TRUE时才执行
```

⚠️：**if的条件中不允许缺失值！**

```R
> if(NA)message("Who knows?")
Error in if (NA) message("Who knows?") : 
  missing value where TRUE/FALSE needed
```

大部分时候欧不会直接输入**TRUE**或**FALSE**，而是传递一个变量或表达式。

```R
> if(runif(1) > 0.5)message("This massage appears with a 50% chance")
> if(runif(1) > 0.5)message("This massage appears with a 50% chance") # 再执行一次！
This massage appears with a 50% chance
```

如果条件中可能会出现缺失值，可以先用`is.na`测试一下：

```R
> if(is.na(NA))message("The value is missing")  # NA is na 为TRUE
The value is missing
```

如果需要有条件地执行多个语句，借助大括号：

```R
> x <- 3
> if(x > 2)
+ {
+   y <- 2 * x
+   z <- 3 * y
+ }
```

💡：建议将条件执行语句（即使只有一个）都用大括号括起来，使代码更具有可读性。

如果if的条件值为FALSE，则会执行else之后的代码:

```R
> if(FALSE)
+ {message("This won't excute...")}else  # 注意这里的else位置
+ {message("but this will!")}
but this will
```

⚠️：else必须和if语句的右边大括号在同一行，否则会出错。

⚠️：if和else是两个独立的词，可以反复用来定义多个条件。

```R
> (r <- round(rnorm(2),1))  # round是舍入函数，此时digits参数等于1
[1] -2.4  1.3
> (x <- r[1]/r[2])          # 注意这里的表达方式，-1.3是r的[2]
[1] -1.846154
> if(is.nan(x))             # nan:not a number
+ {message("x is missing")}else
+ if(x > 0)
+ {message("x is positve")}else
+ if(x < 0)
+ {message("x is negative")}else
+ {message("x is zero")}
x is negative
```

与其他语言不同，R可以对代码重新排序来完成条件赋值:

```r
> x <- sqrt(-1 + 0i)
> (reality <- if(Re(x) ==0)"real" else "imaginary")
```

在上例中**`Re`**返回复数实部；**`Im`**返回复数虚部。

### 1.2 矢量化的if

⚠️：不要给if传递长度超过1的逻辑向量。

**`ifelse`**函数有3个参数：

> ifelse的参数：
>
> - 第一个：逻辑条件向量
> - 第二个：参数值在第一个向量为TRUE时被返回
> - 第三个：参数值在第一个向量为FALSE时被返回

案例：掷硬币过程

```R
> ifelse(rbinom(10, 1, 0.5), "Head", "Tail")   # rbinom二项分布
 [1] "Tail" "Head" "Head" "Tail" "Tail" "Head" "Tail" "Tail" "Head" "Tail"
```

`ifelse`也可以在第二个或者第三个参数中接受向量，它们应该与第一个向量的长度相等（如果不等，那么第二个和第三个参数中的元素将被重复或忽略，以使得它们与第一个参数的长度相同）

```R
> (yn <- rep.int(c(TRUE, FALSE), 6)) # 重复
 [1]  TRUE FALSE  TRUE FALSE  TRUE FALSE  TRUE FALSE  TRUE FALSE  TRUE FALSE
> ifelse(yn, 1:3, -1:-12)
 [1]   1  -2   3  -4   2  -6   1  -8   3 -10   2 -12
```

**如果条件参数中有缺失值，那么结果中的相应位置也是缺失值**：

```R
> yn[c(3, 6, 9, 12)] <- NA  # 表示在yn的3，6，9，12位置替换为NA
> yn
 [1]  TRUE FALSE    NA FALSE  TRUE    NA  TRUE FALSE    NA FALSE  TRUE    NA
> ifelse(yn, 1:3, -1:-12)
 [1]   1  -2  NA  -4   2  NA   1  -8  NA -10   2  NA
```

### 1.3 多个分支

包含太多else语句就会降低代码的可读性。这时我们可以使用**`switch`**函数。

>switch函数的用法：
>
>- 第一个参数：返回字符串的表达式
>- 其后的参数：与第一个参数相匹配时的返回值
>- 匹配参数必须和第一个参数完全一样

```R
> (greek <- switch(
+   "gamma",
+   alpha = 1,
+   beta = sqrt(4),
+   gamma = 
+   { a <- sin(pi/3)
+     4 * a ^ 2 }
+ ))
[1] 3
# 如果找不到任何匹配的名字，那么switch将（隐式地）返回NULL：
> (greek <- switch(
+   "delta",
+   alpha = 1,
+   beta = sqrt(4),
+   gamma = 
+   { a <- sin(pi/3)
+     4 * a ^ 2
+ }
+ ))
NULL
# 对于这种情况，可以在没有其他选择的情况下提供一个没有命名的参数：
> (greek <- switch(
+   "delta",
+   alpha = 1,
+   beta = sqrt(4),
+   gamma = 
+   { a <- sin(pi/3)
+     4 * a ^ 2
+ },
+  4
+ ))
[1] 4
```

`switch`的第一个参数也可以是一个整数。（这种情况下，其余参数不需要名字）

举例：如果第一个参数结果是1，将返回第二个参数的结果；如果第一个参数的结果是2，则返回第三个参数的结果，以此类推：

```R
> switch(
+  3,
+  "first",
+  "second",
+  "third",
+  "fourth"
+ )
[1] "third"
```

如果要测试的整数非常大，需要提供很多参数，将会非常麻烦！这时最好是把第一个参数转换为字符串，使用第一种`switch`语法。

```R
> switch(
+  as.character(2027737937743),
+  "2027737937743" = "a big number",
+  "another number"
+ )
[1] "a big number
```

## 2. 循环

在R中有三种循环：repeat、while和for。

### 2.1 repeat循环

**`repeat`**: 反复执行代码，直到告诉它终止。先执行代码，再检查循环是否应该结束。

举例：

```R
> repeat
+ {message("Happy Groundhog Day！")} # 如果不按下Escape键或者退出R，这个代码能运行到世界末日
```

因此为了终止代码，我们需要插入一个**`break`**语句跳出无限循环。

```R
> repeat
+ {
+    message("Happy Groundhog Day!")
+   action <- sample(
+    c(
+       "Learn French",
+       "Make an ice statue",
+       "Rob a bank",
+       "Win heart of Andie McDowell"
+      ),
+     1,
+    )
+     message("action = ", action)
+     if(action == "Win heart of Andie McDowell")break
+ }
```

有时候，我们不是要退出整个循环，而是跳过当前的迭代，开始next下一次迭代而已：# 注意理解

```R
> repeat
+  {
+   message("Happy Groundhog Day!")
+   action <- sample(
+     c(
+        "Learn French",
+        "Make an ice statue",
+        "Rob a bank",
+        "Win heart of Andie McDowell"
+      ),
+      1
+      )
+     if(action == "Rob a bank")
+     {
+      message("Quietly skipping to the next iteration")
+      next
+      }
+      message("action=", action)
+      if(action == "Win heart of Andie McDowell")break
+ }
Happy Groundhog Day!
action=Make an ice statue
Happy Groundhog Day!
action=Make an ice statue
Happy Groundhog Day!
action=Learn French
Happy Groundhog Day!
action=Win heart of Andie McDowell
```

### 2.2 while循环

while循环特点：先进行检查在（可能）执行代码。检查发生在开始，循环体有可能不被执行。

```R
> action <- sample(       # sample函数抽样
+   c(
+      "Play the piano",
+      "Cook meals",
+      "Go Hiking",
+      "Watch movies",
+      "Test"
+    ),
+     1             # sample函数的参数，抽1次样
+ )
> while(action != "Test")
+ { 
+   message("Happy!")
+   action <- sample(
+     c(
+        "Play the piano",
+        "Cook meals",
+        "Go hiking",
+        "Watch movies",
+        "Test"
+       ),
+        1
+    )
+ message("action = ", action)
+ }
Happy!
action = Cook meals
Happy!
action = Play the piano
Happy!
action = Go hiking
Happy!
action = Watch movies
Happy!
action = Cook meals
Happy!
action = Cook meals
Happy!
action = Test   # 循环截止
```

如果知道循环体必须至少执行一次，使用repeat函数，否则使用while函数。

### 2.3 for循环

for循环适用于<u>已知代码所需执行的循环次数</u>的情形。for循环将接受一个**迭代器变量**和一个向量参数。在每个循环中，迭代器变量会从向量中取一个值。

```R
> for(i in 1:5)message("i=", i)
i=1
i=2
i=3
i=4
i=5
```

如果想要执行多个表达式，与其他循环一样，须要使用大括号把它们括起来：

```R
> for(i in 1:5)
+ {j <- i^2
+  message("j=", j)
+ }
j=1
j=4
j=9
j=16
j=25
```

R的for循环非常灵活，它们的输入不限于整数或数字，还可以传入字符向量、逻辑向量或列表：

```R
# 案例一:for循环输入传入字符向量
> for(month in month.name)
+ {
+   message("The month of ", month)
+ }
The month of January
The month of February
The month of March
The month of April
The month of May
The month of June
The month of July
The month of August
The month of September
The month of October
The month of November
The month of December
# 案例二：for循环输入传入逻辑向量
> for(yn in c(TRUE, FALSE, NA))
+ {
+   message("This statement is ", yn)
+ }
This statement is TRUE
This statement is FALSE
This statement is NA
# 案例三：for循环输入传入列表
> l <- list(
+  pi,
+  LETTERS[1:5],
+  charToRaw("not as complicated as it looks"),
+  list(
+    TRUE
+   )
+ )
> for(i in l)
+ {
+   print(i)
+ }
[1] 3.141593
[1] "A" "B" "C" "D" "E"
 [1] 6e 6f 74 20 61 73 20 63 6f 6d 70 6c 69 63 61 74 65 64 20 61 73 20 69 74 20 6c 6f 6f 6b 73
[[1]]
[1] TRUE

```

for循环操作于向量中的每个元素，提供了一种“伪向量化。

## 小结

- if和else：条件执行语句
- ifelse是if和else所对应的向量化函数
- R中的三种基本循环：repeat、while，for

## ==练习：没做==

# 第九章 高级循环

R能把函数应用于向量、列表或数组中的每个元素中。

> - 如何把函数应用到列表或向量的每一个元素中，或矩阵的每一行或列上。
> - 如何解决拆分-应用-合并的问题
> - 使用plyr包

## 1. replication

`rep`函数可以把输入的参数重复数次；`replicate`能调用表达式数次。

大多数情况两者差不多，只有当使用随机数的时候才不一样。

举例：生成均匀分布随机数的`runif`函数不是矢量化的，`rep`函数每次重复相同的随机数，`replicate`每次结果不同

```R
# 代码示例：rep和replicate的区别
> rep(runif(1), 5)
[1] 0.9553805 0.9553805 0.9553805 0.9553805 0.9553805
> replicate(5, runif(1))
[1] 0.70680522 0.56068789 0.45249148 0.93237508 0.01668097
```

在一些案例中，`replicate`函数有非常重要的作用。比如蒙特卡洛分析（Monte Carlo）：需要重复固定次数的分析。

> **蒙特卡洛方法（Monte Carlo method）**
>
> -  又被称为**”统计模拟方法“**，当所求解问题是某种随机事件出现的概率，或者是某个随机变量的期望值时，通过某种“实验”的方法，以这种事件出现的频率估计这一随机事件的概率，或者得到这个随机变量的某些数字特征，并将其作为问题的解。
>
> - 蒙特卡罗方法的解题过程可以归结为三个主要步骤：构造或描述概率过程；实现从已知概率分布抽样；建立各种估计量。

```R
# 示例代码：分析某人上下班使用不同交通工具所花费的时间
> time_for_commute <- function()      # 定义一个函数
+ {
+   mode_of_transport <- sample(      # sample函数随机抽样
+     c("car", "bus", "train", "bike"),
+     size = 1,                        # size是样本抽取次数
+     prob = c(0.1, 0.2, 0.3, 0.4)     # 抽样向量中元素被抽到的可能性
+    )
+   time <- switch(                    # switch函数，第一个参数传入值，其后的参数与第一个参数保持一致
+     mode_of_transport,
+     car = rlnorm(1, log(30), 0.5),    # 各交通工具时长符合的分布规律
+     bus = rlnorm(1, log(40), 0.5),
+     train = rnorm(1, 30, 10),
+     bike = rnorm(1, 60, 5),
+    ，
+    names(time) <- mode_of_transport    # names函数命名
+    time
+ }
> replicate(5, time_for_commute())
     car      bus     bike     bike     bike 
25.66187 25.63823 59.17297 57.81482 59.80736 
```



## 2. 遍历列表

向量化在R中无所不在。apply系列的函数能够使得代码更加的“伪矢量化”。

**lapply**

`lapply`的输入参数是某个函数，这个函数将依次作用于列表中的每个元素上，并将结果返回到一个列表中。

> **矢量化编程**：是一种提高算法速度的有效方式，是尽量使用被高度优化的数值运算操作来实现学习算法，避免for循环，尽量使用矩阵运算来代替。
>
> 优点：简化代码、运行更快。

```R
> prime_factors <- list(
+  two = 2,
+  three = 3,
+  four = c(2, 2),
+  five = 5,
+  six = c(2, 3),
+  seven = 7,
+  eight = c(2, 2, 2),
+  nine = c(3, 3),
+  ten = c(2, 5)
+ )
> head(prime_factors)
$two
[1] 2

$three
[1] 3

$four
[1] 2 2

$five
[1] 5

$six
[1] 2 3

$seven
[1] 7
# 可以写一个for循环，在每个列表元素中搜索唯一值
> unique_primes <- vector("list", length(prime_factors))# vector函数创建长度为5，类型为list的矢量
> for(i in seq_along(prime_factors))      # seq_along函数指定序列，生成一组列表
+ {
+   unique_primes[[i]] <- unique(prime_factors[[i]])  # 思考：为什么这里是双层括号？两层
+ }
> names(unique_primes) <- names(prime_factors)
> unique_primes
$two
[1] 2

$three
[1] 3

$four     # unique，4有两个相同的因子
[1] 2

$five
[1] 5

$six
[1] 2 3

$seven
[1] 7

$eight
[1] 2

$nine
[1] 3

$ten
[1] 2 5
# 使用lapply简化操作
> lapply(prime_factors, unique)
$two
[1] 2

$three
[1] 3

$four
[1] 2

$five
[1] 5

$six
[1] 2 3

$seven
[1] 7

$eight
[1] 2

$nine
[1] 3

$ten
[1] 2 5
```

> **`unique`**：返回一个把重复元素或行给删除的向量、数据框或数组。
>
> ```R
> > (non_unique_matrix <- matrix(
> +   c(1, 1, 1, 1, 2, 2, 3, 2, 3, 4, 5, 3),
> +   nrow = 4))
>      [,1] [,2] [,3]
> [1,]    1    2    3
> [2,]    1    2    4
> [3,]    1    3    5
> [4,]    1    2    3    # 不unique
> > unique(non_unique_matrix)
>      [,1] [,2] [,3]
> [1,]    1    2    3
> [2,]    1    2    4
> [3,]    1    3    5
> ```

**vapply**

应用于列表返回向量（a2v）。第三个参数是返回值的模板，结果简化为向量或数组。

⚠️：vapply不如lapply灵活。

```R
> vapply(prime_factors, length, numeric(1))
  two three  four  five   six seven eight  nine   ten 
    1     1     2     1     2     1     3     2     2 
```

**sapply**

简化列表应用。输入参数是一个列表和函数。不需要模板。

```R
> sapply(prime_factors, unique) # 返回一个列表
> sapply(prime_factors, length) # 返回一个向量
  two three  four  five   six seven eight  nine   ten 
    1     1     2     1     2     1     3     2     2 
> sapply(prime_factors, summary) # 返回一个数组
        two three four five  six seven eight nine  ten
Min.      2     3    2    5 2.00     7     2    3 2.00
1st Qu.   2     3    2    5 2.25     7     2    3 2.75
Median    2     3    2    5 2.50     7     2    3 3.50
Mean      2     3    2    5 2.50     7     2    3 3.50
3rd Qu.   2     3    2    5 2.75     7     2    3 4.25
Max.      2     3    2    5 3.00     7     2    3 5.00
```

⚠️：不确定输入的是什么，请谨慎使用。

```
> sapply(list(), length)    # 本应该返回一个向量
list()  # 如果列表中的长度为零，无论函数传入了什么参数，sapply总会返回一个列表
```

apply类的函数主要都是与列表一起连用，但也可以接受向量为输入参数。

**`source`**函数用于读取和访问R文件的内容或者说“运行R脚本“，但它却不是向量化的。

如果要运行某个目录下的R script，我们需要先把目录中的内容转换到列表中再传给**`lapply`**。

```R
> r_files <- dir(pattern = "\\.R$") # dir函数返回指定目录的文件名
# 只返回*.R文件
> lapply(r_files, source)
> getwd()   # 当前工作目录
```

⚠️：lapply、vapply和sapply只能传入一个向量化的参数，但可以为其传入其他标量参数。

```R
> complemented <- c(2, 3, 6, 18)
> lapply(complemented, rep.int, times = 4) # 传递到内部函数
[[1]]
[1] 2 2 2 2

[[2]]
[1] 3 3 3 3

[[3]]
[1] 6 6 6 6

[[4]]
[1] 18 18 18 18
# 如果向量参数不是第一个，需要自定义函数封装那个真正想要调用的函数。
> rep4x <- function(x) rep.int(4, times = x) # rep.int是{}里的函数，简化写法
> lapply(complemented, rep4x)  # rep4x是封装后的函数
[[1]]
[1] 4 4

[[2]]
[1] 4 4 4

[[3]]
[1] 4 4 4 4 4 4

[[4]]
 [1] 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
# 继续简化代码，连封装的函数名都不需要了
> lapply(complemented, function(x) rep.int(4, times = x))  # 结果相同
```

**循环遍历环境（非列表——eapply**

在新版本中也可以使用`lapply`。

```R
> env <- new.env()   # 创建环境
> env$abc <- c(1, 1, 2, 2, 3, 0, 4, 5)
> env$bde <- c("pig", "cat", "dog", "bird")
> eapply(env, length)
$bde
[1] 4

$abc
[1] 8
```



## 3. 遍历数组

lapply、vapply以及sapply是把矩阵和数组看作向量，将目标函数作用于每个元素上。

更为常见的情况：当把函数作用于一个数组时，我们希望能按照行或列应用

> **matlab**程序包：提供了matlab具备的功能。

下面用“matlab”程序包举例：

```R
> install.packages("matlab")
> library(matlab)

Attaching package: ‘matlab’

The following object is masked from ‘package:stats’:

    reshape

The following objects are masked from ‘package:utils’:

    find, fix

The following object is masked from ‘package:base’:

    sum
# matlab程序包会覆盖一些base、stas和utils包中的函数，重载成MATLAB中相应函数的行为。
# 使用玩matlab包后要恢复以前的函数行为，可以调用detach（“package：matlab”）来完成恢复
> detach("package:matlab") # 恢复行为
```

```R
# 使用matlab包
> (magic4 <- magic(4))
     [,1] [,2] [,3] [,4]
[1,]   16    2    3   13
[2,]    5   11   10    8
[3,]    9    7    6   12
[4,]    4   14   15    1
> rowSums(magic4)
[1] 34 34 34 34
# apply函数提供了类似的按行/列计算的等价函数，以一个矩阵、维数和函数作为参数
> rowSums(magic4)
[1] 34 34 34 34
> apply(magic4, 1, sum)
[1] 34 34 34 34
> apply(magic4, 1, toString)  # 维数1代表把函数应用于每一行
[1] "16, 2, 3, 13" "5, 11, 10, 8" "9, 7, 6, 12"  "4, 14, 15, 1" 
> apply(magic4, 2, toString)  # 维数2代表把函数应用于每一列
[1] "16, 5, 9, 4"  "2, 11, 7, 14" "3, 10, 6, 15" "13, 8, 12, 1"
```

apply也可以用于数据库：

```R
> (baldwins <- data.frame(
+   name         = c("A", "B", "C", "D"),
+   date_of_birth = c("2022-Apr-01", "2021-May-02", "2021-Oct-03", "2022-Feb-22"),
+   n_spouses     = c(2, 3, 1, 1),
+   n_children    = c(1, 3, 4, 2),
+   stringAsFactors = FALSE   # 注意这里的stringAsFactors
+ ))
  name date_of_birth n_spouses n_children stringAsFactors
1    A   2022-Apr-01         2          1           FALSE
2    B   2021-May-02         3          3           FALSE
3    C   2021-Oct-03         1          4           FALSE
4    D   2022-Feb-22         1          2           FALSE
> apply(baldwins, 1, toString)
[1] "A, 2022-Apr-01, 2, 1, FALSE" "B, 2021-May-02, 3, 3, FALSE" "C, 2021-Oct-03, 1, 4, FALSE"
[4] "D, 2022-Feb-22, 1, 2, FALSE"
> apply(baldwins, 2, toString)
                                                name 
                                        "A, B, C, D" 
                                       date_of_birth 
"2022-Apr-01, 2021-May-02, 2021-Oct-03, 2022-Feb-22" 
                                           n_spouses 
                                        "2, 3, 1, 1" 
                                          n_children 
                                        "1, 3, 4, 2" 
                                     stringAsFactors 
                        "FALSE, FALSE, FALSE, FALSE" 
# sapply的行为与apply相同
# sapply与range结合使用能非常迅速的确定数据范围
> sapply(baldwins, range)
     name date_of_birth n_spouses n_children stringAsFactors
[1,] "A"  "2021-May-02" "1"       "1"        "0"            
[2,] "D"  "2022-Feb-22" "3"       "4"        "0"  
```



## 4. 多个输入的应用函数

lapply函数的缺点：

> - 函数参数只能循环作用于单个向量参数
> - 对于作用于每个元素的函数，不能访问该元素的名称

**`mapply`**: multiple argument list apply。

mapply函数能让你传入尽可能多的向量作为参数。常见的用法是传入一个list，再传入另一个list作为前面list的名字。

⚠️：对于mapply，每一个传递的参数都是函数。

```R
> test_mapply <- function(name, factors)
+ {
+   ifelse(
+    length(factors) == 1,
+    paste(name, "is prime"),
+    paste(name, "has factors", toString(factors))
+   )
+ }
> mapply(test_mapply, names(prime_factors), prime_factors)
                        two                       three                        four 
             "two is prime"            "three is prime"     "four has factors 2, 2" 
                       five                         six                       seven 
            "five is prime"      "six has factors 2, 3"            "seven is prime" 
                      eight                        nine                         ten 
"eight has factors 2, 2, 2"     "nine has factors 3, 3"      "ten has factors 2, 5" 
```

在默认情况下，mapply与sapply的表现相同，并且会简化输出，可通过参数`SIMPLIFY = FALSE`来关闭。

**Instant Vectorization**

`vectorize`是`mapply`的包装函数。

```R
> Medel_genetic_experiment <- function(flower_color)
+ {switch(flower_color,
+         red    = "A dominant individual!",
+         white  = "A recessive individual!",
+         "other")
+ }
> flower_color <- c("Dominant", "Recessive", "other")
> Medel_genetic_experiment(flower_color)
Error in switch(flower_color, red = "A dominant individual!", white = "A recessive individual!",  : 
  EXPR must be a length 1 vector 
# switch函数使得flower_color这个函数不是向量化的
# 可以重写函数使之向量化
> flower_color <- c("red", "white", "other")
> vectorize_Medel_genetic_experiment <- Vectorize(Medel_genetic_experiment)
> vectorize_Medel_genetic_experiment(flower_color)
                      red                     white                     other 
 "A dominant individual!" "A recessive individual!"                   "other"                 
```



## 5. 拆分-应用-合并

如何对已经被分成不同小组的变量进行统计计算？

```R
> (frogger_scores <- data.frame(
+   player = rep(c("A", "B", "c", "D"), times = c(2, 5, 3, 1)),
+   score = round(rlnorm(10, 8), -1)
+ ))
Error in data.frame(player = rep(c("A", "B", "c", "D"), times = c(2, 5,  : 
  arguments imply differing number of rows: 11, 10    # 数据不平稳bug
> (frogger_scores <- data.frame(
+   player = rep(c("A", "B", "c", "D"), times = c(2, 5, 3, 1)),
+   score = round(rlnorm(11, 10), -1)  # rlnorm函数用于计算一系列输入之间的随机对数正态密度
+ ))
   player  score
1       A   8210
2       A  21190
3       B 256500
4       B  11190
5       B  50320
6       B  34020
7       B  41630
8       c   4590
9       c   7010
10      c  98110
11      D  31450
# 原本参考书上的例子
 > (frogger_scores <- data.frame(
+   player = rep(c("A", "B", "c"), times = c(2, 5, 3)),
+   score = round(rlnorm(10, 8), -1)
+ ))
   player score
1       A   870
2       A 15310
3       B  2690
4       B  8750
5       B   780
6       B  1890
7       B  2350
8       c   470
9       c  2500
10      c  1540
# 计算每个玩家的平均得分需要3个步骤
# 首先，来拆分数据集:split
> (scores_by_player <- with(   # with函数就是把所有操作限制在数据框上
+   frogger_scores,
+   split(score, player)   # split：split divides the data in the vector x into the groups defined by f. 
+ ))
$A
[1]   870 15310

$B
[1] 2690 8750  780 1890 2350

$c
[1]  470 2500 1540    
# 然后，将mean函数应用于每个元素
> (list_of_mean_by_player <- lapply(scores_by_player, mean)) # Apply a Function over a List or Vector
$A
[1] 8090

$B
[1] 3292

$c
[1] 1503.333
# 最后，把结果合并到单个向量中
> (mean_by_player <- unlist(list_of_mean_by_player))
       A        B        c 
8090.000 3292.000 1503.333 
# ?unlist:Given a list structure x, unlist simplifies it to produce a vector which contains all the atomic components which occur in x.   
# 如果使用vapply或是sapply函数，最后两个步骤可以简化为一步。                                                       # 拆分-应用-合并是一系列常见的操作，这里有更简便的方法：tapply函数。他能一次执行所有的三个步骤
> with(frogger_scores, tapply(score, player, mean))
       A        B        c 
8090.000 3292.000 1503.333                                                                   
```



## 6. plyr包





# 第十章 包

大部分包都安装在**CRAN**的在线资源库中。除此外还有R-Forage和RForge.net等。

> - 如何加载安装包
> - 如何从本地或互联网安装包
> - 如何管理PC上的包

## 1. 加载包

首先，*“package”*和*“library”*的概念是不同的！

> package：一系列R函数和数据集的集合
>
> library：电脑上的文件夹，包存储于文件夹内的文件中

**library**

我们可以用**`library`**函数来加载PC上哪些已经安装的包，也可以用`load`函数。

```R
# 案例
> library(lattice)
> dotplot(
+   variety ~ yield | site,
+   data = barley,
+   groups = year
+ )
```

<img src="Learning R.assets/image-20220304174742632.png" alt="image-20220304174742632" style="zoom:33%;" />

⚠️：包的名称在传递给library库的时并不需要被引号括起来！

```R
# 如果有很多个包需要加载
> pkgs <- c("lattice", "utils", "rpart")
> for(pkg in pkgs)
+ {
+   library(pkg,character.only = TRUE)  # 用编程的方式把包的名字传递给library，可以设置参数character.only
+ }
```

⚠️：使用`library`来加载一个未安装的包，会抛出错误。

我们可以使用**`require`**函数来通过判断包是否会被成功加载而返回TRUE或FALSE。

**search**

可以使用**`search`**函数查看所有已加载了的包：

```R
> search()
 [1] ".GlobalEnv"        "package:rpart"     "package:lattice"   "tools:rstudio"    # 全局环境永远是第一位
 [5] "package:stats"     "package:graphics"  "package:grDevices" "package:utils"    
 [9] "package:datasets"  "package:methods"   "Autoloads"         "package:base"     
# 注意这里特殊的始终被称为Autoloads的环境和base包
# 举例：定义一个变量var，首先它会从stats包中找到常用的函数，R首先在全局环境中发现它
```

`installed.packages`函数将返回一个数据框包含R知道的你电脑上所有包的信息，以及它所依赖的其他包以及其他信息。

在安装包时，能得到一个只能用户访问的用户库：

> 在Linux下，文件夹同样位于Home目录之下的R/R.version$platform-library/x.y子文件夹中

```R
# R安装时就自带的包的位置
> .Library
[1] "/Library/Frameworks/R.framework/Resources/library"
> R.home("library")
[1] "/Library/Frameworks/R.framework/Resources/library"
> R.version$platform
[1] "aarch64-apple-darwin20"
```

一般情况下，升级R需要重新安装所有的包，保证包的兼容。但是一些场景下，尽可能避免重新安装包也很重要。因此，我们需要创建自己的库，使之适用于R的所有版本。为了达到这一目的，我们需要定义一个环境变量**`R_LIBS`**，它将包含你想要的库位置的路径。

可以用**`.libPaths`**函数查看R所知道的所有字符向量：

```R
> .libPaths()
[1] "/Library/Frameworks/R.framework/Versions/4.1-arm64/Resources/library"
```

## 2. 安装包

```R
> setRepositories()
--- Please select repositories for use in this session ---


1: + CRAN
2:   BioC software
3:   BioC annotation
4:   BioC experiment
5:   CRAN (extras)
6:   R-Forge
7:   rforge.net

Enter one or more numbers separated by spaces and then ENTER, or 0 to cancel
1: 

# 输入setRepositories()，能选择您想要的库
```

Bioconductor：包含了基因组学和分子生物学的包；

R-Forge和RForge.net：包含了开发中的版本，最终会出现在CRAN。

使用**`available.packages`**可以查看库中的包的所有信息：`view(available.package())`。

> 除了这些库，还能从网上很多其他的储存库找到R的包文件，如Github、bitbucket和Google code。

可以使用**`install packages`**来安装包：

```shell
# 案例：尝试下载时间序列分析软件包xts、zoo和它们所依赖的包
> install.packages(
+  c("xts","zoo"),
+   repos = "http://www.stats.bris.ac.uk/R/"
+ )
# 如果想安装到不同的位置，只要加上lib参数，参数传递给install.packages
> install.packages(
  c("xts", "zoo"),
  lib = "some/other/folder/to/install/to",
  repos = "http://www.stats.bris.ac.uk/R/"
```

要直接从**Github**上安装包，首先要安装**devtools**包。`install_github`函数接受GitHub库的名称，例如从Github上获取包：

```shell
 > insatll.packacges("devtools")
 > library(devtools)
 > install_github("packagename1", "packagename2")
```



## 3. 维护包

通过函数`update.packages`可以完成包的更新。在更新每个包之前，函数会提醒了，如果包过多建议设置参数ask = FALSE。

```shell
> update.packages(ask = FALSE)
```

如果想要删除包：

```shell
> remove.packages("zoo")
```

## 小结

- 安装包：`install.packages`；加载包：library或require
- 当加载包时，它们会被添加到search路径，由此R可以找到它们的变量
- 查找已安装的包：`installed.packages`；更新包：`update.packages`
- 删除包：`remove.packages`
- 如何找到包库的位置：`.libPaths`

## 练习

1. 统计安装在个人PC上的每个库下面的软件包数量。

```R
> pkgs <- installed.packages()
> table(pkgs[, "LibPath"])

/Library/Frameworks/R.framework/Versions/4.1-arm64/Resources/library 
                                                                 200 
```





# 第十一章 日期和时间

**lubridate**包能使日期更具可读性。

> - 内置的日期类：POSIXct、POSIXlt和date
> - 如何将字符串转换成日期
> - 显示日期的不同格式
> - lubridate包

## 1. 日期和时间类

**R**中三种日期和时间类：**POSIXct**、**POSIXlt**、**date**。

**POSIX类**

> POSIX是一套定义了需要遵守的Unix的标准。ct是calendar time，POSIXct记录了以世界标准时（UTC）时区为准的从1970年开始计时的秒数计数。POSIXlt将日期存储为一个list，包括秒、分、时、月。
>
> - POSIXct：适用于存储和计算时间
> - POSIXlt：适用于提取日期中的某个特定部分

```R
# 打印POSIXct时间
> (now_ct <- Sys.time())   # 函数Sys.time将以POSIXct的形式返回当前的日期和时间
[1] "2022-03-05 18:27:49 CST"
> class(now_ct)       # now_ct有两个元素
[1] "POSIXct" "POSIXt" 
# 只会看到格式化后的版本，不确定日期是如何被存储的
> unclass(now_ct)
[1] 1646476070   # 可以看到它只是一个数字
```

```R
# 打印POSIXlt时间
> (now_lt <- as.POSIXlt(now_ct))
[1] "2022-03-05 18:27:49 CST"
> class(now_lt)
[1] "POSIXlt" "POSIXt" 
> unclass(now_lt)
$sec
[1] 49.55306

$min
[1] 27

$hour
[1] 18

$mday
[1] 5

$mon
[1] 2

$year
[1] 122

$wday
[1] 6

$yday
[1] 63

$isdst
[1] 0

$zone
[1] "CST"

$gmtoff
[1] 28800

attr(,"tzone")
[1] ""    "CST" "CDT"
# 可以使用列表索引来单独访问POSIXlt日期的每个部分
> now_lt$sec
[1] 49.55306
```

**Date类**

Date类存储了从1970年开始计算的天数。

```R
> (now_date <- as.Date(now_ct))
[1] "2022-03-05"
```

**其他日期类**

其他来自各种插件包的日期时间类包括：date、dates、chron、yearmon、yearqtr、timeDate、ti和Jul。

## 2. 日期与字符串的相互转换

很多数据的文本文件格式没有明确支持某种特定的日期类型。比如在CSV文件中，每个值只是一个字符串，为了使用R中的日期函数，需要把日期字符串转换成某一个日期类型的变量。相反，在往CSV文件中写入数据时，需要首先把日期转换成字符串。

**解析日期**：**把字符串转换为日期变量**

要将字符向量或因子转换为日期，这里我们可以使用`strptime`(string parse time)函数，它将返回POSIXlt日期。日期的格式是用带有百分比符号和字母的字符串来指定。细节可以参考`?strptime`帮助页面。

> %H代表24小时制的小时；%M代表分钟；%S代表秒；%m代表月数；%d代表当月的第几天；%Y代表四位数的年份

```R
> moon_landings_str <- c(
+  "20:17:40 20/07/1969",
+  "06:54:35 19/11/1969",
+  "09:18:11 05/02/1971",
+  "22:16:29 30/07/1971",
+  "02:23:35 21/04/1972"
+ )
> (moon_landings_str <- strptime(
+   moon_landings_str,
+   "%H:%M:%S %d/%m/%Y",    # 20:17:40 20/07/1969时间字符串向量的格式
+   tz = "UTC"      # UTC是世界标准时
+ ))
[1] "1969-07-20 20:17:40 UTC" "1969-11-19 06:54:35 UTC" "1971-02-05 09:18:11 UTC"
[4] "1971-07-30 22:16:29 UTC" "1972-04-21 02:23:35 UTC"
# 如果字符串不匹配格式字符串中的格式，就会取NA值，解析失败
```

**格式化日期**：**把日期变量转换成字符串**

调用`strftime`函数来反转解析操作，也可以使用`format`函数来轻松地完成日期的格式化。

> %I代表12小时制的小时；%p是AM/PM指示；%A是星期几的全名；%B是月的全名

```R
> (now_ct <- Sys.time())  
[1] "2022-03-08 20:47:13 CST"
> strftime(now_ct, "It's %I:%M%p on %A %d %B %Y.")
[1] "It's 08:47PM on Tuesday 08 March 2022."
```



## 3. 时区

解析日期字符串的时候（strptime），可以指定一个时区；格式化（strftime）的时候，可以再次改变时区。使用UTC时区分析时间能很好避免混乱。处理他人的数据，可以使用Olson形式。

```R
> strftime(now_ct, tz = "America/Los_Angeles")
[1] "2022-03-08 04:47:13"
> strftime(now_ct, tz = "Asia/Beijing")
[1] "2022-03-08 12:47:13"
Warning message:
In as.POSIXlt.POSIXct(x, tz = tz) : unknown timezone 'Asia/Beijing'
> strftime(now_ct, tz = "Asia/Shanghai")
[1] "2022-03-08 20:47:13"
```

> 使用`file.path(R.home("share"), "zoneinfo", "zone.tab"`)能找到R中可能的Olson时区列表。

另一个方法是手动添加偏移量（UTC-5)（谨慎使用）。

指定时区的第三个方法是使用缩写(谨慎使用)。

⚠️：如果调用带有POSIXlt参数的连接函数c，它会把时区更改为当地时区。而c函数作用于POSIXct参数上，将彻底除去其时区属性。

## 4. 日期和时间的算术运算

将数字与POSIX日期相加，会以秒为单位增加时间；将数字与Date相加会以天数为单位。

```R
> now_ct + 80000
[1] "2022-03-09 19:00:33 CST"
> (now_date <- Sys.Date())
[1] "2022-03-08"
> now_date + 1000
[1] "2024-12-02"
```

计算案例：

```R
# as.Date函数
> the_start_time <- as.Date("1970-01-01")
> the_end_time <- as.Date("2012-12-21")   # “世界末日”
> (all_time <- the_end_time - the_start_time)
Time difference of 15695 days
```

```R
# difftime函数
> difftime(the_end_time, the_start_time, units = "secs")
Time difference of 1356048000 secs
> difftime(the_end_time, the_start_time, units = "weeks")
Time difference of 2242.143 weeks
```

```R
# seq函数
> seq(the_start_time, the_end_time, by = "1 year")
 [1] "1970-01-01" "1971-01-01" "1972-01-01" "1973-01-01" "1974-01-01" "1975-01-01"
 [7] "1976-01-01" "1977-01-01" "1978-01-01" "1979-01-01" "1980-01-01" "1981-01-01"
[13] "1982-01-01" "1983-01-01" "1984-01-01" "1985-01-01" "1986-01-01" "1987-01-01"
```

还有很多可以操作日期的函数。

## 5. lubridate

lubridate有多种使用了预设格式的解析函数。所有解析函数默认使用UTC时区，都会返回POSIXct日期。

```R
# 示范代码
> join_harrision_birth_date <- c(
+  "1693-03 24",
+  "1693/03\\24",
+  "Tuesday+1693.03*24")
> ymd(join_harrision_birth_date)   # ymd接受年月日的日期形式
[1] "1693-03-24" "1693-03-24" "1693-03-24"
```

lubridate也提供其他函数：ydm、mdy、myd......；ymd_h、ymd_hm......

lubridate包使用`stamp`函数来格式化日期。

```R
# lubridate包邮三种不同类型的变量可以用来处理时间范围
> (duration_one_to_ten_years <- dyears(1:10))
 [1] "31557600s (~1 years)"   "63115200s (~2 years)"   "94672800s (~3 years)"  
 [4] "126230400s (~4 years)"  "157788000s (~5 years)"  "189345600s (~6 years)" 
 [7] "220903200s (~7 years)"  "252460800s (~8 years)"  "284018400s (~9 years)" 
[10] "315576000s (~10 years)"
# today
> today() + duration_one_to_ten_years
 [1] "2023-03-09 06:00:00 UTC" "2024-03-08 12:00:00 UTC" "2025-03-08 18:00:00 UTC"
 [4] "2026-03-09 00:00:00 UTC" "2027-03-09 06:00:00 UTC" "2028-03-08 12:00:00 UTC"
 [7] "2029-03-08 18:00:00 UTC" "2030-03-09 00:00:00 UTC" "2031-03-09 06:00:00 UTC"
[10] "2032-03-08 12:00:00 UTC"
# 其他关于lubridate包的用法略
```

关于lubridate的具体使用方法可以参考：

> -  https://zhuanlan.zhihu.com/p/27612862
> - https://cran.r-project.org/web/packages/lubridate/lubridate.pdf

## 小结

- 有3种内置的存储日期和时间的类：POSIXct、POSIXl以及Date。
- 必须使用POSIXct类来存储数据框中的日期和时间；Date不能存储时间信息
- strptime函数能把字符串解析成日期
- strftime函数能把日期格式化为字符串
- lubridate包

## 练习

1. 解析披头士出生的日期

   | 成员 |  出生日期  |
   | :--: | :--------: |
   |  RS  | 1940-07-07 |
   |  JL  | 1940-10-09 |
   | PMC  | 1942-06-18 |
   |  GH  | 1943-02-25 |

   ```R
   > in_string <- c("1940-07-07", "1940-10-09", "1942-06-18", "1943-02-25")
   > parsed <- strptime(in_string, "%Y-%m-%d")
   > (parsed <- strptime(in_string, "%Y-%m-%d"))
   [1] "1940-07-07 CDT" "1940-10-09 CDT" "1942-06-18 CDT" "1943-02-25 CDT"
   > (out_string <- strftime(parsed, "%a %d %b %y"))
   [1] "Sun 07 Jul 40" "Wed 09 Oct 40" "Thu 18 Jun 42" "Thu 25 Feb 43
   ```

2. 使用编程的方式来读取查找Olson时区名称的文件。
3. 编写一个以日期为输入参数的函数，能返回当天的星座。
