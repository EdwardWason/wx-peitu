# Assets Reference (资源参考)

> 图库、截图美化、图表系统、HTML模板规范的统一参考文件

---

## 1. Image Sources (免费图库接入)

### Three Built-In Libraries

| Library | Strength | Best For | License |
|---------|----------|----------|---------|
| **Pexels** | 中文搜索，覆盖广 | 通用背景、生活、职场、美食、自然 | 免费商用，无需署名 |
| **Unsplash** | 最高画质，艺术感 | 人像、空间/建筑、抽象纹理、氛围 | 免费商用 (Unsplash License) |
| **Wallhaven** | 游戏美术、电影级 | 科幻、游戏、暗色/情绪背景 | 混合许可，需逐张检查 |

Search URLs: `pexels.com/search/{keyword}/` · `unsplash.com/s/photos/{keyword}` · `wallhaven.cc/search?q={keyword}`

### Mode-Based Priority

| Mode | Primary | Secondary | Rationale |
|------|---------|-----------|-----------|
| **Editorial Magazine** | Unsplash | Pexels | 画质匹配杂志美学 |
| **Swiss International** | Pexels | Wallhaven | Pexels 干净产品图；Wallhaven 暗色科技背景 |
| **Dark/Tech** | Wallhaven | Unsplash | 电影级暗色影像 |

### Content Type → Image Type Mapping

| Content Type | Image Role | Source | Search Keywords |
|-------------|-----------|--------|-----------------|
| Cover/Hero | 氛围 + 标题背景 | Unsplash > Pexels | `{topic} abstract`, `{topic} minimal` |
| Data chart | 无图 (CSS/SVG) | N/A | — |
| Quote card | 微妙纹理背景 | Pexels | `paper texture`, `minimal background` |
| Comparison | 证据照片 | Pexels > Unsplash | `{subject} photo`, `{product} closeup` |
| Cases card | 产品/人物照片 | Unsplash > Pexels | `{company} office`, `{person} portrait` |

### Image Quality Requirements

- **Minimum**: 1600px 宽（避免 Retina 模糊）
- **Format**: JPG 照片，PNG 透明 UI 元素
- **Size**: 单张 < 5MB
- **No watermarks**: 拒绝带水印图片
- **Crop**: 每张图设置 `object-position` 定位主体

### Search Strategy

1. 英文关键词优先（三个图库英文索引更好）
2. Pexels 可加中文关键词
3. 背景用抽象词：`minimal dark`, `abstract gradient`, `paper texture`
4. 证据照用具体词：`rocket launch`, `satellite orbit`
5. 按方向筛选：封面 landscape (21:9)，3:4 卡片 portrait，1:1 square

### User Image Priority

**用户自有图片始终优先于图库。**

- 用户提供图片 → 优先使用，仅不足时补充图库
- 无图片时问一次："需要配图吗？A.你自己有照片/截图（推荐）B.我去图库帮你找 C.纯CSS/SVG无图方案"
- 不重复追问

### Attribution

- Pexels/Unsplash：无需署名，建议图注标注
- Wallhaven：检查单张许可，需要时添加署名
- 用户图片：标注"图片来源：用户提供"

---

## 2. Screenshot Styling (截图美化)

### Device Frame Components

| Frame | Use Case | CSS Approach |
|-------|----------|-------------|
| **macOS window** | 桌面应用截图 | 顶栏红黄绿圆点 + 居中标题 + 8px圆角 |
| **iOS device** | 移动端截图 | 圆角矩形 + 灵动岛 + Home指示条 |
| **Browser chrome** | Web应用截图 | 标签栏 + 地址栏 + 书签栏 |

### Material Backgrounds (材质背景)

截图不应浮在白底上，必须放在材质背景上：

