<p align="center"><a href="README.md">🇺🇸 English</a> | <a href="README.zh.md">🇨🇳 中文</a></p>

<h1 align="center">Office Native</h1>

<p align="center">
  <a href="LICENSE"><img alt="License: Apache-2.0" src="https://img.shields.io/badge/license-Apache--2.0-blue"></a>
  <a href="plugins/office-native/plugin.json"><img alt="Plugin version: 0.1.0" src="https://img.shields.io/badge/plugin-0.1.0-green"></a>
</p>

![A direct path from a terminal to the selected object in an editable document](assets/banner.png)

## Introduction

Office Native is a Codex skill that chooses the document the user actually wants to edit. It distinguishes a connected live document, an open desktop app, a cloud document, and a local Office file before making changes. This avoids treating a newly generated copy as if it had updated the document on screen.

## What it does

| Source of truth | Route when available | Verification |
| --- | --- | --- |
| Connected Word, PowerPoint, Excel, or Google Sheets session | Codex Document Control and its supported commands | Read the live document again |
| Open desktop document, including WPS | Computer Use in the exact app window | Inspect the changed object in the app |
| Cloud-native document | Authorized provider connector or MCP | Read the remote document again |
| Local `.docx`, `.pptx`, or `.xlsx` | Format-aware file tools | Reopen the file and inspect a render |

The skill is **instruction-only**. It does not include an MCP server, Office add-in, application, CLI binary, or credentials. Each route depends on the capabilities already connected to the user's Codex environment.

## Install

For the desktop plugin route, add this repository as a marketplace source:

```bash
codex plugin marketplace add JunkaiWang-TheoPhy/office-native
```

Then install **Office Native** from that marketplace in the ChatGPT desktop app. The repository contains a portable plugin manifest and a repository marketplace entry. This GitHub publication does not list the plugin in OpenAI's universal public directory.

For a skill-only installation, ask `$skill-installer` to install [`plugins/office-native/skills/office-native`](plugins/office-native/skills/office-native/SKILL.md) from this repository. You can also copy that folder into your personal Codex skills directory.

## Use

Try a prompt that identifies the source of truth:

```text
Use $office-native to update slide 8 in the PowerPoint presentation I have open. Keep the other slides unchanged and verify the result in PowerPoint.
```

```text
Use $office-native to change the selected chart in my open WPS presentation. Inspect the current window before editing.
```

```text
Use $office-native to update the formulas in this local XLSX file. Save the edited workbook, reopen it, and inspect the affected sheet.
```

## Boundaries

An available MCP tool does not imply that a document session is connected. Computer Use changes the app it controls; file tools change a file on disk. LibreOffice conversion can help verify rendering but does not itself edit content. The skill reports which route was actually used and when the requested live route was unavailable.

## License

The skill, plugin metadata, documentation, and banner in this repository are released under [Apache-2.0](LICENSE).
