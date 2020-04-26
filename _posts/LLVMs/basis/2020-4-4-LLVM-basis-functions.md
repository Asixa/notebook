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

## 声明函数
声明一个函数，我们只需要这个函数的
```cpp
    void FunctionDecl::GenHeader() {
        auto the_function = CodeGen::the_module->getFunction(CodeGen::MangleStr(name));

        if (!the_function) {
            std::vector<llvm::Type*> types;
            if (self_type != nullptr) {
                types.push_back(self_type->getPointerTo());
                args->names.insert(args->names.begin(), L"this");
            }
            for (auto i = 0; i < args->size; i++)
                types.push_back(CodeGen::GetType(args->types[i]));

            const auto func_type = llvm::FunctionType::get(
              CodeGen::GetType(return_type), 
              types, 
              args->isVarArg);

            the_function = llvm::Function::Create(func_type, 
                llvm::Function::ExternalLinkage, 
                CodeGen::MangleStr(name),
                CodeGen::the_module.get());

            unsigned idx = 0;
            for (auto& arg : the_function->args())
                arg.setName(CodeGen::MangleStr(args->names[idx++]));

        }
        else *Debugger::out << "function " << name << " already defined";
    }
```
```cpp
    void FunctionDecl::Gen() {
        if (is_extern)return;
        auto function = CodeGen::the_module->getFunction(CodeGen::MangleStr(name));
        if (!function) {
            *Debugger::out << "function head not found\n";
            return;
        }
        const auto bb = llvm::BasicBlock::Create(CodeGen::the_context, 
                CodeGen::MangleStr(name) + "_entry", function);

        CodeGen::builder.SetInsertPoint(bb);
        CodeGen::fields_table.clear();
        for (auto& arg : function->args())CodeGen::fields_table[arg.getName()] = &arg;

        CodeGen::the_function = function;
        if (statements != nullptr)statements->Gen();

        verifyFunction(*function);
        return;
    }

```

## 主函数
就像C#,Java等语言一样,LLVM IR是需要主函数作为入点的。\\
但是Dragonfly支持类似Python或者JavaScript的无主函数的执行。\\
用户只需要输入一行代码即可执行:
```py
    printf("Hello,world")
```
这就需要编译器隐式构建主函数, 并且主函数的内部字段应储存在堆中。\\
最后让主函数默认返回0。
```cpp
void Program::Gen() {
  // Built-in functions...
  // User declarations...

  const auto main_func = CodeGen::CreateFunc(CodeGen::builder, "main");
  const auto entry = CodeGen::CreateBb(main_func, "entry");
  CodeGen::the_function = main_func;
  CodeGen::builder.SetInsertPoint(entry);
  
  // main function statements...

  CodeGen::builder.CreateRet(llvm::ConstantInt::get(llvm::Type::getInt32Ty(CodeGen::the_context), 0));
  verifyFunction(*main_func);
}
```

## 历史遗留问题

与C/C++一样，函数分为声明和定义,\\
如果我们直接声明和定义一个函数的话，就会出现C++的那个历史遗留问题，\\
也就是前定义的函数无法调用到后定义的函数。类与结构体同理\\
Dragonfly并不有头文件或者`forward declaration`, 而应该像现代编译器一样能够自己找的函数的声明与定义。

实现方法很简单:\\
我们需要一种`Declaration`的AST节点, 函数与类的节点皆继承它,
它继承`Statement`,并且拥有一个`GenHeader`的虚函数。
```cpp
    // Base Class for Statements
    class Statement {
    public:
        virtual ~Statement() = default;
        virtual void Gen() = 0;
        static std::shared_ptr<Statement> Parse();
    };
	
    // Base Class for Declaration, which will generate codes before Statments
    class Declaration : public Statement {
    public:
        virtual void GenHeader() = 0;
    };
	
```
然后在生成IR的时候，
首先遍历所有的`Declaration`的`GenHeader`
再调用它们的`Gen`
```cpp
   void Program::Gen() {
        // Built-in functions...

        // User declarations
        for (auto& declaration : declarations)declaration->GenHeader();
        for (auto& declaration : declarations)declaration->Gen();

        // main function
        // main function statements...
    }

```