| Background | CSS | Best For |
|-----------|-----|----------|
| **格纸** | `background-image: linear-gradient(#e8e5de 1px, transparent 1px), linear-gradient(90deg, #e8e5de 1px, transparent 1px); background-size: 20px 20px;` | Editorial, 教程卡片 |
| **点阵** | `background-image: radial-gradient(circle, #d4d4d2 1px, transparent 1px); background-size: 16px 16px;` | Swiss, 科技产品 |
| **暖白** | `background: #f5f4ed;` | 两种模式，极简风格 |
| **深色** | `background: #1a1a1e;` | Swiss, 暗色主题 |

### Shadow & Radius Rules

| Mode | Shadow | Border Radius |
|------|--------|--------------|
| **Editorial** | `0 4px 24px rgba(0,0,0,0.12)` | 8px (window), 16px (device) |
| **Swiss** | `0 2px 12px rgba(0,0,0,0.08)` | 4px (window), 12px (device) |

### Screenshot Priority

1. 用户截图 → 加设备框 + 材质背景
2. 无截图 → 图库照片
3. 都没有 → 纯 CSS/SVG 布局

---

## 3. Chart System (图表系统)

纯 CSS + 内联 SVG 实现，不依赖外部库。

### Chart Type Decision Tree

```
数据关系是什么？
│
├─ 类别比较
│   ├─ 少类别 (2-6) → bar-chart
│   └─ 多类别 (7+) → horizontal-bar-chart
│
├─ 时间变化
│   ├─ 少数据点 (2-8) → bar-chart
│   ├─ 多数据点 (8+) → line-chart
│   └─ 金融/股票 → candlestick-chart
│
├─ 占比关系
│   ├─ 少分段 (2-5) → donut-chart
│   └─ 多分段 (6+) → treemap
│
├─ 相关性
│   ├─ 2变量 → scatter-plot (有阈值线用 quadrant-chart)
│   └─ 3+变量 → bubble-chart
│
├─ 流程
│   ├─ 顺序步骤 → flow-chart
│   ├─ 并行泳道 → swimlane-chart
│   └─ 状态转换 → state-machine
│
├─ 层级
│   ├─ 树结构 → tree-chart
│   ├─ 分层/嵌套 → layered-diagram
│   └─ 组织架构 → tree-chart (horizontal)
│
├─ 集合重叠
│   └─ 2-3集合 → venn-diagram
│
└─ 累积变化
    └─ 正负贡献 → waterfall-chart
```

### 14 Chart Types (精简)

| # | Type | When | Data Shape | Notes |
|---|------|------|-----------|-------|
| 1 | **bar-chart** | 2-6类别比较 | `[{label, value, color?}]` | CSS flexbox，最多8条 |
| 2 | **horizontal-bar-chart** | 7+类别或长标签 | `[{label, value, color?}]` | CSS grid行，最多15条 |
| 3 | **line-chart** | 8+时间点趋势 | `{labels, series:[{name,values,color?}]}` | SVG polyline，最多3条线 |
| 4 | **donut-chart** | 2-5段占比 | `[{label, value, color}]` | SVG stroke-dasharray，最多5段 |
| 5 | **quadrant-chart** | 2轴+阈值线 | `{xLabel, yLabel, items:[{name,x,y}]}` | SVG四象限+十字线 |
| 6 | **flow-chart** | 3-8步顺序流程 | `{steps:[{id,label,type?}], connections:[{from,to}]}` | CSS grid + SVG箭头 |
| 7 | **swimlane-chart** | 2-4角色并行流程 | `{lanes:[{name,steps}]}` | CSS grid行 + SVG跨道箭头 |
| 8 | **state-machine** | 状态转换+条件 | `{states, transitions}` | SVG圆+路径，最多6状态 |
| 9 | **tree-chart** | 层级结构 | `{root:{label,children}}` | CSS flexbox+连接线，最深3层 |
| 10 | **layered-diagram** | 分层架构 | `{layers:[{name,items,color?}]}` | CSS堆叠矩形，最多6层 |
| 11 | **venn-diagram** | 2-3集合重叠 | `{sets, overlap}` | SVG圆 + mix-blend-mode |
| 12 | **candlestick-chart** | 金融OHLC | `[{date,open,high,low,close}]` | SVG rect+line，最多30点 |
| 13 | **waterfall-chart** | 累积正负贡献 | `[{label,value,type:'positive'|'negative'|'total'}]` | CSS flexbox堆叠，最多10项 |
| 14 | **treemap** | 多类别层级占比 | `[{label,value,color?,children?}]` | CSS grid-area，最多12项 |

