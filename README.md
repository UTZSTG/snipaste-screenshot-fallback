# Snipaste Screenshot Fallback

当 Windows 内置窗口捕获出现 `FrameArrived timed out`，或 Citrix 等远程桌面画面无法获取时，供 AI 助手参考的 Snipaste 截图回退 skill。

## 工作方式

确认前台目标窗口 → 使用已有 Snipaste 保存 PNG → 等待完整落盘 → 读取新图片 → 核对目标画面 → 继续当前已授权任务。

包含异步落盘与旧截图检查、外部截图的坐标限制、远程终端粘贴后单独回车、临时文件清理和会话交接说明。详情见 [SKILL.md](SKILL.md)。

## 使用条件

- Windows 桌面已解锁，已安装并核实 Snipaste 路径。
- AI 助手具有当前任务允许的桌面工具、命令执行和本地图像读取能力。
- 命令示例中的 `C:\Tools` 与 `C:\Work` 路径需要按实际环境修改。
- 此仓库提供操作指引，不包含 Snipaste 软件、电脑控制服务或截图数据。

## 安装与调用

将本仓库文件放入 `~/.codex/skills/snipaste-screenshot-fallback/`，确保该目录直接包含 `SKILL.md`。由客户端重新发现技能后，可在会话中输入：

```text
使用 $snipaste-screenshot-fallback 处理内置截图失败，先确认目标窗口，再继续已经授权的工作。
```

已有会话未发现该技能时，可直接提供本地 `SKILL.md` 的绝对路径让助手阅读。

## 范围与验证

这是截图回退方案，不是 Windows.Graphics.Capture 的底层修复，也不能保证锁屏、受保护画面或所有远程客户端可捕获。它不增加服务器修改、任务终止、数据删除或凭证访问权限；必须遵守当前工具规范与用户授权。

该流程来自实际 Windows/Citrix 使用经验；公开版的通用路径不代表已在每台设备验证。Skill 结构使用官方 `quick_validate.py` 检查。本仓库没有包含原使用环境的账号、服务器目录、项目记录或屏幕截图。
