---
title: "LLVM 快速入门"
header:
  teaser: "https://llvm.org/img/DragonMedium.png"
tags:
  - LLVM
  - Compiler
author_profile: false
category: Code
sidebar:
  title: "目录"
  nav: nav-LLVM

pagenav:
  - title: "浮点"
  - title: "整数"
  - title: "布尔"
  - title: "字符串"


# toc: true
# toc_sticky: true
classes: wide
hidden: true
related: false
read_time: false
showmeta: false
share: false
---


## 类型
一般的编程语言的数据类型可以分为 `浮点数` `整数` `字符串` `布尔`,\
其他的类型基本上都是这些类型在不同储存体积上的变形。 

表达式AST的基本返回值是`llvm::Value*`
### 浮点

``` cpp
llvm::Value* NumberConst::Gen(){
		return ConstantFP::get(CodeGen::the_context, APFloat(value));
}
```

### 整数
根据不同的整数类型，位长度取不同的值。
`short` 取 8,
`int` 取 16,
`long` 取 32。
```cpp
llvm::Value* Integer::Gen(){
		const auto int_type=IntegerType::get(CodeGen::the_context, bit_length);
		return ConstantInt::get(int_type, value);
}
```
### 布尔
布尔用(1比特)整数表示
``` cpp
llvm::Value* Boolean::Gen(){
		const auto bool_type=IntegerType::get(CodeGen::the_context, 1);
		return ConstantInt::get(bool_type, value);
}
```
可以把`true`和`false`在编译器中定义为常量
``` cpp
llvm::Value* CodeGen::True  = 
      llvm::ConstantInt::get(llvm::IntegerType::get(CodeGen::the_context, 1), 1);
llvm::Value* CodeGen::False = 
      llvm::ConstantInt::get(llvm::IntegerType::get(CodeGen::the_context, 1), 0);
```

### 字符串
字符串的类型为 i8* 也就是8比特整数的指针。
编译器应将代码中的字符串储存为常量。
``` cpp
llvm::Value* String::Gen() {
        return CodeGen::builder.CreateGlobalStringPtr(llvm::StringRef(value));
}
```
对于字符串类型，i8*指针与C语言的 `char*` 一样，只是一个raw pointer.\
为了方便用户使用，我们可以把字符串类型制作成一个内置类。\
对于类的定义会在后面的文章讲到。