### Chart Styling Rules

- **Color**: 默认 `--color-accent-1` ~ `--color-accent-4`，单图不超4色
- **Typography**: 轴标 `--text-caption`/`--color-text-muted`；数据标 `--text-small` + `tabular-nums`；标题 `--text-h3`/`--font-display`
- **Spacing**: 内边距 `--sp-4`，图例间距 `--sp-3`，图例项间距 `--sp-2`
- **SVG**: 用 `viewBox` + `width:100%` + `height:auto`，最小宽度320px
- **A11y**: `role="img"` + `aria-label`，不纯靠颜色区分

### Auto-Selection Integration

内容解析后自动建议：
1. 数值比较 → bar-chart / horizontal-bar-chart
2. 时间序列 → line-chart
3. 占比 → donut-chart
4. 流程 → flow-chart
5. 层级 → tree-chart / layered-diagram
6. 跨角色比较 → swimlane-chart

---

## 4. HTML Template Specification (HTML模板规范)

截图友好的自包含HTML模板规范，替代React输出。

### 4.1 HTML文件结构

每个HTML文件必须：
- **完全自包含**：内联CSS，不依赖外部样式表
- **Google Fonts** `@import` 放在 `<style>` 顶部
- **图片用 `<img>` 标签**（非CSS background-image）
- **固定宽高**：`html,body{width:XXXpx;height:XXXpx;overflow:hidden;margin:0;padding:0}`
- **颜色引用CSS变量**：所有颜色通过 `var(--xxx)` 引用 design-tokens

### 4.2 标准HTML骨架模板

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<style>
@import url('https://fonts.googleapis.com/css2?family=Noto+Serif+SC:wght@400;700&family=Noto+Sans+SC:wght@300;400;500;700&display=swap');

:root {
  --color-bg-primary: #FAFAF8;
  --color-bg-secondary: #F0EDE6;
  --color-bg-card: #FFFFFF;
  --color-text-primary: #1A1A1A;
  --color-text-secondary: #666666;
  --color-text-muted: #999999;
  --color-accent-1: #3B82F6;
  --color-accent-2: #10B981;
  --color-accent-3: #F59E0B;
  --color-accent-4: #EF4444;
  --color-border: #E5E5E5;
  --font-display: 'Noto Serif SC', serif;
  --font-body: 'Noto Sans SC', sans-serif;
  --text-hero: 48px;
  --text-h1: 32px;
  --text-h2: 24px;
  --text-h3: 20px;
  --text-body: 16px;
  --text-small: 14px;
  --text-caption: 12px;
  --sp-1: 4px; --sp-2: 8px; --sp-3: 12px; --sp-4: 16px;
  --sp-6: 24px; --sp-8: 32px; --sp-12: 48px;
  --radius-sm: 4px; --radius-md: 8px; --radius-lg: 12px;
  --shadow-sm: 0 1px 2px rgba(0,0,0,0.05);
  --shadow-md: 0 4px 6px rgba(0,0,0,0.07);
}

html, body {
  width: 640px; height: auto;
  margin: 0; padding: 0;
  overflow: hidden;
  font-family: var(--font-body);
  background: var(--color-bg-primary);
  color: var(--color-text-primary);
}
</style>
</head>
<body>
  <div class="container">
    <!-- 内容层 -->
  </div>
