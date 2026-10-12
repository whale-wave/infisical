# Infisical

使用 Docker Compose 部署 Infisical，连接已有 PostgreSQL 和 Redis。

## 配置

镜像版本、监听地址和端口固定在 `docker-compose.yaml`。Infisical 的访问地址、加密密钥、数据库和 Redis 连接配置保存在 `.env`，通过 `env_file` 注入容器；模板见 `.env.example`，真实 `.env` 不提交 Git。

填写实际 PostgreSQL 和 Redis 的地址、端口、数据库及认证信息。模板使用标准端口 `5432`、`6379`；Redis 逻辑数据库需为 Infisical 单独预留。连接串中的密码需要 URL 编码。

`SITE_URL` 填写实际访问地址。已有数据库迁移时应沿用原加密密钥。

## 启动

首次部署，在仓库目录复制模板并填写配置；已有 `.env` 时直接使用：

```sh
cp .env.example .env
chmod 600 .env
```

配置好后启动：

```sh
docker compose up -d
```

默认仅允许宿主机通过 http://localhost:8081 访问。对外提供服务时，可由反向代理转发到该地址，并设置对应的 `SITE_URL`。

## 停止

```sh
docker compose down
```

此命令只停止 Infisical，不管理外部 PostgreSQL 和 Redis。
