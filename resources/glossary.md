# 术语表 (Glossary)

> 本课程核心术语的中英文对照和解释

---

## 如何使用本术语表

- **按字母顺序** 查找术语
- 每个术语包含：**中文名**、**英文名**、**简要解释**
- 带 🔗 标记的术语表示在课程中有专门讲解
- 带 ⭐ 标记的术语表示**核心概念**，必须理解

---

## A

### Algorithm / 算法 ⭐
> 解决问题的明确指令序列

一系列有限的、明确的步骤，用于解决特定问题或完成特定任务。
- **例子**: 排序算法、搜索算法
- **课程**: module-01-04

### API (Application Programming Interface) / 应用程序接口
> 软件组件之间通信的规则和协议

定义了两个软件组件如何交互的接口。通过 API，你可以使用其他程序提供的功能。
- **例子**: 调用 AI 服务的接口、获取天气数据的接口
- **课程**: module-04

### Argument / 参数
> 传递给函数或命令的值

调用函数或执行命令时提供的具体值。
- **例子**: `print("Hello")` 中，`"Hello"` 就是参数

### Array / 数组
> 有序的数据集合

按顺序存储多个值的数据结构，每个值可以通过索引访问。
- **例子**: `[1, 2, 3, 4, 5]`

### Abstraction / 抽象 ⭐
> 隐藏复杂细节，只暴露必要信息

通过简化模型来理解复杂系统的方法。
- **课程**: module-01-03

---

## B

### Binary / 二进制 ⭐
> 使用 0 和 1 表示信息的系统

计算机使用的数字系统，只有两个数字：0 和 1。
- **课程**: module-01-02, LAB-01

### Bit / 比特
> 信息的最小单位，值为 0 或 1

Binary digit 的缩写，计算机存储和处理的最小单位。
- **关系**: 8 bits = 1 byte

### Byte / 字节
> 8 个比特，计算机存储的基本单位

用于衡量数据大小的单位。
- **换算**: 1 KB = 1024 bytes, 1 MB = 1024 KB, 1 GB = 1024 MB

### Boolean / 布尔值
> 只有真 (true) 或假 (false) 两种值的类型

用于逻辑判断的数据类型。
- **例子**: `True`, `False`

### Bug / 程序错误
> 程序中的缺陷或错误

导致程序行为不符合预期的问题。

### Debug / 调试
> 发现并修复程序错误的过程

---

## C

### Command / 命令
> 告诉计算机执行某个操作的指令

在命令行中输入的指令。
- **例子**: `ls`, `cd`, `mkdir`

### Command Line / 命令行
> 通过文本命令与计算机交互的界面

也叫终端 (Terminal) 或 Shell。
- **课程**: module-02

### Compiler / 编译器
> 将高级语言代码转换为机器码的程序

与解释器不同，编译器一次性转换整个程序。
- **例子**: C/C++ 编译器

### CPU (Central Processing Unit) / 中央处理器 ⭐
> 计算机的"大脑"，执行指令

负责执行程序指令的硬件。
- **功能**: 算术运算、逻辑判断、控制流程

### Code / 代码
> 用编程语言写成的指令

程序员写的内容，告诉计算机要做什么。

### Comment / 注释
> 代码中的说明文字，不会被执行

用于解释代码，帮助人理解。
- **Python 例子**: `# 这是一行注释`

### Condition / 条件
> 决定程序执行路径的判断

用于控制流程，根据真假决定是否执行某段代码。
- **例子**: `if x > 0:`

### Context / 上下文
> 理解某事物所需的相关信息

在编程中，指代码执行时的环境和状态。

---

## D

### Data / 数据 ⭐
> 信息的数字化表示

计算机处理和存储的内容。
- **类型**: 数字、文本、图片、声音等

### Data Type / 数据类型
> 数据的分类，决定可以进行的操作

不同类型的数据支持不同的操作。
- **例子**: 整数、浮点数、字符串、布尔值

### Database / 数据库
> 结构化存储和管理数据的系统

用于高效存储、查询和更新大量数据。
- **例子**: MySQL, PostgreSQL, SQLite

### Debugging / 调试
> 定位和修复程序错误的过程

### Directory / 目录
> 用于组织文件的容器

也叫文件夹 (Folder)。

### Documentation / 文档
> 解释如何使用某事物的说明

代码文档解释函数、类、模块的用法。

---

## E

### Editor / 编辑器
> 用于编写和修改文本/代码的软件

- **例子**: VS Code, Sublime Text, nano, vim

### Environment / 环境
> 程序运行的条件设置

包括操作系统、安装的软件、配置等。

### Error / 错误
> 程序执行时出现的问题

- **语法错误**: 代码写错了，无法执行
- **运行时错误**: 执行过程中出错
- **逻辑错误**: 程序能跑，但结果不对

### Exception / 异常
> 程序执行时的意外情况

需要特殊处理的错误情况。

### Execute / 执行
> 运行程序或命令

---

## F

