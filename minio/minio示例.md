
## 编排

```sh
services:
  minio:
    image: pgsty/minio:latest
    container_name: minio
    ports:
      - "9000:9000"
      - "9001:9001"
    environment:
      - MINIO_ROOT_USER=${MINIO_ROOT_USER:-minioadmin}
      - MINIO_ROOT_PASSWORD=${MINIO_ROOT_PASSWORD:-123456}
    volumes:
      - ./data:/data
    command: server /data --console-address ":9001"
    restart: unless-stopped

```

## 运行示例

```shelll
# 1. 创建数据目录（如果还没有）
mkdir -p data

# 2. （可选）创建 .env 文件设置密码，避免写在命令行
# echo "MINIO_ROOT_PASSWORD=your-strong-password" > .env

# 3. 启动服务
docker compose up -d

# 取消
docker compose down

# 4. 查看日志确认启动成功
docker compose logs -f

```

## 常见问题

### 1. 未定义变量

```sh
# MINIO_ROOT_USER
```