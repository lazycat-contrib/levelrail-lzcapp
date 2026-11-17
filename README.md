# Levelrail 懒猫微服打包（LPK）

[Levelrail](https://github.com/glincker/levelrail)（Apache-2.0）的懒猫微服 LPK 打包仓库。Levelrail 是一个轻量级自托管部署平台：git push 即部署到自己的服务器，自带构建队列、回滚、预览环境、托管数据库与内置可观测性，单 Go 二进制、无需 Kubernetes。

本仓库为**镜像模式**打包：直接复用上游官方镜像 `ghcr.io/glincker/levelrail`，由 GitHub Actions（[ca-x/lazycat-github-action](https://github.com/ca-x/lazycat-github-action)）每日跟随上游 stable tag（`^v\d+\.\d+\.\d+$`）自动复制镜像并发布到喵喵商店。不存储上游源码。

## 首次使用

1. 安装后打开应用，登录账号 `levelrail`，密码见安装时的部署参数说明（由平台稳定密钥生成）。
2. Levelrail 通过 Docker socket 管理宿主容器（`compose_override` 挂载 `/var/run/docker.sock`），仅应授权可信管理员使用；应用已设置 `admin_only`。
3. 数据（SQLite、master.key、生成配置）持久化在应用数据目录 `/lzcapp/var/data`。
4. 应用内置 Caddy 边缘入口监听 80/443；在懒猫微服网关下 Levelrail 自身的 Let's Encrypt HTTPS 不可用，部署的应用请通过懒猫域名或内网地址访问。

## 说明

- `min_os_version: 1.5.0`（LPK v2）
- 图标来自上游品牌资源 `docs/assets/brand/levelrail-default.svg`，转为 512x512 PNG
- 请勿在应用内执行自更新，版本跟随由 CI 维护
