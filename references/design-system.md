# Design System v6 (Dual Style)

2 visual modes + constraints + typography + color + brand DNA. Consolidated from 4 reference files.

---

## Phase 0: The Three Constraints (不可协商)

**All modes must obey. Style can vary, constraints are constant.**

### Constraint 1: 克制 (Restraint)

- Brand/accent color covers **≤ 5% of document surface area**
- Brand color is for: title left-bar, tags, CTA buttons, accent numbers only
- More than 5% brand color = ornament, not design
- **Single accent principle**: one chromatic color per design. No second chromatic color (exception: breaking-change badges registered as `--breaking-*` tokens)

### Constraint 2: 呼吸 (Breathing)

- Card spacing ≥ 2× content spacing (gap between cards > gap within cards)
- Section title margin-bottom ≥ 2× margin-above
- Whisper shadow only: `0 4pt 24pt rgba(0,0,0,0.05)`, never hard drop shadows
- Ring shadow for emphasis: `0 0 0 1pt var(--brand)`, not box-shadow with offset > 4px
- Border width: 0.5pt, border-radius: 8pt minimum for cards

### Constraint 3: 温度 (Warmth)

- **All grays must have warm undertone** (R ≈ G > B in RGB). No cool blue-grays.
- Forbidden: `#94A3B8`, `#CBD5E1`, `#E2E8F0`, `#F1F5F9`, `#F8FAFC`
- Required warm gray scale:
  ```css
  --near-black: #141413;   /* warm olive undertone */
  --dark-warm:  #3d3d3a;   /* secondary text */
  --olive:      #504e49;   /* subtext, descriptions */
  --stone:      #6b6a64;   /* tertiary, dates, metadata */
  --border:     #e8e6dc;   /* warm border */
  --parchment:  #f5f4ed;   /* warm cream background */
  --ivory:      #faf9f5;   /* card background */
  ```
- **Never** `#FFFFFF` as page background. Use `--parchment` or `--ivory`.
- **Never** `#000000` as text color. Use `--near-black`.

### Serif Weight Lock

- Serif headings: weight 500 only. **Forbidden**: weight 600/700/900 on serif fonts
- Serif body: weight 400 only

### Anti-Slop Rules (8 Red Lines)

```
🚫 禁止连续三张配图用相同布局
🚫 禁止所有卡片居中排列（至少一张不对称）
🚫 禁止品牌色大面积铺底（≤5%面积）
🚫 禁止纯白背景（必须用暖色底）
🚫 禁止冷蓝灰色系（#94A3B8 这类）
🚫 禁止衬线体 font-weight: 700
🚫 禁止硬投影（box-shadow 偏移量 > 4px）
🚫 禁止 rgba 背景色标签（用 solid hex 替代）
```

---

## Phase 0.5: Dual Style System

Two visual stances — any topic can be rendered in either mode. Pick by editorial intent ("feature story" vs "release note"), not by topic lookup.

### Mode A: Editorial Magazine (杂志社论风)

