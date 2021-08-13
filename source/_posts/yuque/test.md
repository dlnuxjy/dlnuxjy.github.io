---
title: test
urlname: cztf8o
date: '2021-08-12 18:46:10 +0800'
tags: []
categories: []
---

# vscode 安装

1. vscode 官网下载 [https://code.visualstudio.com/](https://code.visualstudio.com/) window 版本，无脑 next 安装
1. 插件安装 CMake 和 CMakeTool

# cygwin 安装

1. cygwin 官网下载 [http://www.cygwin.com/](http://www.cygwin.com/)  ** 找到 **[setup-x86_64.exe](http://www.cygwin.com/setup-x86_64.exe)，双击运行
1. 选择`Install from Internet` ，然后下一页
1. 选择安装路径 如 `C:/cygwin64`, `Install for All Users`,然后下一页
1. 选择一个本地路径用于暂存软件包，安装完成后可删除，然后下一页，然后下一页
1. 选择 `https://mirrors.aliyun.com`,然后下一页
1. 安装 `make gdb gdb-debuginfo gcc-g++ gcc-core gcc-debuginfo gcc-objc gcc-objc++ cygwin32-gcc-core cygwin32-gcc-debuginfo cygwin32-gcc-fortran cygwin32-gcc-g++`

# cmake 安装

1. cmake 官网下载 [https://cmake.org/download/](https://cmake.org/download/) ，本文使用的是 cmake-3.21.0-rc3-windows-x86_64.msi
1. 安装过程中注意选择增加环境变量 PATH

# 验证开发环境

## 配置 cmake 工程，编译运行

1. 新建空文件夹 hello，注意不要有中文路径
1. 使用 vscode 打开文件夹
1. `Ctrl+Shift+P`快捷键，选择`CMake: Quick Start`，`Scan for kit`后，选择`GCC X86-64-pc-cygwin`
1. 输入项目可执行程序名字，如`hello`,回车，选择`Executable`,等待配置完成
1. 点击下 ![Snipaste_2021-08-03_10-56-13.png](https://cdn.nlark.com/yuque/0/2021/png/22199619/1627959683165-b6cfe111-6006-4de6-a5c8-be8d2e0113fd.png#clientId=udd6e48a3-5caf-4&from=drop&id=u99834e2d&margin=%5Bobject%20Object%5D&name=Snipaste_2021-08-03_10-56-13.png&originHeight=19&originWidth=18&originalType=binary∶=1&size=332&status=done&style=none&taskId=ueb76c59c-d5ed-48d8-a479-c15dac61875#id=vt5YI&originHeight=19&originWidth=18&originalType=binary∶=1&status=done&style=none) 启动，当发现`Termeinal`中输出`Hello,World`字样，代表程序编译运行成功。

## 调试运行

1. main.cpp 中加入断点
1. 点击 ![Snipaste_2021-08-03_10-59-23.png](https://cdn.nlark.com/yuque/0/2021/png/22199619/1627959573974-194654d4-1799-4442-bbc3-82108c5c50a2.png#clientId=udd6e48a3-5caf-4&from=drop&id=u27432d33&margin=%5Bobject%20Object%5D&name=Snipaste_2021-08-03_10-59-23.png&originHeight=21&originWidth=24&originalType=binary∶=1&size=585&status=done&style=none&taskId=ubae88a9c-5fed-40ce-a6ad-5c4a4db3318#id=JLkVQ&originHeight=21&originWidth=24&originalType=binary∶=1&status=done&style=none) ，启动调试运行，当发现自动跳转到 main.cpp 中的断点处，代表调试运行成功。

​
