原文地址: [https://www.seas.upenn.edu/~cis194/spring13/lectures/01-intro.html](https://www.seas.upenn.edu/~cis194/spring13/lectures/01-intro.html)

CIS 194 Week 1

14 January 2013

Suggested reading:

* [Learn You a Haskell for Great Good, chapter 2](http://learnyouahaskell.com/starting-out)
* [Real World Haskell](http://book.realworldhaskell.org/), chapters 1 and 2
# Waht is Haskell?
Haskell是一种懒惰的，函数式编程语言。当时有很多函数式编程语言，每一种语言都有自己的特性，并且这些语言很难互相交流互相表达。所以一批人聚在一块准备设计一种新的语言；他们把当下语言的优点聚合起来，并加上自己的理解，发明出了Haskell.(1980's)。

![图片](https://uploader.shimo.im/f/mDBYfOyxORkg4Hpf.png!thumbnail)

Haskell的主要特性有:

Functional:

![图片](https://uploader.shimo.im/f/GqbF2d09LM8poZGN.png!thumbnail)

对于"Functiona"，没有公认的，明确的定义。但是一般当我们说Haskell是函数式的时候，我们经常默认两件事情。

* 函数是一等公民，也就是说，函数可以像其他类型一样使用。(?八成类似于python中的闭包技术，我也不太好解释这个一样使用是什么意思)
* Haskell的中心思想在于值的映射，而非执行过程

把这两点合在一起，Haskell是一种完全不同的编程思考方式。我们这节课程的大部分时间将会培养这种编程方式上。

Pure:

![图片](https://uploader.shimo.im/f/2ZrpHkoOY9IMyUWT.png!thumbnail)

Haskell的表达方式总是 "*referentially transparent" *的:

* 非动态的。所有懂东西（变量、数据结构.....）都是静态的。
* 表达式没有"副作用"。例如：更改全局变量或者输出到屏幕。
* 每次使用相同到参数调用函数会产生相同到结果。

这八成听上去不可思议。怎么能不使用动态的方法并且没有副作用地把所有的活儿都干了？这得改变一下你的思路。（毕竟大家都是从面向过程或者面向对象的阶段走过来的）并且如果你改变的思维方式，你会发现这种编程方法有很多好处。

* *Equational reasoning and refactoring(谷歌翻译为方程推理和重构，感觉可能有偏颇，但是我实在不会翻译这个）*: 在Haskell中，每一项都可以使用其他等价关系去代替。就像你在代数课中学到的那样。
* *Parallelism(并行):  *在表达式不互相影响的情况下，Haskell可以更方便地并行计算。
* *Fewer headaches(治疗你的头痛)*: 简单来说，不受控制的输出，远距离行动(?)让你的程序很难debug，反之亦然。这就是Haskell好的地方。

Lazy:

![图片](https://uploader.shimo.im/f/D03n35H6GH08HYRt.png!thumbnail)

在Haskell中，一个表达式的结果在被使用之前是不会被计算出来的。这个简单的做法有很大的影响。我们将在这学期讨论这个问题。这样做的好处有以下几点:

* 可以更好地使用函数来定义控制结构。
* 使无限的数据结构成为可能。
* 使得编程有更灵活的组合方式。（参照下方意面神教的编程方式)
* 主要缺点: 由于结构复杂，所以程序会有更多的时间消耗和内存消耗。（据说优化得已经很不错了。事实上目前各种语言的编译器解释器都在尽力做得更好）

Statically typed:

![图片](https://uploader.shimo.im/f/ohUM1bQHl98dUPkC.png!thumbnail)

所有的Haskell类型语句都有一个类型，并且在编译的时候会有一个类型检查。所有含有类型错误的语句都不会编译并运行。

# Themes
在这个课程中，我们将重点放在三个方面

**Type**

静态类型看上去很讨人厌，但是事实上，静态类型系统只是在C++和Java上表现得令人讨厌（在C++和Java上得静态类型系统仍然不够完备）。本学期，我们将讨论Haskell使用的静态类型系统。在这个系统中：

* 可以更好地思考并表现在程序结构上

写Haskell程序的第一步一般都是写下所有的类型。因为Haskell的类型系统是很有表现力的。也就是说在一开始的类型设计对之后的编程有巨大帮助。

* 用作文件形式

一个富有表达性的类型系统，只看函数的类型信息就可以获得很多关于函数的信息，也大概可以知道这个函数的作用。这个有时候比阅读函数名阅读文档都有意义。

* 将运行时错误转换为编译错误

如果一个程序编好了，大量测试完成之后，在使用过程中发现了bug会非常不爽的。“如果能过了编译，那八成是对的” ——尼古拉斯•赵四。这句话显然是在开玩笑，除了编译错误，程序还很可能有大量的逻辑错误。但是在Haskell里，如果通过了编译极大的可能这个程序就是对的。

**Abstraction**

“Don't Repeat Yourself" 是编程世界的圣经。这个也经常被称作"Abstraction Principle"，想法不应该被拷贝:所有的想法，算法，甚至每个数据在你的代码里只应该出现一次。使用相似的代码片段去排除代码中相似代码块称为抽象过程。

Haskell在抽象这方便做得非常好:类似于参数多态，高等级函数，并且带类型标记的类都可以有助于抽象。我们这学期学习Haskell的过程中一大部分会详细地去讲如何抽象。

wholemeal programming

先插播一条新闻

>Indexitis是一个混合的自创词汇，Index+itis可以译作索引语言。它的意思是指需要对索引进行繁琐的操作，尤其会在修改时因为索引而引起错误。
>wholemeal programming就是它的反意，在编程时对整个所需要处理的数据进行限定，在haskell中即利用List来行使loop职能。由于List修改时的简易，它会减少因为index错误而引发的种种问题。
>（引自 [https://www.jianshu.com/p/bc6a081a8a2b](https://www.jianshu.com/p/bc6a081a8a2b)，说实话看起来和语言特性很相关，在这里我先不仔细看是什么意思了，说不定学了后面就知道这个全餐编程是啥意思了）

另外一个我们主要要讨论的是 wholemeal programming，首先引用 Ralf Hinze的话:

>“Functional languages excel at wholemeal programming, a term coined by Geraint Jones. Wholemeal programming means to think big: work with an entire list, rather than a sequence of elements; develop a solution space, rather than an individual solution; imagine a graph, rather than a single path. The wholemeal approach often offers new insights or provides new perspectives on a given problem. It is nicely complemented by the idea of projective programming: first solve a more general problem, then extract the interesting bits and pieces by transforming the general program into more specialised ones.”
>>函数式编程语言精通wholemeal programming, 这是Geraint Jones定义的一个概念。wholemeal programming意味着花费精力去考虑如下的事情：使用整个List去工作而不是使用List的子序列去进行开发。制造一个解空间，而不是创造单一解；构建一个图，而不是一个单一的路径。wholemeal方法提供一种新的眼光(8# + 3# + 7# + 12#)或者提供一种新的观点去解决问题。这种想法是易于编程实现的，首先解决通用的问题，然后再转化到解决特定问题上。
>（差不多这么翻译的。说起来眼光真的还是蛮强的。）

举个例子，这边有一个C/Java类型语言的伪代码：

```
int acc = 0;
for ( int i = 0; i < lst.length; i++ ) {
  acc = acc + 3 * lst[i];
}
```
这段代码是Richard Bird说到的"Indexitis"风格代码（插播新闻的时候已经说到了）：这个代码就会去考虑更底层的细节，需要考虑这个i会不会越界。这个问题可以通过两步来解决：首先把整个数组乘3，然后把他们求和获得结果。
在Haskell中，我们只需要写

```
sum (map (3*) lst)
```
这学期我们只需要探索这种编程方式所带来的思维转变。并且探讨为什么Haskell可以很好地做到这一点。
# Literate Haskell
这边不使用课件的翻译，复制一波从别的地方白嫖过来的文字

GHCi和Hugs可以解析扩展名为.hs和.lhs的文件。两者所写程序在语法上完全相同，它们的差别是.lhs（literate Haskell script）文件是为了能让Haskell的代码生成文档。有效程序代码可以用“大于号（>）”和空格开头。比如：

>add :: Int -> Int -> Int
>add x y = x + y
>不以大于号和空格开头的内容将被视作注释处理，且注释与代码间必须有一行以上的间隔。还有一些.lhs代码文件中的代码以begin{code}以end{code}结尾—如果.lhs文件遵守一定的格式，就可以使用lhs2tex生成非常精美的文档以供人们阅读。如何使用读者可以参阅[http://www.andresloeh.de/lhs2tex/](https://yq.aliyun.com/go/articleRenderRedirect?url=http%3A%2F%2Fwww.andresloeh.de%2Flhs2tex%2F)。

使用.lhs文件书写代码的优点很明显。函数式编程的代码往往蕴含了编写者很大的思考量，需要用大段的注释进行解释说明，而代码又不是特别长，这个时候用.lhs最好不过了—哪部分是代码、哪部分是注释一目了然，还能生成.pdf文件方便阅读与传播。

>引用自: https://yq.aliyun.com/articles/91043
# Declarations and variables
首先的话，我也是初学者，在上一段中也提到了，Haskell不产生副作用，类似于输入输出的要进行其他操作。为了让代码可以跑起来，目前我是用的方法是将代码写入filename.hs文件，然后使用ghci filename.hs进行装载。写一个带有Main入口的.hs需要更多的知识，目前我先不考虑。

下面是一些Haskell 代码

```
x :: Int
x = 3
-- Note that normal (non-literate) comments are preceded by two hyphens
{- or enclosed
   in curly brace/hyphen pairs. -}
-- 这段代码也说了一下Haskell的注释风格。
```
上面的代码声明了一个整型变量x(:: 可以读做 "has type") 并且声明x的值是3.注意x的值将永远是3(至少在这段练习程序中是这样)。x的值之后将不会改变。

试着去把下面代码的取消注释，之他会产生一个error，类似于'x'重复声明。

```
-- x = 4
gchi test.hs
test.hs:3:1: error:
    Multiple declarations of ‘x’
    Declared at: test.hs:2:1
                 test.hs:3:1
  |
3 | x = 4
  | ^
```
在Haskell中，变量不是用来装数值的盒子，他们只是值的别名。

从另外一方面来说， =不代表赋值，在Haskell中，=就像在数学中一样。所以x=4不能读作“x被赋值为4”，应该读作“定义x为4“。

（这段听上去有点解方程的意思，给定任意一个值x去求解y值）

思考题，下面这段代码如何理解

```
y :: Int
y = y + 1
```
（我也不知道怎么理解）
# Basic Type
```
-- Machine-sized integers
i :: Int
i = -78
```
Haskell编程语言标准需要保证Int类型最大值应不小于2^29。最大值究竟是多少取决于你的计算机。例如，在我的64-bit计算机上，Int的范围大概就是[-2^63, 2^63]。你可以通过以下命令来获得你所使用计算机的Int范围:
```
biggestInt, smallestInt :: Int
biggestInt  = maxBound
smallestInt = minBound
```
(注意在Haskell编程语言中习惯使用驼峰命名法。如果你不喜欢驼峰命名法，那你学起来会很难受)
Integer类型的大小取决于你的机器可以分配出多少内存。

```
-- Arbitrary-precision integers
n :: Integer
n = 1234567890987654321987340982334987349872349874534

reallyBig :: Integer
reallyBig = 2^(2^(2^(2^2)))

numDigits :: Int
numDigits = length (show reallyBig)
```
对于浮点数，这是Double类型:

```
-- Double-precision floating point
d1, d2 :: Double
d1 = 4.5387
d2 = 6.2831e-4
```
同样也提供了单精度浮点类型, Float。

最终，Haskell也提供了布尔类型，字符类型，和字符串：

```
-- Booleans
b1, b2 :: Bool
b1 = True
b2 = False

-- Unicode characters
c1, c2, c3 :: Char
c1 = 'x'
c2 = 'Ø'
c3 = 'ダ'

-- Strings are lists of characters with special syntax
s :: String
s = "Hello, Haskell!"
```
# GCHI
GCHi是由GHC产生的一个交互式的Haskell REPL(读取-计算-打印-循环)。在GCHi模式下，你可以评估一个表达式的值，使用:load(:l)来加载一个文件(或者使用 :reload(:r)来重新加载文件),使用:t来查询表达式的类型。以及其他很多很多事情。

# Arithmetic
猜猜GHCi的计算结果:

```
ex01 = 3 + 2
ex02 = 19 - 27
ex03 = 2.35 * 8.6
ex04 = 8.7 / 3.1
ex05 = mod 19 3
ex06 = 19 `mod` 3
ex07 = 7 ^ 222
ex08 = (-3) * (-7)
```
注意，在这里`反引号`让函数名变为中缀操作符。注意负数一般都需要加括号来避免把负号当作减号处理。（非常丑陋的代码方式）
在这儿，我们给出一个错误:

```
-- badArith1 = i + n
```
加法只能是两个数字类型之间的操作，并且Haskell不能执行隐式的类型转换，所以你必须明确地使用以下命令进行类型转换。
* fromIntegerl: 将任何其他的整数类型(Int 或者 Integer)转化为其他数字类型。
* round, floor, ceiling: 将浮点类型转化为Int或者Integer。

现在，尝试下一段代码:

```
--badArith2 = i / i
```
这段代码错误因为 / 只能对浮点数进行操作。对于整数除法，我们得用 div
```
ex09 = i `div` i
ex10 = 12 `div` 5
```
如果你曾经使用其他的一些会帮你做隐式转换的编程语言，这种特性一开始会让你觉得非常拘束又很傻逼。但是我建议你接着学Haskell，甚至学多了你会感谢Haskell。隐式类型转换会惯着你让你懒得在数值类型相关代码上多进行思考。
# Boolean logic
就像你期待的一样，Boolean类型的变量可以使用逻辑运算符 &&, ||。

举个例子

```
ex11 = True && False
ex12 = not (False || True)
```
在Haskell里，也可以使用 == 来比较是否相等， (/=来表示不等), 或者使用(<), (>), (<=), (>=)来比较大小。
```
ex13 = ('a' == 'a')
ex14 = (16 /= 3)
ex15 = (5 > 3) && ('p' <= 'q')
ex16 = "Haskell" > "C++"
```
Haskell同样有if-表达式: if b then t else f 这种表达式表示如果Boolean表达式b是真，就执行t，否则执行f。注意if-表达式和if-语句是完全的两码事。举个例子，在if-语句中，会有一个else选项。省略的else选项表示“如果if里面的语句是假的，就不做任何事情”。可是在if-表达式中，else的部分是一定需要的，因为if-表达式必须要有一些值当作执行结果。
Haskell中不经常使用if表达式，而是经常使用匹配的方法或者使用guards去代替。（以后说）

（这一小节应该是Haskell if的一个语法特点。就我目前学习来看，Haskell的If一定要带else，说不定可以这么理解，然后八成直接翻译如果表达式更好。）

# Defining basic functions
我们可以用下面的方法声明一个Integer类型的函数。

```
-- Compute the sum of the integers from 1 to n.
sumtorial :: Integer -> Integer
sumtorial 0 = 0
sumtorial n = n + sumtorial (n-1)
```
注意函数的命名方式:  sumtorial :: Integer -> Integer 说这个叫sumtorial的函数是输入Integer然后返回另一个Integer的函数。
每一个函数都会从上往下进行扫描，并且会选择第一个匹配到到clause。举个例子，sumtorial 0的值是0，从第一个式子就匹配到了。sumtorial 3在第一个式子上不会被匹配到，所以会从第二个式子开始匹配(就是sumtorial n = n + sumtorial (n - 1)这个递归式)。所以第二个式子计算的结果为 3 + sumtorial(2)。然后再继续进行迭代。


选择项同样可以基于一个使用守卫的布尔表达式，例如:

```
hailstone :: Integer -> Integer
hailstone n
  | n `mod` 2 == 0 = n `div` 2
  | otherwise      = 3*n + 1
```
一个函数可以接收任意多的Guard。每一个守卫都是布尔表达式。如果进入了守卫模式，那守卫就会从上到下进行计算，并且第一个值为True的语句会执行。如果没有guards的值是True，则会继续向下匹配别的语句。
举个例子，加入我们计算 hailstone 3，首先3可以匹配到n（因为变量可以匹配所有到东西）。然后n % 2 == 0是假的，不会计算，所以会执行 3 * n + 1,所以hailstone 3的结果是10。

给一个更复杂的例子：

```
foo :: Integer -> Integer
foo 0 = 16
foo 1 
  | "Haskell" > "C++" = 3
  | otherwise         = 4
foo n
  | n < 0            = 0
  | n `mod` 17 == 2  = -43
  | otherwise        = n + 3
```
What is foo (-3)? foo 0? foo 1? foo 36? foo 38?
最后注意布尔表达式和guards，假设我们想抽象出一个可以判定奇偶性的函数（使用hailstone)，我们最初的尝试可能会这么干: 

```
isEven :: Integer -> Bool
isEven n 
  | n `mod` 2 == 0 = True
  | otherwise      = False
```
这种做法可以完成这个需求，可是这种做法有些麻烦。你可以试着优化一下。

# Pairs
我们可以把一些变量打包成二元组，就像这样: 

```
p :: (Int, Char)
p = (3, 'x')
```
注意(x, y)是用于成对的类型成对对值。
同样可以对Pair元素进行元素匹配。

```
sumPair :: (Int,Int) -> Int
sumPair (x,y) = x + y
```
Haskell 同样也有 triples， quadruples ...但是八成你永远也用不到他们，我们下星期会介绍一种打包三种元素或更多信息的更好方法。

# Using functions, and multiple arguments
为了匹配有很多参数的函数，只需要在函数名后面列出所有参数，使用空格分开，例子： 

```
f :: Int -> Int -> Int -> Int
f x y z = x + y + z
ex17 = f 3 17 8
```
上面这个例子说的是参数f接收参数(3, 17, 9)。同样大家需要注意函数的声明部分。声明的格式是“参数1类型 -> 参数2类型 -> ... -> 结果类型"。这个可能你觉得很奇怪（但是你也必须这么干）。为什么所有都是箭头呢？为啥不能写成 Int Int Int -> Int?事实上，这种方法绝非偶然：这里有一种非常深邃黑暗美丽(DDF)的原因。之后我们会学为啥，现在你记住就行。
注意，函数比其他中缀表达式有更高的优先级。所以可能一些不正确的写法:

```
f 3 n+1 7
```
如果你希望把(n + 1)当作参数传入f，所以这个会解读为:
```
(f 3 n) + (1 7)
```
如果你想解读为正确的形式，你需要将代码写成:
```
f 3 (n+1) 7
```
# Lists
List是Haskell中比较基础的一个数据类型

```
nums, range, range2 :: [Integer]
nums   = [1,2,3,19]
range  = [1..100]
range2 = [2,4..100]
```
Haskell(像python一样)也有list解析能力，你可以在 [LYAH](http://learnyouahaskell.com/starting-out)中了解更多
String就是字符的一个List。也就是说，String就是[Char]的语法糖。String的常量就是Char的列表的语法糖。

```
-- hello1 and hello2 are exactly the same.

hello1 :: [Char]
hello1 = ['h', 'e', 'l', 'l', 'o']

hello2 :: String
hello2 = "hello"

helloSame = hello1 == hello2
```
这表示了所有用于处理List的函数同样可以用作处理String。

# Constructing lists
最简单的List是一个空的List。

```
emptyList = []
```
其他的List是由空的List使用冒号运算符构造出来的(:)，冒号接收一个元素和一个list，运算结果是把元素放在list的头。
```
ex18 = 1 : []
ex19 = 3 : (1 : [])
ex20 = 2 : 3 : 4 : []
```
ex21 = [2,3,4] == 2 : 3 : 4 : []

我们可以看到[2,3,4]只是 2:3:4:[]的缩写。这个特性和链表很像，而非数组。
```
-- Generate the sequence of hailstone iterations from a starting number.
hailstoneSeq :: Integer -> [Integer]
hailstoneSeq 1 = [1]
hailstoneSeq n = n : hailstoneSeq (hailstone n)
```
当程序运行到hailstoneSql 1的时候停止，并返回单独的1，hailstone序列是给定一个数值，然后反复执行hailstone函数(在上面例子给了hailstone函数是啥),获得的序列。
# Functions on lists
我们可以使用模式匹配写个函数

```
-- Compute the length of a list of Integers.
intListLength :: [Integer] -> Integer
intListLength []     = 0
intListLength (x:xs) = 1 + intListLength xs
```
最开始的匹配方式说，如果是个空list，就返回0。第二个模式说，如果输入可以被匹配成(x : xs)，也就是说，第一个元素匹配到x，剩下的扔进list xs，然后这个list的长度就比xs大1.
因为从来不会用到x，也可以用下划线去匹配: intListLegnth(_:xs) = 1 + intListLength xs.

我们可以使用嵌套的方法去进行匹配：

```
sumEveryTwo :: [Integer] -> [Integer]
sumEveryTwo []         = []     -- Do nothing to the empty list
sumEveryTwo (x:[])     = [x]    -- Do nothing to lists with a single element
sumEveryTwo (x:(y:zs)) = (x + y) : sumEveryTwo zs
```
注意，最后一个语句匹配语句是一个嵌套形式，但是其实我们不需要这么麻烦，写成 sumEveryTwo(x:y:zs) = ...是等价的。
# Combining functions
把很多简单的函数组成复杂的函数是Haskell的惯用作风。

```
-- The number of hailstone steps needed to reach 1 from a starting
-- number.
hailstoneLen :: Integer -> Integer
hailstoneLen n = intListLength (hailstoneSeq n) - 1
```
这个做法在你看来或许很低效，他首先会生成所有的hailstone元素然后再找他的长度，浪费了很大一部分内存。实际上它不会这样。因为Haskell是一种lazy编程语言。只有在元素被需要的时候才会计算出来。所以长度计算和数据生成是交错进行的。整个过程的内存消耗为O(1)，无论整个数列多长。（但是说实话，说O（1）有点假，但是想解释需要很长时间，你就当是O（1）吧）。
之后的时间我们会仔细学习Haskell的lazy特性，现在你就大胆随便嵌套复杂的函数就行。一开始你会觉得很不自然，但是这是Haskell的惯用手法，并且如果你习惯了这种写法，你就会觉得很爽。

# A word about error messages
事实上，很六（我也不知道这玩意怎么翻译，原文就是Actually, six，八成是说给出六个单词？）：

**Don’t be scared of error messages!**

别害怕错误提示

GHC的错误信息非常长并且看上去很吓人，但是事实上他们比较长不是因为错误模糊不清，恰好相反，是因为错误信息中隐含了大部分的有用信息，给个例子：

```
Prelude> 'x' ++ "foo"

<interactive>:1:1:
    Couldn't match expected type `[a0]' with actual type `Char'
    In the first argument of `(++)', namely 'x'
    In the expression: 'x' ++ "foo"
    In an equation for `it': it = 'x' ++ "foo"
```
首先，我们被告知了想要一个[a0]但是给了一个Char，这个意思是想要一个list但是你给了一个Char。下一行告诉我们， '++'的第一个参数出现了问题，下一行告诉了我们更多细节。现在我们看到问题具体出现在哪里了。大概就是'x'是一个Char类型，但是++需要一个list来当参数。
如果你发现了一个错误信息，就深呼吸好好看仔细读，然后你就可以改正错误。


Generated 2013-03-14 14:39:58.567681

translate: Thara

