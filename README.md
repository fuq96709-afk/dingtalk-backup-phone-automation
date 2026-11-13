# 钉钉 备用机控制自动化 打卡流程

这份中文教程记录 Apple Silicon Mac、安卓工作手机与 Codex 的实测接法，包含钉钉考勤案例。配套的 [Codex Skill](skills/droidline-phone-control/SKILL.md) 可以复用设备检查、界面操作和结果核验流程。

- [安装、配对与接入](skills/droidline-phone-control/references/setup.md)
- [钉钉上下班打卡与定时排查](skills/droidline-phone-control/references/attendance.md)

要在 Codex 中使用，将整个 `skills/droidline-phone-control` 文件夹复制到项目的 `.agents/skills/` 下。开启对话后可输入 `$droidline-phone-control`，先让它查询手机状态或打开安卓设置。Skill 是操作指南，实际控制依赖已安装并配对的 Droidline。

历史实测使用 Droidline v0.1.11。按你安装的版本核对命令参数；手机界面和考勤规则以实时显示为准。

本仓库的教程与 Skill 采用 [MIT 许可证](LICENSE)。Droidline 是 [KnifeLemon 的独立项目](https://github.com/KnifeLemon/Droidline)，安装包请从上游获取。
