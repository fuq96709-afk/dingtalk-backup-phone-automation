# 安装、配对与接入

## Mac 和安卓

1. 从 [Droidline Releases](https://github.com/KnifeLemon/Droidline/releases) 下载 Mac 的 `darwin_arm64` 版本和对应安卓 APK。参考[官方安装说明](https://droidline.dev/docs/install/)安装。
2. 在手机安装 Agent，按应用引导启用控制所需的无障碍服务。首次验证让 Mac 和手机处于同一可互访的 Wi-Fi。此接法无需 ADB、USB 调试或 root。
3. 在 Mac 启动服务，保留状态目录。手机端按配对向导连接 Mac；具体流程见[官方快速开始](https://droidline.dev/docs/quick-start/)。

```sh
DROIDLINE="$HOME/.local/bin/droidline"
DROIDLINE_STATE="$HOME/.local/share/droidline-work"
"$DROIDLINE" --home "$DROIDLINE_STATE" serve
```

服务运行时在另一个终端使用同一程序路径和状态目录：

```sh
"$DROIDLINE" --home "$DROIDLINE_STATE" devices
"$DROIDLINE" --home "$DROIDLINE_STATE" --device DEVICE_ID current
"$DROIDLINE" --home "$DROIDLINE_STATE" --device DEVICE_ID screenshot /tmp/droidline-screen.png
```

把 `DEVICE_ID` 替换为设备列表中的稳定 ID。右侧 Inspector 是否可用取决于是否启动该服务。浏览器页面、实时截图和操作工具的可用性应分别验证；`127.0.0.1` 指打开页面的那台机器。

## Codex、Hermes 和个人手机

- **Codex**：按 [Droidline 的 MCP 接入说明](https://droidline.dev/docs/mcp/)添加本机 Droidline，确保指向同一状态目录。依次验证设备列表、截图、打开安卓设置。工具列表中没有点击动作时，界面可读但无法仅靠该 MCP 导航。
- **个人手机**：可尝试用 ChatGPT App 的远程连接作为入口，通过 Mac 上的 Codex 操作工作手机。个人手机连接 Mac 与工作手机连接 Droidline 是两条独立链路。历史测试中手机端与 Mac 的 Codex 远程配对未完成。
- **Hermes + 微信**：链路是个人微信 → Hermes 网关 → Droidline MCP → 工作手机。收到微信回复只证明第一段可用。历史测试中网关可收消息，MCP 能做部分读取，但 Hermes 未完成考勤导航。先验证私聊发送者白名单，再逐项检查读取、唤醒、打开应用及点击工具是否可用。仅在使用者授权后开放对应动作。模型返回 `HTTP 404: Model not exist` 时，先核对模型 ID 与实际服务提供商。
- **WorkBuddy**：可以保留现有连接。安排自动化时避免两个助手同时控制一个界面。

## 连接失败怎么查

| 现象 | 先检查 |
| --- | --- |
| MCP 报 EOF 或 broken pipe | 用同一状态目录单独跑 `devices`。旧版实测出现过 MCP 传输提前关闭，CLI 仍可用。 |
| CLI 查到设备离线 | 确认 Mac 服务仍在运行、手机仍在原 Wi-Fi、Agent 无障碍与后台活动仍可用。先等已有配对恢复。 |
| 有设备但截图黑 | 检查是否熄屏或锁屏。唤醒不等于解锁，锁屏验证由使用者完成。 |
| 定时任务没有按点运行 | 对照 Mac 睡眠/唤醒时间、Codex 运行记录、网络或 VPN 连通性、设备在线状态，逐段定位。历史上 Mac 睡眠曾推迟触发。 |