</body>
</html>
```

### 4.3 各配图类型HTML模板骨架

#### Cover (900×383) — 照片背景 + 标题叠加

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
<meta charset="UTF-8">
<style>
@import url('https://fonts.googleapis.com/css2?family=Noto+Serif+SC:wght@400;700&display=swap');
:root { /* design-tokens */ }
html, body { width: 900px; height: 383px; margin: 0; padding: 0; overflow: hidden; }
.cover { position: relative; width: 900px; height: 383px; overflow: hidden; }
.cover__img {
  position: absolute; inset: 0; width: 100%; height: 100%;
  object-fit: cover; object-position: center 30%;
}
.cover__gradient {
  position: absolute; inset: 0;
  background: linear-gradient(to top, rgba(0,0,0,0.65), transparent 60%);
}
.cover__content {
  position: relative; z-index: 2;
  padding: 40px 48px; display: flex; flex-direction: column;
  justify-content: flex-end; height: 100%; box-sizing: border-box;
}
.cover__title {
  font-family: var(--font-display); color: #fff;
  font-size: 48px; font-weight: 700; line-height: 1.15; margin: 0;
}
.cover__subtitle {
  color: rgba(255,255,255,0.85); font-size: 18px;
  margin-top: 12px; line-height: 1.5;
}
</style>
</head>
<body>
<div class="cover">
  <img class="cover__img" src="PHOTO_URL" crossorigin="anonymous" />
  <div class="cover__gradient"></div>
  <div class="cover__content">
    <h1 class="cover__title">标题文字</h1>
    <p class="cover__subtitle">副标题</p>
  </div>
</div>
</body>
</html>
```

#### Body Illustration (640×auto) — 内容配图

```html
<!-- 在标准骨架基础上，body内替换为： -->
<div class="container" style="padding: var(--sp-8);">
  <h2 style="font-family:var(--font-display);font-size:var(--text-h2);margin:0 0 var(--sp-4);">
    章节标题
  </h2>
  <div style="display:grid;grid-template-columns:1fr 1fr;gap:var(--sp-4);">
    <!-- 内容卡片等 -->
  </div>
</div>
```

#### Quote Card (640×640) — 金句图

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
<meta charset="UTF-8">
<style>
@import url('https://fonts.googleapis.com/css2?family=Noto+Serif+SC:wght@400;700&display=swap');
:root { /* design-tokens */ }
html, body { width: 640px; height: 640px; margin: 0; padding: 0; overflow: hidden; }
.quote {
  width: 640px; height: 640px; display: flex; flex-direction: column;
  justify-content: center; align-items: center; padding: 64px;
  box-sizing: border-box; background: var(--color-bg-primary);
  text-align: center;
}
.quote__mark { font-size: 72px; color: var(--color-accent-1); line-height: 1; }
.quote__text {
  font-family: var(--font-display); font-size: 28px; font-weight: 700;
  line-height: 1.6; max-width: 480px; margin: 24px 0;
}
.quote__author { font-size: var(--text-small); color: var(--color-text-muted); }
</style>
</head>
<body>
<div class="quote">
  <div class="quote__mark">"</div>
  <p class="quote__text">金句内容</p>
  <span class="quote__author">— 作者</span>
</div>
</body>
</html>
```

#### Section Divider (640×200) — 章节分隔

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
<meta charset="UTF-8">
<style>
@import url('https://fonts.googleapis.com/css2?family=Noto+Serif+SC:wght@400;700&display=swap');
:root { /* design-tokens */ }
html, body { width: 640px; height: 200px; margin: 0; padding: 0; overflow: hidden; }
.divider {
  width: 640px; height: 200px; display: flex; align-items: center;
  justify-content: center; background: var(--color-bg-secondary);
}
.divider__line { width: 60px; height: 2px; background: var(--color-accent-1); margin: 0 20px; }
.divider__text {
  font-family: var(--font-display); font-size: var(--text-h2);
  font-weight: 700; color: var(--color-text-primary);
}
</style>
</head>
<body>
<div class="divider">
  <div class="divider__line"></div>
  <span class="divider__text">章节名</span>
  <div class="divider__line"></div>
</div>
</body>
</html>
```

#### Back Cover (900×383) — 照片背景 + 品牌信息

