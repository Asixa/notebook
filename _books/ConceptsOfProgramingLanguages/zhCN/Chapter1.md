---
title: "第一章 序言"
excerpt: ""
exclude: true
sidebar:
  nav: "Books_CoPL_zhCN"
---
{% include toc icon="cog" title="本章目录" %}

## 正交性 Orthogonality
 
IBM 指令集 整数相加
```
A   Reg1,Memory_cell
AR  Reg1,Reg2
```
 
VAX 指令集 整数相加
```
ADDL operand_1, operand_2
```
operand 可以为寄存器或者内存单元。

VAX的设计具有正交性.
IMB的设计具有限制性所以难写.

正交性与语言复杂度紧密相关。

__语言的正交性越高，exception(例外?)越少。这也意味着规律性(regularity)越高，这个语言也就更加易学易懂。__

C语言的正交性较低（C++表示正交性是什么？）

但是过高的正交性也会产生问题，书中给的例子是ALGOL，但是我觉得Python这种动态类型语言，写大项目会很难受。