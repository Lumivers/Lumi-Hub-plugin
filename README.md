# Lumi-Hub 交互终端

> 🌟 跨平台私有化 Agent 交互终端与消息路由中枢 · AstrBot 平台适配器插件

[![GitHub](https://img.shields.io/badge/GitHub-Lumivers%2FLumi--Hub--plugin-blue?logo=github)](https://github.com/Lumivers/Lumi-Hub-plugin)
[![AstrBot](https://img.shields.io/badge/AstrBot-%3E%3D4.16-green)](https://github.com/AstrBotdevs/AstrBot)

---

## 简介

本插件是 [Lumi-Hub](https://github.com/Lumivers/Lumi-Hub) 项目的 AstrBot 端适配器，作为 **自定义消息平台** 接入 AstrBot，将 Lumi-Hub Flutter 客户端与 AstrBot LLM 引擎全链路打通。

- **Host 端（本插件）**：运行在 AstrBot 中，作为自定义平台适配器，负责 WebSocket Server、消息路由与 MCP 工具执行。
- **Client 端（Flutter 应用）**：由用户自行下载安装，提供跨平台聊天界面（Windows 桌面端，后续规划 Android/macOS）。

> **本项目不是通用 IM 平台桥接插件**，而是一套完整的私有化 Agent 交互框架的服务端组件。

---

## 功能特性

- **WebSocket 通信桥梁**：启动内置 WebSocket Server，承接 Flutter 客户端连接，将消息以标准 AstrBot 平台消息形式提交给 LLM 引擎。
- **流式响应转发**：实时将 AstrBot 的 LLM 流式回复透传至客户端，实现打字机动效体验。
- **双轨制工具执行**：
  - 🏃 **原生轨**：直接在 Host 进程内执行高频文件操作（读/写/搜索替换），0 延迟响应。
  - 🔌 **MCP 轨**：内置原生 MCP Client，直接挂载各类 MCP Server（MySQL、Docker、GitHub 等标准生态）。
- **人工审批拦截（HitL）**：高危操作在执行前挂起，通过 Client 端弹出审批界面，等待用户手动确认。
- **灾备缓存**：任何文件写操作前强制备份至 `.Lumi_cache/`，若备份失败则中止操作（Fail-Safe）。
- **人格管理**：与 AstrBot 数据库同步人格列表，支持前端直接修改 System Prompt。
- **MCP 热重载**：支持通过 WebSocket 接口实时更新 MCP 配置，无需重启。
- **账户鉴权**：接入 SQLite 数据库实现连接鉴权与会话隔离。

---

## 安装与使用

### 方式一：通过 AstrBot 插件市场安装（推荐）

在 AstrBot WebUI 的插件市场中搜索 `lumi-hub-plugin` 或 `Lumi-Hub-plugin` 即可一键安装。

### 方式二：手动安装

```bash
# 进入 AstrBot 插件目录
cd <你的AstrBot路径>/data/plugins

# 克隆本仓库
git clone https://github.com/Lumivers/Lumi-Hub-plugin.git lumi_hub
```

### 配置说明

插件安装后会在 AstrBot Data 目录下自动创建配置文件。首次使用需在 AstrBot WebUI 的插件配置页填写：

| 参数 | 说明 |
|------|------|
| `ws_host` | WebSocket 监听地址（默认 `0.0.0.0`） |
| `ws_port` | WebSocket 监听端口（默认 `8765`） |

---

## 配套客户端

客户端（Flutter 桌面应用）请前往主仓库下载：

👉 **[Lumi-Hub 主仓库 Releases](https://github.com/Lumivers/Lumi-Hub/releases)**

> **⚠️ 注意**：当前 Beta 阶段，客户端仅支持连接 **本机** 的 AstrBot（即 AstrBot 本体必须与客户端运行在同一台电脑上）。

---

## 系统要求

- **AstrBot** `>= 4.16`
- Python 依赖见 `requirements.txt`（AstrBot 会自动安装）

---

## 相关链接

- [Lumi-Hub 主仓库](https://github.com/Lumivers/Lumi-Hub)（含 Flutter 客户端）
- [AstrBot 官网](https://astrbot.app)
- [问题反馈 / Issues](https://github.com/Lumivers/Lumi-Hub-plugin/issues)

---

## 许可证

本项目与主仓库保持相同许可证。**仅供个人学习与合法用途，严禁用于任何违法违规活动。**
