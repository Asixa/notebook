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

## 安装必要程序

首先需要安装LLVM的[Pre-Built Binaries](https://releases.llvm.org/download.html).

如果你不知道下载哪个文件的话，可以选择 [Windows](https://github.com/llvm/llvm-project/releases/download/llvmorg-10.0.0/LLVM-10.0.0-win64.exe),
[Ubuntu](https://github.com/llvm/llvm-project/releases/download/llvmorg-10.0.0/clang+llvm-10.0.0-x86_64-linux-gnu-ubuntu-18.04.tar.xz)
{: .notice--primary}


这个程序包中含有Clang编译器等，\\
可以用来调试我们自己生产的LLVM IR (LLVM Intermediate Representations).

其次我们需要下载LLVM的[源码](https://releases.llvm.org/download.html)

如果你不知道下载哪个文件的话，选择`LLVM source code (.sig)` 或直接点击[这里](https://github.com/llvm/llvm-project/releases/download/llvmorg-10.0.0/llvm-10.0.0.src.tar.xz)
{: .notice--primary}

下载完成并解压后，使用CMake或者Cmake-gui生成Build文件夹.\\
如果你是Windows用户并且使用Visual Studio作为generator生成了的话，你会在Build文件夹里找到`LLVM.sln`.

流程上你需要打开这个解决方案并且编译,因为我们需要一个特殊的执行文件`llc.exe`,\\
但是编译整个LLVM需要花费很久的时间。\\
您可以直接到Dragonfly的GitHub的tools目录单独下载这个执行文件。

## 项目配置
Visual Studio支持直接对Cmake文件夹进行构建。
{: .notice--primary}
我们在CMakeLists.txt中加入如下的内容，将星号替换为LLVM源码所在的目录。
```cmake
# ......

#LLVM
if(${LLVM_DIR} MATCHES "LLVM_DIR-NOTFOUND" )
	message("Using LLVM_DIR From cmake/FindLLVM.cmake")
	#include("${PROJECT_SOURCE_DIR}/cmake/FindLLVM.cmake")
        set(LLVM_DIR ********/llvm-10.0.0.src/build/lib/cmake/llvm)
endif(${LLVM_DIR} MATCHES "LLVM_DIR-NOTFOUND" )

find_package(LLVM REQUIRED CONFIG)
message(STATUS "Found LLVM ${LLVM_PACKAGE_VERSION}")
message(STATUS "Using LLVM_DIR: ${LLVM_DIR}")

include_directories(${LLVM_INCLUDE_DIRS})
add_definitions(${LLVM_DEFINITIONS})
llvm_map_components_to_libnames(llvm_libs support core irreader bitwriter)

# ......
```
完整CMakeLists可以在[这里]()查看。

## 项目配置
```
llvm::LLVMContext CodeGen::the_context;
std::unique_ptr<llvm::Module> CodeGen::the_module = std::make_unique<llvm::Module>("Program", CodeGen::the_context);
llvm::IRBuilder<> CodeGen::builder(CodeGen::the_context);

std::map<std::string, llvm::Value*> CodeGen::fields_table;
std::map<std::string, parser::ClassDecl*> CodeGen::types_table;
```

