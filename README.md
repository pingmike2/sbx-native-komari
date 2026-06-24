# Sbx Native

本仓库提供不同运行环境的 sing-box native 启动器，用于部署 VMess Ws + Argo、VLESS Reality、Hysteria2、TUIC、AnyTLS、SOCKS5 等代理；Komari agent 可选按官方安装脚本接入。

请选择对应环境查看说明：

| 环境 | 说明文档 | 入口文件 |
| --- | --- | --- |
| Java | [JAVA.md](JAVA.md) | [java/src/main/java/dev/sbxnative/App.java](java/src/main/java/dev/sbxnative/App.java) |
| Node.js | [NODE.md](NODE.md) | [nodejs/index.js](nodejs/index.js) |
| Python | [PYTHON.md](PYTHON.md) | [pyhton/app.py](pyhton/app.py) |

## 环境变量

| 变量 | 默认值 | 说明 |
| --- | --- | --- |
| `UPLOAD_URL` | 空 | Merge-sub 上传地址。填写后可上传订阅或节点。 |
| `PROJECT_URL` | 空 | 项目公网 URL。用于上传订阅和自动保活。 |
| `AUTO_ACCESS` | `false` | 设置为 `true` 时向保活服务提交 `PROJECT_URL`。 |
| `YT_WARPOUT` | `false` | 设置为 `true` 时强制 YouTube 走 WARP 出站规则。 |
| `FILE_PATH` | 依运行环境而定 | 运行目录，存放动态库、配置、订阅和临时文件。 |
| `SUB_PATH` | `sub` | HTTP 订阅路径，例如 `/sub`。 |
| `UUID` | 固定 UUID | 节点 UUID。建议自行修改。 |
| `KOMARI_SERVER` | 空 | Komari 面板地址，例如 `https://komari.example.com`。 |
| `KOMARI_PORT` | 空 | Komari 面板端口，可选；`KOMARI_SERVER` 已带端口时不用填。 |
| `KOMARI_KEY` | 空 | Komari agent token。 |
| `ARGO_DOMAIN` | 空 | Cloudflare 固定隧道域名。为空时使用临时隧道。 |
| `ARGO_AUTH` | 空 | Cloudflare tunnel token 或 TunnelSecret JSON。 |
| `ARGO_PORT` | `8001` | cloudflared 反代到本地的端口。 |
| `S5_PORT` | 空 | SOCKS5 入站端口。为空不启用。 |
| `TUIC_PORT` | 空 | TUIC 入站端口。为空不启用。 |
| `HY2_PORT` | 空 | Hysteria2 入站端口。为空不启用。 |
| `ANYTLS_PORT` | 空 | AnyTLS 入站端口。为空不启用。 |
| `REALITY_PORT` | 空 | VLESS Reality 入站端口。为空不启用。 |
| `CFIP` | 依运行环境而定 | VMess Argo 节点中的优选域名或 IP。 |
| `CFPORT` | `443` | `CFIP` 对应端口。 |
| `PORT` | `3000` | HTTP 订阅服务监听端口。 |
| `NAME` | 空 | 节点名称前缀。 |
| `CHAT_ID` | 空 | Telegram chat id。 |
| `BOT_TOKEN` | 空 | Telegram bot token。`CHAT_ID` 和 `BOT_TOKEN` 都存在才推送。 |
| `DISABLE_ARGO` | `false` | 设置为 `true` 时禁用 Argo/cloudflared。 |

## Komari Agent

设置 `KOMARI_SERVER` 和 `KOMARI_KEY` 后，程序会执行 Komari 官方安装脚本：

```bash
wget -qO- https://raw.githubusercontent.com/komari-monitor/komari-agent/refs/heads/main/install.sh | sudo bash -s -- -e <KOMARI_SERVER> -t <KOMARI_KEY>
```

如果环境中没有 `sudo`，会自动改用 `bash` 执行。`KOMARI_PORT` 仅在 `KOMARI_SERVER` 没有显式端口时追加。

## 目录结构

```text
.
├── java/
│   ├── pom.xml
│   └── src/main/java/dev/sbxnative/App.java
├── nodejs/
│   ├── index.js
│   └── package.json
├── pyhton/
│   ├── app.py
│   └── requirements.txt
├── JAVA.md
├── NODE.md
├── PYTHON.md
└── README.md
```

## 简要说明

- 请先确认端口在部署平台开放并未被占用。
- sing-box 版本由官方 1.13.13 正式版源码构建，公开透明，如有疑问，可以自行构建替换。
- Reality 会首次生成并持久化 `keypair.properties`，后续重启会复用同一对 key。
- HY2、TUIC、AnyTLS 会使用自签证书，客户端需要开启 `allow_insecure` 或等效选项。
- 请在符合当地法律法规和服务商规则的前提下使用。
