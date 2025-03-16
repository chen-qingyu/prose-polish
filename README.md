## 简介

prose-polish 是一个通过拖拽卡片的方式即可于 AI 交互的工具，专注于文案、稿件的编辑。

它可以识别 Markdown 格式的文稿，将其自动导入为段落卡片。

你可以将常用的提示词预制成卡片，并且快速连接需要修改的稿件。

修改后的稿件依然以卡片的形式呈现，只需要把它拖拽出来，就能作为新的段落。

想要流畅地使用，只需要记住唯一一条规则：**插头插在插座上！**

## 使用

### 安装环境

- Node.js：[下载地址](https://nodejs.org/)
- Ollama（可选，用于本地模式）：[下载地址](https://ollama.ai)

### 配置 API Key（仅在线 API 模式需要）

- 复制 `config.example.js` ，并将新文件重命名为 `config.js`
- 根据其中的备注，配置至少一个在线模型的 API Key

### 启动项目

项目中已经准备好了启动脚本，直接使用 Git Bash 执行 `./start.sh` 即可。

启动脚本会自动：

- 检查环境依赖
- 安装所需包
- 启动服务器

### 选择模式

- 完整模式（选项 1）：支持所有功能

  - 访问地址：http://localhost:3000
  - 使用 localhost 以支持完整的服务器功能
  - 适用于：需要使用在线 API 或本地模型的场景
  - 需要：如使用在线 API，需配置相应的 API Key

- 本地模式（选项 2）：使用 Ollama 本地模型
  - 访问地址：http://127.0.0.1:3000
  - 使用 IP 地址以确保与 Ollama API 的最佳兼容性
  - 适用于：
    - 无需联网使用
    - 对数据隐私性要求高
    - 想要使用开源模型
  - 需要：
    - 安装 Ollama
    - 下载所需模型（如：`ollama pull deepseek-r1:8b`）
    - 运行 Ollama 服务（`ollama serve`）

### 支持的大语言模型

目前支持以下模型：

- 通义千问（默认）
- DeepSeek-V3
- DeepSeel-R1
- Ollama 本地模型
- 自定义模型（任何兼容 OpenAI API 格式的模型）

### 一些可能需要知道的细节

- "导出 Markdown"按钮的规则是，将现有的段落卡片从上至下拼接为完成的 markdown 文件，每个卡片一段。
- 预制提示词中形如`{{带有双花括号}}`的内容会被识别为黄色插头，作为接线端口。
- 紫色插头图标可以用于连接其他段落卡片。
- 预制提示词可以以 json 格式导入和导出。

## 开发者信息

以下记录相关开发信息。如果你基于此项目二次开发，这里可能有你需要的信息。

- Ollama 端口配置：如果 Ollama 端口发生变化，请于 `script.js` 中的`OLLAMA_BASE_URL`项修改。

- 虽然 localhost 和 127.0.0.1 都指向本机，但我们在不同模式下使用不同的地址是为了：
  1. 确保完整模式下的服务器功能正常运行
  2. 保持与 Ollama 本地 API（使用 127.0.0.1:11434）的一致性
  3. 避免在本地模式下不必要的 DNS 解析

### 通过 Docker 部署

> 本项目可以通过 Docker 部署。如果你不知道什么是 Docker，请跳过本节。使用上文介绍过的方法足以部署该项目。

**前提条件**

- 安装 Docker: [Get Started | Docker](https://www.docker.com/get-started/)
- （可选）安装 Docker Compose: [Install | Docker Docs](https://docs.docker.com/compose/install/)
- `git clone`该项目并`cd`到项目目录，根据 config.example.js 在项目目录下创建 config.js 并配置

**构建与启动容器**

1. git clone 并 cd 到项目路径（包含 Dockerfile）
2. `docker build -t prose-polish:latest .`
3. 启动项目：
   1. 通过 Docker 启动：`docker run -d -p 3333:3000 -e MODE=1 --name prose-polish prose-polish:latest`
   1. 通过 Docker Compose 启动：`docker compose up -d`

**参数解释**

- 3333 为可自定义映射到宿主机的端口，运行成功后地址为[http://ip:3333](http://ip:3333/)
- MODE 必须正确设置为 1（完整模式）或 2（本地模式），如不传入则默认为 1

### AI 附注文档

本项目专为 AI 准备了详细的[开发文档](README_FOR_AI.md)。
