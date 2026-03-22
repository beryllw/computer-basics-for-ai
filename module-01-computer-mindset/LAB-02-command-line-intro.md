# 实验 02：命令行基础

> 学会和计算机"对话"的第一步

---

## 🎯 实验目标

- 熟悉终端/命令行环境
- 掌握基础文件操作命令
- 理解路径的概念
- 建立使用命令行的信心

---

## 📋 实验准备

**时间：** 45-60 分钟

**需要：**
- 终端应用（Terminal、iTerm、Windows Terminal 等）
- 本实验指南

---

## 🔬 实验步骤

### 第一部分：认识终端（10 分钟）

#### 步骤 1：打开终端

**Linux/macOS:** 搜索 "Terminal" 或 "终端"

**Windows (WSL2):** 打开 "Ubuntu" 或 "Windows Terminal"

#### 步骤 2：理解提示符

你会看到类似这样的内容：

```bash
admin@computer:~$
```

或

```bash
➜  ~
```

**各部分含义：**
```
admin     ← 你的用户名
@
computer  ← 计算机名
:
~         ← 当前目录（~ 表示家目录）
$         ← 提示符，表示可以输入命令
```

#### 步骤 3：第一个命令

```bash
echo "Hello, World!"
```

**输出：**
```
Hello, World!
```

`echo` 命令的作用：输出文字到屏幕。

---

### 第二部分：文件操作基础（20 分钟）

#### 命令 1：`pwd` — 我在哪？

```bash
pwd
```

**输出示例：**
```
/home/admin
```

**含义：** Print Working Directory（打印工作目录）

#### 命令 2：`ls` — 这里有什么？

```bash
ls
```

**输出示例：**
```
Documents  Downloads  Pictures  Desktop
```

**含义：** List（列出目录内容）

**常用选项：**
```bash
ls -l      # 详细信息（大小、时间等）
ls -a      # 显示隐藏文件（以.开头的文件）
ls -la     # 组合选项
```

#### 命令 3：`cd` — 换个地方

```bash
cd Documents    # 进入 Documents 目录
pwd             # 确认当前位置
cd ..           # 返回上一级
cd ~            # 回到家目录
cd /            # 到根目录
```

**含义：** Change Directory

#### 命令 4：`mkdir` — 创建目录

```bash
mkdir test_dir        # 创建名为 test_dir 的目录
ls                    # 确认创建成功
cd test_dir           # 进入新目录
pwd                   # 确认位置
```

**含义：** Make Directory

#### 命令 5：`touch` — 创建文件

```bash
touch hello.txt       # 创建空文件
ls                    # 确认创建成功
```

#### 命令 6：`cat` — 查看文件内容

```bash
echo "Hello, File!" > hello.txt   # 写入内容
cat hello.txt                      # 查看内容
```

**输出：**
```
Hello, File!
```

#### 命令 7：`cp` — 复制

```bash
cp hello.txt hello_copy.txt   # 复制文件
ls                            # 确认
```

**含义：** Copy

#### 命令 8：`mv` — 移动/重命名

```bash
mv hello_copy.txt new_name.txt   # 重命名
ls                               # 确认

mkdir another_dir
mv new_name.txt another_dir/     # 移动到目录
ls another_dir/                  # 确认
```

**含义：** Move

#### 命令 9：`rm` — 删除

```bash
rm hello.txt              # 删除文件
ls                        # 确认消失

rm -r test_dir            # 删除目录（-r = recursive）
ls                        # 确认消失
```

**含义：** Remove

⚠️ **警告：** `rm` 删除的文件不会进入回收站，谨慎使用！

---

### 第三部分：路径概念（10 分钟）

#### 绝对路径 vs 相对路径

```
目录结构：
/
├── home/
│   └── admin/
│       ├── Documents/
│       └── Pictures/
└── tmp/
```

**绝对路径：** 从根目录 `/` 开始的完整路径
```bash
/home/admin/Documents
/tmp
```

