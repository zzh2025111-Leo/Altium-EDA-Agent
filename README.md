# Altium EDA Agent

嵌入 Altium Designer 的脚本化 EDA Agent，通过 DelphiScript / Pascal 脚本桥接 MCP（Model Context Protocol），让 AI 助手能够直接读取、修改、审查和生成 Altium 原理图与 PCB 设计。

## 项目概述

本项目是一组 Altium Scripting 项目（`.PrjScr`）与 Pascal 单元，运行在 Altium Designer 内部，作为 AI 辅助硬件设计的本地服务端。它把 Altium 的 PCB、SCH、库、规则、ERC/DRC 等能力封装成结构化接口，供外部 MCP 客户端调用。

## 目录结构

| 文件 | 说明 |
|------|------|
| `Altium_API.PrjScr` | Altium 脚本项目入口 |
| `Main.pas` | MCP 服务主循环与消息处理 |
| `Application.pas` | Altium 应用层封装（文档、窗口、状态等） |
| `Project.pas` | 项目级操作（打开、编译、ERC、变体、BOM 等） |
| `PCB.pas` | PCB 操作（布局、走线、规则、铺铜、DRC 等） |
| `PCBGeneric.pas` | PCB 通用几何与对象操作 |
| `Library.pas` | SchLib / PcbLib 库操作 |
| `Audit.pas` | 设计审查与可制造性检查 |
| `Generic.pas` | 通用对象查询与修改 |
| `Dispatcher.pas` | MCP 请求分发与工具路由 |
| `Utils.pas` | 通用工具函数 |
| `SelfTest.pas` | 自检与冒烟测试 |
| `StatusForm.dfm / StatusForm.pas` | 运行状态窗口 |
| `History/` | Altium 本地历史备份（可忽略） |

## 运行方式

1. 在 Altium Designer 中打开 `Altium_API.PrjScr`。
2. 运行 `StartMCPServer` 过程启动 MCP 服务。
3. 外部 MCP 客户端通过文件/本地通道与服务通信。
4. 服务响应 MCP 工具调用，执行对应的 Altium 操作。

## 典型应用场景

- 让 AI 读取原理图/PCB 网表并检查连接问题
- 自动生成/修改元件参数、封装、BOM
- 批量放置元件、布线、生成 Gerber/STEP
- 运行 DRC/ERC 并解释违规项
- 根据自然语言需求辅助生成电路方案

## 开发说明

- 语言：DelphiScript / Object Pascal（Altium Designer 脚本环境）
- 运行环境：Altium Designer 18 及以上（建议 24+）
- 通信方式：基于本地文件的 MCP 轮询桥
- 注意：部分工具会触发 Altium 模态对话框，不适合完全无人值守运行

## 免责声明

本项目为个人学习与 AI 辅助硬件开发使用。直接操作 Altium 设计的脚本具有破坏性，请在运行前备份项目。