### File / 文件
> 存储信息的基本单位

计算机存储数据的基本单元，有名称和扩展名。
- **例子**: `README.md`, `script.py`

### File System / 文件系统
> 组织和管理文件的机制

决定文件如何存储、命名、访问。

### Flow Control / 流程控制
> 决定代码执行顺序的机制

- **类型**: 顺序、条件分支、循环

### Framework / 框架
> 提供基础功能的软件库

帮助你更快开发程序的工具集合。
- **例子**: Django, Flask, React

### Function / 函数 ⭐
> 可复用的代码块，执行特定任务

将一组指令打包，可以多次调用。
- **组成**: 函数名、参数、返回值
- **课程**: module-03

---

## G

### Garbage Collection / 垃圾回收
> 自动管理内存的机制

自动释放不再使用的内存空间。

### GUI (Graphical User Interface) / 图形用户界面
> 使用图形元素与用户交互的界面

与命令行界面相对。
- **例子**: Windows 桌面、macOS 界面

---

## H

### Hardware / 硬件
> 计算机的物理组成部分

可以触摸到的部分。
- **例子**: CPU、内存、硬盘、显示器

### HTTP (Hypertext Transfer Protocol) / 超文本传输协议
> Web 浏览器和服务器通信的协议

用于在网上传输网页数据。
- **版本**: HTTP/1.1, HTTP/2, HTTP/3

### HTTPS / 安全超文本传输协议
> HTTP 的安全版本，使用加密

### Hard-coding / 硬编码
> 将数据直接写在代码中

而不是通过配置或输入获取。

---

## I

### IDE (Integrated Development Environment) / 集成开发环境
> 集成了编辑、调试、运行等功能的软件

- **例子**: VS Code, PyCharm, IntelliJ IDEA

### Input / 输入 ⭐
> 进入系统的数据

程序或函数接收的数据。
- **课程**: module-01-01

### Integer / 整数
> 不带小数点的数字

- **例子**: `1`, `-5`, `1000`

### Interpreter / 解释器
> 逐行执行代码的程序

与编译器不同，解释器一行一行执行。
- **例子**: Python 解释器

### Iteration / 迭代
> 重复执行的过程

通常指循环执行代码。

---

## J

### JSON (JavaScript Object Notation) / JSON 数据格式
> 轻量级的数据交换格式

用于在不同程序之间传递数据。
- **格式**: `{"key": "value"}`
- **课程**: module-04

---

## K

### Kernel / 内核
> 操作系统的核心部分

管理硬件资源和系统服务。

### Keyboard Shortcut / 键盘快捷键
> 通过按键组合快速执行操作

- **例子**: Ctrl+C (复制), Ctrl+V (粘贴)

---

## L

### Library / 库
> 可复用的代码集合

提供特定功能的代码集合，可以被其他程序使用。
- **例子**: `math` 库、`requests` 库

### Linux ⭐
> 开源的操作系统

本课程主要使用的操作系统环境。
- **课程**: module-02

### Loop / 循环
> 重复执行代码的结构

- **类型**: for 循环、while 循环
- **课程**: module-03

---

## M

### Machine Learning / 机器学习
> 让计算机从数据中学习的技术

AI 的核心技术之一。
- **课程**: module-05

### Memory / 内存
> 计算机临时存储数据的地方

断电后数据会丢失。
- **类型**: RAM (随机存取存储器)

### Module / 模块
> 组织代码的单元

将相关功能组织在一起的文件或代码块。

---

## N

### Network / 网络
> 计算机之间通信的系统

用于计算机之间交换数据。
- **课程**: module-04

### Node / 节点
> 网络中的连接点

在网络中表示一个设备或连接点。

### Null / 空值
> 表示"无"或"不存在"的值

在编程中表示没有值。

---

## O

### Object / 对象
> 包含数据和操作的数据结构

面向对象编程的基本单元。

### Operating System (OS) / 操作系统 ⭐
> 管理计算机硬件和软件资源的系统软件

- **例子**: Linux, macOS, Windows
- **功能**: 文件管理、进程管理、内存管理

### Output / 输出 ⭐
> 系统产生的数据

程序或函数执行后产生的结果。
- **课程**: module-01-01

---

## P

### Parameter / 参数
> 函数定义时声明的变量

与 Argument 类似，但更常用于函数定义时。

### Path / 路径
> 文件或目录在文件系统中的位置

- **绝对路径**: 从根目录开始的完整路径 `/home/user/file.txt`
- **相对路径**: 相对于当前目录的路径 `./file.txt`

### Pipeline / 管道
> 将一个命令的输出连接到另一个命令的输入

- **课程**: module-02-03
- **符号**: `|`

### Process / 进程
> 运行中的程序

操作系统调度的基本单位。

### Program / 程序
> 执行特定任务的指令集合

代码的可执行形式。

### Programming Language / 编程语言
> 用于编写程序的形式化语言

- **例子**: Python, JavaScript, C++, Java
- **课程**: module-03

