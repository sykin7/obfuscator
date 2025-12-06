
# 🛡️ JS-Obfuscator-UI (JSCrypt Dashboard)

> 一个基于 `javascript-obfuscator` 的现代化、仪表盘风格的 Web UI 界面。
> 
> A modern, dashboard-style Web UI wrapper for `javascript-obfuscator`.

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![Docker](https://img.shields.io/badge/docker-supported-2496ED?logo=docker&logoColor=white)
![Language](https://img.shields.io/badge/language-HTML%2FJS-orange)

## 📖 简介 / Introduction

这是一个出于个人兴趣制作的单页 Web 工具（Just for fun）。

官方的 `javascript-obfuscator` 功能非常强大，但配置项繁多。本项目旨在**简化 UI**，提供一个类似商业级 SaaS 的仪表盘界面，让你能更直观、更舒服地进行代码混淆。

核心混淆引擎依然基于强大的开源项目 [javascript-obfuscator](https://github.com/javascript-obfuscator/javascript-obfuscator)。

## ✨ 特性 / Features

*   🎨 **现代化 UI**：深色模式、仪表盘布局，告别枯燥的表单。
*   🌐 **中英双语**：内置中英文一键切换，默认中文。
*   ⚡ **即开即用**：单文件架构（Single HTML），无复杂的后端依赖。
*   🐳 **容器友好**：支持 Docker/Docker Compose 极速部署。
*   🔧 **核心参数**：精选了最常用的混淆参数（僵尸代码、控制流平坦化、域名锁定、防调试等）。
*   📊 **实时统计**：直观展示混淆前后的文件大小对比。

## 🚀 快速开始 / Quick Start

### 方式一：直接运行 (Static HTML)

本项目核心只是一个 `index.html` 文件。

1. 下载本仓库。
2. 双击打开 `index.html`。
3. 也就是这么简单。

### 方式二：Docker 部署 (Container)

如果你想把它跑在服务器上（如 NAS、VPS、Zeabur、Leaflow 等）：

#### 1. 使用 Docker CLI

```bash
# 假设你的 index.html 在当前目录
docker run -d \
  --name js-obfuscator \
  -p 8080:80 \
  -v $(pwd)/index.html:/usr/share/nginx/html/index.html \
  nginx:alpine
````

访问 `http://localhost:8080` 即可。

#### 2\. 使用 Docker Compose (推荐)

创建一个 `docker-compose.yml`：

```yaml
version: '3'
services:
  web:
    image: nginx:alpine
    container_name: js-obfuscator-ui
    ports:
      - "8080:80"
    volumes:
      - ./index.html:/usr/share/nginx/html/index.html
    restart: always
```

然后运行：

```bash
docker-compose up -d
```

### 方式三：部署到静态托管 (Vercel/Cloudflare Pages)

直接将 `index.html` 上传至 GitHub，连接 Vercel 或 Cloudflare Pages 即可直接部署，无需任何构建命令。

## 🛠️ 技术栈 / Tech Stack

  * **Core**: [javascript-obfuscator (Browser Build)](https://github.com/javascript-obfuscator/javascript-obfuscator)
  * **UI**: Native HTML5 + CSS3 (No Frameworks, No Build Step)
  * **Icons**: FontAwesome CDN

## ⚠️ 免责声明 / Disclaimer

本项目仅作为一个 UI 包装壳，核心混淆逻辑由 `javascript-obfuscator` 提供。
This project is merely a UI wrapper. The core obfuscation logic is provided by `javascript-obfuscator`.

请勿将混淆后的代码用于恶意用途。
Do not use obfuscated code for malicious purposes.

## 📄 License

MIT License

````

---

### 💡 给你的额外建议

为了配合这个 README 里的 Docker 部署部分，建议你在 GitHub 仓库里除了上传 `index.html`，最好也真的放一个极简的 `Dockerfile`（虽然我在 README 里用了挂载卷的方式，但有个 Dockerfile 显得更正式，方便云平台直接识别）：

**新建一个 `Dockerfile` 文件：**

```dockerfile
FROM nginx:alpine
COPY index.html /usr/share/nginx/html/index.html
EXPOSE 80
````

这样如果你把项目推送到 GitHub，像 Zeabur、Leaflow 这种平台就能自动识别并部署了。
