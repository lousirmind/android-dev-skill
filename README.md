# android-dev-skill

一个独立的 Claude Code agent，通过 Flutter 开发 Android App 的全流程 skill — 从需求讨论到模拟器测试的完整工作流。

## 概述

采用 3-Agent 协作模型（主 Agent 编排、开发者 Agent 实现、测试者 Agent 验证），覆盖 Flutter/Dart Android 项目的完整生命周期。每个 phase 产出可交付的文档或代码，phase 之间前后衔接。

## 安装

### 方式一：直接安装（推荐）

```bash
# 下载 skill 文件
curl -O https://raw.githubusercontent.com/lousirmind/android-dev-skill/main/android-dev-skill.skill

# 安装到 Claude Code
# 将 .skill 文件拖入 Claude Code 的 skills 目录
# 或使用 Claude Code 的 /skills 命令导入
```

### 方式二：手动复制

将 `SKILL.md` 复制到 `.claude/skills/android-dev-skill/SKILL.md`。

## 触发方式

安装后，在 Claude Code 中提及以下任一场景即可自动触发：

- "从零开发一个 Android App"
- "帮我写一个 Flutter 项目"
- "安卓开发流程"
- "帮我规划 Android 应用开发"
- 或直接输入 `/android-dev-skill`

## 工作流

```
Phase 0: 需求与设计
  ├── AskUserQuestion 讨论需求（定位/模块/技术栈）
  ├── prd skill → docs/PRD.md
  ├── karpathy-guidelines skill → CLAUDE.md
  └── docs/DEVELOPMENT.md + docs/PROJECT.md

Phase 1: 数据层 + 算法引擎
  ├── flutter create 项目脚手架
  ├── Models → Constants → Engines → Database
  └── dart analyze lib/ 零错误

Phase 2: 独立模块 UI
  ├── Theme + Routing + 通用组件
  ├── 各模块独立页面（输入页 + 结果页）
  └── LLM 服务抽象（placeholder → API）

Phase 3: 融合功能
  ├── 映射逻辑（Strategy Pattern）
  ├── 跨模块 UI 链
  └── DeepSeek/Claude API 集成

Phase 4: 其余模块
  └── 同 Phase 2 模式

Phase 5: 收尾与测试
  ├── 历史记录 + 设置页
  ├── Android minSdk 配置
  └── 模拟器全功能测试
```

## 3-Agent 协作模型

```
Main Agent (你) ←→ Developer Agent (写代码) ←→ Tester Agent (测试验证)
     │                    │                        │
     ├─ 拆分任务 ───────►  │                        │
     │                   ├─ 实现 + 自测              │
     │  ◄── Review ────  │                        │
     │                                            │
     ├─ 派发测试 ────────────────────────────►     │
     │                   │                        ├─ 写用例 + 执行
     │  ◄── Bug 报告 ─────────────────────────     │
     │                                            │
     ├─ 修复 ───────────►  │                      │
     │  ◄── 回归 ───────  │  ◄── 验证 ─────────── │
```

## 文件结构

```
android-dev-skill/
├── SKILL.md       # Skill 主文件（348 行）
├── README.md       # 本文件
└── references/     # 参考文档（可选）
```

## 关键决策模板

| 决策点 | 选项 | 参考 |
|--------|------|------|
| 融合策略 | 独立合并 vs 级联映射 | 级联映射提供统一叙事 |
| LLM 选择 | Claude / DeepSeek / OpenAI | DeepSeek 性价比高 |
| 离线策略 | 降级 vs 提示联网 | 算法可降级，LLM 提示联网 |
| UI 风格 | Material Design vs 自定义主题 | Material = 快速开发 |
| 状态管理 | Provider / Riverpod / Bloc | Provider 适合中小项目 |

## 常见坑点

- Dart 3.12+ 用 `withValues(alpha:)` 而非 `withOpacity()`
- JSON 数据文件必须在 `pubspec.yaml` 的 `flutter: assets:` 中声明
- Navigator 路由参数通过 `settings.arguments` 传递，用 `ModalRoute.of(context)!.settings.arguments` 接收
- `DropdownButtonFormField` 的 `value` 参数已废弃，改用 `initialValue`
- Android minSdk 设置为 26（`android/app/build.gradle.kts` 中配置）
- 模拟器需先创建 AVD，再启动 `emulator -avd <name>`，等待 boot_completed 后才能安装应用

## 许可证

MIT
