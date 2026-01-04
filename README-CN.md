[English](./README.md) | 中文

## OpenDocvivid（中文）

OpenDocvivid 是一款现代化、由 AI 驱动的文档生成视频平台。  
你可以上传文档或网页内容，由大语言模型进行处理，并自动生成图文并茂的视频。

## 截图

![Screenshot](./img/main.png)

## ✨ 核心特性

- **AI 视频生成**：基于文档、文件、网址内容，经大模型处理后自动生成视频。
- **任务驱动的处理流程**：内置异步任务系统，适合视频渲染、积分/用量统计等长耗时操作。
- **用户与订阅体系**：支持用户登录、订阅套餐与积分/额度结算。
- **现代 Web 界面**：基于 Next.js/React 的前端，提供响应式、应用化的使用体验。
- **可扩展后端**：FastAPI + Celery 架构，方便扩展新的路由、任务与业务模型。

---

## 🧱 技术栈

- **后端**：Python、FastAPI、Celery、PostgreSQL、Redis、LLM 服务提供商  
- **前端**：Next.js（App Router）、TypeScript、组件化 UI

---

## 🚀 快速开始

### 后端

```bash
cd backend

# 创建并激活虚拟环境（以 venv 为例）
python -m venv .venv
source .venv/bin/activate  # Windows 上为 .venv\Scripts\activate

# 安装依赖
uv sync  # 或：pip install -e .

# 启动 API 服务
python main.py
```

通过环境变量（如 `.env` 文件）配置：

- **PostgreSQL** / **Redis** 连接
- **LLM 服务** API Key
- **认证 / 安全** 配置（JWT 密钥等）

### 前端

```bash
cd frontend
pnpm install
pnpm dev
```

Next.js 开发服务器通常运行在 `http://localhost:3000`。  
请通过 `NEXT_PUBLIC_API_URL` 等环境变量配置前端所连接的后端 API 地址。

---

## 📄 许可协议

本项目基于 **Apache License 2.0** 开源，详情见 [Apache License, Version 2.0](./LICENSE). 文件。