```html
<!-- 与Cover结构相同，cover__content改为： -->
<div class="cover__content" style="justify-content:center;align-items:center;text-align:center;">
  <p style="color:rgba(255,255,255,0.9);font-size:20px;font-family:var(--font-display);">
    品牌Slogan
  </p>
  <p style="color:rgba(255,255,255,0.6);font-size:var(--text-small);margin-top:12px;">
    公众号名称 · 关注我们
  </p>
</div>
```

#### Flow Chart (流程图) — 640×auto

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=640">
<style>
@import url('https://fonts.googleapis.com/css2?family=Noto+Sans+SC:wght@300;400;500;700&display=swap');
* { margin: 0; padding: 0; box-sizing: border-box; }
html { width: 640px; font-family: 'Noto Sans SC', sans-serif; background: #fafaf8; }
body { width: 640px; }
.page { width: 640px; padding: 40px 48px; background: #fafaf8; }
.eyebrow { font-size: 11px; font-weight: 500; letter-spacing: 0.15em; color: #002FA7; text-transform: uppercase; margin-bottom: 8px; }
.title { font-size: 28px; font-weight: 400; color: #0a0a0a; line-height: 1.3; margin-bottom: 32px; }
.flow { display: flex; flex-direction: column; gap: 0; align-items: center; }
.flow-step { width: 100%; display: flex; align-items: center; gap: 20px; }
.step-num { width: 40px; height: 40px; border-radius: 50%; display: flex; align-items: center; justify-content: center; font-size: 16px; font-weight: 500; flex-shrink: 0; }
.step-num.active { background: #002FA7; color: #ffffff; }
.step-num.dim { background: #d4d4d2; color: #737373; }
.step-num.fail { background: #0a0a0a; color: #fafaf8; }
.step-content { flex: 1; padding: 16px 20px; border-radius: 4px; }
.step-content.success { background: #f0f0ee; border-left: 3px solid #002FA7; }
.step-content.warning { background: #f0f0ee; border-left: 3px solid #d4d4d2; }
.step-content.fail { background: #0a0a0a; border-left: 3px solid #737373; }
.step-title { font-size: 16px; font-weight: 500; margin-bottom: 4px; }
.step-content.success .step-title { color: #002FA7; }
.step-content.warning .step-title { color: #737373; }
.step-content.fail .step-title { color: #fafaf8; }
.step-desc { font-size: 14px; font-weight: 400; line-height: 1.5; }
.step-content.success .step-desc { color: #0a0a0a; }
.step-content.warning .step-desc { color: #737373; }
.step-content.fail .step-desc { color: rgba(255,255,255,0.6); }
.flow-arrow { width: 2px; height: 24px; background: #d4d4d2; margin-left: 19px; }
.flow-arrow-head { width: 0; height: 0; border-left: 5px solid transparent; border-right: 5px solid transparent; border-top: 7px solid #d4d4d2; margin-left: 15px; }
</style>
</head>
<body>
<div class="page">
  <div class="eyebrow">流程标题</div>
  <h2 class="title">主标题</h2>
  <div class="flow">
    <div class="flow-step">
      <div class="step-num active">1</div>
      <div class="step-content success"><div class="step-title">步骤1</div><div class="step-desc">描述</div></div>
    </div>
    <div class="flow-arrow"></div><div class="flow-arrow-head"></div>
    <div class="flow-step">
      <div class="step-num dim">2</div>
      <div class="step-content warning"><div class="step-title">步骤2</div><div class="step-desc">描述</div></div>
    </div>
    <div class="flow-arrow"></div><div class="flow-arrow-head"></div>
    <div class="flow-step">
      <div class="step-num fail">3</div>
      <div class="step-content fail"><div class="step-title">步骤3</div><div class="step-desc">描述</div></div>
    </div>
  </div>
</div>
</body>
</html>
```

#### Funnel (漏斗图) — 640×auto

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=640">
<style>
@import url('https://fonts.googleapis.com/css2?family=Noto+Sans+SC:wght@300;400;500;700&display=swap');
* { margin: 0; padding: 0; box-sizing: border-box; }
html { width: 640px; font-family: 'Noto Sans SC', sans-serif; background: #fafaf8; }
body { width: 640px; }
.page { width: 640px; padding: 40px 48px; background: #fafaf8; }
.eyebrow { font-size: 11px; font-weight: 500; letter-spacing: 0.15em; color: #002FA7; text-transform: uppercase; margin-bottom: 8px; }
.title { font-size: 28px; font-weight: 400; color: #0a0a0a; line-height: 1.3; margin-bottom: 32px; }
.funnel { display: flex; flex-direction: column; align-items: center; gap: 0; }
.funnel-bar { height: 56px; border-radius: 4px; display: flex; align-items: center; justify-content: center; position: relative; }
.funnel-bar.s1 { width: 544px; background: #d4d4d2; }
.funnel-bar.s2 { width: 380px; background: #737373; }
.funnel-bar.s3 { width: 220px; background: #002FA7; }
.funnel-bar.s4 { width: 120px; background: #0a0a0a; }
.funnel-num { font-size: 28px; font-weight: 300; color: #ffffff; }
.funnel-bar.s1 .funnel-num { color: #737373; }
.funnel-label { position: absolute; right: -8px; transform: translateX(100%); font-size: 13px; font-weight: 400; color: #737373; white-space: nowrap; }
.arrow { width: 2px; height: 20px; background: #d4d4d2; margin: 0 auto; }
.arrow-head { width: 0; height: 0; border-left: 6px solid transparent; border-right: 6px solid transparent; border-top: 8px solid #d4d4d2; margin: 0 auto; }
</style>
</head>
<body>
<div class="page">
  <div class="eyebrow">漏斗标题</div>
  <h2 class="title">主标题</h2>
  <div class="funnel">
    <div class="funnel-bar s1"><span class="funnel-num">54</span><span class="funnel-label">总尝试</span></div>
    <div class="arrow"></div><div class="arrow-head"></div>
    <div class="funnel-bar s2"><span class="funnel-num">6</span><span class="funnel-label">成功</span></div>
    <div class="arrow"></div><div class="arrow-head"></div>
    <div class="funnel-bar s3"><span class="funnel-num">4</span><span class="funnel-label">不同漏洞</span></div>
  </div>
</div>
</body>
</html>
```

#### VS Split (VS对战) — 640×auto

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=640">
<style>
@import url('https://fonts.googleapis.com/css2?family=Noto+Sans+SC:wght@300;400;500;700&display=swap');
* { margin: 0; padding: 0; box-sizing: border-box; }
html { width: 640px; font-family: 'Noto Sans SC', sans-serif; background: #fafaf8; }
body { width: 640px; }
.page { width: 640px; padding: 40px 48px; background: #fafaf8; }
.eyebrow { font-size: 11px; font-weight: 500; letter-spacing: 0.15em; color: #002FA7; text-transform: uppercase; margin-bottom: 8px; }
.title { font-size: 28px; font-weight: 400; color: #0a0a0a; line-height: 1.3; margin-bottom: 28px; }
.vs-container { display: flex; align-items: stretch; gap: 0; min-height: 280px; }
.vs-side { flex: 1; padding: 28px 24px; display: flex; flex-direction: column; justify-content: center; }
.vs-left { background: #0a0a0a; border-radius: 4px 0 0 4px; }
.vs-right { background: #002FA7; border-radius: 0 4px 4px 0; }
.vs-divider { width: 48px; display: flex; align-items: center; justify-content: center; background: #fafaf8; }
.vs-badge { width: 36px; height: 36px; background: #0a0a0a; border-radius: 50%; display: flex; align-items: center; justify-content: center; font-size: 12px; font-weight: 700; color: #002FA7; }
.side-label { font-size: 10px; font-weight: 500; letter-spacing: 0.15em; margin-bottom: 16px; }
.vs-left .side-label { color: #737373; }
.vs-right .side-label { color: rgba(255,255,255,0.6); }
.side-claim { font-size: 18px; font-weight: 400; line-height: 1.4; margin-bottom: 16px; }
.vs-left .side-claim { color: #fafaf8; }
.vs-right .side-claim { color: #ffffff; }
.side-stat { font-size: 36px; font-weight: 300; line-height: 1; }
.vs-left .side-stat { color: #737373; }
.vs-right .side-stat { color: #ffffff; }
</style>
</head>
<body>
<div class="page">
  <div class="eyebrow">对比标题</div>
  <h2 class="title">主标题</h2>
  <div class="vs-container">
    <div class="vs-side vs-left">
      <div class="side-label">左侧标签</div>
      <div class="side-claim">左侧声明</div>
      <div class="side-stat">数据</div>
    </div>
    <div class="vs-divider"><div class="vs-badge">VS</div></div>
    <div class="vs-side vs-right">
      <div class="side-label">右侧标签</div>
      <div class="side-claim">右侧声明</div>
      <div class="side-stat">数据</div>
    </div>
  </div>
</div>
</body>
</html>
```

### 4.4 背景图兼容性规则

Puppeteer 截图必须用 `<img>` 标签，**禁止** CSS `background-image`。

**正确模式**：
```html
<div style="position:relative;width:900px;height:383px;overflow:hidden">
  <img src="https://images.unsplash.com/photo-xxx?w=1200&q=80"
       style="position:absolute;inset:0;width:100%;height:100%;object-fit:cover"
       crossorigin="anonymous" />
  <div style="position:absolute;inset:0;background:linear-gradient(to top, rgba(0,0,0,0.6), transparent 60%)"></div>
  <div style="position:relative;z-index:2;padding:40px">
    <!-- 文字内容 -->
  </div>
</div>
```

**错误模式**（截图可能白屏）：
```html
<div style="background-image:url('https://images.unsplash.com/...');background-size:cover">
  Content
</div>
```

**关键规则**：
- 外部图片 `<img>` 必须加 `crossorigin="anonymous"`
- 容器设固定 `width` 和 `height`（不用 auto）
- 用 `object-fit:cover` + `object-position` 对齐主体
- 渐变遮罩层用独立 `<div>`，夹在图片和文字之间

### 4.5 自适应字号

#### 标题长度→字号映射

| 标题长度 | 中文字数 | 尺寸 (640px画布) | Weight | 行限制 |
|---------|---------|-----------------|--------|-------|
| Short | ≤6 | 56-72px | 200-400 | 1行 |
| Medium | 7-14 | 40-52px | 300-500 | 1-2行 |
| Long | 15-24 | 28-36px | 400-500 | 2行 |
| Extended | 25+ | 22-28px | 500 | 2-3行 |

#### 纯JS实现

```javascript
function getTitleStyle(text, baseSize) {
  baseSize = baseSize || 56;
  var len = text.length;
  if (len <= 6) return { fontSize: baseSize + 'px', fontWeight: '300', lineHeight: '1.15' };
  if (len <= 14) return { fontSize: Math.round(baseSize * 0.72) + 'px', fontWeight: '400', lineHeight: '1.2' };
  if (len <= 24) return { fontSize: Math.round(baseSize * 0.52) + 'px', fontWeight: '500', lineHeight: '1.3' };
  return { fontSize: Math.round(baseSize * 0.4) + 'px', fontWeight: '500', lineHeight: '1.4',
           WebkitLineClamp: '3', display: '-webkit-box', WebkitBoxOrient: 'vertical', overflow: 'hidden' };
}
```

#### 动态调整规则

1. **永不溢出**：文字溢出容器时，先降一级字号，再加 `line-clamp` 兜底
2. **最小可读**：640px画布上，正文最小14px，说明文字最小10px
3. **数字强调**：数据卡片中的数字始终用最大字号（如 "$186.74亿" 用48px）
4. **CJK换行**：中文任意字符处可换行，不依赖空格 word-break
5. **行高随字号**：Display 1.1-1.2，Body 1.5-1.6，Caption 1.3-1.4
