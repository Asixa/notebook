---
title: "LLVM 快速入门"
header:
  teaser: "https://llvm.org/img/DragonMedium.png"
excerpt: "LLVM 快速入门"
tags:
  - LLVM
  - Compiler
author_profile: false
category: Code

sidebar:
  title: "目录"
  nav: nav-LLVM
# toc: true
# toc_sticky: true
classes: wide
hidden: true
related: false
read_time: false
showmeta: false
share: false
---

## 准备AST
无论是手撸前端还是使用Yacc/Bison 之类的编译器生成器。\\
我们需要一棵抽象语法树(Abstract Syntax Tree，AST)，\\
本文并不会涉及Parser和Lexer的知识，所以我假设您已经准备好了。
## 结构

表达式节点的基类如下,`Gen`是生成 Generate 的缩写.\\
对于表达式节点，返回一个**值**`llvm::Value*`.\\
`cmd`参数用于处理特殊情况下的生成。
```cpp
    class Expr {
    public:
        virtual ~Expr() = default;
        virtual llvm::Value* Gen(int cmd = 0) = 0;
    };
```
其他表达式节点皆继承`Expr`，例子如下：
```cpp
    // 数字常量节点
    class NumberConst final : public Expr {
    public:
        int type;
        double value;
        explicit NumberConst(const double d, const int t) : value(d) { type = t; }
        void ToString() override;
        llvm::Value* Gen(const int cmd = 0) override;
    };
```
```cpp
    // 二元操作符节点，op为操作符的类型，LHS 和LHS 是二叉树节点的子节点。
    class Binary final : public Expr {
    public:
        int op;
        std::shared_ptr<Expr> LHS,RHS;
        Binary(std::shared_ptr<Expr> lhs, std::shared_ptr<Expr> rhs, int op): 
            op(op), LHS(lhs), RHS(rhs) {}

        llvm::Value* Gen(const int cmd = 0) override;
        //... 其他被Parser用到的函数
    };
```



处理完表达式节点后，Statement的定义如下，\\
其他语法比如`if`, `for`, `return`, `def` 皆继承`Statement`\\
`Statement`的`Gen` 不需要有返回值。
```cpp
    class Statement {
    public:
        virtual ~Statement() = default;
        virtual void Gen() = 0;
        //... 其他被Parser用到的函数
    };
```

完整的AST节点定义可以在[这里]()找到。