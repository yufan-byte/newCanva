# Infinite Canvas - 豫帆智能科技

AI 多模态创作工作站 | 支持 ComfyUI / API / ModelScope

---

## 功能概览

### 🎨 AI 图像生成
- 支持几乎所有 OpenAI 协议的 API / 异步协议 / Gemini 协议 / 方舟协议
- RunningHub 工作流 / AI 应用 / 收费模型调用
- 火山引擎调用
- ModelScope 免费 LLM 模型和图像模型调用
- 即梦 CLI 调用（文生图 / 图生图 / 文生视频 / 图生视频）
- 支持调用本地局域网的 ComfyUI

### 🖼️ 图像处理
- 图片扩展 / 细节增强
- 360° 全景图预览截图
- 视频帧抽取
- 循环节点等高级功能

### 💬 AI 对话
- 多模型 Chat 对话
- Agent 智能体模式
- 图片理解与生成

### 📦 素材管理
- 素材库分类管理
- Chrome 批量采集插件
- Photoshop 直连画布插件

### 🔒 权限认证
- JWT + HTTP-only Cookie 安全认证
- 管理员账号管理（添加 / 删除用户）
- 环境变量配置初始管理员
- 支持一键关闭认证（开发调试）

### 🔄 一键更新
- 自动检测 GitHub / ModelScope 新版本
- 一键更新 + 自动重启
- 更新前自动备份，支持回滚

### 🎯 无限画布
- 自由拖拽、缩放的无限画布
- 多图层管理
- 实时协作

---

## 快速开始

### 环境要求

- Python 3.10+
- pip

### 安装依赖

```bash
pip install -r requirements.txt
```

### 启动服务

```bash
# 带认证启动（推荐）
AUTH_ENABLED=true ADMIN_USER=admin ADMIN_PASSWORD=你的密码 python main.py

# 关闭认证（开发调试）
AUTH_ENABLED=false python main.py
```

启动后访问 http://localhost:3000

### 环境变量说明

| 变量 | 默认值 | 说明 |
|------|--------|------|
| `PORT` | `3000` | 服务端口 |
| `AUTH_ENABLED` | `true` | 是否启用登录认证 |
| `ADMIN_USER` | - | 初始管理员用户名（首次启动时创建） |
| `ADMIN_PASSWORD` | - | 初始管理员密码 |
| `JWT_SECRET` | 自动生成 | JWT 签名密钥，生产环境建议固定设置 |
| `DATA_ROOT` | 程序目录 | 数据存储根目录 |

---

## Docker 部署

```bash
docker-compose up -d
```

Docker 部署时，通过环境变量配置管理员账号：

```yaml
# docker-compose.yml
services:
  app:
    build: .
    environment:
      - PORT=3000
      - AUTH_ENABLED=true
      - ADMIN_USER=admin
      - ADMIN_PASSWORD=your-secure-password
```

---

## API 配置

启动后在界面左下角「API 设置」中配置：

- **OpenAI 兼容 API**：支持大部分第三方 API 服务
- **ComfyUI**：本地或远程 ComfyUI 实例
- **RunningHub**：云端 ComfyUI 工作流
- **ModelScope**：免费模型调用
- **即梦**：字节跳动 AI 图像/视频生成

---

## 项目结构

```
├── main.py                 # 后端服务（FastAPI）
├── requirements.txt        # Python 依赖
├── VERSION                 # 版本号
├── Dockerfile              # Docker 构建文件
├── docker-compose.yml      # Docker Compose 配置
├── static/                 # 前端资源
│   ├── index.html          # 主页面
│   ├── login.html          # 登录页
│   ├── admin.html          # 账号管理页
│   ├── canvas.html         # 无限画布
│   ├── gpt-chat.html       # AI 对话
│   ├── zimage.html         # 文生图
│   ├── js/                 # JavaScript
│   └── vendor/             # 第三方库
├── workflows/              # ComfyUI 工作流
├── data/                   # 运行时数据（自动生成）
└── tools/                  # 辅助工具
    ├── chrome-local-asset-importer/  # Chrome 素材采集插件
    └── photoshop-asset-connector/    # Photoshop 插件
```

---

## 更新日志

### v2026.06.22
- ✨ 新增 JWT + Cookie 登录认证系统
- ✨ 新增账号管理页面（管理员可添加/删除用户）
- ✨ 支持通过环境变量配置初始管理员
- 🐛 修复若干已知问题

### v2026.06.17
- 🎉 初始开源版本

---

## 技术栈

- **后端**：Python / FastAPI / Uvicorn
- **前端**：原生 HTML/CSS/JS / Tailwind CSS / Three.js
- **存储**：JSON 文件（无数据库依赖）
- **认证**：JWT / bcrypt / HTTP-only Cookie

---

## 许可协议

已经申请著作权，禁止商业用途。

Commercial use is prohibited.

- 可以自己使用和公司使用，禁止用于任何形式的修改封装成商业产品，商用须取得授权
- 根据代码二次开发的软件必须保持开源并注明来源作者
- This software is for personal and company use only. Commercial use requires authorization
- Software developed based on this code must remain open source and the original author must be credited

---

## 联系方式

- B站：https://space.bilibili.com/78652351
- GitHub：https://github.com/yufan-byte/newCanva
