# 公众号长文配图生成器 v6.0.0

> 输入 MD 长文，输出公众号配图 PNG 包，同步到飞书云盘

[![版本](https://img.shields.io/badge/version-6.0.0-blue)](https://github.com/EdwardWason/wx-peitu)
[![License](https://img.shields.io/badge/license-MIT--0-green)](LICENSE)
[![ClawHub](https://img.shields.io/badge/ClawHub-wx--peitu-orange)](https://clawhub.ai/skills/wx-peitu)

## 功能

- **双风格系统**：Editorial Magazine（衬线+暖纸底）+ Swiss International（无衬线+灰白底+单一accent）
- **20种配图类型**：封面/封底/金句图/数据图/逻辑链/流程管道/版本线/判断卡/认知纠偏/宣言卡等
- **10种版式类型**：流程图/决策树/漏斗图/VS对战/路径图/条形图/网格卡片/时间线/照片叠加/文字块，禁止连续3张同版式
- **4-Purpose框架**：每张配图标注 purpose（attention/readability/memorability/conversion），驱动设计参数
- **HTML→PNG交付**：生成纯HTML → Puppeteer截图 → PNG → 桌面文件夹 → 飞书云盘同步
- **公众号尺寸适配**：封面900×383, 正文640×auto, 金句640×640, 分隔640×200
- **信息密度门控**：3维15分评分，≥9分及格，8类48条反模式
- **10品类自动检测**：深度观察/科技产品/人文文化/职场干货等，自动推荐风格
- **3大图库接入**：Pexels/Unsplash/Wallhaven，用户图片优先
- **微调模式**：指定某张配图修改，不重新生成全部

## 快速开始

```bash
# ClawHub 安装
clawhub install wx-peitu

# 或手动安装
git clone https://github.com/EdwardWason/wx-peitu.git
```

## 使用方式

在 TRAE / Claude Code / 任何 Agent 平台中，提供 MD 文章即可触发：

```
帮这篇文章做一套公众号配图
```

```
大师推荐，直接来
```

### 触发词

| 触发词 | 触发模式 |
|--------|---------|
| 公众号配图 / 文章配图 / 长文配图 / 公众号排版 | Multi-Illustration Mode |
| 大师推荐 / 你定 / 直接来 | Master Mode（全自动） |
| 第N张颜色太深 / 第N张换个版式 | 微调模式（Tweak Mode） |

## 执行流程

```
MD文章 → Step A: 解析 → Step B: 方案(确认1) → Step C: 风格(确认2) → Step D: 生成HTML → Step E: 使用指南 → Step F: 截图+云盘同步
```

1. **Step A 解析**：提取20种可视化单元，标注Purpose
2. **Step B 方案**：展示配图方案（emoji+描述），密度评分内部计算
3. **Step C 风格**：3个问题定风格 + 品类检测 + 视觉节奏规划
4. **Step D 生成HTML**：每张配图独立HTML文件（内联CSS+`<img>`标签+固定尺寸），版式多样性检查
5. **Step E 使用指南**：文章章节↔配图映射 + 快速修改指令
6. **Step F 截图交付**：Puppeteer→PNG→桌面文件夹→飞书云盘同步

## 配置

| 配置项 | 默认值 | 说明 |
|--------|--------|------|
| Style | 品类自动检测 | Editorial Magazine 或 Swiss International |
| Accent | IKB Blue (Swiss) / ink-blue (Editorial) | Swiss 4种accent可选 |
| Density Threshold | 9/15 | 最低信息密度分数 |
| Font Strategy | local-first | 本地CJK字体优先 |
| Screenshot DPI | 2x (deviceScaleFactor:2) | 高清截图 |
| Cloud Sync | 飞书云盘 | lark-cli drive +upload |

## 文档

| 文档 | 说明 |
|------|------|
| [工作流](references/workflow.md) | 6步工作流 + 微调模式 + 版式多样性 + 截图交付 + 云盘同步 |
| [设计系统](references/design-system.md) | 双风格 + 640px字号 + 900px封面字号 + 色板 + 品牌DNA |
| [质量门控](references/quality-gates.md) | 密度评分 + 48条反模式 + AI去污染 |
| [资源](references/assets.md) | 图库接入 + 图表系统 + 8种HTML模板骨架 |

## License

MIT-0 © 2026

---

# WeChat Article Illustration Generator v6.0.0

> Input MD article, output WeChat illustration PNG pack, sync to Lark Drive

[![Version](https://img.shields.io/badge/version-6.0.0-blue)](https://github.com/EdwardWason/wx-peitu)
[![License](https://img.shields.io/badge/license-MIT--0-green)](LICENSE)
[![ClawHub](https://img.shields.io/badge/ClawHub-wx--peitu-orange)](https://clawhub.ai/skills/wx-peitu)

## Features

- **Dual Style System**: Editorial Magazine (serif + warm paper) + Swiss International (sans-serif + gray-white + single accent)
- **20 Illustration Types**: Cover/back-cover/quote/data-chart/logic-chain/process/verdict/myth-fact/manifesto etc.
- **10 Layout Types**: Flow-chart/decision-tree/funnel/VS-split/path-diagram/bar-chart/grid-cards/timeline/photo-overlay/text-block, no 3+ consecutive same layout
- **4-Purpose Framework**: Each illustration tagged with purpose (attention/readability/memorability/conversion), driving design parameters
- **HTML→PNG Delivery**: Generate pure HTML → Puppeteer screenshot → PNG → Desktop folder → Lark Drive sync
- **WeChat Size Compliance**: Cover 900×383, Body 640×auto, Quote 640×640, Divider 640×200
- **Density Gate**: 3-dimension 15-point scoring, ≥9 pass, 8 categories 48 anti-patterns
- **10 Category Auto-detection**: Deep observation/Tech product/Humanities/Workplace etc., auto-recommend style
- **3 Free Image Libraries**: Pexels/Unsplash/Wallhaven, user images first
- **Tweak Mode**: Modify specific illustration without regenerating all

## Quick Start

```bash
# ClawHub install
clawhub install wx-peitu

# Or manual install
git clone https://github.com/EdwardWason/wx-peitu.git
```

## Usage

Provide an MD article in TRAE / Claude Code / any Agent platform:

```
帮这篇文章做一套公众号配图
```

### Triggers

| Trigger | Mode |
|---------|------|
| 公众号配图 / 文章配图 / 长文配图 / 公众号排版 | Multi-Illustration Mode |
| 大师推荐 / 你定 / 直接来 | Master Mode (fully automatic) |
| 第N张颜色太深 / 第N张换个版式 | Tweak Mode |

## Workflow

```
MD Article → Step A: Parse → Step B: Plan (confirm 1) → Step C: Style (confirm 2) → Step D: Generate HTML → Step E: Guide → Step F: Screenshot + Cloud Sync
```

## Configuration

| Setting | Default | Description |
|---------|---------|-------------|
| Style | Auto-detect by category | Editorial Magazine or Swiss International |
| Accent | IKB Blue (Swiss) / ink-blue (Editorial) | 4 Swiss accent options |
| Density Threshold | 9/15 | Minimum information density score |
| Font Strategy | local-first | Local CJK fonts first |
| Screenshot DPI | 2x (deviceScaleFactor:2) | High-res screenshots |
| Cloud Sync | Lark Drive | lark-cli drive +upload |

## Documentation

| Doc | Description |
|-----|-------------|
| [Workflow](references/workflow.md) | 6-step workflow + tweak mode + layout diversity + screenshot delivery + cloud sync |
| [Design System](references/design-system.md) | Dual style + 640px type scale + 900px cover type scale + palettes + brand DNA |
| [Quality Gates](references/quality-gates.md) | Density scoring + 48 anti-patterns + AI voice decontamination |
| [Assets](references/assets.md) | Image libraries + chart system + 8 HTML template skeletons |

## License

MIT-0 © 2026
