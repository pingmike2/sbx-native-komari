# Node Sbx Native

这是一个 Node.js 项目，用于下载并加载 `bot.so`、`sbx.so` 和 `v1.so` 的配置启动方式。

## 使用说明

1. 进入项目目录：

   ```bash
   cd node-sbx
   ```

2. 安装依赖：

   ```bash
   npm install
   ```

3. 配置环境变量或修改 `.env或 直接export 命令定义`

   - `ARGO_DOMAIN` / `ARGO_AUTH`：启用 cloudflared 固定隧道模式
   - `NEZHA_SERVER` / `NEZHA_KEY`：启用 nezha-agent
   - `FILE_PATH`：运行时文件目录，默认为 `.mpm`

4. 启动：

   ```bash
   npm start
   ```

## 说明

- 该项目会从 `download.baseUrl` 下载三份 `.so` 文件
- 通过 `ffi-napi` 加载本机库中的 `Start*` 和 `Stop*` 函数
- 运行后按 `Ctrl+C` 停止并依次调用停止函数

## 注意

- 需要在 Linux/x86_64 或对应平台上运行，以便加载 `.so` 库
- 如果当前系统是 Windows，则无法直接加载 `.so`
- `sing-box` 和 `nezha-agent` 仍然需要各自的配置文件，如果启动失败,检查环境变量配置