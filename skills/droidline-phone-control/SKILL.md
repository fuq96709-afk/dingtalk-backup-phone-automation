---
name: droidline-phone-control
description: 使用已配对的 Droidline 检查安卓设备在线状态、读取屏幕、操作应用和核实结果。适用于从 Mac 控制安卓手机、排查 Codex 或 Hermes 的 Droidline 接入，以及按用户授权操作钉钉考勤。
---

# Droidline 手机操作

- 先确认目标设备。用设备列表中的稳定 ID，配对码只用于首次配对。
- 优先使用已连接的 Droidline MCP；若报 EOF、broken pipe 或缺少所需工具，使用已安装的官方 CLI，保留同一状态目录。先用设备列表区分 MCP 故障和设备离线。
- 读取当前应用、界面结构及必要截图，再决定点击目标。界面树缺少控件时才用当前截图定位。黑屏先核实亮屏和锁屏状态。
- 工作手机同时连接 WorkBuddy 等工具时，同一时间只由一端操作。发现界面被另一端持续切换就停止并报告。
- 打开应用和提交记录是不同动作。仅在用户授权了提交时点击最终按钮；提交结果不明时先读取记录，避免重复操作。

初次配置或连接故障时读 [安装、配对与接入](references/setup.md)。处理考勤或安排定时执行时读 [考勤流程](references/attendance.md)。
