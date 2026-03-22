# 环境配置指南

> 开始学习前，请按照本指南配置好你的学习环境

---

## 📋 所需工具

本课程需要的工具都是**免费**和**开源**的：

| 工具 | 用途 | 必需程度 |
|------|------|----------|
| 终端/命令行 | 执行命令、运行脚本 | ⭐⭐⭐ 必需 |
| 文本编辑器 | 查看和编辑代码 | ⭐⭐⭐ 必需 |
| Python 3 | 运行 Python 示例 | ⭐⭐⭐ 必需 |
| 浏览器 | 查阅资料、使用 AI | ⭐⭐⭐ 必需 |
| Git | 版本控制（可选） | ⭐ 推荐 |

---

## 🖥️ 系统要求

### 操作系统

本课程主要使用 **Linux/Unix** 命令行：

- **Linux** (Ubuntu、Debian、CentOS 等) — 原生支持
- **macOS** — 原生支持（基于 Unix）
- **Windows** — 需要 WSL2（Windows Subsystem for Linux）

> 💡 **Windows 用户**: 请安装 WSL2
> ```
> 1. 打开 PowerShell（管理员）
> 2. 运行：wsl --install
> 3. 重启电脑
> 4. 按提示完成 Ubuntu 安装
> ```

### 硬件要求

- **内存**: 4GB 以上（8GB 推荐）
- **存储**: 1GB 可用空间
- **网络**: 用于查阅资料和 AI 协作

---

## 🔧 安装步骤

### 步骤 1：检查终端

打开终端应用：

**Linux/macOS**: 搜索"Terminal"或"终端"

**Windows (WSL2)**: 在 Microsoft Store 安装 Ubuntu，然后打开

测试终端：
```bash
echo "Hello, World!"
```

如果看到 `Hello, World!` 输出，终端工作正常。✅

### 步骤 2：检查 Python

```bash
python3 --version
```

如果看到版本号（如 `Python 3.10.12`），Python 已安装。✅

**如果没有安装 Python**:

```bash
# Ubuntu/Debian
sudo apt update
sudo apt install python3 python3-pip

# macOS (使用 Homebrew)
brew install python

# Windows (WSL2)
sudo apt update
sudo apt install python3 python3-pip
```

### 步骤 3：选择文本编辑器

推荐以下任一编辑器：

| 编辑器 | 特点 | 适合人群 |
|--------|------|----------|
| **VS Code** | 功能强大、免费、插件丰富 | 大多数人 |
| **Sublime Text** | 轻量、快速 | 喜欢简洁 |
| **nano** | 终端内编辑、无需额外安装 | 命令行爱好者 |
| **vim** | 强大但学习曲线陡 | 进阶用户 |

**推荐：VS Code**

下载地址：https://code.visualstudio.com/

安装后推荐插件：
- Python (Microsoft)
- Markdown All in One

### 步骤 4：创建学习目录

```bash
# 创建课程目录
mkdir -p ~/computer-basics
cd ~/computer-basics

# 创建笔记目录
mkdir notes

# 创建练习目录
mkdir exercises

# 查看结构
ls -la
```

### 步骤 5：测试 AI 访问

确保你可以访问 AI 助手（如本课程中的 AI）：

- 本课程集成在 OpenClaw 中
- 或使用其他 AI 工具（Claude、ChatGPT 等）

---

## 📦 可选工具

### Git（版本控制）

```bash
# 检查是否安装
git --version

# 安装
# Ubuntu/Debian
sudo apt install git

# macOS
brew install git
```

### curl（API 调用）

```bash
# 检查是否安装
curl --version

# 通常预装，如没有：
sudo apt install curl
```

### jq（JSON 处理）

```bash
# 检查是否安装
jq --version

# 安装
sudo apt install jq
```

---

## ✅ 环境检查清单

完成以下检查，确保环境就绪：

```bash
# 1. 终端工作正常
echo "终端测试"

# 2. Python 可用
python3 --version

# 3. 能创建文件
echo "test" > test.txt
cat test.txt
rm test.txt

# 4. 能创建目录
mkdir test_dir
cd test_dir
cd ..
rmdir test_dir

# 5. 网络正常
curl -I https://www.google.com 2>/dev/null || curl -I https://www.bing.com
```

全部通过？🎉 你准备好了！

---

## 🎯 下一步

环境配置完成后：

1. 回到课程主目录
2. 开始学习 **模块 1：计算机思维基础**

```bash
cd /home/admin/claw-workspace/computer-basics-for-ai
cat module-01-computer-mindset/01-what-is-computation.md
```

---

## 🆘 遇到问题？

### 常见问题

**Q: 终端命令找不到？**
A: 确保你在正确的目录，或命令已安装

**Q: Python 版本太低？**
A: 本课程需要 Python 3.6+，建议 3.8+

**Q: 权限错误？**
A: 有些命令需要 `sudo`，但请小心使用

**Q: 不确定操作是否正确？**
A: 问 AI！把错误信息发给 AI 寻求帮助

---

## 📞 获取帮助

学习中遇到环境问题：

1. 仔细阅读错误信息
2. 搜索错误信息（Google/AI）
3. 问 AI 助手，提供：
   - 你做了什么
   - 期望什么结果
   - 实际看到什么错误

---

**准备好开始学习了吗？** 🚀

```bash
cd module-01-computer-mindset
cat 01-what-is-computation.md
```
