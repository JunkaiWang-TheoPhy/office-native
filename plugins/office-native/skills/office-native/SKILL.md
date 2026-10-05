---
name: office-native
description: Route native or in-place edits of Word, PowerPoint, Excel, WPS, and Google Sheets documents through a connected document session, desktop app, provider API, or local Office file tools. Use when the user wants to edit the open document or explicitly asks for MCP, CLI, or Computer Use.
---

# Office Native

Identify the user's actual source of truth before editing. A local Office file, an open desktop document, and a cloud document may have the same title but are different targets. Honor an explicit app, format, and destination.

## Choose the route

1. **Connected live document.** If Codex Document Control is available and the request concerns an open Word, PowerPoint, Excel, or Google Sheets document, list document sessions. Select the exact document and surface, fetch the supported tool schemas, then execute only supported commands. Read the document again to verify the result. An available tool with no connected session is not a live editing route.
2. **Desktop app without a structured session.** If Computer Use is available, select the exact Word, PowerPoint, Excel, or WPS window. Inspect its current state, make the requested edit in that app, and verify the changed object in the app. Prefer a structured document connection when both routes can do the job. Never edit a different open document merely because it is in the foreground.
3. **Cloud-native document.** Use an authorized provider connector or MCP that supports edits to the named document. Confirm the document identity and verify the remote result. Do not silently substitute an exported Office copy for a requested live cloud edit.
4. **Local `.docx`, `.pptx`, or `.xlsx`.** Use a format-aware document, presentation, or spreadsheet workflow available in the host; for example, installed Office artifact skills or existing OOXML libraries. Edit the intended file, reopen it to check its structure and values, and inspect a render of affected pages, slides, or sheets. LibreOffice `soffice` can help render or convert when installed; conversion alone is not content editing.

## Completion boundary

Report the route actually used, the file or live document changed, and the verification performed. Say when a requested live route was unavailable. This skill contains routing instructions only: it does not ship an MCP server, Office add-in, application, CLI binary, or connector credentials. Do not install one or broaden app permissions without task authorization.
