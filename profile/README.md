# BetterTIA

Tools that let an AI assistant work with Siemens TIA Portal V21 through the Openness API: read a project,
change it in small reviewed steps, draw the change before it is made and watch the result on the running PLC.

| Repository | What it is |
|---|---|
| [reader](https://github.com/BetterTIA/reader) | Read-only MCP server: project tree, export of blocks, tags and WinCC Unified screens to a folder, cross-references. Fork of [Czarnak/tia-portal-mcp](https://github.com/Czarnak/tia-portal-mcp). |
| [writer](https://github.com/BetterTIA/writer) | MCP server with write tools: batch renames, network texts, member renames, WinCC Unified tags and screens, fail-safe impact checks. Fork of [heilingbrunner/tiaportal-mcp](https://github.com/heilingbrunner/tiaportal-mcp). |
| [editor](https://github.com/BetterTIA/editor) | Local web app that renders a LAD or FBD network from the export, lets you compose a change and tracks it from proposal to tested. |
| [watch](https://github.com/BetterTIA/watch) | Read-only MCP server for live values from a running TIA Portal: PLC online state, actual values of data blocks, a capture of a monitored watch table, tag table or block. It never writes values to the PLC. |

## How the four fit together

1. The **reader** exports the project to text (`.s7dcl` / `.s7res`). It never writes.
2. A change is proposed and reviewed, for a single network in the **editor**.
3. The **writer** applies it in one small batch. Changes stay in memory until the project is saved.
4. The **reader** exports again and the result is compared with what was approved.
5. After the change is compiled and downloaded by a person, **watch** shows the live values on the PLC. It only reads.

Only one tool writes; the others read and check. Fail-safe (F) blocks are handled by hand, one named block at a time.
Compiling the safety program and downloading to the PLC stay in the hands of a person; watch goes online
only to an allowed address.

## Requirements

- Windows with **Siemens TIA Portal V21** and TIA Portal Openness V21; the user must be in the
  "Siemens TIA Openness" group.
- The MCP servers (reader, writer, watch) attach to a TIA Portal that is already running. The editor is a
  local web app and works on the exported text.

## Status

Work in progress, not a product. **Developed, used and tested only with TIA Portal V21.** Other versions
have not been tried; the Openness API differs between versions, so expect breakage there.
Each repository says what has been verified against a running TIA Portal and what has not.
Use it on a copy or an archived project.

TIA Portal, SIMATIC and WinCC are trademarks of Siemens AG. BetterTIA is not affiliated with or endorsed by
Siemens.
