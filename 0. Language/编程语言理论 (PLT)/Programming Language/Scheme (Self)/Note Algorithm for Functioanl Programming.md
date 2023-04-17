# AFP

- [AFP](#afp)
- [Ch1. 基本符号](#ch1-基本符号)
  - [1. 简单值](#1-简单值)
  - [2. 标识符、表达式](#2-标识符表达式)
  - [3. 函数、过程](#3-函数过程)
  - [4. 算数函数](#4-算数函数)
  - [5. 过程调用（惰性求值）](#5-过程调用惰性求值)
  - [6. Lambda Calculate](#6-lambda-calculate)
    - [1. 变长参数 (列表参数)](#1-变长参数-列表参数)
    - [2. 列表的创建](#2-列表的创建)
    - [3. 列表的解绑](#3-列表的解绑)
  - [7. 谓词](#7-谓词)


# Ch1. 基本符号

## 1. 简单值

## 2. 标识符、表达式

```Common Scheme
if, and, or

let, define, rec, receive, define-record-type

quote,  sect, source
```

## 3. 函数、过程

## 4. 算数函数

## 5. 过程调用（惰性求值）

使用括号调用某个过程体，过程的数值看成一个整体可以作为数值等进行计算。



## 6. Lambda Calculate

```Common Scheme
(lambda (固定参数列表)
  过程体)
```

### 1. 变长参数 (列表参数)


```Common Scheme
(lambda 可变长参数
  过程体)
```

- apply
  ```Common Scheme
  (apply lambda表达式 某个list)
  ```

### 2. 列表的创建

```Common Scheme
(list 数据)
```

### 3. 列表的解绑

- values
  values: args -> args
  将参数列表里的参数原封不动的返回


- delist
  列表的解绑等价于：
  ```Common Scheme
  (lambda (ls)
    apply values ls)
  ```

  
## 7. 谓词

