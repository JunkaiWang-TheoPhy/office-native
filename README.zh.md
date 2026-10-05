<p align="center"><a href="README.md">🇺🇸 English</a> | <a href="README.zh.md">🇨🇳 中文</a></p>

<h1 align="center">Office Native</h1>

<p align="center">
  <a href="LICENSE"><img alt="许可协议：Apache-2.0" src="https://img.shields.io/badge/license-Apache--2.0-blue"></a>
  <a href="plugins/office-native/plugin.json"><img alt="插件版本：0.1.0" src="https://img.shields.io/badge/plugin-0.1.0-green"></a>
</p>

![从终端直达可编辑文档选区的路径](assets/banner.png)

## 引言

Office Native 是一个帮助 Codex 选对编辑对象的技能。它会先区分已连接的实时文档、桌面应用中打开的文档、云端文档和本地 Office 文件，再执行修改。这样就不会把新生成的副本误报为屏幕上的原文档已更新。

## 功能

| 实际编辑对象 | 可用时采用的路径 | 验证方式 |
| --- | --- | --- |
| 已连接的 Word、PowerPoint、Excel 或 Google Sheets 会话 | Codex Document Control 及该会话支持的命令 | 重新读取实时文档 |
| 桌面应用中打开的文档，包括 WPS | 在准确的应用窗口中使用 Computer Use | 在应用中检查修改后的对象 |
| 云端原生文档 | 已授权的服务连接器或 MCP | 重新读取远端文档 |
| 本地 `.docx`、`.pptx` 或 `.xlsx` | 理解文件格式的编辑工具 | 重新打开文件并检查渲染结果 |

本技能**只提供操作指引**，不附带 MCP 服务器、Office 加载项、应用程序、命令行工具或凭据。每条路径都取决于使用者的 Codex 环境中已经接入的能力。

## 安装

若要通过桌面插件使用，先把本仓库添加为插件来源：

```bash
codex plugin marketplace add JunkaiWang-TheoPhy/office-native
```

随后在 ChatGPT 桌面应用中，从该来源安装 **Office Native**。仓库包含可移植插件清单和仓库级插件目录。发布到 GitHub 不等于已上架 OpenAI 的通用公开插件目录。

若只想安装技能，可让 `$skill-installer` 从本仓库的 [`plugins/office-native/skills/office-native`](plugins/office-native/skills/office-native/SKILL.md) 安装，也可以把这个文件夹复制到个人 Codex 技能目录。

## 使用

在请求中指出真正要修改的文档：

```text
用 $office-native 修改我当前打开的 PowerPoint 第 8 张幻灯片。其余幻灯片保持不变，并在 PowerPoint 中核对结果。
```

```text
用 $office-native 修改当前 WPS 演示文稿里选中的图表。编辑前先核对应用窗口。
```

```text
用 $office-native 更新这个本地 XLSX 文件里的公式。保存后重新打开工作簿，检查受影响的工作表。
```

## 边界

能看到 MCP 工具，不代表已有文档会话连接。Computer Use 修改它操作的应用，文件工具修改磁盘上的文件。LibreOffice 格式转换可以辅助核对渲染，但转换本身不等于内容编辑。技能会说明实际使用的路径，以及所请求的实时路径是否可用。

## 许可

仓库中的技能、插件元数据、文档和横幅均以 [Apache-2.0](LICENSE) 发布。