**相对路径：** 从当前位置开始的路径
```bash
# 假设你在 /home/admin

cd Documents      # 相对路径：进入 Documents
cd ./Documents    # 同上，. 表示当前目录
cd ..             # 返回上一级
cd ../tmp         # 到上一级的 tmp 目录
```

#### 特殊符号

| 符号 | 含义 | 例子 |
|------|------|------|
| `.` | 当前目录 | `./script.sh` |
| `..` | 上一级目录 | `cd ..` |
| `~` | 家目录 | `cd ~` |
| `/` | 根目录或路径分隔符 | `/home/admin` |

#### 练习：路径导航

```bash
# 1. 回到家目录
cd ~

# 2. 创建练习目录结构
mkdir -p practice/a/b/c
# -p 选项：自动创建父目录

# 3. 进入最深层
cd practice/a/b/c
pwd
# 输出：/home/admin/practice/a/b/c

# 4. 用一行命令回到家
cd ~/practice

# 5. 删除整个练习目录
cd ~
rm -rf practice
# -r: 递归删除
# -f: 强制，不确认
```

---

### 第四部分：综合练习（15 分钟）

#### 练习 1：创建项目结构

**任务：** 创建以下目录结构

```
my_project/
├── docs/
├── src/
└── data/
```

**命令：**
```bash
mkdir -p my_project/{docs,src,data}
cd my_project
ls -la
tree  # 如果安装了 tree 命令
```

#### 练习 2：文件操作

**任务：** 在项目目录中创建文件并组织

```bash
# 创建文件
echo "# My Project" > docs/README.md
echo "print('Hello')" > src/main.py
echo "some,data" > data/input.csv

# 查看结构
ls -R  # 递归列出所有文件
```

#### 练习 3：文件内容操作

```bash
# 查看文件内容
cat docs/README.md

# 追加内容
echo "This is my first project." >> docs/README.md
cat docs/README.md

# 查看文件行数
wc -l docs/README.md
```

#### 练习 4：清理

```bash
# 确认要删除
ls -R my_project/

# 删除
cd ~
rm -rf my_project

# 确认删除
ls my_project 2>&1
# 应该看到：ls: cannot access 'my_project': No such file or directory
```

---

## 📊 命令速查表

| 命令 | 全称 | 作用 |
|------|------|------|
| `pwd` | Print Working Directory | 显示当前目录 |
| `ls` | List | 列出目录内容 |
| `cd` | Change Directory | 切换目录 |
| `mkdir` | Make Directory | 创建目录 |
| `touch` | - | 创建空文件 |
| `cat` | Concatenate | 查看文件内容 |
| `cp` | Copy | 复制文件 |
| `mv` | Move | 移动/重命名 |
| `rm` | Remove | 删除文件 |

---

## 🤔 思考题

1. `cd ..` 和 `cd ~` 有什么区别？
2. 如何查看隐藏文件？
3. 为什么 `rm` 命令要小心使用？
4. 绝对路径和相对路径各有什么使用场景？

---

## ✅ 实验检查清单

完成实验后，确认你能：

- [ ] 打开终端并理解提示符
- [ ] 使用 `pwd` 知道当前位置
- [ ] 使用 `ls` 查看目录内容
- [ ] 使用 `cd` 切换目录
- [ ] 使用 `mkdir` 创建目录
- [ ] 使用 `touch` 创建文件
- [ ] 使用 `cat` 查看文件内容
- [ ] 使用 `cp` 复制文件
- [ ] 使用 `mv` 移动/重命名文件
- [ ] 使用 `rm` 删除文件
- [ ] 理解绝对路径和相对路径的区别

---

## 📚 延伸阅读

- 抽象层次 → 03-abstraction-layers.md
- 命令速查表 → resources/command-cheatsheet.md

---

## 🚀 下一步

命令行还有很多强大功能：

- **管道和重定向** → module-02/03-pipes-redirection.md
- **文本处理** → module-02/02-text-processing.md
- **Shell 脚本** → module-02/05-shell-scripting-intro.md

---

**实验完成！** 🎉

你已经迈出了命令行使用的第一步！
