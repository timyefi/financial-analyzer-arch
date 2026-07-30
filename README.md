# Financial Analyzer — 技术架构文档

> 作者：叶青 | 版本：v2.6.1 | 更新日期：2026-07-30

Financial Analyzer 是一套 **14 Agent × 5 阶段** 的企业年报附注优先财务分析引擎，
覆盖偿债能力、盈利运营、现金流杠杆、有息债务与融资成本全维度。

本仓库开源其 **技术架构文档与使用教程**（HTML），Skill 源码本身不在此仓库中。

## 📄 文档

| 文档 | 面向 | 内容 |
|------|------|------|
| [architecture.html](./architecture.html) | 集成者 / 二次开发者 | 分层架构、6 模块解耦、接口契约、集成模式 |
| [usage-guide.html](./usage-guide.html) | 分析师 / 信评研究员 | 手把手使用教程、Onboarding 定制、全流程实操 |

直接用浏览器打开即可阅读（自包含 HTML，无外部依赖，ECharts 通过 CDN 加载）。

## 🏗️ 架构概览

```
┌─────────────────────────────────────────────────┐
│  L4 · Customization (meta / onboarding)         │  ← 可跳过
├─────────────────────────────────────────────────┤
│  L3 · Orchestration (pipeline_state.py)         │  ← 可替换
├─────────────────────────────────────────────────┤
│  L2 · Analysis Engine (14 Agents + KnowledgeBase)│  ← 核心价值
├─────────────────────────────────────────────────┤
│  L1 · Data (多源下载器 + MinerU VLM 解析)        │  ← 可独立替换
├─────────────────────────────────────────────────┤
│  L0 · Infrastructure (Python / Excel / JSON)    │  ← 基础依赖
└─────────────────────────────────────────────────┘
```

依赖方向自上而下，任何一层都可单独摘出使用。

## 🔌 三种集成模式

- **模式 A · 全流程**：下载 → 解析 → 14 Agent 分析 → 报告（~1.5-2h）
- **模式 B · 只取底稿**：运行 Agent-01~06，获得结构化 Excel 底稿（~30-40min）
- **模式 C · 只用知识库**：直接读取 13 维度指标/公式/阈值定义（<1min）

## 📐 设计体系

文档使用 [fioutput](https://github.com/timyefi) Report 设计系统（Navy 配色，McKinsey 风格）。

## 📜 License

文档内容采用 [CC BY-NC 4.0](https://creativecommons.org/licenses/by-nc/4.0/) 协议。
