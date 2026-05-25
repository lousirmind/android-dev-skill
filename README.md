# android-dev-skill

Android App 全流程开发 skill — 从需求讨论到模拟器测试的完整工作流。

## 概述

基于"灵犀天机"（塔罗 + 梅花易数 + 八字命理 Android App）实战经验提炼的可复用开发流程。采用 3-Agent 协作模型（主 Agent 编排、开发者 Agent 实现、测试者 Agent 验证），覆盖 Flutter/Dart 项目的完整生命周期。

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

- 八卦二进制模式（0-7）≠ 先天数（1-8），需查表映射（公式: `value==0 ? 8 : 8-value`）
- 64 卦爻掩码 MSB/LSB 约定必须一致，用 `>> (5-i)` 而非 `>> i`
- 八字年柱以立春为界（非农历正月初一）
- Dart 3.12+ 用 `withValues(alpha:)` 而非 `withOpacity()`
- JSON 数据文件必须在 `pubspec.yaml` 的 `flutter: assets:` 中声明

## 许可证

MIT