**Visual anchors**: Serif/Songti display title + quiet sans body · Warm paper background (#f5f4ed) · Atmosphere layer (grain/wash/gradient) · Magazine structure (columns, pull-quotes, marginalia) · Large purposeful whitespace · Fine rules (0.5pt)

**Good fits**: humanistic, cultural, narrative, reflective — also workplace essays, AI think-pieces, product retrospectives

**Palettes**: warm, elegant, earth, kami-parchment, morandi-journal, or any Brand DNA palette
**Font presets**: 古典书卷, 瘦金风骨, 纸墨书卷(Kami), 官方权威

### Mode B: Swiss International (瑞士国际主义风)

**Visual anchors**: Full sans-serif (Inter / Noto Sans SC), no serif · Light paper (#fafaf8) + near-black (#0a0a0a) · Grid/dot matrix background · One high-saturation accent only · Strict left-aligned grid, hairline rules · Card-fill matrices, KPI towers, h-bar charts

**Good fits**: tech products, data reports, engineering, design, annual summaries

**Palettes**: Swiss-specific (see below)
**Font presets**: 现代简约 only (Inter + Noto Sans SC)

### Swiss Accent Palettes (4 options, pick one)

| Accent | Hex | accent-on | Vibe | Best For |
|--------|-----|-----------|------|----------|
| **IKB Blue** (克莱因蓝) | #002FA7 | #ffffff | Academic, rational | AI/tech/design, default |
| **Lemon Yellow** (柠檬黄) | #FFD500 | #0a0a0a | Active, vibrant | Youth, retail, consumer |
| **Lemon Green** (柠檬绿) | #C5E803 | #0a0a0a | Future, emerging | Eco, Gen-Z, new tech |
| **Safety Orange** (安全橙) | #FF6B35 | #ffffff | Industrial, urgent | Industrial, automotive |

**Swiss hard rules**: One accent only per set · No gradients · No serif fonts · No rounded corners on accent blocks · Headings sit top-left

### Swiss Gray Scale

```css
--swiss-paper: #fafaf8;    /* warm white */
--swiss-grey-1: #f0f0ee;   /* light grey block bg */
--swiss-grey-2: #d4d4d2;   /* mid grey, dividers */
--swiss-grey-3: #737373;   /* dark grey, secondary text */
--swiss-ink: #0a0a0a;      /* near-black */
```

### Style Identity Test

**Swiss** (ALL four must hold):
1. Every display title (≥48px) has font-weight ≤ 400
2. No serif family loaded. No `font-family: serif`
3. Separators are hairline rules or grid gutters, not card borders + drop shadows
4. Exactly one accent palette. No mixed accents

**Editorial** (ALL three must hold):
1. Background has atmosphere layer beyond flat fill (grain, gradient, wash)
2. Display title uses serif-zh family (Noto Serif SC / 汇文明朝体 / TsangerJinKai02)
3. Contains at least one: large photo well, serif pull-quote, marginalia column, or ledger

### Aesthetic Guardrails

- **Palette Lock**: Swiss → only 4 Swiss Accent Palettes; Editorial → only warm/elegant/earth/kami/morandi
- **Single Accent (Swiss)**: One chromatic accent per design set. No mixing
- **No Cross-Mode Mixing**: Swiss gray scale ≠ Editorial warm grays
- **Custom color**: Allow only with explicit brand hex + brand context → register as `--brand-accent`

---

## Typography Rules

### WeChat Card Type Scale (640px canvas) ⭐ PRIMARY

| Role | Size (640px) | Weight | Tracking | Rationale |
|------|-------------|--------|----------|-----------|
| Display/Hero | 36-44px | 300-400 | +0.03em | Confident, not overwhelming |
| Section title | 24-32px | 400-500 | +0.02em | Clear hierarchy anchor |
| Body | 14-16px | 400-500 | normal | Comfortable mobile reading |
| Captions/meta | 10-12px | 500-600 | +0.1-0.15em | Legible at small size |
| Data numbers | 28-36px | 300-400 | normal | Metric cards — larger than body, smaller than titles |

**Hard rules**: 44px+ at weight 600+ = instant downgrade · Chinese display: weight 500 max (serif) or 300-400 (sans) · WeChat covers (900×383): Display up to 48px · 1:1 square (640×640): Display max 36px

### Cover Type Scale (900×383 canvas) ⭐ 封面/封底专用

封面和封底是 900×383 画布，比正文 640px 宽 40%，字号需要更大才能在手机缩略图中可读。

| Role | Size (900px) | Weight | Tracking | Rationale |
|------|-------------|--------|----------|-----------|
| Cover Title | 44-52px | 300-400 | +0.03em | 手机缩略图必须1秒可读 |
| Cover Subtitle | 15-18px | 400 | normal | 辅助信息，不抢标题 |
| Cover Meta | 11-13px | 500 | +0.1em | 来源/作者/日期 |
| Cover Eyebrow | 12-13px | 500 | +0.15em | 分类标签 |

**Hard rules**: 封面标题最小 44px · 封底标题最小 28px · 封面/封底必须照片背景

### The Larger The Lighter

Large text → lighter weight; small text → heavier weight. This is the single most impactful rule for "premium" feel. A 44px+ title at weight 600+ reads as "generic landing page", not "magazine".

### CJK Letter-Spacing

- Chinese body text with serif: `letter-spacing: 0.3pt`
- Chinese display text (24px+): `letter-spacing: 0.2-1pt`
- English body: `letter-spacing: 0`
- Small labels (< 10pt): `+0.2 to +0.5pt`

### Font Pairing System (6 Presets)

| Preset | Display (标题) | Body (正文) | Mono | Vibe | Mode |
|--------|---------------|------------|------|------|------|
| **古典书卷** | 汇文明朝体 | 楷体-GB2312 | Ubuntu Mono | 文化感、书卷气 | Editorial |
| **瘦金风骨** | 宋徽宗瘦金体 | 汇文明朝体 | Ubuntu Mono | 极致个性、锋利 | Editorial |
| **官方权威** | 方正小标宋 | Noto Sans SC | Ubuntu Mono | 正式、商务 | Editorial |
| **现代简约** | Source Han Serif SC Heavy | Noto Sans SC | Ubuntu Mono | 干净、现代 | Swiss |
| **手写教育** | 楷体-GB2312 | Noto Sans SC | Ubuntu Mono | 温和、亲切 | Editorial |
| **纸墨书卷(Kami)** | TsangerJinKai02 | Noto Sans SC | JetBrains Mono | 克制、雅致 | Editorial |

### Local Font Registry

| Font Name | CSS Name | Category |
|-----------|---------|----------|
| 汇文明朝体 | `'汇文明朝体'` | Serif/明朝 — elegant, scholarly |
| 宋徽宗瘦金体 | `'宋徽宗瘦金体'` | Calligraphy — extreme thin strokes |
| 方正小标宋 | `'方正小标宋简体'` | Song — official, authoritative |
| 楷体 | `'楷体-GB2312'` | Kai — handwritten, warm |
| 仿宋 | `'仿宋－GB2312'` | Fang — classical, formal |
| 不坑盒子 | `'不坑盒子'` | Creative — playful |
| Noto Sans SC | `'Noto Sans SC'` | Sans — clean, universal |
| Source Han Serif SC Heavy | `'Source Han Serif SC Heavy'` | Serif — elegant, powerful |
| TsangerJinKai02 | `'TsangerJinKai02'` | Kai/Serif — restrained, Kami default |

### Adaptive Title Sizing

```
getTitleStyle(titleLength):
  if len ≤ 6:  { size: 44px, weight: 300, tracking: +0.04em }
  if len ≤ 12: { size: 36px, weight: 400, tracking: +0.03em }
  if len ≤ 20: { size: 28px, weight: 400, tracking: +0.02em }
  if len ≤ 30: { size: 24px, weight: 500, tracking: +0.02em }
  else:        { size: 20px, weight: 500, tracking: +0.01em }
```

CJK titles: use 1.1× the English size. CJK body: minimum 14px. CJK line-height: 1.7-1.8.

---

## Color Rules

### Editorial Palettes

| Palette | bg-primary | text-primary | Accents |
|---------|-----------|-------------|---------|
| **warm** | #FAF8F5 | #2D2418 | #E8913A, #D4583A, #5B8C5A, #3D7EA6 |
| **elegant** | #F8F7F4 | #1A1A2E | #2D4A7A, #C9A84C, #6B5B8D, #3A6B5E |
| **earth** | #F5F0E8 | #3D3529 | #8B6F47, #5B7B5E, #C17F59, #6B8FA3 |
| **kami-parchment** | #F5F4ED | #141413 | #1B365D (ink-blue, sole accent) |
| **morandi-journal** | #F5F0E8 | #3D3529 | #8B7E74, #A89F91, #6B8FA3, #B5A89A |

### Swiss Palettes (4 accent options)

See Phase 0.5 Swiss Accent Palettes. Background: `--swiss-paper: #fafaf8`, Text: `--swiss-ink: #0a0a0a`.

### Kami Full Token System (Editorial mode, kami variant)

```css
:root {
  --kami-brand: #1B365D; --kami-brand-light: #2D5A8A;
  --kami-parchment: #f5f4ed; --kami-ivory: #faf9f5;
  --kami-warm-sand: #e8e6dc; --kami-dark-surface: #30302e; --kami-deep-dark: #141413;
  --kami-near-black: #141413; --kami-dark-warm: #3d3d3a;
  --kami-olive: #504e49; --kami-stone: #6b6a64;
  --kami-border: #e8e6dc; --kami-border-soft: #e5e3d8;
  --kami-brand-tint: #EEF2F7; --kami-tag-bg: #E4ECF5;
  --kami-breaking-bg: #f0e0d8; --kami-breaking-fg: #8b4513;
}
```

### Brand DNA Palettes (auto-applied on content source detection)

| Palette | bg-primary | text-primary | Accents | Font Override |
|---------|-----------|-------------|---------|---------------|
| **economist-red** | #FDFCFA | #1D1D1B | #E3120B | 方正小标宋 + 汇文明朝体 |
| **wechat-green** | #FFFFFF | #333333 | #07C160 | Noto Sans SC |
| **peoples-red-gold** | #FFF9F0 | #1D1D1B | #DE2910, #FFDE00 | 方正小标宋 + 仿宋 |
| **xhs-red** | #FFF5F5 | #333333 | #FF2442, #FFB5C2 | Noto Sans SC |
| **zhihu-blue** | #FFFFFF | #1A1A1A | #0066FF | Noto Sans SC |

### Color Application Rules

- **60-30-10**: 60% background, 30% card/section, 10% accent highlights
- Never > 4 accent colors in one design
- Dark text on light bg: never pure #000. Light text on dark bg: never pure #FFF
- Accents must pass WCAG AA contrast

### Image-Text Conflict Bans (5 rules)

1. **Quiet zone test**: Photo must have low-detail area for text. No quiet zone → use framed-photo layout
2. **Subject mapping**: Identify photo focal point, place text in safe zones only
3. **object-position discipline**: Set inline on every `<img>` (face: `center 30%`, mid-body: `center 62%`, sky: `center 70%`)
4. **Thumbnail test**: Downscale to 360px wide — if title illegible, move/swap/tint
5. **No full-canvas falloffs**: If tint needed, apply only around text area, matching image color temperature

---

## Brand DNA Registry

| Brand | Detection Signals | Palette | Font Override | Layout Traits |
|-------|------------------|---------|---------------|---------------|
| **The Economist** | economist.com, "经济学人" | eco-red #E3120B | 方正小标宋 + 汇文明朝体 | Thick rules, no radius, mobile-first 640px |
| **WeChat / 微信** | mp.weixin.qq.com, "公众号" | WeChat green #07C160 | Noto Sans SC | Rounded cards, loose spacing, 578px |
| **Apple** | apple.com, "苹果" | Pure white + black | SF Pro / PingFang SC | Large whitespace, centered, hero image |
| **36Kr** | 36kr.com, "36氪" | 36Kr blue + dark | Source Han Sans | Dense, compact, tech-news |
| **People's Daily** | people.com.cn, "人民日报" | Red #DE2910 + gold #FFDE00 | 方正小标宋 + 仿宋 | Formal, symmetrical |
| **Xiaohongshu** | xiaohongshu.com, "小红书" | XHS red #FF2442 | Noto Sans SC | Card waterfall, photo-heavy |
| **Zhihu** | zhihu.com, "知乎" | Zhihu blue #0066FF | Noto Sans SC | Q&A layout, long-form |
| **GitHub** | github.com, "GitHub" | Dark bg + green accent | Monospace-heavy | Code blocks, repo stats |
| **Notion** | notion.so, "Notion" | Off-white + minimal | System UI | Block-based, toggle lists |
| **Kami / 纸墨** | tw93/kami, "Kami", "纸墨风" | kami-parchment + ink-blue #1B365D | TsangerJinKai02 | Kami Ten Invariants apply |
| **ByteDance / 字节** | bytedance.com, "字节跳动", "抖音" | 字节蓝 #325AB4 | Noto Sans SC | 紧凑卡片、数据密集 |
| **少数派 / sspai** | sspai.com, "少数派" | sspai-red #D93A31 | Noto Sans SC | 长文排版、留白舒适 |
| **极客时间** | time.geekbang.org, "极客时间" | 极客蓝 #3564D9 | Noto Sans SC | 知识卡片、步骤清晰 |

---

## Brand Profile System

Four-layer priority resolution for visual identity:

```
┌──────────────────────────────────────────────┐
│  Layer 1: Explicit Prompt                    │  ← --palette / --style / --layout
│  (Highest priority, always wins)             │
├──────────────────────────────────────────────┤
│  Layer 2: Brand DNA Auto-Detection           │  ← URL/keyword scan
│  (Auto-applied when content source detected) │
├──────────────────────────────────────────────┤
│  Layer 3: User Brand Profile                 │  ← ~/.config/react-design-draft/brand.md
│  (Persistent user preferences)               │
├──────────────────────────────────────────────┤
│  Layer 4: Dual-Style Auto-Selection          │  ← Editorial vs Swiss matching
│  (Lowest priority, default fallback)         │
└──────────────────────────────────────────────┘
```

**User Brand Profile** (`~/.config/react-design-draft/brand.md`): Define default colors, typography, layout preferences, brand rules. Partial override — only defined dimensions apply.

**Application rules**: Never silently override user intent · Always inform user of applied layers · Partial application is fine · User can always override with explicit flags · When Layer 2 and Layer 3 conflict, ask user

---

## Layout Types (Multi-Illustration)

Only layouts used by the Multi-Illustration pipeline:

| Layout | Content Type | When to Use |
|--------|-------------|-------------|
| **hero-center** | 封面/封底/宣言 | Article cover, manifesto, section divider |
| **single-focus** | 金句/判断 | Key quote, single assertion, judgment |
| **grid-cards** | 规则/案例 | 3-12 parallel items, equal weight |
| **vertical-list** | 清单 | Checklist, ordered items, red-lines |
| **dense-grid** | 速查表 | Compact reference, number+name+example |
| **flow-chart** | 逻辑链/流程 | Causal chain, argument structure, process |
| **timeline** | 版本演进 | Chronological events, version history |
| **split-comparison** | 读者匹配/认知纠偏 | 2-3 way comparison, pros/cons |
| **binary-comparison** | 对比 | Strict A vs B with shared criteria |
| **center-stack** | 封底/关注引导 | Article ending, CTA, brand close |

---

## Keyword Shortcuts

User phrases auto-map to Layout × Mode combinations:

| User Says | Layout | Mode | Palette |
|-----------|--------|------|---------|
| "高密度信息大图" / "信息密集" | dense-grid | Swiss | IKB Blue or Lemon Yellow |
| "对比分析" / "vs" | binary-comparison | Swiss | Safety Orange |
| "流程图" / "步骤" | flow-chart | Swiss | IKB Blue |
| "时间线" / "演进" | timeline | Editorial | earth |
| "知识卡片" / "干货" | grid-cards | Editorial | warm |
| "杂志风" / "排版" | hero-center | Editorial | elegant or kami-parchment |
| "纸墨风" / "Kami" / "雅致" | grid-cards | Editorial | kami-parchment |
| "金句" / "引述" | single-focus | Editorial | auto-match |
| "速查表" / "cheatsheet" | dense-grid | Swiss | IKB Blue |
| "清单" / "红线" | vertical-list | Editorial | warm |
