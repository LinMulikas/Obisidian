
## [[(2. Get Started)]]

### Basic Philosophy

首先，一个编程语言应当包含一系列属于该编程语言的关键内容，以完成对数据的操作和计算等功能。为此，我们只讨论 *Scheme* 语言范畴下的编程内容。所有的编程语言本质是对计算机内部数据的处理，也就是说一门编程语言必须包含处理数据的能力。只不过有的编程语言直接针对的是数据层的内容进行反复读写操作，这不是 *Scheme* 的哲学。

而 *Scheme* 语言的哲学，界定了这门语言处理的内容 *S-Exp* 包含两种内容：*data* 和 *procedure*，第一个东西是不可再分的数据，通过一些人为规定的符号与真实世界的事物对应起来。如 *integer* 类型的数据在计算机中是 *1, 2, 3* 等事物对应。

处理 *procedure* 中的内容到达 *data* 数据层的过程叫做 *Evaluate*，使之能够在屏幕上看到为 *print* 等。我们默认用括号括起来的 *(procedure)* 表示对该过程求值。

总之，括号作用在被括住的主体上，得到的一定是 *Data*.

而从外界语言（包含正在编写的代码语言）到达 *Scheme* 语言，有可能出现不符合语法之类的问题。我们首先用 *quote* 把这些输入的内容与处理内容的代码区分，而 *parse* 要做的就是将 *quote* 了的语言转化成 *S-Exp*。

### Data

数据实际上有两种，一种是不可再分的，或者无需再分的 *atom*，一种是用 *atom* 构造出来的 *construction*，我们只需要提供 *cons* 关键字表示一种 *quote* 内容的连接，就可以实现构造。

#### Atom 


#### Cons

我们可以用 cons 符号构造新的数据类型

##### List
一些常用的内容，如列表，其构造被内置了。

*List* 在 *quote* 层用 *quote ()* 作为一个核心标志，如果用 *'.* 表示 cons 的简写，那么列表 [1, 2, 3, 4] 等价于：
$$(1 . (2. (3. (4 .()))))$$
我们对于所有上述类型构造的 *List* 简写为 *(1 2 3 4)*，并在 *Scheme* 内部实现了这个认定。



### Lambda Calculus

使用 [[(Lambda Calculus)]] 为该门语言的计算模型，具体表达式为：
```Scheme
(lambda x
	  (body-procedure))
```

*lambda* 表达式所做的就是描述了右侧的 *自由变量* 参与的计算。*自由变量* 在 *Scheme* 中用字母表示，并默认支持模式匹配以解决多参数的列表。

*l-map* 的调用的时候，默认为多参数表达式，写为：
```Scheme
(l-map arg1 arg2 ...)
```

实际上，右侧的多参数会被打包为一个 list 之后传入第一种标准表达式，用 lambda calculus 的格式写的话，是 $(l-map)[args]$.

而赋值计算等价于 *let* 关键字，那么用 *Scheme* 语言就是：
```Scheme
(let ([x list arg1 arg2 ...])
	  (l-map))
```

同时，所有的 lambda 表达式的结果，实际上是代入了变量后的 procedure，都会被默认打包为 *(procedure)*，意味尝试计算带入后的 procedure

也就是严格来说，说所有的 lambda 表达式在 *Scheme* 中都是定义为单参数的，而默认通过 *pattern-match* 右侧是一个 list 来解决多个 *自由变量* 的问题。

默认支持了如下的 *pattern-match*，也就是变长参数列表：
- (arg1 arg2 ~ argn)
	定长参数匹配，如果不符合数量则出错。

- (arg1 arg2 ~ argn . argr)
	不定长参数匹配，属于是拿着打包后的参数从右往左走。
	实现了为前面 n 个变量命名并局部绑定，剩余的变量（作为一个 list）命名为 argr.
	至于变长参数为 0 个的时候，写为 (argr)

### Let, Define, Set!

上述 let 是 l-map 求值必备的，而 define 定义一个全局的名称，set! 是更改某个变量的名称。

Define 的作用是将左侧名称与右侧 Evaluate Procedure 全局绑定，let 是在作用域内绑定。

绑定的作用均是某种指针的行为。对于可以更改的 pair，car 和 cdr 的作用也是类似于指针的修改。而指针会寻找到最小的名称进行终极的绑定。

```Scheme
#lang scheme
(define queue
    (lambda ()
        (let([Nil (mcons 'nil '())])
            (let([data Nil][tail Nil])
                (mcons data tail)))))



(define put!
    (lambda (queue value)
        (let([Nil (mcons 'nil '())])
            (let([tail (mcdr queue)])
                ;同时修改两个
                ;相当于 append
                (println queue)
                (set-mcar! tail value)
                (println queue)
                (set-mcdr! tail Nil)
                ; (println tail)
                ; (println data)
                (println queue)
                (set-mcdr! queue Nil)
                ; (println tail)
                ; (println data)
                (println queue)))))



(define mq (queue))
(put! mq 'a)
```

```Scheme
{{nil} nil}
{{a} a}
{{a nil} a nil}
{{a nil} nil}
```




### Conditions

支持条件表达式
```Scheme
(cond
	 []
	 []
	 ...)
```
方括号实际上和圆括号等价，只是交替使用不会很视觉疲劳罢了。

每一个括号内都是一个单独的可判断的语句：
```Scheme
[expr Data_result]
```

从上往下执行，当遇到一个判断为真的内容的时候就停下，输出后面的 Data_result.

最后可以写上一个万能匹配符号 else，作为一定拥有的结果。


### Objective Programming

考虑一类特殊的 procedure，能够实现 *Objective Programming*。

该 *procedure* 用 *let* 让内部绑定一系列属性，并且定义了一个默认的调用方法的方法，并用 *cond* 去支持了一些预制的 *l-map*（我们叫它 *methods*）.

```Scheme
(define class-name
	(lambda ()
			(let ([inner-data '()]
				(lambda (method . args)
					(cond
						[(eqv? method 'method-1) (method-1 body)
						[...]
						[...]
						[else "Error: No such method."]]))))))
```

这就实现了一套面向对象编程的范式。


### Quote 迷思

实际上，感觉所有代码都是 quote，quote 的嵌套也会默认计算已经有的内容中的 quote。lambda 等内置表达式也是某种针对 quote 的 Evalue。


## [[(3. Going Further)]]

### [[(3.1 Syntactic Extension)]]

本部分介绍了基于最 *core* 的的 *scheme* 基本的关键字去扩展一套合适的编程语言的语义学要素。给出了一个关键的结构树：

![[Pasted image 20230328194306.png]]


