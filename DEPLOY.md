# Infinite Canvas 部署指南

## 快速开始（Docker Compose）

```bash
# 1. 构建并启动
docker compose up -d --build

# 2. 访问
# http://你的服务器IP
# （Nginx 默认监听 80 端口）
```

启动后在网页左下角设置 API Key 即可使用。

## 直接端口访问（不需要 Nginx）

编辑 `docker-compose.yml`，注释掉 nginx 服务，取消 app 的 ports 注释：

```yaml
services:
  app:
    build: .
    container_name: infinite-canvas
    restart: unless-stopped
    environment:
      - PORT=3000
      - DATA_ROOT=/app/data_root
    volumes:
      - app_data:/app/data_root
    ports:
      - "3000:3000"

volumes:
  app_data:
```

然后：
```bash
docker compose up -d --build
# 访问 http://你的服务器IP:3000
```

## 不用 Docker 直接运行

```bash
pip install -r requirements.txt
python main.py
# 访问 http://localhost:3000
```

## 数据持久化

所有用户数据（画布、素材、生成的图片、API 配置）存储在 Docker volume `app_data` 中。

- `docker compose down` — 数据保留
- `docker compose down -v` — **删除所有数据**（慎用）

## 环境变量

| 变量 | 默认值 | 说明 |
|------|--------|------|
| `PORT` | `3000` | 服务端口 |
| `DATA_ROOT` | 程序目录 | 数据存储根目录 |
| `API_KEY` | - | API 密钥 |
| `API_BASE_URL` | - | API 请求地址 |
| `MODELSCOPE_API_KEY` | - | ModelScope 密钥（免费生成） |
| `COMFYUI_INSTANCES` | `127.0.0.1:8188` | ComfyUI 地址 |
| `PUBLIC_BASE_URL` | - | 公网访问地址 |

也可以在 Web 界面左下角的设置面板中配置 API。

## HTTPS 配置

在 Nginx 前加一层（如 Cloudflare、Caddy），或修改 `nginx.conf` 添加 SSL 证书配置。