### Prompt / 提示词
> 给 AI 的指令或问题

用于引导 AI 生成期望的输出。
- **课程**: module-05

### Python
> 高级编程语言

本课程使用的编程语言，简洁易读。
- **课程**: module-03

---

## R

### Recursion / 递归
> 函数调用自身的技术

一种解决问题的方法，函数在自己内部调用自己。

### Redirection / 重定向
> 改变命令的输入或输出方向

- **课程**: module-02-03
- **符号**: `>`, `<`, `>>`

### Refactor / 重构
> 改进代码结构而不改变功能

让代码更清晰、更易维护。

### Repository / 仓库
> 存储代码和项目文件的地方

通常指 Git 仓库。

### Return / 返回
> 函数执行后给出的结果

函数可以给调用者返回一个值。

### Root / 根
> 文件系统的顶层目录

在 Linux 中是 `/`，也是管理员账户的名称。

---

## S

### Script / 脚本
> 自动执行任务的程序

通常是较短的程序，用于自动化任务。
- **例子**: Shell 脚本、Python 脚本

### Server / 服务器
> 提供服务的计算机或程序

- **硬件**: 提供计算能力的计算机
- **软件**: 提供服务（如 Web 服务器）的程序

### Shell ⭐
> 命令行界面的程序

用户与操作系统内核之间的接口。
- **例子**: bash, zsh
- **课程**: module-02

### Software / 软件
> 计算机程序和数据的总称

与硬件相对，是看不见摸不着的部分。

### Source Code / 源代码
> 程序员编写的原始代码

用编程语言写成的、未编译的代码。

### Storage / 存储
> 保存数据的设备或空间

- **类型**: 硬盘、SSD、云存储

### String / 字符串
> 文本数据

用引号括起来的字符序列。
- **例子**: `"Hello, World!"`

### Syntax / 语法
> 编程语言的规则

决定代码如何书写的规则。

### System / 系统
> 相互协作的组件集合

多个部分协同工作形成一个整体。

---

## T

### Terminal / 终端
> 命令行界面的应用

与 Shell 类似，是用户与系统交互的窗口。

### Token ⭐
> AI 处理文本的基本单位

AI 模型处理文本时的最小单元，可以是字、词或子词。
- **课程**: module-05

### Type / 类型
> 数据的分类

见 Data Type。

---

## U

### URL (Uniform Resource Locator) / 统一资源定位符
> 网络资源的地址

用于定位互联网上的资源。
- **格式**: `https://example.com/path`

### User / 用户
> 使用计算机系统的人

### User Interface (UI) / 用户界面
> 用户与系统交互的部分

包括图形界面和命令行界面。

### Utility / 工具程序
> 执行特定任务的小程序

通常是系统提供的辅助工具。

---

## V

### Variable / 变量 ⭐
> 存储数据的命名容器

程序中用于保存和引用数据的命名位置。
- **例子**: `x = 5` 中，`x` 是变量
- **课程**: module-03

### Version Control / 版本控制
> 跟踪和管理代码变更的系统

- **例子**: Git
- **用途**: 记录修改历史、多人协作

### Virtual / 虚拟的
> 模拟的、非物理的存在

- **例子**: 虚拟机、虚拟环境

---

## W

### Web / 网络、万维网
> 基于互联网的信息系统

通过 HTTP 协议访问的网页集合。

### Workflow / 工作流
> 完成任务的一系列步骤

描述如何从开始到结束完成一项任务。
- **课程**: module-05

---

## 常用缩写速查

| 缩写 | 全称 | 含义 |
|------|------|------|
| AI | Artificial Intelligence | 人工智能 |
| API | Application Programming Interface | 应用程序接口 |
| CLI | Command Line Interface | 命令行界面 |
| CPU | Central Processing Unit | 中央处理器 |
| CSS | Cascading Style Sheets | 层叠样式表 |
| DNS | Domain Name System | 域名系统 |
| Git | - | 版本控制系统 |
| GUI | Graphical User Interface | 图形用户界面 |
| HTML | HyperText Markup Language | 超文本标记语言 |
| HTTP | HyperText Transfer Protocol | 超文本传输协议 |
| IDE | Integrated Development Environment | 集成开发环境 |
| IP | Internet Protocol | 网络协议 |
| JSON | JavaScript Object Notation | JSON 数据格式 |
| OS | Operating System | 操作系统 |
| RAM | Random Access Memory | 随机存取存储器 |
| SDK | Software Development Kit | 软件开发工具包 |
| SSH | Secure Shell | 安全外壳协议 |
| TCP | Transmission Control Protocol | 传输控制协议 |
| UI | User Interface | 用户界面 |
| URL | Uniform Resource Locator | 统一资源定位符 |
| UX | User Experience | 用户体验 |
| WWW | World Wide Web | 万维网 |

---

**提示**: 本术语表会随着课程进展不断更新。建议使用浏览器的搜索功能 (Ctrl+F) 快速查找术语。
