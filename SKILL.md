---
name: "bird-science-video-generator"
description: "Cinematic bird science PiP generator with 640px editorial left-panel, plumage auto-coloring, and blur crossfade scenes. Dual-mode: Light Mode (晨曦暖色版, #F0EDE4 warm paper) and Dark Mode (暮影电影版, #000000 pure black). Invoke when user asks for鸟类科普画中画视频, wildlife documentary side panel, or科学鸟种介绍短片."
---

# Bird-Science-Video-Generator (V7.0)

## 核心定位

**双版本专业预设**：将鸟类生物学知识与人类文明链接转化为**实色背景上悬浮的极简信息层**。两个版本均为 100% 不透明实色背景，不依赖任何透明/毛玻璃效果。

- **左侧 1/3（640px）= "鸟类以鸟之名面板"**（Bird Universe Link Panel）：承载鸟的生物学信息（分类、羽色、习性、繁殖、分布）与文化联想（古建筑、鸟与人文、音乐、邮票、电影、IP形象、科技）。面板背景为实色（A 版暖黄 `#F0EDE4` / B 版纯黑 `#000000`）。
- **右侧 2/3（1280px）= 透明区域**：留给鸟类实拍素材，不渲染任何元素。

### 版本 A：晨曦暖色版（Light Mode）

| 属性 | 值 |
|------|-----|
| **背景色** | `#F0EDE4`（经典暖黄，100% 不透明） |
| **html, body** | `background: #F0EDE4` |
| **.scene** | `background: #F0EDE4` |
| **.left-panel** | `background: #F0EDE4`，`border-right: 1px solid rgba(0,0,0,0.1)` |
| **.closing-card** | `background: #F0EDE4` |
| **主文字色** | `#5C5040`（深咖啡色，WCAG AA 合规） |
| **副文字色** | `#8B7B6B`（中咖啡色，标签/副标题） |
| **文字阴影** | 无（暖色背景上不需要阴影） |
| **标题字重** | `700`（粗体，不过度） |
| **正文字重** | `400`（常规） |
| **入场动画** | **1/3 左侧滑入**：`x: -40 → 0`，`power3.out`，从左侧滑入面板 |
| **剪映混合模式** | **正片叠底**（Multiply）→ 在明亮/杂乱背景上获得极佳质感 |
| **适配场景** | 明亮天空、杂乱树林、花丛、草地、浅色生态背景 |

### 版本 B：暮影电影版（Dark Mode）

| 属性 | 值 |
|------|-----|
| **背景色** | `#000000`（纯黑，100% 不透明） |
| **html, body** | `background: #000000` |
| **.scene** | `background: #000000` |
| **.left-panel** | `background: #000000`，`border-right: 1px solid rgba(255,255,255,0.2)` |
| **.closing-card** | `background: #000000` |
| **主文字色** | `#FFFFFF`（纯白） |
| **副文字色** | `rgba(255,255,255,0.75)`（半透白，标签/副标题） |
| **文字阴影** | `text-shadow: 0 2px 2px rgba(0,0,0,0.9)`（2px 黑色投影） |
| **标题字重** | `900`（极粗） |
| **正文字重** | `600`（中粗） |
| **入场动画** | 标准淡入：`opacity: 0 → 1`，`y: 35 → 0`，`expo.out` |
| **剪映混合模式** | **滤色**（Screen）→ 在深色/暗光背景上获得发光电影感 |
| **适配场景** | 深色背景、纯净暗光、夜景、深色生态背景 |

7 个场景通过模糊交叉渐变切换。自动从羽毛颜色中提取主题色，**并匹配中国古典色谱名称**，构建统一的视觉辨识系统。**强制配甜美女生 TTS 旁白**（Edge-TTS `zh-CN-XiaoxiaoNeural`，rate=-10%），场景时长由 TTS 实测驱动。**视频总时长控制在 1–2 分钟（60–120s）**。若鸟种为某国国鸟，S1 展示国鸟 badge 并在 S6 自然融入。若为候鸟，S3 标注迁徙类型，S5 可视化迁徙路线/距离/途经国家。S6 文化维度覆盖古建筑、鸟与人文、鸟与音乐、鸟与邮票、鸟与电影、IP形象、**鸟与科技**、**鸟与天文/星座**八个方向，**最大化命中**——每个维度经 WebSearch 验证有真实关联即展示，无真实信息则不显示。

### 版本选择指南

```
┌─────────────────────────────────────────────────────┐
│ 你的视频背景素材是什么类型的？                        │
├─────────────────────────────────────────────────────┤
│ 明亮/杂乱/浅色（天空、花丛、草地、树林）              │
│   → 选择 A 版：晨曦暖色版                            │
│   → 在剪映中：正片叠底（Multiply）                   │
│   → 效果：暖纸底色融入背景，如翻开一本鸟类百科         │
├─────────────────────────────────────────────────────┤
│ 深色/纯净/暗光（夜景、深林、暗色背景）                │
│   → 选择 B 版：暮影电影版                            │
│   → 在剪映中：滤色（Screen）                         │
│   → 效果：纯白文字如电影字幕悬浮于暗夜                 │
└─────────────────────────────────────────────────────┘
```

**构建铁律**：每次构建视频时，必须同时输出 A 和 B 两个版本，在 HTML 中分别以 `_A` 和 `_B` 后缀命名，供用户根据背景素材选择最合适的版本。若用户已明确指定背景类型，则仅构建对应版本。

## Reference: Proven Production Style

本规范从多个已渲染验证的视频中提取：

| 参考视频 | 场景数 | 时长 | 面板风格 | 主题色系 |
|----------|--------|------|----------|----------|
| 蓝喉蜂虎 | 6 | 58s | 暖纸色 `#F0EDE4`（V5.2） | 酒红#6B3A2A / 宝蓝#3A7CA5 / 蓝绿#2D8B7E / 天蓝#5BA0C8 |
| 红头长尾山雀 | 6 | 49s | 暖纸色 `#F0EDE4`（V5.2） | 栗红#8B3A3A / 蓝灰#6B7B8D / 棕栗#A0522D |
| 戴胜 | 6 | 51s | 暖纸色 `#F0EDE4`（V5.2） | 暖橙褐#D4835A / 墨黑#1C1C1C / 象牙白#F5F0E8 |
| 红耳鹎 | 6 | 107s | 暖纸色 `#F0EDE4`（V5.2） | 胭脂#CC3333 / 玄青#1C1C1C / 赭石#8B6B4A |
| 戴胜（V5.6） | 7 | 88s | 纯黑 `#000000`（V5.6） | 棕栗#D4702A / 玄黑#1A1A1A / 葡萄酒#9B3A44 |

**V6.0 起所有新视频使用双版本预设**：A 版（晨曦暖色 `#F0EDE4`）+ B 版（暮影电影 `#000000`），两个版本同时输出。不再使用透明/毛玻璃方案。

---

## 1. 布局规范（Layout）

### 版本 A：晨曦暖色版 CSS

```css
/* ═══ V6.0-A: 晨曦暖色版 — 经典暖黄底 ═══ */
body, .scene {
  margin: 0; width: 1920px; height: 1080px;
  overflow: hidden; background: #F0EDE4;
  font-family: serif;
}

.left-panel {
  position: absolute; top: 0; left: 0;
  width: 640px; height: 1080px;
  background: #F0EDE4;
  border-right: 1px solid rgba(0,0,0,0.1);
  display: flex; flex-direction: column;
  padding: 80px 56px;
  box-sizing: border-box;
  overflow: hidden;
  gap: 22px;
}
.left-panel.center { justify-content: center; }

.scene { position: absolute; top: 0; left: 0; width: 1920px; height: 1080px; }
```

### 版本 B：暮影电影版 CSS

```css
/* ═══ V6.0-B: 暮影电影版 — 纯黑底 ═══ */
body, .scene {
  margin: 0; width: 1920px; height: 1080px;
  overflow: hidden; background: #000000;
  font-family: serif;
}

.left-panel {
  position: absolute; top: 0; left: 0;
  width: 640px; height: 1080px;
  background: #000000;
  border-right: 1px solid rgba(255,255,255,0.2);
  display: flex; flex-direction: column;
  padding: 80px 56px;
  box-sizing: border-box;
  overflow: hidden;
  gap: 22px;
}
.left-panel.center { justify-content: center; }

.scene { position: absolute; top: 0; left: 0; width: 1920px; height: 1080px; }
```

**硬约束**：
- 面板宽度 **640px**（精确 1/3），绝不改变
- A 版：面板背景 `#F0EDE4`（暖黄），文字 `#5C5040`（深咖啡）
- B 版：面板背景 `#000000`（纯黑），文字 `#FFFFFF`（纯白），`text-shadow: 0 2px 2px rgba(0,0,0,0.9)`
- 场景叠放：`#scene1` 可见，其余通过 GSAP 控制
- 两个版本均为 100% 不透明实色背景，**无透明、无毛玻璃、无 backdrop-filter**

---

## 2. 字体层级（Typography Scale）

### 版本 A：晨曦暖色版字体

```css
/* V6.3-A: 暖色系文字 — 深咖啡色，无阴影，最小字号 16px */
.hero-title   { font-size: 80px; font-weight: 700; color: #5C5040; line-height: 1.15; letter-spacing: 0.04em; }
.section-title { font-size: 56px; font-weight: 700; color: #5C5040; line-height: 1.2;  letter-spacing: 0.03em; }
.body-text     { font-size: 26px; font-weight: 400; color: #5C5040; line-height: 1.65; }
.body-text.lg  { font-size: 28px; }
.body-text.sm  { font-size: 22px; }
.label-text    { font-size: 20px; font-weight: 400; color: #8B7B6B; line-height: 1.4; letter-spacing: 0.08em; }
.stat-number   { font-size: 84px; font-weight: 700; line-height: 1; /* color 由主题色注入 */ }
.stat-label    { font-size: 24px; font-weight: 400; color: #8B7B6B; line-height: 1.4; }
.hero-subtitle { font-size: 28px; font-weight: 400; color: #8B7B6B; line-height: 1.4; }
```

### 版本 B：暮影电影版字体

```css
/* V6.3-B: 纯白文字 — 极粗字重 + 2px黑色投影，最小字号 16px */
.hero-title   { font-size: 80px; font-weight: 900; color: #FFFFFF; line-height: 1.15; letter-spacing: 0.04em; text-shadow: 0 2px 2px rgba(0,0,0,0.9); }
.section-title { font-size: 56px; font-weight: 900; color: #FFFFFF; line-height: 1.2;  letter-spacing: 0.03em; text-shadow: 0 2px 2px rgba(0,0,0,0.9); }
.body-text     { font-size: 26px; font-weight: 600; color: #FFFFFF; line-height: 1.65; text-shadow: 0 2px 2px rgba(0,0,0,0.9); }
.body-text.lg  { font-size: 28px; }
.body-text.sm  { font-size: 22px; }
.label-text    { font-size: 20px; font-weight: 400; color: rgba(255,255,255,0.75); line-height: 1.4; letter-spacing: 0.08em; text-shadow: 0 2px 2px rgba(0,0,0,0.9); }
.stat-number   { font-size: 84px; font-weight: 900; line-height: 1; text-shadow: 0 2px 2px rgba(0,0,0,0.9); /* color 由主题色注入 */ }
.stat-label    { font-size: 24px; font-weight: 400; color: rgba(255,255,255,0.75); line-height: 1.4; text-shadow: 0 2px 2px rgba(0,0,0,0.9); }
.hero-subtitle { font-size: 28px; font-weight: 400; color: rgba(255,255,255,0.75); line-height: 1.4; text-shadow: 0 2px 2px rgba(0,0,0,0.9); }
```

### 移动端适配（≤768px）— 两版本通用

```css
@media (max-width: 768px) {
  .hero-title   { font-size: 52px; }
  .section-title { font-size: 38px; }
  .body-text     { font-size: 24px; }
  .body-text.lg  { font-size: 26px; }
  .label-text    { font-size: 20px; }
  .stat-number   { font-size: 96px; }
  .stat-label    { font-size: 22px; }
  .hero-subtitle { font-size: 24px; }
  .info-tag      { font-size: 22px; }
  .swatch-label  { font-size: 16px; }
}
```

| 层级 | 字号 | A 版色值 | B 版色值 | 用途 |
|------|------|----------|----------|------|
| `hero-title` | 80px | `#5C5040` | `#FFFFFF` | 物种中文名 / 终极标题 |
| `section-title` | 50-58px | `#5C5040` | `#FFFFFF` | 场景标题 |
| `body-text` | 26px / 28px(lg) | `#5C5040` | `#FFFFFF` | 描述文字 |
| `label-text` | 20px | `#8B7B6B` | `rgba(255,255,255,0.75)` | 科属标签 / 场景副标签 |
| `stat-number` | 84px | 主题色注入 | 主题色注入 | 关键数字 |
| `stat-label` | 24px | `#8B7B6B` | `rgba(255,255,255,0.75)` | 数字说明 |
| `hero-subtitle` | 28px | `#8B7B6B` | `rgba(255,255,255,0.75)` | 英文名 / 俗称 |

### 对比度验证

| 版本 | 文字类型 | 背景色 | 文字色 | WCAG 对比度 |
|------|----------|--------|--------|------------|
| A 版 | hero-title | `#F0EDE4` | `#5C5040` | ~5.5:1 ✓ AA |
| A 版 | label-text | `#F0EDE4` | `#8B7B6B` | ~4.0:1 ✓ AA |
| B 版 | hero-title | `#000000` | `#FFFFFF` | 21:1 ✓ AAA |
| B 版 | label-text | `#000000` | `rgba(255,255,255,0.75)` | ~15:1 ✓ AAA |

---

## 3. 自动主题色系统（Auto Color Extraction + 中国古典色谱）

### Step A: 从羽色研究中提取 3-5 种 HEX + 匹配中国古典色谱名称

在研究阶段提取鸟种主色调，**每色匹配一个中国古典色谱名称**。参考《中国传统色：故宫里的色彩美学》等权威来源：

| 现代色系 | HEX 范围 | 古典色谱名参考 |
|----------|----------|---------------|
| 墨黑/玄黑 | `#1A1A1A`–`#2D2D2D` | 玄青、墨色、乌黑 |
| 天蓝/灰蓝 | `#5B8FA8`–`#6BA5C0` | 窃蓝、月白、天水碧 |
| 宝蓝/靛蓝 | `#3A6B8A`–`#3A7CA5` | 靛青、靛蓝、群青 |
| 酒红/绛红 | `#6B2A2A`–`#8B3A3A` | 绛紫、胭脂、檀色 |
| 栗红/棕红 | `#8B3A3A`–`#A0522D` | 赭石、绛色、茜色 |
| 橙褐/暖褐 | `#C08050`–`#D4835A` | 秋香、驼色、赭石 |
| 蓝灰/灰蓝 | `#5B6B80`–`#6B7B8D` | 鸦青、黛蓝、苍色 |
| 暖灰/银灰 | `#A89580`–`#C4BDB5` | 银鼠、霜色、月影 |
| 沙色/米白 | `#A88D63`–`#D4C5A0` | 缃色、驼色、牙色 |
| 乳白/纯白 | `#F0EDE4`–`#F5F0E8` | 素色、月白、霜色 |
| 蓝绿/碧色 | `#2D7B6E`–`#3A8B7E` | 碧色、石青、翠微 |
| 蓝紫/青紫 | `#4A5080`–`#5B5588` | 青莲、黛紫、藕荷 |

例如：

| 鸟种 | 提取色 | 古典色谱名 |
|------|--------|-----------|
| 蓝喉蜂虎 | 酒红 `#6B3A2A` / 宝蓝 `#3A7CA5` / 蓝绿 `#2D8B7E` / 天蓝 `#5BA0C8` / 沙色 `#A88D63` | 绛紫 / 靛青 / 碧色 / 月白 / 缃色 |
| 红头长尾山雀 | 栗红 `#8B3A3A` / 蓝灰 `#6B7B8D` / 棕栗 `#A0522D` / 墨黑 `#1C1C1C` / 乳白 `#F5F0E8` | 檀色 / 鸦青 / 赭石 / 玄青 / 素色 |
| 灰喜鹊 | 墨黑 `#2D2D2D` / 天蓝 `#5B8FA8` / 暖灰 `#B0A89C` / 纯白 `#F5F0E8` / 蓝紫 `#4A5580` | 玄青 / 窃蓝 / 银鼠 / 素色 / 青莲 |

### Step B: 映射到 CSS 变量

```css
/* ═══ Auto-generated per bird species ═══ */
/* Primary accent → divider, info-tag border, stat-number */
.divider { background: <primary-hex>; }

/* Secondary accents → info-tag variants, color swatch dots */
.info-tag { border-color: <primary-hex>; color: <darkened-primary>; }
.info-tag.slate  { border-color: <secondary-hex>; color: <darkened-secondary>; }
.info-tag.brown  { border-color: <tertiary-hex>; color: <darkened-tertiary>; }

/* Accent text classes */
.accent-primary   { color: <primary-hex>; }
.accent-secondary { color: <secondary-hex>; }
.accent-tertiary  { color: <tertiary-hex>; }

/* stat-number always uses primary accent */
.stat-number { color: <primary-hex>; }

/* fact-card left border = primary accent */
.fact-card { border-left: 4px solid <primary-hex>; }
```

---

## 3.5 羽色提取铁律（V4.9 新增 — 零遗漏、零错误）

**强制逐部位核对清单**。在研究阶段提取羽色时，必须遍历以下所有部位，不可跳过任何一项：

| 部位 | 必问 | 易犯错误 |
|------|------|----------|
| **头顶/额/冠** | 什么颜色？有无条纹/斑点？ | 忽略冠纹、中央冠纹 |
| **眼先/眼圈/眉纹** | 什么颜色？有无眼先斑？ | 眼先和眼圈是最易遗漏的区域 |
| **后颈/颈侧** | 与头顶同色还是异色？ | 后颈常被误与背羽合并 |
| **背/肩/上背** | 什么颜色？雄性雌性有无差异？ | 只取最显眼的背色，忽略肩羽 |
| **腰/尾上覆羽** | 什么颜色？飞行时可见的腰羽色？ | 翠鸟的腰羽钻蓝色是最经典特征，极易遗漏 |
| **胸** | 什么颜色？有无斑纹/横斑/鳞状斑？ | 胸腹连写，忽略胸腹间的渐变过渡 |
| **腹/胁/尾下覆羽** | 什么颜色？与胸部有色差吗？ | 胁部颜色常与腹部不同 |
| **翅/飞羽/覆羽** | 闭合时和展开时各是什么颜色？初级飞羽与次级飞羽有无色差？ | 只写"翅膀是某色"，忽略飞羽与覆羽的色差 |
| **尾羽** | 什么颜色？长度/形状？中央尾羽与外侧尾羽有无色差？ | 尾羽被完全忽略 |
| **喉/颏** | 什么颜色？与胸是否同色？ | 喉部白色斑块是许多鸟的关键鉴别特征 |
| **喙** | 什么颜色？上下喙是否同色？雄雌有无差异？ | 翠鸟雌鸟下喙橙红、雄全黑——这种性别差异极易漏写 |
| **脚/腿/跗跖** | 什么颜色？ | 脚爪颜色经常被遗忘 |
| **虹膜** | 什么颜色？ | 虹膜色常被忽略 |

**双重来源交叉验证**：
- 至少使用 **2 个独立来源**（如《中国鸟类野外手册》+ eBird/Macaulay Library 照片库 + 学术论文）交叉核对每处颜色
- 若两个来源矛盾 → 查阅第 3 个来源，或使用 Macaulay Library 高清照片人工目测验证
- **禁止仅凭百度百科或单一来源确定 HEX 色值**

**常见遗漏排行榜**（历史错误高发区）：
1. 🚨 **腰羽/尾上覆羽**：翠鸟的钻蓝色腰羽、鸫类白色腰斑——飞行时才显露的关键特征，最易忽略
2. 🚨 **喙的性别差异**：翠鸟雌下喙橙红、雄全黑——性别二态性极易遗漏
3. 🚨 **虹膜色**：多数鸟种描述不包含虹膜，但这是关键鉴别特征
4. ⚠️ **脚爪色**："体型特征"和"羽毛颜色"中都不包含脚爪，需单独核查

**HEX 取色原则**：
- 取典型光照下的实物照片（非标本，非极度逆光/过曝），取色区域中心的平均值
- 不得凭想象或"常见该色"赋值
- 最终 5 个 swatch 必须覆盖鸟体最主要、最具辨识度的 5 种羽色部位，不得遗漏任何大面积色块

---

## 4. 场景结构（Scene Architecture）

### 标准 7 场景模板

| 场景 | 参考时长 | 标签 | 标题 | 核心组件 |
|------|----------|------|------|----------|
| **S1 初见** | 10–18s | `label-text` (科属) | `hero-title` (物种名) | divider + hero-subtitle + national-bird-badge(若有) + body-text |
| **S2 羽色** | 10–18s | `label-text` "羽色密码" | `section-title` (羽色亮点) | color-swatch × 5 (swatch-dot + swatch-label) + body-text |
| **S3 习性** | 10–20s | `label-text` (习性标签) | `section-title` (习性标题) | body-text.lg + info-tag × N + **migration-tag(若为候鸟)** + **endemic-tag(V6.1: 中国特有/非特有标注)** + **fact-card(独特生物特性)** + body-text(note) |
| **S4 社交/巢穴** | 10–20s | `label-text` (社交/巢穴) | `section-title` | body-text.lg + info-tag + stat-number + stat-label + body-text(note) |
| **S5 迁徙/分布** | 12–24s | `label-text` | `section-title` | 迁徙路线/距离/途经国家（候鸟）或分布范围（留鸟） + body-text + info-tag × N + **migration-route-card(候鸟)** + **habitat-card(V6.2: 国内栖息地特点+关联湿地/保护区)** |
| **S6 收束** | 12–24s | `label-text` (文化/象征) | `hero-title` (升华词) | body-text.lg 文化关联 + body-text(secondary) 生态寄寓 + info-tag(closing) + **culture-image(V4.8: AI文化插图，极简淡墨)** |
| **S7 生态现状** | 10–20s | `label-text` "生态现状" | `section-title` (保护呼吁) | **protection-badge(保护等级重申)** + **conservation-status-card(种群趋势+威胁+保护文案)** + threat-tag × N + **conservation-call(呼吁文案)** |

**时长策略**（V5.0 强制 1–2 分钟）：
- 解说词总计 250–360 字，配合 Edge-TTS 晓晓 rate=-10% 约 60–120s
- 场景时长 = TTS 段长 + 0.5s 缓冲
- 总时长 = ceil(TTS 实测) + 1s（尾缓冲）
- 若 TTS 实测 < 60s → 增加解说词内容，重新生成 TTS，直到达标
- 若 TTS 实测 > 120s → 精简解说词，重新生成 TTS，直到达标
- 6 场景按解说词自然分布分配时长，不强制平均分割
- 最终淡出占用最后 1–1.5s

### S6 文化维度（V6.1 国际化 · 八维覆盖 · 最大化命中）—— 中国 + 国际双维度

S6 的使命是"鸟在人类文明中的投影"。**V6.1 起，每个文化维度都必须在检索时同步覆盖中国和国外内容**——既要探寻鸟在中国文化中的印记，也要挖掘它在世界文明中的回响。八个维度逐一检索，**最大化命中**——只要经 WebSearch 验证有真实关联就展示，能命中几个用几个，不设上限：

| 维度 | 检索关键词（中国） | 检索关键词（国际） | 典型关联 | 示例 |
|------|-----------|----------|------|------|
| **古建筑** | `<鸟名> 建筑 装饰 构件` + `燕尾枋 雀替 斗拱 脊兽` | `<bird name> architecture temple fresco column ornament` + `<bird> ancient Egypt Minoan Greek column` | 燕子→燕尾枋（中国）· 戴胜→米诺斯壁画/古埃及圣书体（国际）· 鹰→罗马军团徽章（国际） | "北京的燕尾枋，屋脊两端飞翘如燕；三千年前克里特岛米诺斯壁画中的戴胜，已在爱琴海边梳理羽冠" |
| **鸟与人文** | `<鸟名> 民间工艺 非遗 传统技艺` + `点翠 刺绣 青花 剪纸` | `<bird name> folklore mythology Bible Quran Torah legend national symbol` | 翠鸟→点翠（中国）· 戴胜→古兰经/所罗门王/示巴女王（国际）· 鸽子→诺亚方舟橄榄枝（国际）· 鹤→日本折纸千纸鹤（国际） | "在古兰经中，戴胜为所罗门王带来了示巴女王的消息——它也是跨三大宗教的信使" |
| **鸟与音乐** | `<鸟名> 音乐 古典音乐 歌曲 芭蕾` + `<鸟名> 作曲家 作品` | `<bird name> music symphony composer opera ballet` | 天鹅→柴可夫斯基《天鹅湖》（国际）· 云雀→沃恩·威廉斯（国际）· 百鸟朝凤→唢呐名曲（中国） | "从柴可夫斯基的天鹅湖到东方的百鸟朝凤，它的羽翼掠过每一种文明的乐谱" |
| **鸟与邮票** | `<鸟名> 邮票 中国邮政 香港邮政 澳门邮电 中华邮政` + `<鸟名> 邮票编号 志号` | `<bird name> stamp postal service country` + `<bird> postage stamp Israel India France UK` | 戴胜→中国T79（中国）· 戴胜→以色列/印度/法国/摩洛哥等数十国邮票（国际）· 丹顶鹤→中日联合发行 | "不只中国邮政把它的身影印上方寸——从以色列到印度，从法国到摩洛哥，数十个国家让它跨越国界" |
| **鸟与电影** | `<鸟名> 电影 纪录片 动画` + `<鸟名> 影视 角色` | `<bird name> movie film documentary animation` | 企鹅→《帝企鹅日记》（国际）· 金刚鹦鹉→《里约大冒险》（国际）· 鸬鹚→《三峡好人》（中国） | "雅克·贝汉用四年追踪候鸟跨越大陆——每一帧都是对天空最虔诚的叩问" |
| **IP形象** | `<鸟名> IP形象 原型 吉祥物` + `<鸟名> 品牌 logo 动漫` | `<bird name> mascot logo brand cartoon game` | 雪鸮→海德薇《哈利·波特》（国际）· 皇帝企鹅→Linux Tux（国际）· 蜂鸟→Twitter logo | "海德薇的纯白羽翼承载着魔法世界的每一封信——它的原型正是北极圈的雪鸮" |
| **鸟与科技** | `<鸟名> 仿生学 空气动力学 工程 biomimicry` | `<bird name> biomimicry engineering technology` | 游隼→B-2飞翼（国际）· 翠鸟→新干线车头（日本/国际）· 猫头鹰→锯齿尾缘静音（国际） | "游隼用四亿年打磨出的空气动力学，至今仍是人类工程师的最高教材" |
| **鸟与天文/星座** | `<鸟名> 星座 天文 星宿 二十八宿 三垣` | `<bird name> constellation astronomy zodiac star` | 天鹅→天鹅座（国际）· 天鹰→天鹰座（国际）· 朱雀→二十八宿南方七宿（中国） | "夏季夜空，天鹅座展翅横跨银河；在中国，朱雀统领南方七宿——同一天空，不同文明各自仰望" |

**V6.1 国际化铁律**：
- 每个维度检索时必须**同步检索中国和国外两组关键词**，不得只看中文资料
- 展示内容必须**至少涵盖一个国际/国外文化关联**（除非该维度确实无国际关联，如燕尾枋确为中国独有）
- 国外内容来源必须可靠：Wikipedia、大英百科全书、BBC、学术论文、各国邮政官网等
- 国外文化关联的引入应自然融入，不额外增加板块——"一句话串联中外"是最佳形式
- **零幻觉原则仍优先**——没有真实国际关联的维度，不硬凑

**V5.0 鸟与科技严选规则**：
- 必须有**具体的、知名的工程应用**（如翠鸟喙→新干线500系车头），不能是泛泛的"飞行启发"或"空气动力学原理"
- 若该鸟种无突出的科技关联 → **完全不展示科技维度**，不凑数、不硬写
- 典型的合格科技关联：翠鸟→新干线车头、游隼→B-2飞翼、猫头鹰→锯齿尾缘静音、天鹅→机身流线型、大型猛禽→翼梢小翼
- 典型的不合格关联："XX鸟的飞行姿态启发了人类对飞行的向往"（太泛）、"XX鸟的羽毛结构启发了保温材料"（无具体产品名）

**V5.2 最大化命中原则**：
- 八个维度逐一检索，每个维度只要经 WebSearch 验证有真实关联 → **就展示**，能命中几个用几个
- 不设"至少命中一个"的下限，也不设"不超过N个"的上限——完全由真实关联的数量驱动
- 四个最常命中的普适维度优先检索：鸟与人文 > 鸟与邮票 > 鸟与天文/星座 > 古建筑
- 四个需要特定条件的维度后检索：鸟与音乐 > 鸟与电影 > IP形象 > 鸟与科技
- S6 内容按命中维度数自适应排版：≤2 个 → 标准版式；3–4 个 → body-text 区用 `.body-text.sm`（22px）多行承载；≥5 个 → 启用双列布局或紧凑列表

**V4.9 幻觉控制**：音乐、邮票、电影、IP、**科技**和**天文星座**信息必须经 WebSearch 交叉验证。若该鸟种确实有知名作品关联或被发行过邮票/有真实科技应用/有对应星座星宿 → 可写；若没有真实信息 → **完全不显示、不提及该维度**。最大化命中 ≠ 无中生有，零幻觉原则优先于命中数量。

**V6.3 邮票零幻觉铁律**：
- 鸟与邮票维度必须包含**三个硬性字段**：① **发行年份**（如"2005年"）② **邮票编号/志号**（如"T79""2005-15""2024-9"）③ **发行机构**（如"中国邮政"）
- 三个字段缺一不可，缺少任何一个 → 视为"未验证"，**不展示邮票维度**
- 邮票编号必须经 WebSearch 交叉验证，从权威来源（中国邮政官网、邮票目录网站、集邮数据库）确认
- 常见的邮票编号格式：中国邮政 → "T79""2005-15""2024-9"；香港邮政 → "HKxxx"；澳门邮电 → "Sxxx"；中华邮政（台湾）→ "特xxx""纪xxx"
- 若该鸟种确实被发行过邮票但无法确认编号 → 标注"邮票存在但编号待验证"，**待验证状态下不展示**
- 示例合格展示：`"中国邮政 2005年 编号2005-15《向海自然保护区》"`
- 示例不合格展示（禁止）：`"中国邮政发行过邮票"`（无年份无编号）、`"出现在邮票上"`（太模糊）
- **若该鸟种无邮票发行 → 完全不显示、不提及邮票维度**

**国鸟维度（V4.5 新增）**：若鸟种确为某国国鸟（经 WebSearch 交叉验证），在 `body-text` 生态寄寓收束句中自然提及国鸟身份。例如戴胜：`body-text` 中"2008年当选以色列国鸟，跨越万里的生命传奇"。**若并非国鸟则完全不提及**。

**S6 写作约束**（V5.2 最大化命中版）：
- `body-text.lg`（28px）：1-2 句文化关联核心句，将鸟的生物学特征与人类文明节点精准对应
- `body-text`（26px）：N 句文化关联展开句，**按命中维度逐一展开**——每个命中的维度用 1 句凝练表达（如"在邮票的方寸之间……""夏季星空的天鹅座……"）
- `body-text.sm`（22px，V6.3 更新）：命中维度 > 3 时启用，承载额外维度文字，确保不因空间限制删减内容
- `info-tag(closing)`：一组文化标签（如"青鸟信使 · 花鸟画主角 · 台湾邮票1997"），**紧接收束句之后**
- 八个维度最大化命中，**不贪多但也不自限**——真实关联有多少就展示多少

---

## 5. 组件库（Component Library）

### 5.0 开幕卡片（Opening Card）— V5.2 新增 / V5.3 透明化

**视频第 0–2s**。在 S1 之前先展示一张全屏开幕卡片，作为视频的"封面"。展示物种名、英文名和一句凝练的主题标签，然后通过毛玻璃过渡到 S1。

```html
<!-- ═══ Opening Card: 插在 #scene1 之前 ═══ -->
<div id="scene0" class="scene" style="z-index: 10; opacity: 1;">
  <div class="left-panel opening-panel center">
    <div class="radial-glow s0-g1" style="width:400px;height:400px;top:200px;left:120px;background:radial-gradient(circle,rgba(255,255,255,0.06) 0%,rgba(255,255,255,0) 70%);" data-layout-allow-overflow></div>
    <div class="radial-glow s0-g2" style="width:280px;height:280px;bottom:100px;right:-60px;background:radial-gradient(circle,rgba(255,255,255,0.04) 0%,rgba(255,255,255,0) 70%);" data-layout-allow-overflow></div>
    <div class="opening-eyebrow s0-eyebrow">鸟类以鸟之名</div>
    <div class="hero-title s0-hero" style="font-size:88px;">{{SPECIES_NAME}}</div>
    <div class="divider s0-div" style="width:100px;"></div>
    <div class="hero-subtitle s0-sub">{{ENGLISH_NAME}}</div>
    <div class="opening-tag s0-tag">{{THEME_TAG}}</div>
  </div>
</div>
```

CSS（V5.3 更新）:
```css
.opening-eyebrow {
  font-size: 16px; font-weight: 400;
  color: {{PRIMARY_HEX}}; letter-spacing: 0.12em;
  text-transform: uppercase;
  text-shadow: 0 2px 4px rgba(0,0,0,0.5);  /* ← V5.3 */
}
.opening-tag {
  font-size: 20px; font-weight: 400;
  color: rgba(255,255,255,0.75); letter-spacing: 0.06em;  /* ← V5.3: 亮色 */
  margin-top: 12px;
  text-shadow: 0 2px 4px rgba(0,0,0,0.5);  /* ← V5.3 */
}
```

**`THEME_TAG` 取值**：一句话凝练该鸟种的独特标签，如"长尾鹊 · 青鸟信使""翠羽点金 · 空中猎手""五色浓缩在九厘米"。

GSAP 动画（开幕卡的使命是"先声夺人，快速退场"）:
```js
// ═══ Opening Card (0–2s) ═══
tl.to(".s0-g1", { scale: 1.06, duration: 2.5, ease: "sine.inOut", yoyo: true, repeat: 0 }, 0.1);
tl.to(".s0-g2", { scale: 1.05, duration: 2.2, ease: "sine.inOut", yoyo: true, repeat: 0 }, 0.15);
tl.fromTo(".s0-eyebrow", { opacity: 0, y: 10 }, { opacity: 1, y: 0, duration: 0.5, ease: "power2.out" }, 0.1);
tl.fromTo(".s0-hero",    { opacity: 0, y: 40, scale: 0.95 }, { opacity: 1, y: 0, scale: 1, duration: 0.8, ease: "expo.out" }, 0.25);
tl.fromTo(".s0-div",     { scaleX: 0, transformOrigin: "center" }, { scaleX: 1, duration: 0.5, ease: "power3.out" }, 0.7);
tl.fromTo(".s0-sub",     { opacity: 0, x: -15 }, { opacity: 1, x: 0, duration: 0.5, ease: "power2.out" }, 1.0);
tl.fromTo(".s0-tag",     { opacity: 0, y: 10 }, { opacity: 1, y: 0, duration: 0.5, ease: "power2.out" }, 1.2);

var OPENING_EXIT = 2.0;
// Opening → S1: blur crossfade (same as scene transitions)
tl.to("#scene0",  { filter: "blur(20px)", scale: 1.04, duration: 0.55, ease: "power1.in" }, OPENING_EXIT);
tl.to("#scene0",  { opacity: 0, duration: 0.35, ease: "power1.in" }, OPENING_EXIT + 0.4);
tl.fromTo("#scene1", { filter: "blur(20px)", scale: 0.96, opacity: 0 }, { filter: "blur(20px)", scale: 0.96, opacity: 1, duration: 0.3, ease: "power1.inOut" }, OPENING_EXIT + 0.5);
tl.to("#scene1",  { filter: "blur(0px)", scale: 1, duration: 0.55, ease: "power1.out" }, OPENING_EXIT + 0.75);
tl.set("#scene0", { visibility: "hidden" }, OPENING_EXIT + 1.4);
```

**硬约束**：
- 开幕卡片占据 `#scene0`，z-index: 10，在 S1 之上
- 总停留时间 **2.0s**，快速建立印象后退场
- 过渡方式与场景间完全一致（blur crossfade）
- 开幕卡片退场后，S1 入场动画正常执行（S1 GSAP 时间基于 `S1_START = 2.0`，即开幕卡片结束后 S1 才开始）
- `THEME_TAG` 必须与鸟种的文化/生物核心亮点精准对应

### 5.1 色彩色板（color-swatch）— V4.8 新增古典色谱名

```html
<div class="color-swatch s2-s1">
  <div class="swatch-dot" style="background:#6B3A2A;"></div>
  <div class="swatch-label">头顶·酒红</div>
  <div class="swatch-label-cn">绛紫</div>
</div>
```

CSS（V5.3 更新）:
```css
.color-swatch { display: flex; flex-direction: column; align-items: center; gap: 8px; }
.swatch-dot   { width: 40px; height: 40px; border-radius: 50%; border: 1px solid rgba(255,255,255,0.4); }  /* ← V5.4: 白色边框 */
.swatch-label { font-size: 16px; color: rgba(255,255,255,0.85); text-shadow: 2px 2px 4px rgba(0,0,0,0.8); }  /* ← V5.4: 强阴影 */
.swatch-label-cn { font-size: 16px; color: rgba(255,255,255,0.55); letter-spacing: 0.05em; text-shadow: 2px 2px 4px rgba(0,0,0,0.8); }  /* ← V5.4: 强阴影 */
```

GSAP 入场:
```js
tl.fromTo(".s2-s1", { opacity: 0, scale: 0.7 }, { opacity: 1, scale: 1, duration: 0.4, ease: "back.out(1.3)" }, start + 1.2);
tl.fromTo(".s2-s2", { opacity: 0, scale: 0.7 }, { opacity: 1, scale: 1, duration: 0.4, ease: "back.out(1.3)" }, start + 1.35);
// ... stagger each by 0.15s
```

### 5.2 信息标签（info-tag）

```html
<span class="info-tag">蜻蜓 38%</span>
<span class="info-tag brown">松毛虫卵</span>
<span class="info-tag slate">鸟界最强社交达人</span>
```

CSS（V5.3 更新）:
```css
.info-tag {
  font-size: 20px; font-weight: 400;
  border: 2px solid {{PRIMARY_HEX}}; color: {{PRIMARY_HEX}};  /* ← V5.3: 亮色主题色，非加深色 */
  padding: 5px 14px; border-radius: 3px;
  text-shadow: 0 1px 3px rgba(0,0,0,0.4);  /* ← V5.3 */
}
.info-tag.sec { border-color: {{SECONDARY_HEX}}; color: {{SECONDARY_HEX}}; }
.info-tag.tri { border-color: {{TERTIARY_HEX}}; color: {{TERTIARY_HEX}}; }
/* V6.3: 移动端 ≤768px 时 info-tag 字号 22px */
@media (max-width: 768px) {
  .info-tag { font-size: 22px; }
}
.tag-row { display: flex; gap: 12px; flex-wrap: wrap; }
```

GSAP 入场:
```js
tl.fromTo(".s3-tags", { opacity: 0, y: 12 }, { opacity: 1, y: 0, duration: 0.5, ease: "power1.out" }, start + 1.6);
```

### 5.3 知识点卡片（fact-card）

### 5.2b 迁徙类型标签（migration-tag）— V4.7 新增

**仅当鸟种为候鸟时展示**。放在 S3 info-tag 组之后、fact-card 之前，用于标识迁徙类型。

```html
<span class="migration-tag s3-mig">🕊 夏候鸟 · 每年往返繁殖地与越冬地</span>
```

CSS（V5.3 更新）:
```css
.migration-tag {
  font-size: 20px; font-weight: 400;
  color: {{PRIMARY_HEX}};
  background: rgba(255,255,255,0.06);  /* ← V5.3: 白色半透明底 */
  border: 1px solid rgba(255,255,255,0.2);  /* ← V5.3: 白色边框 */
  padding: 5px 14px; border-radius: 3px;
  display: inline-block; width: fit-content;
  text-shadow: 0 1px 3px rgba(0,0,0,0.4);  /* ← V5.3 */
}
```

**迁徙类型值**（必须经 WebSearch 验证）：
| 类型 | 含义 | 标签示例 |
|------|------|----------|
| 夏候鸟 | 春夏在本地区繁殖，秋冬南迁越冬 | "🕊 夏候鸟 · 春夏来此繁殖" |
| 冬候鸟 | 秋冬来本地区越冬，春夏北返繁殖 | "🕊 冬候鸟 · 深秋飞来越冬" |
| 旅鸟 | 迁徙途中经过本地区，不停留繁殖或越冬 | "🕊 旅鸟 · 迁徙途经此地" |
| 留鸟 | 不迁徙，终年居留 | **不显示 migration-tag，S5 展示分布范围代替** |

GSAP 入场（紧跟 info-tag 之后）:
```js
tl.fromTo(".s3-mig", { opacity: 0, y: 8 }, { opacity: 1, y: 0, duration: 0.5, ease: "power2.out" }, start + 1.8);
```

### 5.2c 中国特有标注（endemic-tag）— V6.1 新增

**任何鸟种都必须展示**。放在 S3 migration-tag 之后（若无则接 info-tag 之后），标明该鸟种是否为中国特有。

```html
<!-- 若为中国特有种 -->
<span class="endemic-tag s3-endemic">🇨🇳 中国特有鸟种 · {{ENDEMIC_LEVEL}}</span>

<!-- 若非中国特有 -->
<span class="endemic-tag s3-endemic" style="border-style:dashed;">🌍 非中国特有 · 广布于{{DISTRIBUTION_SUMMARY}}</span>
```

CSS（V6.1，A版暖色）：
```css
.endemic-tag {
  font-size: 20px; font-weight: 400;
  color: {{PRIMARY_HEX}};
  background: rgba(0,0,0,0.03);
  border: 1px solid rgba(0,0,0,0.1);
  padding: 5px 14px; border-radius: 3px;
  display: inline-block; width: fit-content;
}
/* 非中国特有：虚线边框以示区分 */
.endemic-tag:has(+ .fact-card, .s3-endemic[style*="dashed"]) {
  /* style directly on element via inline */
}
```

**特有等级值**（必须经 WebSearch 验证）：
| 类型 | 含义 | 标签示例 | 边框样式 |
|------|------|----------|----------|
| 全国特有 | 仅分布于中国境内 | "🇨🇳 中国特有鸟种 · 仅分布于中国" | 实线（solid） |
| 区域特有 | 仅分布于中国某区域 | "🇨🇳 中国特有鸟种 · 仅分布于横断山区" | 实线（solid） |
| 非特有·广布种 | 分布超出中国 | "🌍 非中国特有 · 广布于欧亚非三大洲" | **虚线（dashed）** |

**已知中国特有鸟种参考**（每次仍需 WebSearch 交叉验证）：
| 鸟种 | 特有等级 | 分布 |
|------|----------|------|
| 震旦鸦雀 | 中国特有 | 长江中下游、东北芦苇荡 |
| 红腹锦鸡 | 中国特有 | 秦岭及中国中西部 |
| 黄腹角雉 | 中国特有 | 中国东南部山区 |
| 四川山鹧鸪 | 中国特有 | 四川盆地周边 |
| 绿尾虹雉 | 中国特有 | 青藏高原东缘 |
| 海南山鹧鸪 | 中国特有 | 仅海南岛 |

GSAP 入场（紧跟 migration-tag 之后）:
```js
tl.fromTo(".s3-endemic", { opacity: 0, x: -20 }, { opacity: 1, x: 0, duration: 0.5, ease: "power3.out" }, start + 2.0);
```

### 5.3 知识点卡片（fact-card）

```html
<div class="fact-card s3-card">
  <div class="body-text" style="font-size:22px;">
    <span class="accent-primary">捕蜂绝技：</span>捕获蜜蜂后<br/>用喙反复敲击树枝<br/>敲掉毒刺，从容吞下
  </div>
</div>
```

CSS（V5.3 更新）:
```css
.fact-card {
  display: flex; flex-direction: column;
  padding: 24px 28px;
  background: rgba(255,255,255,0.06);  /* ← V5.3: 白色半透明底 */
  border-left: 4px solid {{PRIMARY_HEX}};
  border: 1px solid rgba(255,255,255,0.15);  /* ← V5.3: 白色边框 */
  border-left: 4px solid {{PRIMARY_HEX}};  /* ← 左侧强调色保留 */
  gap: 10px;
}
```

GSAP 入场（延迟于文字，从右侧滑入）:
```js
tl.fromTo(".s3-card", { opacity: 0, x: 20 }, { opacity: 1, x: 0, duration: 0.6, ease: "power3.out" }, start + 0.7);
```

### 5.4 大数据展示（stat-number + stat-label）

```html
<div style="display:flex; align-items:baseline; gap:18px;">
  <div class="stat-number s4-stat">5–7月</div>
  <div class="stat-label s4-statl">繁殖季节</div>
</div>
```

GSAP 入场（弹性动画）:
```js
tl.fromTo(".s4-stat",  { opacity: 0, scale: 0.8 }, { opacity: 1, scale: 1, duration: 0.7, ease: "elastic.out(1, 0.5)" }, start + 0.8);
tl.fromTo(".s4-statl", { opacity: 0, y: 8 },     { opacity: 1, y: 0, duration: 0.5, ease: "power2.out" }, start + 1.1);
```

**V4.1 移动端适配**：`≤768px` 时 `.stat-number` 字号 +15% → 94px（见 Section 2 媒体查询）。

### 5.5 迁徙/分布可视化

**迁徙流向**（候鸟用）：
```html
<div style="display:flex; gap:24px; align-items:center;">
  <div style="..."><div class="migration-label s5-t1">东南亚</div><div class="body-text" style="font-size:18px;">越冬地</div></div>
  <div class="body-text" style="font-size:36px; color:<primary-hex>;">→</div>
  <div style="..."><div class="migration-label s5-t2">中国华南</div><div class="body-text" style="font-size:18px;">繁殖地</div></div>
</div>
```

**迁徙路线卡片（migration-route-card）— V4.7 新增，候鸟必选**：

```html
<div class="migration-route-card s5-route">
  <div class="route-header">
    <span class="route-icon">🗺</span>
    <span class="route-name">{{ROUTE_NAME}}</span>
  </div>
  <div class="route-stat s5-dist">
    <span class="route-stat-num">{{MIGRATION_DISTANCE}}</span>
    <span class="route-stat-unit">公里</span>
  </div>
  <div class="route-path s5-path">
    <span class="route-dot"></span>
    <span class="route-line"></span>
    <span class="route-dot"></span>
    <span class="route-line"></span>
    <span class="route-dot"></span>
  </div>
  <div class="route-countries s5-countries">{{COUNTRIES_LIST}}</div>
  <div class="route-label s5-label">{{SPECIAL_LABEL}}</div>
</div>
```

CSS（V5.3 更新）:
```css
.migration-route-card {
  display: flex; flex-direction: column;
  padding: 20px 24px;
  background: rgba(255,255,255,0.06);  /* ← V5.3: 白色半透明底 */
  border: 1px solid rgba(255,255,255,0.2);  /* ← V5.3: 白色边框 */
  border-radius: 4px;
  gap: 12px;
}
.route-header { display: flex; align-items: center; gap: 10px; }
.route-icon   { font-size: 22px; }
.route-name   { font-size: 19px; font-weight: 600; color: #F5F0E8; text-shadow: 0 2px 4px rgba(0,0,0,0.5); }  /* ← V5.3 */
.route-stat { display: flex; align-items: baseline; gap: 8px; }
.route-stat-num  { font-size: 42px; font-weight: 700; color: {{PRIMARY_HEX}}; line-height: 1; text-shadow: 0 2px 6px rgba(0,0,0,0.6); }  /* ← V5.3 */
.route-stat-unit { font-size: 18px; color: rgba(255,255,255,0.85); text-shadow: 0 2px 4px rgba(0,0,0,0.5); }  /* ← V5.3 */
.route-path { display: flex; align-items: center; gap: 4px; }
.route-dot  { width: 8px; height: 8px; border-radius: 50%; background: {{PRIMARY_HEX}}; }
.route-line { flex: 1; height: 1px; background: rgba(255,255,255,0.25); }  /* ← V5.3 */
.route-countries { font-size: 18px; color: rgba(255,255,255,0.85); line-height: 1.6; text-shadow: 0 2px 4px rgba(0,0,0,0.5); }  /* ← V5.3 */
.route-label {
  font-size: 16px; font-weight: 600;
  color: {{PRIMARY_HEX}};
  background: rgba(255,255,255,0.08);  /* ← V5.3 */
  padding: 4px 12px; border-radius: 2px;
  width: fit-content;
  text-shadow: 0 1px 3px rgba(0,0,0,0.4);  /* ← V5.3 */
}
```

**迁徙路线数据要求（V4.7 零幻觉约束）**：
| 字段 | 来源 | 示例 | 验证规则 |
|------|------|------|----------|
| `ROUTE_NAME` | WebSearch `<鸟名> 迁徙路线 迁飞路线` | "东亚-澳大利西亚迁飞路线" | **必须是公认的科学命名**，如"密西西比迁飞路线""东大西洋迁飞路线""中亚迁飞路线"等 |
| `MIGRATION_DISTANCE` | WebSearch `<鸟名> 迁徙距离 公里` | "12,000" | 必须是数字，取整数 |
| `COUNTRIES_LIST` | WebSearch `<鸟名> 迁徙 途经国家` | "途经：俄罗斯→中国→朝鲜半岛→日本→东南亚→澳大利亚" | 必须列举真实途经国家/地区，用 → 连接 |
| `SPECIAL_LABEL` | 综合分析 | "跨洲迁徙""跨北极圈""丝绸之路沿线""跨三大洲"等 | 若迁徙路线跨越洲界/洋界/极地/丝绸之路沿线，必须标注；若无特殊地理标签则不显示 |

GSAP 入场（stagger 逐层揭示）:
```js
tl.fromTo(".s5-route",    { opacity: 0, y: 20 }, { opacity: 1, y: 0, duration: 0.6, ease: "power2.out" }, start + 1.0);
tl.fromTo(".s5-dist",     { opacity: 0, y: 10 }, { opacity: 1, y: 0, duration: 0.5, ease: "power2.out" }, start + 1.12);
tl.fromTo(".s5-path",     { opacity: 0, scaleX: 0, transformOrigin: "left center" }, { opacity: 1, scaleX: 1, duration: 0.5, ease: "power3.out" }, start + 1.24);
tl.fromTo(".s5-countries",{ opacity: 0, y: 8 },  { opacity: 1, y: 0, duration: 0.5, ease: "power2.out" }, start + 1.36);
tl.fromTo(".s5-label",    { opacity: 0, scale: 0.9 }, { opacity: 1, scale: 1, duration: 0.4, ease: "back.out(1.2)" }, start + 1.48);
```

**分布范围**（留鸟用）：
```html
<div class="body-text lg s6-body">
  从西藏雪山到台湾海峡<br/>从秦岭山脉到海南椰林<br/>整个中国南部<br/>都是它的家
</div>
```

### 5.5b 栖息地卡片（habitat-card）— V6.2 新增

**S5 专属，候鸟留鸟均展示**。位于 migration-route-card（候鸟）或分布范围描述（留鸟）之后，展示该鸟种在中国境内的典型栖息地生态环境特征，以及关联的知名湿地/自然保护区。

```html
<div class="habitat-card s5-habitat">
  <div class="habitat-header">
    <span class="habitat-icon">🌿</span>
    <span class="habitat-title">{{HABITAT_TYPE}}</span>
  </div>
  <div class="habitat-desc s5-habitat-desc">{{HABITAT_DESCRIPTION}}</div>
  {{WETLAND_SECTION}}
</div>
```

**湿地子卡片**（若有关联湿地/保护区，嵌套在 habitat-card 内）：
```html
<div class="wetland-subcard s5-wetland">
  <div class="wetland-header">
    <span class="wetland-icon">💧</span>
    <span class="wetland-name">{{WETLAND_NAME}}</span>
  </div>
  <div class="wetland-desc s5-wetland-desc">{{WETLAND_DESCRIPTION}}</div>
  <div class="wetland-tag s5-wetland-tag">{{WETLAND_TAG}}</div>
</div>
```

CSS（V6.2，A/B 两版通用基类，颜色由版本变量控制）:
```css
.habitat-card {
  display: flex; flex-direction: column;
  padding: 20px 24px;
  background: rgba(255,255,255,0.06);  /* B版：白色半透明底 | A版：rgba(0,0,0,0.03) */
  border: 1px solid rgba(255,255,255,0.2);  /* B版：白色边框 | A版：rgba(0,0,0,0.1) */
  border-radius: 4px;
  gap: 12px;
}
.habitat-header { display: flex; align-items: center; gap: 10px; }
.habitat-icon   { font-size: 22px; }
.habitat-title  { font-size: 19px; font-weight: 600; color: #FFFFFF; text-shadow: 0 2px 2px rgba(0,0,0,0.9); }  /* B版 | A版：color: #5C5040 */
.habitat-desc   { font-size: 18px; color: rgba(255,255,255,0.85); line-height: 1.6; text-shadow: 0 2px 2px rgba(0,0,0,0.9); }  /* B版 | A版：color: #5C5040 */

/* 湿地子卡片 */
.wetland-subcard {
  display: flex; flex-direction: column;
  padding: 16px 20px;
  background: rgba(255,255,255,0.04);  /* B版 | A版：rgba(0,0,0,0.02) */
  border: 1px solid rgba(255,255,255,0.12);  /* B版 | A版：rgba(0,0,0,0.08) */
  border-radius: 3px;
  gap: 8px;
  margin-top: 4px;
}
.wetland-header { display: flex; align-items: center; gap: 8px; }
.wetland-icon   { font-size: 18px; }
.wetland-name   { font-size: 17px; font-weight: 600; color: #FFFFFF; text-shadow: 0 2px 2px rgba(0,0,0,0.9); }  /* B版 | A版：color: #5C5040 */
.wetland-desc   { font-size: 16px; color: rgba(255,255,255,0.75); line-height: 1.55; text-shadow: 0 2px 2px rgba(0,0,0,0.9); }  /* B版 | A版：color: #8B7B6B */
.wetland-tag {
  font-size: 16px; font-weight: 600;
  color: {{PRIMARY_HEX}};
  background: rgba(255,255,255,0.08);  /* B版 | A版：rgba(0,0,0,0.05) */
  padding: 3px 10px; border-radius: 2px;
  width: fit-content;
  text-shadow: 0 2px 2px rgba(0,0,0,0.9);  /* B版 | A版：无 */
}
```

**栖息地数据要求（V6.2 零幻觉约束）**：
| 字段 | 来源 | 示例 | 验证规则 |
|------|------|------|----------|
| `HABITAT_TYPE` | WebSearch `<鸟名> 栖息地 生态环境` | "亚热带常绿阔叶林" / "芦苇湿地与河口滩涂" / "高山草甸与灌丛" | 必须是公认的生态学术语，描述该鸟种在中国的典型栖息地类型 |
| `HABITAT_DESCRIPTION` | 综合研究 | "偏好低山丘陵的阔叶林和混交林，常活动于林缘、溪流附近，海拔300-1800米" | 1-2 句凝练描述，涵盖植被类型、地形特征、海拔范围等关键生态要素 |
| `WETLAND_NAME` | WebSearch `<鸟名> 湿地 自然保护区 国家公园` | "江西鄱阳湖国家级自然保护区" / "云南大山包黑颈鹤自然保护区" | 必须是官方正式名称，经 WebSearch 交叉验证 |
| `WETLAND_DESCRIPTION` | WebSearch `<湿地名> 生态特征` | "中国最大的淡水湖湿地，国际重要湿地（Ramsar Site），每年吸引数十万只候鸟在此停歇" | 1 句凝练描述湿地生态特征+与该鸟种的具体关联 |
| `WETLAND_TAG` | 综合分析 | "国际重要湿地" / "国家级自然保护区" / "世界自然遗产" / "Ramsar Site" | 标注湿地保护等级或国际认证 |

**湿地关联规则**：
- 若该鸟种在中国境内有明确的湿地/自然保护区分布 → 展示 1-2 处关键湿地
- 若该鸟种不依赖湿地生态（如纯森林鸟类）→ 仅展示 `habitat-card`，不展示 `wetland-subcard`
- 若该鸟种为留鸟且分布广泛 → 选择最具代表性的保护区/国家公园
- 若该鸟种为候鸟 → 优先选择繁殖地或越冬地的关键湿地
- 湿地信息必须经 WebSearch 交叉验证，**不得编造湿地名称**

GSAP 入场（紧跟 migration-route-card 或分布描述之后）:
```js
tl.fromTo(".s5-habitat",      { opacity: 0, y: 20 }, { opacity: 1, y: 0, duration: 0.6, ease: "power2.out" }, start + 1.6);
tl.fromTo(".s5-habitat-desc", { opacity: 0, y: 10 }, { opacity: 1, y: 0, duration: 0.5, ease: "power2.out" }, start + 1.72);
tl.fromTo(".s5-wetland",      { opacity: 0, y: 15 }, { opacity: 1, y: 0, duration: 0.5, ease: "power2.out" }, start + 1.84);
tl.fromTo(".s5-wetland-desc", { opacity: 0, y: 8 },  { opacity: 1, y: 0, duration: 0.5, ease: "power2.out" }, start + 1.94);
tl.fromTo(".s5-wetland-tag",  { opacity: 0, scale: 0.9 }, { opacity: 1, scale: 1, duration: 0.4, ease: "back.out(1.2)" }, start + 2.04);
```

migration-label CSS（V5.3 更新）:
```css
.migration-label {
  font-size: 20px; font-weight: 600;
  color: #F5F0E8;  /* ← V5.3: 亮色文字 */
  background: {{PRIMARY_HEX}};
  padding: 6px 16px;
  display: inline-block;
  text-shadow: 0 2px 4px rgba(0,0,0,0.5);  /* ← V5.3 */
}
```

### 5.6 装饰元素

**径向光晕**（radial-glow）— 每个场景 1-2 个（V5.3 改为白色微光）：
```html
<div class="radial-glow s1-g1"
  style="width:350px; height:350px; top:40px; left:280px;
  background:radial-gradient(circle, rgba(255,255,255,0.06) 0%, rgba(255,255,255,0) 70%);"
  data-layout-allow-overflow></div>
```

CSS:
```css
.radial-glow { position: absolute; border-radius: 50%; pointer-events: none; }
```

GSAP: 持续呼吸，yoyo + repeat:
```js
tl.to(".s1-g1", { scale: 1.05, duration: 3.0, ease: "sine.inOut", yoyo: true, repeat: 1 }, 0.2);
```

**V5.3 移除**：`.grain-overlay`（纸纹肌理）在全透明模式下不再有意义，所有场景删除 `.grain-overlay` 元素。

### 5.7 国鸟徽章（national-bird-badge）— V4.5 新增

**仅当鸟种为某国国鸟时展示**。放在 S1 hero-subtitle 下方和 S6 body-text 收束句中。使用国家级 flag emoji。

```html
<div class="national-bird-badge s1-badge">
  <span class="badge-flag">{{FLAG_EMOJI}}</span>
  <span class="badge-text">国鸟 · {{COUNTRY_NAME}} · {{YEAR}}</span>
</div>
```

CSS（V5.3 更新）:
```css
.national-bird-badge {
  display: flex; align-items: center; gap: 10px;
  padding: 8px 16px;
  background: rgba(255,255,255,0.06);   /* ← V5.3: 白色半透明底 */
  border: 1px solid rgba(255,255,255,0.2);  /* ← V5.3: 白色边框 */
  border-radius: 4px;
  width: fit-content;
}
.badge-flag  { font-size: 22px; }
.badge-text  { font-size: 17px; font-weight: 400; color: {{PRIMARY_HEX}}; text-shadow: 0 1px 3px rgba(0,0,0,0.4); }  /* ← V5.3 */
```

GSAP 入场（跟 hero-subtitle 之后）:
```js
tl.fromTo(".s1-badge", { opacity: 0, y: 10 }, { opacity: 1, y: 0, duration: 0.5, ease: "power2.out" }, 1.5);
```

**国鸟验证规则**：
1. 搜索 `<鸟名> 国鸟 national bird` 获取候选国
2. 对每个候选国，二次搜索 `<鸟名> <国名> national bird` 交叉验证
3. 查阅权威来源（Wikipedia、政府官网）确认
4. **不是国鸟 → 完全不显示 national-bird-badge，S6 不提及国鸟**
5. 仅一个来源说"国鸟"但其他权威来源否认 → 视为"不是"，不展示

**已知国鸟参考**（仅用于交叉验证起点，每次仍需 WebSearch 确认）：
| 鸟种 | 国家 | 当选年份 | 国旗 emoji |
|------|------|----------|-----------|
| 戴胜 | 以色列 | 2008 | 🇮🇱 |
| 白头海雕 | 美国 | 1782 | 🇺🇸 |
| 绿雉 | 日本 | 1947 | 🇯🇵 |
| 知更鸟 | 英国 | 1961 | 🇬🇧 |
| 丹顶鹤 | 中国（民间公认） | — | 🇨🇳 |

### 5.8 文化配图（culture-image）— V6.4 重写：联网搜图 + 本地下载

**S6 专属**。当命中任何 S6 文化维度时，**必须通过 WebSearch 搜索该维度的真实图片**，下载到项目本地 `images/` 目录，并嵌入 HTML 中。**不依赖 AI 生图、不使用极简淡墨**——以真实照片/扫描件/实物图为第一原则。

**多图模式**（V6.4 升级）：若 S6 命中 N 个文化维度，则为每个维度分别搜图，在左侧面板底部横向排列或纵向堆叠显示。

#### HTML 模板（多图模式）

```html
<!-- 每命中一个维度，插入一张对应配图 -->
<div class="culture-image s6-img-stamp">
  <img src="images/{{BIRD_SLUG}}_stamp.jpg" alt="{{ALT_TEXT}}" />
</div>
<div class="culture-image s6-img-painting">
  <img src="images/{{BIRD_SLUG}}_painting.jpg" alt="{{ALT_TEXT}}" />
</div>
<div class="culture-image s6-img-costume">
  <img src="images/{{BIRD_SLUG}}_costume.jpg" alt="{{ALT_TEXT}}" />
</div>
```

#### CSS（V6.4 更新：降低透明度，取消混合模式）

```css
.culture-image {
  position: absolute; bottom: 40px; left: 56px; right: 56px;
  height: 200px; opacity: 0.18;  /* ← V6.4: 从0.12提高到0.18，真实照片需要稍高可见度 */
  overflow: hidden; pointer-events: none;
  z-index: 0;
}
.culture-image img {
  width: 100%; height: 100%;
  object-fit: contain;  /* ← V6.4: contain代替cover，完整展示邮票/画作原比例 */
  mix-blend-mode: normal;  /* ← V6.4: 不做风格化混合 */
}
/* 多图并排时缩小单图尺寸 */
.culture-image.multi {
  height: 150px;
  width: calc(50% - 10px);
}
```

#### 搜图工作流（Step 1 研究阶段执行）

**每个命中的文化维度，按以下流程获取图片**：

```
1. WebSearch 搜索图片 → 获取图片 URL
   - 邮票维度：搜索 "<鸟名> 邮票 图片 志号"
   - 古画维度：搜索 "<画作名> 高清 图片"
   - 补服维度：搜索 "<鸟名> 补服 纹样 图片"
   - 文物维度：搜索 "<鸟名> <器物名> 图片"
   - 电影/IP维度：搜索 "<作品名> 海报 剧照"
   等等...

2. 用 WebFetch 验证 URL 可访问，确认是真实图片链接

3. 下载图片到项目 images/ 目录
   - 文件名格式: {bird-slug}_{dimension}.{ext}
   - 例: shoudai_stamp.jpg, shoudai_painting.jpg, shoudai_costume.jpg

4. 在 HTML 中引用本地路径: src="images/{filename}"
```

#### 各维度搜图关键词表

| 文化维度 | 搜图关键词 | 图片内容预期 | 文件命名 |
|----------|-----------|-------------|----------|
| **鸟与邮票** | `<鸟名> 邮票 图片` + `<邮票志号> 邮票 高清` | 邮票实物扫描件/照片 | `{slug}_stamp.jpg` |
| **古建筑** | `<鸟名> <建筑构件> 图片`（如"燕尾枋 图片"） | 建筑构件实物照片 | `{slug}_architecture.jpg` |
| **鸟与人文** | `<鸟名> <工艺/非遗> 图片`（如"点翠 首饰 图片"） | 工艺品实物照片 | `{slug}_folkart.jpg` |
| **鸟与音乐** | `<作品名> 乐谱 封面 图片` | 乐谱封面/演出剧照 | `{slug}_music.jpg` |
| **鸟与电影** | `<片名> 海报 或 剧照` | 电影海报/截图 | `{slug}_film.jpg` |
| **IP形象** | `<IP名> 图片` | IP形象图案 | `{slug}_ip.jpg` |
| **鸟与科技** | `<技术名> <鸟名> 对比图` | 仿生设计对比图 | `{slug}_tech.jpg` |
| **鸟与天文/星座** | `星座 <星座名> 星图 图片` | 古典星图/星座插画 | `{slug}_astro.jpg` |
| **古代画作** | `<画作名> 高清 图片` | 古画实物照片/扫描件 | `{slug}_painting.jpg` |

#### 下载命令示例

```bash
# 使用 curl 下载图片到 images/ 目录
mkdir -p images

# 示例：下载邮票图片
curl -o images/shoudai_stamp.jpg "https://example.com/stamp.jpg"

# 示例：下载古画图片
curl -o images/shoudai_painting.jpg "https://example.com/painting.jpg"
```

#### GSAP 动态呼吸动画（不变）

```js
// 微弱呼吸：scale 1.00 → 1.03，sine.inOut 循环
tl.to(".s6-img-stamp",    { scale: 1.03, duration: 4.0, ease: "sine.inOut", yoyo: true, repeat: -1 }, S6 + 0.5);
tl.to(".s6-img-painting", { scale: 1.03, duration: 4.5, ease: "sine.inOut", yoyo: true, repeat: -1 }, S6 + 0.7);
tl.to(".s6-img-costume",  { scale: 1.03, duration: 5.0, ease: "sine.inOut", yoyo: true, repeat: -1 }, S6 + 0.9);
// stagger 每个图延迟 0.2s 起步
```

#### 硬约束（V6.4 更新）

- 图片仅放在 S6 左侧面板底部，**不跨场景**
- `opacity: 0.18`，`mix-blend-mode: normal`，`object-fit: contain`——真实图片保留原比例
- 动画必须极其微弱（scale 1.00→1.03），不能喧宾夺主
- **图片内容必须与 S6 文字内容精确对应**（写的是"特586邮票" → 图是那张邮票的扫描件；写的是"枇杷绶带图" → 图是那幅古画）
- **严禁使用 AI 生成的虚假图片替代真实图片**
- 逐张容错：某一张搜索/下载失败 → 跳过该张，不影响其他维度配图。全部失败 → 不阻塞构建，culture-image 区域留空
- **V6.4 零幻觉扩展**：不能确定图片真实性的 → 不下载不展示。模糊的/疑似AI生成的/水印遮盖原图的 → 搜索备用源

### 5.9 S7 生态现状 · 保护呼吁（Conservation Status）— V7.0 新增

**S7 的使命——Skill 的灵魂**：本 Skill 的终极目标是让公众了解鸟类、爱上鸟类，最终**保护鸟类**。S7 是整支视频的最高潮和情感落点——在所有生物学知识和文化关联铺垫之后，将观众的视线引回现实：**这种鸟现在过得好吗？我们能做什么？**

```html
<!-- ═══ S7: 生态现状 · 保护呼吁 ═══ -->
<div id="scene7" class="scene" style="visibility: hidden; opacity: 0;">
  <div class="left-panel s7-panel">
    <div class="radial-glow s7-g1" style="width:320px;height:320px;top:30px;left:220px;background:radial-gradient(circle,rgba(255,255,255,0.04) 0%,rgba(255,255,255,0) 70%);" data-layout-allow-overflow></div>
    <div class="label-text s7-label">生态现状</div>
    <div class="section-title s7-hero">{{S7_TITLE}}</div>
    <div class="divider s7-div"></div>

    <!-- 保护等级重申徽章 -->
    <div class="protection-badge s7-badge">
      <span class="protection-icon">🛡</span>
      <span class="protection-text">{{PROTECTION_LEVEL}}</span>
    </div>

    <!-- 种群趋势卡片 -->
    <div class="conservation-status-card s7-status">
      <div class="status-header">
        <span class="status-icon">{{TREND_ICON}}</span>
        <span class="status-trend">{{POPULATION_TREND}}</span>
      </div>
      <div class="status-detail s7-detail">{{CONSERVATION_DETAIL}}</div>
    </div>

    <!-- 威胁标签 -->
    <div class="tag-row s7-threats">
      {{THREAT_TAGS}}
    </div>

    <!-- 保护呼吁文案 — 这是 S7 的灵魂句 -->
    <div class="conservation-call s7-call">
      {{CONSERVATION_CALL}}
    </div>

    <div class="body-text sm s7-note">
      {{CONSERVATION_NOTE}}
    </div>
  </div>
</div>
```

#### 保护等级重申徽章（protection-badge）

```html
<div class="protection-badge s7-badge">
  <span class="protection-icon">🛡</span>
  <span class="protection-text">国家二级重点保护野生动物 · IUCN 近危(NT)</span>
</div>
```

CSS — 版本 A（晨曦暖色版）:
```css
.protection-badge {
  display: flex; align-items: center; gap: 10px;
  padding: 12px 20px;
  background: rgba(0,0,0,0.04);
  border: 2px solid {{PRIMARY_HEX}};
  border-radius: 4px; width: fit-content;
}
.protection-icon  { font-size: 24px; }
.protection-text  { font-size: 18px; font-weight: 600; color: {{PRIMARY_HEX}}; line-height: 1.4; }
```

CSS — 版本 B（暮影电影版）:
```css
.protection-badge {
  display: flex; align-items: center; gap: 10px;
  padding: 12px 20px;
  background: rgba(255,255,255,0.06);
  border: 2px solid {{PRIMARY_HEX}};
  border-radius: 4px; width: fit-content;
  box-shadow: 0 0 12px rgba({{PRIMARY_RGB}},0.25);
}
.protection-icon  { font-size: 24px; }
.protection-text  { font-size: 18px; font-weight: 600; color: {{PRIMARY_HEX}}; line-height: 1.4; text-shadow: 0 2px 2px rgba(0,0,0,0.9); }
```

#### 种群趋势卡片（conservation-status-card）

```html
<div class="conservation-status-card s7-status">
  <div class="status-header">
    <span class="status-icon">📉</span>
    <span class="status-trend">种群数量下降 · 栖息地持续丧失</span>
  </div>
  <div class="status-detail s7-detail">
    全球种群估计不足{{POPULATION_ESTIMATE}}只，<br/>
    因{{HABITAT_LOSS_REASON}}，<br/>
    分布区已被压缩至{{REMAINING_RANGE}}。
  </div>
</div>
```

CSS — 版本 A（晨曦暖色版）:
```css
.conservation-status-card {
  display: flex; flex-direction: column;
  padding: 20px 24px;
  background: rgba(0,0,0,0.03);
  border: 1px solid rgba(0,0,0,0.1);
  border-left: 4px solid {{WARNING_COLOR}};
  border-radius: 4px; gap: 10px;
}
.status-header { display: flex; align-items: center; gap: 10px; }
.status-icon    { font-size: 24px; }
.status-trend   { font-size: 19px; font-weight: 600; color: #5C5040; }
.status-detail  { font-size: 18px; color: #5C5040; line-height: 1.6; }
```

CSS — 版本 B（暮影电影版）:
```css
.conservation-status-card {
  display: flex; flex-direction: column;
  padding: 20px 24px;
  background: rgba(255,255,255,0.06);
  border: 1px solid rgba(255,255,255,0.15);
  border-left: 4px solid {{WARNING_COLOR}};
  border-radius: 4px; gap: 10px;
}
.status-header { display: flex; align-items: center; gap: 10px; }
.status-icon    { font-size: 24px; }
.status-trend   { font-size: 19px; font-weight: 600; color: #FFFFFF; text-shadow: 0 2px 2px rgba(0,0,0,0.9); }
.status-detail  { font-size: 18px; color: rgba(255,255,255,0.85); line-height: 1.6; text-shadow: 0 2px 2px rgba(0,0,0,0.9); }
```

**Warning Color**：`{{WARNING_COLOR}}` 为一组暖红色预警色系（`#C47A5A` / `#D4835A`），与 left-border 和强调文字共用，在保护呼吁场景中制造视觉紧迫感。

#### 威胁标签（threat-tag）

```html
<span class="threat-tag">芦苇收割</span>
<span class="threat-tag">湿地围垦</span>
<span class="threat-tag">栖息地破碎</span>
```

CSS — 两版本通用:
```css
.threat-tag {
  font-size: 20px; font-weight: 400;
  border: 2px solid {{WARNING_COLOR}}; color: {{WARNING_COLOR}};
  padding: 5px 14px; border-radius: 3px;
}
/* B 版追加 */
.threat-tag { text-shadow: 0 2px 2px rgba(0,0,0,0.9); }
```

#### 保护呼吁文案（conservation-call）— S7 灵魂句

```html
<div class="conservation-call s7-call">
  每一片消失的芦苇荡，<br/>都是一只震旦鸦雀失去的家。<br/>保护湿地，就是保护它的世界。
</div>
```

CSS — 版本 A（晨曦暖色版）:
```css
.conservation-call {
  font-size: 24px; font-weight: 600; color: {{WARNING_COLOR}};
  line-height: 1.7; letter-spacing: 0.03em;
  padding: 16px 0; border-top: 1px solid rgba(0,0,0,0.08);
  border-bottom: 1px solid rgba(0,0,0,0.08);
}
```

CSS — 版本 B（暮影电影版）:
```css
.conservation-call {
  font-size: 24px; font-weight: 600; color: {{WARNING_COLOR}};
  line-height: 1.7; letter-spacing: 0.03em; text-shadow: 0 2px 2px rgba(0,0,0,0.9);
  padding: 16px 0; border-top: 1px solid rgba(255,255,255,0.15);
  border-bottom: 1px solid rgba(255,255,255,0.15);
}
```

#### GSAP 入场动画

```js
// S7 入场 — 版本 A（左侧滑入，但与 warning 色配合增强紧迫感）
tl.fromTo(".s7-label",  { opacity: 0, x: -40 }, { opacity: 1, x: 0, duration: 0.5, ease: "power3.out" }, S7 + 0.3);
tl.fromTo(".s7-hero",   { opacity: 0, x: -40, scale: 0.95 }, { opacity: 1, x: 0, scale: 1, duration: 0.65, ease: "power3.out" }, S7 + 0.45);
tl.fromTo(".s7-div",    { scaleX: 0, transformOrigin: "left center" }, { scaleX: 1, duration: 0.5, ease: "power3.out" }, S7 + 0.8);
tl.fromTo(".s7-badge",  { opacity: 0, x: -30, scale: 0.95 }, { opacity: 1, x: 0, scale: 1, duration: 0.55, ease: "back.out(1.15)" }, S7 + 1.0);
tl.fromTo(".s7-status", { opacity: 0, y: 20 }, { opacity: 1, y: 0, duration: 0.6, ease: "power2.out" }, S7 + 1.3);
tl.fromTo(".s7-detail", { opacity: 0, y: 10 }, { opacity: 1, y: 0, duration: 0.5, ease: "power2.out" }, S7 + 1.5);
tl.fromTo(".s7-threats",{ opacity: 0, x: -20 }, { opacity: 1, x: 0, duration: 0.5, ease: "power3.out" }, S7 + 1.7);
tl.fromTo(".s7-call",   { opacity: 0, y: 15, scale: 0.97 }, { opacity: 1, y: 0, scale: 1, duration: 0.7, ease: "back.out(1.2)" }, S7 + 2.0);
tl.fromTo(".s7-note",   { opacity: 0, x: -20 }, { opacity: 1, x: 0, duration: 0.5, ease: "power3.out" }, S7 + 2.3);

// S7 退出（模糊交叉渐变到闭幕卡）
tl.to("#scene7",  { filter: "blur(20px)", scale: 1.04, duration: 0.55, ease: "power1.in", overwrite: "auto" }, S7_TRANS);
tl.to("#scene7",  { opacity: 0, duration: 0.35, ease: "power1.in", overwrite: "auto" }, S7_TRANS + 0.4);
tl.to(".closing-card", { opacity: 1, visibility: "visible", duration: 0.8, ease: "power2.out" }, S7_TRANS);
tl.fromTo(".s0-echo", { opacity: 0, y: 15 }, { opacity: 1, y: 0, duration: 0.6, ease: "power2.out" }, S7_TRANS + 0.6);
tl.set("#scene7", { visibility: "hidden" }, S7_TRANS + 1.4);
```

#### S7 数据要求（V7.0 零幻觉约束）

对 Step 1 研究阶段新增检索维度：

| 维度 | 检索词 | 输出 |
|------|--------|------|
| **生态现状与保护** | `<物种名> 种群数量 保护现状` + `<物种名> 威胁 栖息地丧失 人为干扰` + `<物种名> 保护措施 保育行动` | 种群数量估算 / 变化趋势（增/降/稳）、主要威胁（≥2个具体威胁）、已采取的保护措施、一句凝练的保护呼吁 |

**S7 写作铁律**：
- `protection-badge` 必须**重申 S1 出现的保护等级**（国家保护+IUCN），但换一种更有紧迫感的表述方式（如 S1 写"国家二级重点保护野生动物"，S7 写"🛡 国家二级重点保护 — 一纸名录之外的生存挑战"）
- `conservation-status-card` 的 `status-trend` 必须是事实判断：种群增/降/稳，数据经 WebSearch 交叉验证
- `conservation-call` 是 S7 的核心——**必须写一句有感染力但不煽情的保护呼吁**，将鸟的生存与人的行动直接关联。如"每一片消失的芦苇荡，都是一只震旦鸦雀失去的家"
- `threat-tag` 列举 2-4 个具体的、经 WebSearch 验证的主要威胁
- S7 灵魂 = 科学事实 + 情感共鸣 + 行动指引，**不做空洞的"保护动物人人有责"**

#### 写作示例

**震旦鸦雀**：
- protection-badge: "🛡 国家二级重点保护野生动物 · IUCN 近危(NT)"
- status-trend: "📉 栖息地丧失 · 种群面临持续压力"
- status-detail: "依赖芦苇湿地生存，而芦苇收割与湿地围垦正在压缩其最后的家园。中国东部沿海湿地面积在过去五十年间减少了超过一半。"
- threat-tags: "芦苇收割" "湿地围垦" "栖息地破碎"
- conservation-call: "每一片消失的芦苇荡，都是一只震旦鸦雀失去的家。芦苇在，它就在——我们的每一次选择，都在决定它的未来。"

---

## 6. 场景过渡（Blur Crossfade）

所有场景间使用统一的毛玻璃模糊交叉渐变：

```js
function crossfade(tl, sceneOut, sceneIn, transTime) {
  // 1. Outgoing: blur + slight scale-up
  tl.to(sceneOut, { filter: "blur(20px)", scale: 1.04, duration: 0.55, ease: "power1.in", overwrite: "auto" }, transTime);
  // 2. Fade out
  tl.to(sceneOut, { opacity: 0, duration: 0.35, ease: "power1.in", overwrite: "auto" }, transTime + 0.4);
  // 3. Incoming: pre-blurred, scale-down snapshot
  tl.fromTo(sceneIn,
    { filter: "blur(20px)", scale: 0.96, opacity: 0 },
    { filter: "blur(20px)", scale: 0.96, opacity: 1, duration: 0.3, ease: "power1.inOut", overwrite: "auto" },
    transTime + 0.5);
  // 4. Sharpen + scale to 1
  tl.to(sceneIn, { filter: "blur(0px)", scale: 1, duration: 0.55, ease: "power1.out" }, transTime + 0.75);
  // 5. Hide outgoing
  tl.set(sceneOut, { visibility: "hidden" }, transTime + 1.4);
}
```

**参数**：blur=20px，总过渡时长≈1.4s。所有 6 个场景使用完全相同的函数签名。

---

## 7. GSAP 动画配方（Animation Recipe Book）

### 场景开场入场序列 — 版本 A（晨曦暖色版 · 1/3 左侧滑入）

```js
var S = <scene_start_time>;

// 装饰呼吸
tl.to(".sN-g1", { scale: 1.05, duration: 3.0, ease: "sine.inOut", yoyo: true, repeat: 1 }, S + 0.2);

// 标签：左侧滑入
tl.fromTo(".sN-label", { opacity: 0, x: -40 }, { opacity: 1, x: 0, duration: 0.5, ease: "power3.out" }, S + 0.3);

// 标题：左侧滑入 + 微缩放
tl.fromTo(".sN-hero",  { opacity: 0, x: -40, scale: 0.95 }, { opacity: 1, x: 0, scale: 1, duration: 0.7, ease: "power3.out" }, S + 0.5);

// 分割线
tl.fromTo(".sN-div",   { scaleX: 0, transformOrigin: "left center" }, { scaleX: 1, duration: 0.5, ease: "power3.out" }, S + 0.9);

// 正文：左侧滑入
tl.fromTo(".sN-body",  { opacity: 0, x: -30 }, { opacity: 1, x: 0, duration: 0.6, ease: "power3.out" }, S + 1.2);
```

### 场景开场入场序列 — 版本 B（暮影电影版 · 标准淡入）

```js
var S = <scene_start_time>;

// 装饰呼吸
tl.to(".sN-g1", { scale: 1.05, duration: 3.0, ease: "sine.inOut", yoyo: true, repeat: 1 }, S + 0.2);

// 标签
tl.fromTo(".sN-label", { opacity: 0, y: 20 }, { opacity: 1, y: 0, duration: 0.5, ease: "power2.out" }, S + 0.3);

// 标题
tl.fromTo(".sN-hero",  { opacity: 0, y: 35, scale: 0.95 }, { opacity: 1, y: 0, scale: 1, duration: 0.7, ease: "expo.out" }, S + 0.5);

// 分割线
tl.fromTo(".sN-div",   { scaleX: 0, transformOrigin: "left center" }, { scaleX: 1, duration: 0.5, ease: "power3.out" }, S + 0.9);

// 正文
tl.fromTo(".sN-body",  { opacity: 0, y: 15 }, { opacity: 1, y: 0, duration: 0.6, ease: "sine.out" }, S + 1.2);
```

### 各组件专用缓动

| 组件 | A 版缓动 | B 版缓动 | 说明 |
|------|----------|----------|------|
| `label-text` | `power3.out` x:-40→0 | `power2.out` y:20→0 | A 版侧滑，B 版上浮 |
| `hero-title` / `section-title` | `power3.out` x:-40→0 + scale | `expo.out` y:35→0 + scale | A 版侧滑弹出，B 版下浮弹出 |
| `divider` | `power3.out` scaleX:0→1 | `power3.out` scaleX:0→1 | 两版本相同 |
| `body-text` | `power3.out` x:-30→0 | `sine.out` y:15→0 | A 版侧滑，B 版上浮 |
| `color-swatch` | `back.out(1.3)` stagger 0.15s | `back.out(1.3)` stagger 0.15s | 两版本相同 |
| `info-tag` (群组) | `power3.out` x:-20→0 | `power1.out` y:12→0 | A 版侧滑，B 版上浮 |
| `fact-card` | `power3.out` x:20→0 | `power3.out` x:20→0 | 两版本相同 |
| `stat-number` | `elastic.out(1, 0.5)` scale:0.8→1 | `elastic.out(1, 0.5)` scale:0.8→1 | 两版本相同 |
| `stat-label` | `power3.out` x:-15→0 | `power2.out` y:8→0 | A 版侧滑，B 版上浮 |
| `migration-label` | `power3.out` x:-15→0 | `power2.out` x:±15→0 | 两版本相似 |
| `radial-glow` | `sine.inOut` yoyo repeat | `sine.inOut` yoyo repeat | 两版本相同 |
| `hero-subtitle` | `power3.out` x:-20→0 | `power2.out` x:-20→0 | 两版本相同 |
| `national-bird-badge` | `power3.out` x:-20→0 | `power2.out` y:10→0 | A 版侧滑，B 版上浮 |
| `culture-image`（V4.8） | `sine.inOut` yoyo repeat:-1 | `sine.inOut` yoyo repeat:-1 | 两版本相同 |
| `habitat-card`（V6.2） | `power2.out` y:20→0 | `power2.out` y:20→0 | 两版本相同 |
| `wetland-subcard`（V6.2） | `power2.out` y:15→0 | `power2.out` y:15→0 | 两版本相同 |

### 最终淡出序列（场景 6 专用）

```js
var EXIT = <total_duration - 1>;
tl.to(".s6-hero",  { opacity: 0, y: -12, duration: 0.5, ease: "power2.in" }, EXIT);
tl.to(".s6-body",  { opacity: 0, duration: 0.4, ease: "power1.in" }, EXIT + 0.1);
tl.to(".s6-body2", { opacity: 0, duration: 0.4, ease: "power1.in" }, EXIT + 0.2);
tl.to(".s6-div",   { opacity: 0, duration: 0.3, ease: "power1.in" }, EXIT + 0.3);
tl.to(".s6-tag",   { opacity: 0, scale: 0.95, duration: 0.4, ease: "power2.in" }, EXIT + 0.4);
tl.to(".s6-img",   { opacity: 0, duration: 0.5, ease: "power2.in" }, EXIT + 0.4);  /* ← V4.8: AI插图同步淡出 */
tl.to(".s6-g1",    { opacity: 0, duration: 0.5, ease: "power2.in" }, EXIT + 0.5);
// 闭幕卡片淡入
tl.to(".closing-card", { opacity: 1, duration: 0.8, ease: "power2.out" }, EXIT);
// V5.2: SVG以鸟之名卡延迟淡入
tl.fromTo(".s0-echo", { opacity: 0, y: 15 }, { opacity: 1, y: 0, duration: 0.6, ease: "power2.out" }, EXIT + 0.6);
```

### 闭幕卡片（Closing Card）— V5.2 升级 / V5.3 透明化

视频末尾不再空白——S6 退出时，一张满屏闭幕卡片淡入，展示物种名、英文名，**并在下方展示 SVG"以鸟之名"摘要卡**：

```html
<div class="closing-card">
  <div class="hero-title closing-title">{{SPECIES_NAME}}</div>
  <div class="closing-divider"></div>
  <div class="hero-subtitle closing-sub">{{ENGLISH_NAME}}<br/>{{NICKNAME}}</div>
  <!-- V5.2: SVG以鸟之名摘要卡 -->
  <svg class="echo-card s0-echo" viewBox="0 0 600 180" width="600" height="180" xmlns="http://www.w3.org/2000/svg">
    <rect width="600" height="180" rx="4" fill="rgba(255,255,255,0.06)" stroke="rgba(255,255,255,0.2)" stroke-width="1" />
    <text x="300" y="36" text-anchor="middle" font-family="serif" font-size="18" font-weight="700" fill="#F5F0E8" letter-spacing="0.06em">鸟 类 万 物 回 响</text>
    {{ECHO_ROWS}}
  </svg>
</div>
```

```css
/* V6.0-A: 晨曦暖色版闭幕卡 */
.closing-card {
  position: absolute; top: 0; left: 0;
  width: 1920px; height: 1080px;
  background: #F0EDE4;
  display: flex; flex-direction: column;
  align-items: center; justify-content: center;
  gap: 24px; z-index: 10;
  opacity: 0; pointer-events: none;
}
.closing-title { font-size: 96px; color: #5C5040; }
.closing-divider { width: 200px; height: 3px; background: {{PRIMARY_HEX}}; border-radius: 1px; }
.closing-sub { font-size: 36px; color: #8B7B6B; }

/* V6.0-B: 暮影电影版闭幕卡 */
.closing-card {
  position: absolute; top: 0; left: 0;
  width: 1920px; height: 1080px;
  background: #000000;
  display: flex; flex-direction: column;
  align-items: center; justify-content: center;
  gap: 24px; z-index: 10;
  opacity: 0; pointer-events: none;
}
.closing-title { font-size: 96px; color: #FFFFFF; text-shadow: 0 2px 2px rgba(0,0,0,0.9); }
.closing-divider { width: 200px; height: 3px; background: {{PRIMARY_HEX}}; border-radius: 1px; }
.closing-sub { font-size: 36px; color: rgba(255,255,255,0.75); text-shadow: 0 2px 2px rgba(0,0,0,0.9); }
```

**V5.3 SVG echo card 更新**：`fill` 改为 `rgba(255,255,255,0.06)`，`stroke` 改为 `rgba(255,255,255,0.2)`，`<text>` 的 `fill` 改为 `#F5F0E8` 或 `rgba(255,255,255,0.85)`。

---

## 8. 研究工作流（Workflow）

### Step 1 — Species Research

WebSearch 抓取，结构化输出：

| 维度 | 检索词 | 输出 |
|------|--------|------|
| **分类与保护** | `<物种名> 学名 科属` + `IUCN` + `国家重点保护名录` | 学名、科属、IUCN等级、中国保护等级 |
| **羽色提取** | `<物种名> 羽毛 颜色 外形特征` + `<物种名> 雌雄 外形差异` | **逐部位输出**（按 Section 3.5 铁律对照 13 个部位），**3-5 种 HEX 色值** + 部位描述 + **中国古典色谱名称**（参考 Section 3 映射表），至少 2 个独立来源交叉验证 |
| **★习性与食性（V5.0强化）** | `<物种名> 食性 行为 习性` + `<物种名> 独特 特殊 有趣 行为` + `<物种名> 生理特征 特殊能力` | 主食类型 + **独特生物特性**（必须挖掘该鸟种与其他鸟不同的、有趣的独特习性/生理特征，这是 S3 fact-card 的核心内容）。例如：翠鸟→水下视觉自动修正光线折射、蜂虎→敲击树枝去蜂毒刺、啄木鸟→舌骨绕脑防震、蜂鸟→悬停飞行唯一鸟类、猫头鹰→270°转头。**不能写"飞行迅速""叫声清脆"等泛泛之谈** |
| **★迁徙类型（V4.7）** | `<物种名> 候鸟 留鸟 迁徙类型` | **明确判断**：夏候鸟/冬候鸟/旅鸟/留鸟，为 S3 migration-tag 和 S5 迁徙详情提供依据 |
| **★中国特有鸟种（V6.1 新增）** | `<物种名> 中国特有 特有种` + `<物种名> endemic China` | **明确判断是/否**：是否为仅分布于中国境内的鸟类？是→记录特有等级（全国特有/区域特有），可列举中国特有鸟种对照（如震旦鸦雀、红腹锦鸡、黄腹角雉、四川山鹧鸪等）；否→标注"非中国特有·广布种"并在 S3 用 info-tag 标明。**无论是否为中国特有都在 S3 展示该标签**，让观众了解鸟种的分布特性 |
| **巢穴与繁殖** | `<物种名> 筑巢 繁殖 巢结构` | 巢穴材料、结构、繁殖季节 |
| **分布/迁徙** | `<物种名> 分布 栖息地 迁徙` | 分布范围、候鸟/留鸟、迁徙路线 |
| **★迁徙路线详情（V4.7）** | `<物种名> 迁徙路线 迁飞路线` + `<物种名> 迁徙距离 公里` + `<物种名> 迁徙 途经国家` | **若为候鸟**：迁徙路线科学命名（如"东亚-澳大利西亚迁飞路线"）、迁徙距离（km）、途经国家/地区列表、是否跨洲/跨洋/跨极地/丝绸之路沿线 |
| **★栖息地生态（V6.2新增）** | `<物种名> 栖息地 生态环境` + `<物种名> 植被类型 海拔 生境` | **栖息地类型**（如"亚热带常绿阔叶林""芦苇湿地""高山草甸"）、植被特征、地形特征、海拔范围——为该鸟种 S5 `habitat-card` 提供数据 |
| **★国内湿地/保护区（V6.2新增）** | `<物种名> 湿地 自然保护区 国家公园` + `<鸟名> 栖息地 保护区 分布` | **若有关联湿地/保护区**：记录 1-2 处关键湿地/保护区官方名称+生态特征+与该鸟种的具体关联+保护等级（国际重要湿地/国家级/世界遗产等）；**若无关联湿地 → 不展示 wetland-subcard** |
| **地域关联** | `<物种名> <指定地区> 出现原因` | 当地生态环境与鸟类关联（如已指定） |
| **文化关联** | `<鸟名> 建筑 装饰 构件` + `<鸟名> 民间工艺 非遗` | 至少 1 个文化节点：古建筑（燕尾枋/雀替/脊兽）或鸟与人文（点翠/刺绣/谐音吉祥物） |
| **★鸟与音乐（V4.6）** | `<鸟名> 音乐 古典音乐 歌曲 芭蕾` + `<鸟名> 作曲家 作品` | **交叉验证**：是否有知名音乐作品以此为原型？是→记录作品名+作曲家+年份；否→标注"无音乐关联" |
| **★鸟与邮票（V6.3强化）** | `<鸟名> 邮票 中国邮政 发行 香港邮政 澳门邮电 中华邮政` + `<鸟名> 邮票编号 志号 特种邮票` + `<鸟名> 纪念邮票 发行年份` | **交叉验证**：是否被中国邮政/香港邮政/澳门邮电/中华邮政（台湾）发行过邮票？是→记录**发行年份 + 邮票编号/志号 + 邮票名称 + 发行机构**（三项缺一不可）；否→标注"无邮票发行" |
| **★鸟与电影（V4.7）** | `<鸟名> 电影 纪录片 动画` + `<鸟名> 影视 角色` | **交叉验证**：是否有知名电影/纪录片以该鸟为主角或重要元素？是→记录片名+年份+导演+关联说明；否→标注"无电影关联" |
| **★IP形象（V4.7）** | `<鸟名> IP形象 原型 吉祥物` + `<鸟名> 品牌 logo 动漫 游戏` | **交叉验证**：是否有知名 IP/品牌/游戏以该鸟为原型？是→记录 IP 名称+原型鸟种+关联说明；否→标注"无IP关联" |
| **★鸟与科技（V4.9新增）** | `<鸟名> 仿生学 空气动力学 工程 biomimicry` + `<鸟名> 飞机 高铁 技术 启发` | **交叉验证**：是否有真实的技术/工程应用受到该鸟启发？是→记录技术名称+工程应用+关联说明（如翠鸟→新干线500系车头降噪提速10%、游隼→B-2飞翼气动外形/战斗机鸭翼、猫头鹰→锯齿尾缘静音降噪、天鹅→飞机机身流线型/翼型升力优化）；否→标注"无科技关联" |
| **★鸟与天文/星座（V5.2新增）** | `<鸟名> 星座 天文 星宿 星官` + `<鸟名> 二十八宿 三垣` + `<鸟名> 神话 星图` | **交叉验证**：是否有以该鸟命名的星座/星宿/星官？是→记录星座名+对应星区/季节+关联说明（如天鹅→天鹅座北天夏季大三角之一、天鹰→天鹰座牛郎星所在、鹊→牛郎织女鹊桥会、朱雀→二十八宿南方七宿）；否→标注"无天文关联" |
| **★国鸟（V4.5）** | `<鸟名> 国鸟 national bird` + `<鸟名> <候选国名> national bird` | **逐国交叉验证**：是→记录国名+当选年份+国旗emoji；否→明确标注"非国鸟" |
| **★文化配图搜图（V6.4新增）** | **每命中维度分别搜图**（见下表） | 为 S6 每个命中维度下载 1 张真实图片到 `images/` 目录，文件命名 `{bird-slug}_{dimension}.{ext}`。单张失败→跳过该张；全部失败→不阻塞构建 |

**S6 各维度配图搜图关键词（V6.4 新增）**：

| 文化维度 | WebSearch 检索词 | 图片内容预期 | 文件命名 |
|----------|-----------------|-------------|----------|
| **鸟与邮票** | `<鸟名> 邮票 图片` + `<邮票志号> 邮票 高清` | 邮票实物扫描件/照片 | `{slug}_stamp.jpg` |
| **古建筑** | `<鸟名> <建筑构件> 图片` | 建筑构件实物照片 | `{slug}_architecture.jpg` |
| **鸟与人文** | `<鸟名> <工艺/非遗> 图片` | 工艺品实物照片 | `{slug}_folkart.jpg` |
| **鸟与音乐** | `<作品名> 乐谱 封面 图片` | 乐谱封面/演出剧照 | `{slug}_music.jpg` |
| **鸟与电影** | `<片名> 海报 或 剧照` | 电影海报/截图 | `{slug}_film.jpg` |
| **IP形象** | `<IP名> 图片` | IP形象图案 | `{slug}_ip.jpg` |
| **鸟与科技** | `<技术名> <鸟名> 对比图` | 仿生设计对比图 | `{slug}_tech.jpg` |
| **鸟与天文/星座** | `星座 <星座名> 星图 图片` | 古典星图/星座插画 | `{slug}_astro.jpg` |
| **古代画作** | `<画作名> 高清 图片` | 古画实物照片/扫描件 | `{slug}_painting.jpg` |
| **补服/服饰** | `<鸟名> 补服 纹样 图片` | 补服实物照片 | `{slug}_costume.jpg` |

### Step 2 — Narration + Duration Planning（V4.5 强制 1–2 分钟 TTS）

**必须配甜美女生旁白**。为每个场景写 3-6 句解说词，存入 `narration.txt`（纯文本文件），然后生成 TTS 并实测时长来校准场景计时。

```bash
# 1. 写解说词
cat > narration.txt << 'NAR'
黄眉柳莺，体长仅九至十一厘米，体重不足七克……它是中国最小的鸟类之一……
它的羽色是绝妙的伪装——橄榄绿背羽与林间光影融为一体……
……
……
……
……
NAR

# 2. 生成甜美女生 TTS（Edge-TTS 晓晓）
python3 -c "
import asyncio, edge_tts
async def gen():
    text = open('narration.txt').read()
    comm = edge_tts.Communicate(text, 'zh-CN-XiaoxiaoNeural', rate='-10%')
    await comm.save('narration.mp3')
asyncio.run(gen())
"

# 3. 实测总时长
ffprobe -i narration.mp3 -show_entries format=duration -v quiet -of csv="p=0"
# 例如输出: 78.350000

# 4. 检查时长是否在 60-120s 范围内
# 若 < 60s → 增加解说词内容，重新 TTS
# 若 > 120s → 精简解说词，重新 TTS
# 达标后：总时长 = ceil(TTS实测) + 1s
```

**解说词写作规范**：

| 约束 | 要求 |
|------|------|
| 语气 | 甜美温润，娓娓道来，像在读睡前故事 |
| 内容 | 每个场景 3-6 句中文，覆盖场景中的关键视觉元素（标题、正文、标签、数字） |
| 字数 | 总共约 **300–420 字**，配合 Edge-TTS 晓晓 rate=-10% 约 **60–120s** |
| 国鸟提及 | 若为国鸟：S1 自然带出（"它是某某国的国鸟"），S6 可融入收束句；**若非国鸟：完全不提** |
| 文件 | 项目根目录 `narration.txt`，纯文本 |
| **V5.1 格式** | **禁止含 (S1)、(S2) 等场景编号前缀**：narration.txt 会被 TTS 直接朗读，会读出"S一""S二"等杂音。解说词必须是**纯连续中文文本**，场景之间仅以换行分隔，不含任何标注性前缀 |

**场景时长计算**（必用实测值）：
- 先用 `ffprobe` 测 TTS 总时长
- 总时长必须在 **60–120s** 范围内，否则重新写解说词 + 重新 TTS
- 目标总时长 = ceil(TTS) + 1s（尾缓冲）
- 6 场景按解说词自然分布分配时长，不强制平均分割
- 最终淡出占用最后 1–1.5s

### Step 3 — Build + Render

1. 写解说词 → **TTS 生成 → 实测时长 → 计算场景分段时间**
2. 从主题色映射 CSS 变量 + **匹配中国古典色谱名称**
3. **V6.4: S6 文化配图搜图+下载**：对 Step 1 研究表中每个命中的 S6 文化维度，按 [Section 5.8 搜图工作流](#58-文化配图culture-image-v64-重写联网搜图--本地下载) 执行：
   - WebSearch 搜索对应维度的图片（使用上表关键词）
   - WebFetch 验证 URL 可访问，确认是真实图片链接
   - `curl` 下载图片到项目 `images/` 目录，命名 `{bird-slug}_{dimension}.{ext}`
   - 在 HTML 中为每个维度插入对应的 `.culture-image` 元素，引用本地路径
   - **逐张容错**：单张失败→跳过该张；全部失败→不阻塞构建
4. 按 **7 场景模板**构建 HTML body（用时长为场景分段时间）
5. 按 GSAP 配方书写 `<script>` 块
6. **插入 `<audio>` 标签**（固定格式，见下方）
7. `npx hyperframes lint` → 0 errors
8. `npx hyperframes render --quality draft --format mp4`

### TTS 流水线（V6.5 Edge-TTS 晓晓）

```bash
# 用 Edge-TTS zh-CN-XiaoxiaoNeural 生成甜美女生旁白
python3 -c "
import asyncio, edge_tts
async def gen():
    text = open('narration.txt').read()
    comm = edge_tts.Communicate(text, 'zh-CN-XiaoxiaoNeural', rate='-10%')
    await comm.save('narration.mp3')
asyncio.run(gen())
"
# 转为 HyperFrames 需要的 PCM WAV
ffmpeg -y -i narration.mp3 -acodec pcm_s16le narration.wav
```

| 参数 | 值 | 说明 |
|------|-----|------|
| 声音 | `zh-CN-XiaoxiaoNeural`（晓晓） | 微软 Edge-TTS 中文女声，温暖自然，比 macOS Tingting 更甜美 |
| 语速 | `rate='-10%'` | 比默认慢 10%，确保文字动画先于或同步于声音出现 |
| 格式 | `.mp3` → `ffmpeg` → `.wav` | HyperFrames 需 PCM WAV |
| 理论时长 | **60–120s** | 250–360 字 @ 约 3.5 字/秒 |

**audio 标签模板**（插在 `<div id="root">` 内第一个子元素位置）：

```html
<audio
  data-track-index="3"
  data-format="wav"
  src="narration.wav"
  data-rendersilence="false"
  data-role="narration"
  data-visibility="invisible"
  style="display:none;"
></audio>
```

---

### 声画同步铁律（V5.0 新增）

**核心原则**：文字必须先于或同步于声音出现。观众先看到文字，再听到旁白读出它——绝不出现"声音在说，画面还没出现"的情况。

**动画前置规则**：

| 约束 | 要求 |
|------|------|
| **场景入场窗口** | 每个场景的**核心视觉元素（标题 + 正文）必须在 1.5s 内完成入场**，不得拖到 2s 以上 |
| **标签与标题** | label-text 和 hero/section-title 必须在 0.8s 内可见 |
| **正文与数据** | body-text、info-tag、fact-card 等必须在 1.5s 内全部入场完毕 |
| **TTS 语速** | `rate='-10%'`（比默认慢 10%），给视觉动画更多时间 |
| **过渡期** | 场景交叉渐变占用 1.4s，过渡期间新场景的旁白可以开始（因为模糊画面已有新内容），但核心文字必须在新场景清晰后立即出现 |

**GSAP 时间线检查清单**（每场景必检）：

```
场景开始时间 = S
✓ label-text 入场完成时间 ≤ S + 0.8s
✓ hero/section-title 入场完成时间 ≤ S + 1.2s
✓ body-text 入场完成时间 ≤ S + 1.5s
✓ info-tag / fact-card / stat 入场完成时间 ≤ S + 2.0s
✓ 所有入场动画总窗口 ≤ 2.0s（从场景开始算起）
```

**反面示例**（禁止）：
- 场景开始后 2.5s 正文才出现，但旁白早在 1.0s 就开始读这段文字
- 场景标签在 1.0s 才出现，但旁白 0.5s 就开始说"在羽色密码这一页……"

**正面示例**（合格）：
- 场景开始 0.3s 标签出现，0.5s 标题出现，1.2s 正文出现，旁白在 1.0s 开始——文字先出现
- 所有文字在 1.5s 内全部就位，旁白在 1.5s 后开始娓娓道来

---

## 9. 完整生产级模板（Production Template）— V6.0 双版本

以下是 V6.0 双版本完整 HTML 骨架。每次构建视频时，**必须同时生成两个 HTML 文件**：
- `index_A.html`（晨曦暖色版，`#F0EDE4` 暖黄底，`#5C5040` 深咖啡文字）
- `index_B.html`（暮影电影版，`#000000` 纯黑底，`#FFFFFF` 纯白文字 + 2px 黑色投影）

### 版本 A：晨曦暖色版模板

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8" />
  <script src="https://cdn.jsdelivr.net/npm/gsap@3.14.2/dist/gsap.min.js"></script>
  <style>
    /* ═══ V6.0-A: 晨曦暖色版 ═══ */
    body {
      margin: 0; width: 1920px; height: 1080px;
      overflow: hidden; background: #F0EDE4; font-family: serif;
    }
    .scene {
      position: absolute; top: 0; left: 0;
      width: 1920px; height: 1080px;
      overflow: hidden; background: #F0EDE4;
    }
    .left-panel {
      position: absolute; top: 0; left: 0;
      width: 640px; height: 1080px;
      background: #F0EDE4;
      border-right: 1px solid rgba(0,0,0,0.1);
      display: flex; flex-direction: column;
      padding: 80px 56px; box-sizing: border-box;
      overflow: hidden; gap: 22px;
    }
    .left-panel.center { justify-content: center; }

    /* ═══ 暖色系文字 ═══ */
    .hero-title   { font-size: 80px; font-weight: 700; color: #5C5040; line-height: 1.15; letter-spacing: 0.04em; }
    .hero-subtitle { font-size: 28px; font-weight: 400; color: #8B7B6B; line-height: 1.4; }
    .section-title { font-size: 56px; font-weight: 700; color: #5C5040; line-height: 1.2; letter-spacing: 0.03em; }
    .body-text     { font-size: 26px; font-weight: 400; color: #5C5040; line-height: 1.65; }
    .body-text.lg  { font-size: 28px; }
    .body-text.sm  { font-size: 22px; }
    .label-text    { font-size: 20px; font-weight: 400; color: #8B7B6B; line-height: 1.4; letter-spacing: 0.08em; }
    .stat-number   { font-size: 84px; font-weight: 700; line-height: 1; }
    .stat-label    { font-size: 24px; font-weight: 400; color: #8B7B6B; line-height: 1.4; }

    .accent-pri  { color: {{PRIMARY_HEX}}; }
    .accent-sec  { color: {{SECONDARY_HEX}}; }
    .accent-tri  { color: {{TERTIARY_HEX}}; }

    .divider { width: 140px; height: 3px; background: {{PRIMARY_HEX}}; border-radius: 1px; }
    .divider.sec { background: {{SECONDARY_HEX}}; }
    .divider.tri { background: {{TERTIARY_HEX}}; }

    .radial-glow { position: absolute; border-radius: 50%; pointer-events: none; }
    .color-swatch { display: flex; flex-direction: column; align-items: center; gap: 8px; }
    .swatch-dot   { width: 40px; height: 40px; border-radius: 50%; border: 1px solid rgba(0,0,0,0.15); }
    .swatch-label { font-size: 16px; color: #5C5040; }
    .swatch-label-cn { font-size: 16px; color: #8B7B6B; letter-spacing: 0.05em; }

    .fact-card {
      display: flex; flex-direction: column;
      padding: 24px 28px;
      background: rgba(0,0,0,0.03);
      border: 1px solid rgba(0,0,0,0.1);
      border-left: 4px solid {{PRIMARY_HEX}};
      gap: 10px;
    }
    .tag-row { display: flex; gap: 12px; flex-wrap: wrap; }
    .info-tag {
      font-size: 20px; font-weight: 400;
      border: 2px solid {{PRIMARY_HEX}}; color: {{PRIMARY_HEX}};
      padding: 5px 14px; border-radius: 3px;
    }
    .info-tag.sec { border-color: {{SECONDARY_HEX}}; color: {{SECONDARY_HEX}}; }
    .info-tag.tri { border-color: {{TERTIARY_HEX}}; color: {{TERTIARY_HEX}}; }
    .migration-label {
      font-size: 20px; font-weight: 600;
      color: #F0EDE4; background: {{PRIMARY_HEX}};
      padding: 6px 16px; display: inline-block;
    }

    .closing-card {
      position: absolute; top: 0; left: 0;
      width: 1920px; height: 1080px;
      background: #F0EDE4;
      display: flex; flex-direction: column;
      align-items: center; justify-content: center;
      gap: 24px; z-index: 10;
      opacity: 0; pointer-events: none;
    }
    .closing-title { font-size: 96px; color: #5C5040; }
    .closing-divider { width: 200px; height: 3px; background: {{PRIMARY_HEX}}; border-radius: 1px; }
    .closing-sub { font-size: 36px; color: #8B7B6B; }

    .national-bird-badge {
      display: flex; align-items: center; gap: 10px;
      padding: 8px 16px;
      background: rgba(0,0,0,0.03);
      border: 1px solid rgba(0,0,0,0.1);
      border-radius: 4px; width: fit-content;
    }
    .badge-flag  { font-size: 22px; }
    .badge-text  { font-size: 17px; font-weight: 400; color: {{PRIMARY_HEX}}; }

    .opening-eyebrow { font-size: 16px; font-weight: 400; color: {{PRIMARY_HEX}}; letter-spacing: 0.12em; text-transform: uppercase; }
    .opening-tag { font-size: 20px; font-weight: 400; color: #8B7B6B; letter-spacing: 0.06em; margin-top: 12px; }

    .migration-route-card {
      display: flex; flex-direction: column;
      padding: 20px 24px;
      background: rgba(0,0,0,0.03);
      border: 1px solid rgba(0,0,0,0.1);
      border-radius: 4px; gap: 12px;
    }
    .route-header { display: flex; align-items: center; gap: 10px; }
    .route-icon   { font-size: 22px; }
    .route-name   { font-size: 19px; font-weight: 600; color: #5C5040; }
    .route-stat { display: flex; align-items: baseline; gap: 8px; }
    .route-stat-num  { font-size: 42px; font-weight: 700; color: {{PRIMARY_HEX}}; line-height: 1; }
    .route-stat-unit { font-size: 18px; color: #8B7B6B; }
    .route-path { display: flex; align-items: center; gap: 4px; }
    .route-dot  { width: 8px; height: 8px; border-radius: 50%; background: {{PRIMARY_HEX}}; }
    .route-line { flex: 1; height: 1px; background: rgba(0,0,0,0.15); }
    .route-countries { font-size: 18px; color: #5C5040; line-height: 1.6; }
    .route-label {
      font-size: 16px; font-weight: 600;
      color: {{PRIMARY_HEX}};
      background: rgba(0,0,0,0.05);
      padding: 4px 12px; border-radius: 2px; width: fit-content;
    }
    .migration-tag {
      font-size: 20px; font-weight: 400;
      color: {{PRIMARY_HEX}};
      background: rgba(0,0,0,0.03);
      border: 1px solid rgba(0,0,0,0.1);
      padding: 5px 14px; border-radius: 3px;
      display: inline-block; width: fit-content;
    }
    /* V6.2: 栖息地卡片 — A版暖色 */
    .habitat-card {
      display: flex; flex-direction: column;
      padding: 20px 24px;
      background: rgba(0,0,0,0.03);
      border: 1px solid rgba(0,0,0,0.1);
      border-radius: 4px; gap: 12px;
    }
    .habitat-header { display: flex; align-items: center; gap: 10px; }
    .habitat-icon   { font-size: 22px; }
    .habitat-title  { font-size: 19px; font-weight: 600; color: #5C5040; }
    .habitat-desc   { font-size: 18px; color: #5C5040; line-height: 1.6; }
    .wetland-subcard {
      display: flex; flex-direction: column;
      padding: 16px 20px;
      background: rgba(0,0,0,0.02);
      border: 1px solid rgba(0,0,0,0.08);
      border-radius: 3px; gap: 8px; margin-top: 4px;
    }
    .wetland-header { display: flex; align-items: center; gap: 8px; }
    .wetland-icon   { font-size: 18px; }
    .wetland-name   { font-size: 17px; font-weight: 600; color: #5C5040; }
    .wetland-desc   { font-size: 16px; color: #8B7B6B; line-height: 1.55; }
    .wetland-tag {
      font-size: 16px; font-weight: 600;
      color: {{PRIMARY_HEX}};
      background: rgba(0,0,0,0.05);
      padding: 3px 10px; border-radius: 2px; width: fit-content;
    }
    .echo-card { display: block; opacity: 0; max-width: 640px; }
  </style>
</head>
<body>
  <div id="root"
    data-composition-id="{{PROJECT_ID}}_A"
    data-width="1920" data-height="1080"
    data-start="0" data-duration="{{TOTAL_DURATION}}">
    <audio id="narration" data-track-index="3" data-format="wav" src="narration.wav" data-rendersilence="false" data-role="narration" data-visibility="invisible" style="display:none;" data-start="0" data-duration="{{TTS_DURATION}}"></audio>

    <!-- V6.0-A: Opening Card -->
    <div id="scene0" class="scene" style="z-index: 10; opacity: 1;">
      <div class="left-panel opening-panel center">
        <div class="radial-glow s0-g1" style="width:400px;height:400px;top:200px;left:120px;background:radial-gradient(circle,rgba(0,0,0,0.04) 0%,rgba(0,0,0,0) 70%);" data-layout-allow-overflow></div>
        <div class="radial-glow s0-g2" style="width:280px;height:280px;bottom:100px;right:-60px;background:radial-gradient(circle,rgba(0,0,0,0.03) 0%,rgba(0,0,0,0) 70%);" data-layout-allow-overflow></div>
        <div class="opening-eyebrow s0-eyebrow">鸟类以鸟之名</div>
        <div class="hero-title s0-hero" style="font-size:88px;">{{SPECIES_NAME}}</div>
        <div class="divider s0-div" style="width:100px;"></div>
        <div class="hero-subtitle s0-sub">{{ENGLISH_NAME}}</div>
        <div class="opening-tag s0-tag">{{THEME_TAG}}</div>
      </div>
    </div>

    <!-- S1: 初见 -->
    <div id="scene1" class="scene">
      <div class="left-panel s1-panel">
        <div class="radial-glow s1-g1" style="width:350px;height:350px;top:40px;left:280px;background:radial-gradient(circle,rgba(0,0,0,0.04) 0%,rgba(0,0,0,0) 70%);" data-layout-allow-overflow></div>
        <div class="radial-glow s1-g2" style="width:260px;height:260px;bottom:-40px;left:-40px;background:radial-gradient(circle,rgba(0,0,0,0.03) 0%,rgba(0,0,0,0) 70%);" data-layout-allow-overflow></div>
        <div class="label-text s1-label">{{FAMILY_LABEL}}</div>
        <div class="hero-title s1-hero">{{SPECIES_NAME}}</div>
        <div class="divider s1-div"></div>
        <div class="hero-subtitle s1-sub">{{ENGLISH_NAME}}<br/>{{NICKNAME}}</div>
        {{NATIONAL_BIRD_BADGE}}
        <div class="body-text s1-body">{{S1_BODY}}</div>
      </div>
    </div>

    <!-- S2-S6: follow Section 4 scene template -->

    <div class="closing-card">
      <div class="hero-title closing-title">{{SPECIES_NAME}}</div>
      <div class="closing-divider"></div>
      <div class="hero-subtitle closing-sub">{{ENGLISH_NAME}}<br/>{{NICKNAME}}</div>
      <svg class="echo-card s0-echo" viewBox="0 0 600 180" width="600" height="180" xmlns="http://www.w3.org/2000/svg">
        <rect width="600" height="180" rx="4" fill="none" stroke="rgba(0,0,0,0.15)" stroke-width="1" />
        <text x="300" y="36" text-anchor="middle" font-family="serif" font-size="18" font-weight="700" fill="#5C5040" letter-spacing="0.06em">鸟 类 万 物 回 响</text>
        {{ECHO_ROWS}}
      </svg>
    </div>
  </div>
  <script>
    window.__timelines = window.__timelines || {};
    var tl = gsap.timeline({ paused: true });

    // ═══ V6.0-A: Opening Card — 左侧滑入动画 ═══
    tl.to(".s0-g1", { scale: 1.06, duration: 2.5, ease: "sine.inOut" }, 0.1);
    tl.to(".s0-g2", { scale: 1.05, duration: 2.2, ease: "sine.inOut" }, 0.15);
    tl.fromTo(".s0-eyebrow", { opacity: 0, x: -40 }, { opacity: 1, x: 0, duration: 0.5, ease: "power3.out" }, 0.1);
    tl.fromTo(".s0-hero",    { opacity: 0, x: -40, scale: 0.95 }, { opacity: 1, x: 0, scale: 1, duration: 0.8, ease: "power3.out" }, 0.25);
    tl.fromTo(".s0-div",     { scaleX: 0, transformOrigin: "center" }, { scaleX: 1, duration: 0.5, ease: "power3.out" }, 0.7);
    tl.fromTo(".s0-sub",     { opacity: 0, x: -30 }, { opacity: 1, x: 0, duration: 0.5, ease: "power3.out" }, 1.0);
    tl.fromTo(".s0-tag",     { opacity: 0, x: -20 }, { opacity: 1, x: 0, duration: 0.5, ease: "power3.out" }, 1.2);

    var OPENING_EXIT = 2.0;
    tl.to("#scene0",  { filter: "blur(20px)", scale: 1.04, duration: 0.55, ease: "power1.in", overwrite: "auto" }, OPENING_EXIT);
    tl.to("#scene0",  { opacity: 0, duration: 0.35, ease: "power1.in", overwrite: "auto" }, OPENING_EXIT + 0.4);
    tl.fromTo("#scene1", { filter: "blur(20px)", scale: 0.96 }, { filter: "blur(20px)", scale: 0.96, opacity: 1, visibility: "visible", duration: 0.3, ease: "power1.inOut", overwrite: "auto" }, OPENING_EXIT + 0.5);
    tl.to("#scene1",  { filter: "blur(0px)", scale: 1, duration: 0.55, ease: "power1.out" }, OPENING_EXIT + 0.75);
    tl.set("#scene0", { visibility: "hidden" }, OPENING_EXIT + 1.4);

    // --- S1: 左侧滑入动画 ---
    var S1 = {{S1_START}};
    var S1_TRANS = {{S1_END}};
    tl.to(".s1-g1", { scale: 1.05, duration: 3.0, ease: "sine.inOut", yoyo: true, repeat: 1 }, S1 + 0.2);
    tl.to(".s1-g2", { scale: 1.06, duration: 2.8, ease: "sine.inOut", yoyo: true, repeat: 1 }, S1 + 0.3);
    tl.fromTo(".s1-label", { opacity: 0, x: -40 }, { opacity: 1, x: 0, duration: 0.5, ease: "power3.out" }, S1 + 0.3);
    tl.fromTo(".s1-hero",  { opacity: 0, x: -40, scale: 0.95 }, { opacity: 1, x: 0, scale: 1, duration: 0.7, ease: "power3.out" }, S1 + 0.5);
    tl.fromTo(".s1-div",   { scaleX: 0, transformOrigin: "left center" }, { scaleX: 1, duration: 0.5, ease: "power3.out" }, S1 + 0.8);
    tl.fromTo(".s1-sub",   { opacity: 0, x: -30 }, { opacity: 1, x: 0, duration: 0.5, ease: "power3.out" }, S1 + 1.1);
    tl.fromTo(".s1-badge", { opacity: 0, x: -20 }, { opacity: 1, x: 0, duration: 0.5, ease: "power3.out" }, S1 + 1.5);
    tl.fromTo(".s1-body",  { opacity: 0, x: -30 }, { opacity: 1, x: 0, duration: 0.6, ease: "power3.out" }, S1 + 1.8);

    // Crossfade 1→2
    tl.to("#scene1",  { filter: "blur(20px)", scale: 1.04, duration: 0.55, ease: "power1.in", overwrite: "auto" }, S1_TRANS);
    tl.to("#scene1",  { opacity: 0, duration: 0.35, ease: "power1.in", overwrite: "auto" }, S1_TRANS + 0.4);
    tl.fromTo("#scene2", { filter: "blur(20px)", scale: 0.96 }, { filter: "blur(20px)", scale: 0.96, opacity: 1, visibility: "visible", duration: 0.3, ease: "power1.inOut", overwrite: "auto" }, S1_TRANS + 0.5);
    tl.to("#scene2",  { filter: "blur(0px)", scale: 1, duration: 0.55, ease: "power1.out" }, S1_TRANS + 0.75);
    tl.set("#scene1", { visibility: "hidden" }, S1_TRANS + 1.4);

    // --- S2-S5: repeat Section 7 recipe with Version A left-slide-in ---

    // --- S6 final exit ---
    tl.to(".s6-hero",  { opacity: 0, y: -12, duration: 0.5, ease: "power2.in" }, {{EXIT_TIME}});
    tl.to(".s6-body",  { opacity: 0, duration: 0.4, ease: "power1.in" }, {{EXIT_TIME}} + 0.1);
    tl.to(".s6-body2", { opacity: 0, duration: 0.4, ease: "power1.in" }, {{EXIT_TIME}} + 0.2);
    tl.to(".s6-div",   { opacity: 0, duration: 0.3, ease: "power1.in" }, {{EXIT_TIME}} + 0.3);
    tl.to(".s6-tag",   { opacity: 0, scale: 0.95, duration: 0.4, ease: "power2.in" }, {{EXIT_TIME}} + 0.4);
    tl.to(".s6-g1",    { opacity: 0, duration: 0.5, ease: "power2.in" }, {{EXIT_TIME}} + 0.5);
    tl.to(".closing-card", { opacity: 1, visibility: "visible", duration: 0.8, ease: "power2.out" }, {{EXIT_TIME}});
    tl.fromTo(".s0-echo", { opacity: 0, y: 15 }, { opacity: 1, y: 0, duration: 0.6, ease: "power2.out" }, {{EXIT_TIME}} + 0.6);

    window.__timelines["{{PROJECT_ID}}_A"] = tl;
  </script>
</body>
</html>
```

### 版本 B：暮影电影版模板

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8" />
  <script src="https://cdn.jsdelivr.net/npm/gsap@3.14.2/dist/gsap.min.js"></script>
  <style>
    /* ═══ V6.0-B: 暮影电影版 ═══ */
    body {
      margin: 0; width: 1920px; height: 1080px;
      overflow: hidden; background: #000000; font-family: serif;
    }
    .scene {
      position: absolute; top: 0; left: 0;
      width: 1920px; height: 1080px;
      overflow: hidden; background: #000000;
    }
    .left-panel {
      position: absolute; top: 0; left: 0;
      width: 640px; height: 1080px;
      background: #000000;
      border-right: 1px solid rgba(255,255,255,0.2);
      display: flex; flex-direction: column;
      padding: 80px 56px; box-sizing: border-box;
      overflow: hidden; gap: 22px;
    }
    .left-panel.center { justify-content: center; }

    /* ═══ 纯白文字 + 2px 黑色投影 ═══ */
    .hero-title   { font-size: 80px; font-weight: 900; color: #FFFFFF; line-height: 1.15; letter-spacing: 0.04em; text-shadow: 0 2px 2px rgba(0,0,0,0.9); }
    .hero-subtitle { font-size: 28px; font-weight: 400; color: rgba(255,255,255,0.75); line-height: 1.4; text-shadow: 0 2px 2px rgba(0,0,0,0.9); }
    .section-title { font-size: 56px; font-weight: 900; color: #FFFFFF; line-height: 1.2; letter-spacing: 0.03em; text-shadow: 0 2px 2px rgba(0,0,0,0.9); }
    .body-text     { font-size: 26px; font-weight: 600; color: #FFFFFF; line-height: 1.65; text-shadow: 0 2px 2px rgba(0,0,0,0.9); }
    .body-text.lg  { font-size: 28px; }
    .body-text.sm  { font-size: 22px; }
    .label-text    { font-size: 20px; font-weight: 400; color: rgba(255,255,255,0.75); line-height: 1.4; letter-spacing: 0.08em; text-shadow: 0 2px 2px rgba(0,0,0,0.9); }
    .stat-number   { font-size: 84px; font-weight: 900; line-height: 1; text-shadow: 0 2px 2px rgba(0,0,0,0.9); }
    .stat-label    { font-size: 24px; font-weight: 400; color: rgba(255,255,255,0.75); line-height: 1.4; text-shadow: 0 2px 2px rgba(0,0,0,0.9); }

    .accent-pri  { color: {{PRIMARY_HEX}}; }
    .accent-sec  { color: {{SECONDARY_HEX}}; }
    .accent-tri  { color: {{TERTIARY_HEX}}; }

    .divider { width: 140px; height: 4px; background: {{PRIMARY_HEX}}; border-radius: 1px; filter: drop-shadow(0 0 5px {{PRIMARY_HEX}}); }
    .divider.sec { background: {{SECONDARY_HEX}}; }
    .divider.tri { background: {{TERTIARY_HEX}}; }

    .radial-glow { position: absolute; border-radius: 50%; pointer-events: none; }
    .color-swatch { display: flex; flex-direction: column; align-items: center; gap: 8px; }
    .swatch-dot   { width: 40px; height: 40px; border-radius: 50%; border: 1px solid rgba(255,255,255,0.4); }
    .swatch-label { font-size: 16px; color: #FFFFFF; text-shadow: 0 2px 2px rgba(0,0,0,0.9); }
    .swatch-label-cn { font-size: 16px; color: rgba(255,255,255,0.55); letter-spacing: 0.05em; text-shadow: 0 2px 2px rgba(0,0,0,0.9); }

    .fact-card {
      display: flex; flex-direction: column;
      padding: 24px 28px;
      background: rgba(255,255,255,0.06);
      border: 1px solid rgba(255,255,255,0.15);
      border-left: 4px solid {{PRIMARY_HEX}};
      gap: 10px;
    }
    .tag-row { display: flex; gap: 12px; flex-wrap: wrap; }
    .info-tag {
      font-size: 20px; font-weight: 400;
      border: 2px solid {{PRIMARY_HEX}}; color: {{PRIMARY_HEX}};
      padding: 5px 14px; border-radius: 3px;
      text-shadow: 0 2px 2px rgba(0,0,0,0.9);
    }
    .info-tag.sec { border-color: {{SECONDARY_HEX}}; color: {{SECONDARY_HEX}}; }
    .info-tag.tri { border-color: {{TERTIARY_HEX}}; color: {{TERTIARY_HEX}}; }
    .migration-label {
      font-size: 20px; font-weight: 600;
      color: #FFFFFF; background: {{PRIMARY_HEX}};
      padding: 6px 16px; display: inline-block;
      text-shadow: 0 2px 2px rgba(0,0,0,0.9);
    }

    .closing-card {
      position: absolute; top: 0; left: 0;
      width: 1920px; height: 1080px;
      background: #000000;
      display: flex; flex-direction: column;
      align-items: center; justify-content: center;
      gap: 24px; z-index: 10;
      opacity: 0; pointer-events: none;
    }
    .closing-title { font-size: 96px; color: #FFFFFF; text-shadow: 0 2px 2px rgba(0,0,0,0.9); }
    .closing-divider { width: 200px; height: 4px; background: {{PRIMARY_HEX}}; border-radius: 1px; filter: drop-shadow(0 0 5px {{PRIMARY_HEX}}); }
    .closing-sub { font-size: 36px; color: rgba(255,255,255,0.75); text-shadow: 0 2px 2px rgba(0,0,0,0.9); }

    .national-bird-badge {
      display: flex; align-items: center; gap: 10px;
      padding: 8px 16px;
      background: rgba(255,255,255,0.06);
      border: 1px solid rgba(255,255,255,0.2);
      border-radius: 4px; width: fit-content;
    }
    .badge-flag  { font-size: 22px; }
    .badge-text  { font-size: 17px; font-weight: 400; color: {{PRIMARY_HEX}}; text-shadow: 0 2px 2px rgba(0,0,0,0.9); }

    .opening-eyebrow { font-size: 16px; font-weight: 400; color: {{PRIMARY_HEX}}; letter-spacing: 0.12em; text-transform: uppercase; text-shadow: 0 2px 2px rgba(0,0,0,0.9); }
    .opening-tag { font-size: 20px; font-weight: 400; color: rgba(255,255,255,0.75); letter-spacing: 0.06em; margin-top: 12px; text-shadow: 0 2px 2px rgba(0,0,0,0.9); }

    .migration-route-card {
      display: flex; flex-direction: column;
      padding: 20px 24px;
      background: rgba(255,255,255,0.06);
      border: 1px solid rgba(255,255,255,0.2);
      border-radius: 4px; gap: 12px;
    }
    .route-header { display: flex; align-items: center; gap: 10px; }
    .route-icon   { font-size: 22px; }
    .route-name   { font-size: 19px; font-weight: 600; color: #FFFFFF; text-shadow: 0 2px 2px rgba(0,0,0,0.9); }
    .route-stat { display: flex; align-items: baseline; gap: 8px; }
    .route-stat-num  { font-size: 42px; font-weight: 700; color: {{PRIMARY_HEX}}; line-height: 1; text-shadow: 0 2px 2px rgba(0,0,0,0.9); }
    .route-stat-unit { font-size: 18px; color: rgba(255,255,255,0.75); text-shadow: 0 2px 2px rgba(0,0,0,0.9); }
    .route-path { display: flex; align-items: center; gap: 4px; }
    .route-dot  { width: 8px; height: 8px; border-radius: 50%; background: {{PRIMARY_HEX}}; }
    .route-line { flex: 1; height: 1px; background: rgba(255,255,255,0.25); }
    .route-countries { font-size: 18px; color: rgba(255,255,255,0.85); line-height: 1.6; text-shadow: 0 2px 2px rgba(0,0,0,0.9); }
    .route-label {
      font-size: 16px; font-weight: 600;
      color: {{PRIMARY_HEX}};
      background: rgba(255,255,255,0.08);
      padding: 4px 12px; border-radius: 2px; width: fit-content;
      text-shadow: 0 2px 2px rgba(0,0,0,0.9);
    }
    .migration-tag {
      font-size: 20px; font-weight: 400;
      color: {{PRIMARY_HEX}};
      background: rgba(255,255,255,0.06);
      border: 1px solid rgba(255,255,255,0.2);
      padding: 5px 14px; border-radius: 3px;
      display: inline-block; width: fit-content;
      text-shadow: 0 2px 2px rgba(0,0,0,0.9);
    }
    /* V6.2: 栖息地卡片 — B版暮影 */
    .habitat-card {
      display: flex; flex-direction: column;
      padding: 20px 24px;
      background: rgba(255,255,255,0.06);
      border: 1px solid rgba(255,255,255,0.2);
      border-radius: 4px; gap: 12px;
    }
    .habitat-header { display: flex; align-items: center; gap: 10px; }
    .habitat-icon   { font-size: 22px; }
    .habitat-title  { font-size: 19px; font-weight: 600; color: #FFFFFF; text-shadow: 0 2px 2px rgba(0,0,0,0.9); }
    .habitat-desc   { font-size: 18px; color: rgba(255,255,255,0.85); line-height: 1.6; text-shadow: 0 2px 2px rgba(0,0,0,0.9); }
    .wetland-subcard {
      display: flex; flex-direction: column;
      padding: 16px 20px;
      background: rgba(255,255,255,0.04);
      border: 1px solid rgba(255,255,255,0.12);
      border-radius: 3px; gap: 8px; margin-top: 4px;
    }
    .wetland-header { display: flex; align-items: center; gap: 8px; }
    .wetland-icon   { font-size: 18px; }
    .wetland-name   { font-size: 17px; font-weight: 600; color: #FFFFFF; text-shadow: 0 2px 2px rgba(0,0,0,0.9); }
    .wetland-desc   { font-size: 16px; color: rgba(255,255,255,0.75); line-height: 1.55; text-shadow: 0 2px 2px rgba(0,0,0,0.9); }
    .wetland-tag {
      font-size: 16px; font-weight: 600;
      color: {{PRIMARY_HEX}};
      background: rgba(255,255,255,0.08);
      padding: 3px 10px; border-radius: 2px; width: fit-content;
      text-shadow: 0 2px 2px rgba(0,0,0,0.9);
    }
    .echo-card { display: block; opacity: 0; max-width: 640px; }
  </style>
</head>
<body>
  <div id="root"
    data-composition-id="{{PROJECT_ID}}_B"
    data-width="1920" data-height="1080"
    data-start="0" data-duration="{{TOTAL_DURATION}}">
    <audio id="narration" data-track-index="3" data-format="wav" src="narration.wav" data-rendersilence="false" data-role="narration" data-visibility="invisible" style="display:none;" data-start="0" data-duration="{{TTS_DURATION}}"></audio>

    <!-- V6.0-B: Opening Card -->
    <div id="scene0" class="scene" style="z-index: 10; opacity: 1;">
      <div class="left-panel opening-panel center">
        <div class="radial-glow s0-g1" style="width:400px;height:400px;top:200px;left:120px;background:radial-gradient(circle,rgba(255,255,255,0.06) 0%,rgba(255,255,255,0) 70%);" data-layout-allow-overflow></div>
        <div class="radial-glow s0-g2" style="width:280px;height:280px;bottom:100px;right:-60px;background:radial-gradient(circle,rgba(255,255,255,0.04) 0%,rgba(255,255,255,0) 70%);" data-layout-allow-overflow></div>
        <div class="opening-eyebrow s0-eyebrow">鸟类以鸟之名</div>
        <div class="hero-title s0-hero" style="font-size:88px;">{{SPECIES_NAME}}</div>
        <div class="divider s0-div" style="width:100px;"></div>
        <div class="hero-subtitle s0-sub">{{ENGLISH_NAME}}</div>
        <div class="opening-tag s0-tag">{{THEME_TAG}}</div>
      </div>
    </div>

    <!-- S1: 初见 -->
    <div id="scene1" class="scene">
      <div class="left-panel s1-panel">
        <div class="radial-glow s1-g1" style="width:350px;height:350px;top:40px;left:280px;background:radial-gradient(circle,rgba(255,255,255,0.06) 0%,rgba(255,255,255,0) 70%);" data-layout-allow-overflow></div>
        <div class="radial-glow s1-g2" style="width:260px;height:260px;bottom:-40px;left:-40px;background:radial-gradient(circle,rgba(255,255,255,0.04) 0%,rgba(255,255,255,0) 70%);" data-layout-allow-overflow></div>
        <div class="label-text s1-label">{{FAMILY_LABEL}}</div>
        <div class="hero-title s1-hero">{{SPECIES_NAME}}</div>
        <div class="divider s1-div"></div>
        <div class="hero-subtitle s1-sub">{{ENGLISH_NAME}}<br/>{{NICKNAME}}</div>
        {{NATIONAL_BIRD_BADGE}}
        <div class="body-text s1-body">{{S1_BODY}}</div>
      </div>
    </div>

    <!-- S2-S6: follow Section 4 scene template -->

    <div class="closing-card">
      <div class="hero-title closing-title">{{SPECIES_NAME}}</div>
      <div class="closing-divider"></div>
      <div class="hero-subtitle closing-sub">{{ENGLISH_NAME}}<br/>{{NICKNAME}}</div>
      <svg class="echo-card s0-echo" viewBox="0 0 600 180" width="600" height="180" xmlns="http://www.w3.org/2000/svg">
        <rect width="600" height="180" rx="4" fill="rgba(255,255,255,0.06)" stroke="rgba(255,255,255,0.2)" stroke-width="1" />
        <text x="300" y="36" text-anchor="middle" font-family="serif" font-size="18" font-weight="700" fill="#FFFFFF" letter-spacing="0.06em">鸟 类 万 物 回 响</text>
        {{ECHO_ROWS}}
      </svg>
    </div>
  </div>
  <script>
    window.__timelines = window.__timelines || {};
    var tl = gsap.timeline({ paused: true });

    // ═══ V6.0-B: Opening Card — 标准淡入动画 ═══
    tl.to(".s0-g1", { scale: 1.06, duration: 2.5, ease: "sine.inOut" }, 0.1);
    tl.to(".s0-g2", { scale: 1.05, duration: 2.2, ease: "sine.inOut" }, 0.15);
    tl.fromTo(".s0-eyebrow", { opacity: 0, y: 10 }, { opacity: 1, y: 0, duration: 0.5, ease: "power2.out" }, 0.1);
    tl.fromTo(".s0-hero",    { opacity: 0, y: 40, scale: 0.95 }, { opacity: 1, y: 0, scale: 1, duration: 0.8, ease: "expo.out" }, 0.25);
    tl.fromTo(".s0-div",     { scaleX: 0, transformOrigin: "center" }, { scaleX: 1, duration: 0.5, ease: "power3.out" }, 0.7);
    tl.fromTo(".s0-sub",     { opacity: 0, x: -15 }, { opacity: 1, x: 0, duration: 0.5, ease: "power2.out" }, 1.0);
    tl.fromTo(".s0-tag",     { opacity: 0, y: 10 }, { opacity: 1, y: 0, duration: 0.5, ease: "power2.out" }, 1.2);

    var OPENING_EXIT = 2.0;
    tl.to("#scene0",  { filter: "blur(20px)", scale: 1.04, duration: 0.55, ease: "power1.in", overwrite: "auto" }, OPENING_EXIT);
    tl.to("#scene0",  { opacity: 0, duration: 0.35, ease: "power1.in", overwrite: "auto" }, OPENING_EXIT + 0.4);
    tl.fromTo("#scene1", { filter: "blur(20px)", scale: 0.96 }, { filter: "blur(20px)", scale: 0.96, opacity: 1, visibility: "visible", duration: 0.3, ease: "power1.inOut", overwrite: "auto" }, OPENING_EXIT + 0.5);
    tl.to("#scene1",  { filter: "blur(0px)", scale: 1, duration: 0.55, ease: "power1.out" }, OPENING_EXIT + 0.75);
    tl.set("#scene0", { visibility: "hidden" }, OPENING_EXIT + 1.4);

    // --- S1: 标准淡入动画 ---
    var S1 = {{S1_START}};
    var S1_TRANS = {{S1_END}};
    tl.to(".s1-g1", { scale: 1.05, duration: 3.0, ease: "sine.inOut", yoyo: true, repeat: 1 }, S1 + 0.2);
    tl.to(".s1-g2", { scale: 1.06, duration: 2.8, ease: "sine.inOut", yoyo: true, repeat: 1 }, S1 + 0.3);
    tl.fromTo(".s1-label", { opacity: 0, y: 20 }, { opacity: 1, y: 0, duration: 0.5, ease: "power2.out" }, S1 + 0.3);
    tl.fromTo(".s1-hero",  { opacity: 0, y: 40, scale: 0.96 }, { opacity: 1, y: 0, scale: 1, duration: 0.7, ease: "expo.out" }, S1 + 0.5);
    tl.fromTo(".s1-div",   { scaleX: 0, transformOrigin: "left center" }, { scaleX: 1, duration: 0.5, ease: "power3.out" }, S1 + 0.8);
    tl.fromTo(".s1-sub",   { opacity: 0, x: -20 }, { opacity: 1, x: 0, duration: 0.5, ease: "power2.out" }, S1 + 1.1);
    tl.fromTo(".s1-badge", { opacity: 0, y: 10 }, { opacity: 1, y: 0, duration: 0.5, ease: "power2.out" }, S1 + 1.5);
    tl.fromTo(".s1-body",  { opacity: 0, y: 20 }, { opacity: 1, y: 0, duration: 0.6, ease: "sine.out" }, S1 + 1.8);

    // Crossfade 1→2
    tl.to("#scene1",  { filter: "blur(20px)", scale: 1.04, duration: 0.55, ease: "power1.in", overwrite: "auto" }, S1_TRANS);
    tl.to("#scene1",  { opacity: 0, duration: 0.35, ease: "power1.in", overwrite: "auto" }, S1_TRANS + 0.4);
    tl.fromTo("#scene2", { filter: "blur(20px)", scale: 0.96 }, { filter: "blur(20px)", scale: 0.96, opacity: 1, visibility: "visible", duration: 0.3, ease: "power1.inOut", overwrite: "auto" }, S1_TRANS + 0.5);
    tl.to("#scene2",  { filter: "blur(0px)", scale: 1, duration: 0.55, ease: "power1.out" }, S1_TRANS + 0.75);
    tl.set("#scene1", { visibility: "hidden" }, S1_TRANS + 1.4);

    // --- S2-S5: repeat Section 7 recipe with Version B standard fade-in ---

    // --- S6 final exit ---
    tl.to(".s6-hero",  { opacity: 0, y: -12, duration: 0.5, ease: "power2.in" }, {{EXIT_TIME}});
    tl.to(".s6-body",  { opacity: 0, duration: 0.4, ease: "power1.in" }, {{EXIT_TIME}} + 0.1);
    tl.to(".s6-body2", { opacity: 0, duration: 0.4, ease: "power1.in" }, {{EXIT_TIME}} + 0.2);
    tl.to(".s6-div",   { opacity: 0, duration: 0.3, ease: "power1.in" }, {{EXIT_TIME}} + 0.3);
    tl.to(".s6-tag",   { opacity: 0, scale: 0.95, duration: 0.4, ease: "power2.in" }, {{EXIT_TIME}} + 0.4);
    tl.to(".s6-g1",    { opacity: 0, duration: 0.5, ease: "power2.in" }, {{EXIT_TIME}} + 0.5);
    tl.to(".closing-card", { opacity: 1, visibility: "visible", duration: 0.8, ease: "power2.out" }, {{EXIT_TIME}});
    tl.fromTo(".s0-echo", { opacity: 0, y: 15 }, { opacity: 1, y: 0, duration: 0.6, ease: "power2.out" }, {{EXIT_TIME}} + 0.6);

    window.__timelines["{{PROJECT_ID}}_B"] = tl;
  </script>
</body>
</html>
```

---

## 10. Post-Render Checklist

### 通用检查（两版本均需满足）

- [ ] `hyperframes lint`: **0 errors**
- [ ] 面板 `640px × 1080px`，实色背景，无透明、无毛玻璃
- [ ] **7 个场景**，blur(20px) 交叉渐变
- [ ] 羽色 HEX 已正确映射到 divider / info-tag / accent / stat-number
- [ ] color-swatch 逐个 stagger 0.15s，`back.out(1.3)`
- [ ] stat-number 使用 `elastic.out(1, 0.5)`
- [ ] fact-card 使用 `power3.out` + x:20→0
- [ ] 每个场景含 radial-glow，**无 grain-overlay**
- [ ] 闭幕卡片 `.closing-card` 已插入，物种名 + 英文名居中，z-index: 10
- [ ] 闭幕卡片在 S7 退出时同步淡入（`power2.out`，0.8s）
- [ ] `narration.txt` 已生成，语气甜美温润，每场景 3-6 句，总字数 300–420
- [ ] TTS 已通过 Edge-TTS `zh-CN-XiaoxiaoNeural` 生成 `narration.mp3`，并转为 `narration.wav`
- [ ] `ffprobe` 已实测 TTS 时长，场景分段时间基于实测值计算
- [ ] `<audio>` 标签已插入 `<div id="root">` 内第一子元素，`data-track-index="3"`
- [ ] 最终视频有声音，晓晓甜美女声与画面同步
- [ ] 视频总时长在 **60–120s** 范围内
- [ ] 解说词总计 300–420 字，每场景 3-6 句
- [ ] 国鸟信息经 WebSearch 交叉验证
- [ ] S6 文化维度最大化命中，每个有真实关联的维度都展示
- [ ] **V6.3 邮票验证**：若有邮票维度，年份+编号+发行机构三项齐全，经 WebSearch 交叉验证；若无则完全不显示
- [ ] 鸟与科技仅当有具体知名工程应用才展示，泛泛的"飞行启发"一律不写
- [ ] S3 fact-card 承载独特生物特性，不得写泛泛之谈
- [ ] narration.txt 不含任何 (S1)、(S2) 等场景编号前缀
- [ ] 开幕卡片 `#scene0` 已插入，2.0s 停留后 blur crossfade 过渡到 S1
- [ ] 闭幕卡片包含 SVG "以鸟之名"摘要卡
- [ ] 若为候鸟 → S3 有 `migration-tag`，S5 有 `migration-route-card`（路线+距离+途经国家）
- [ ] 迁徙路线名称必须是公认的科学命名，不得编造
- [ ] **V6.2**: S5 有 `habitat-card`（栖息地类型+生态描述），候鸟留鸟均需展示
- [ ] **V6.2**: 若有关联湿地/保护区 → S5 有 `wetland-subcard`（湿地名称+生态特征+保护等级），湿地名称经 WebSearch 交叉验证，不得编造
- [ ] **V6.0**: 已同时生成 A 版和 B 版两个 HTML 文件（`index_A.html` + `index_B.html`）
- [ ] **V6.0**: 两版 HTML 中的 `{{PROJECT_ID}}` 分别用 `_A` 和 `_B` 后缀区分
- [ ] **V7.0: S7 生态现状**：已插入 S7 场景，位于 S6 与闭幕卡之间，含 `protection-badge` + `conservation-status-card` + `threat-tag` × N + `conservation-call`
- [ ] **V7.0: protection-badge** 重申了 S1 的保护等级，但换用更有紧迫感的表述
- [ ] **V7.0: conservation-status-card** 的种群趋势（增/降/稳）经 WebSearch 交叉验证
- [ ] **V7.0: conservation-call** 写了一句有感染力但不煽情的保护呼吁文案，将鸟的生存与人的行动直接关联
- [ ] **V7.0: threat-tag** 列举了 2-4 个经 WebSearch 验证的具体威胁
- [ ] **V7.0: S7 不写空洞的"保护动物人人有责"**，必须是基于物种真实困境的具体呼吁
- [ ] **V6.4: S6 配图来源**：所有 S6 配图均为 WebSearch 联网搜索的真实图片（邮票扫描件/古画照片/实物照），**严禁 AI 生成**
- [ ] **V6.4: 图片下载**：每个命中维度的配图已通过 `curl` 下载到 `images/` 目录，文件命名 `{bird-slug}_{dimension}.{ext}`
- [ ] **V6.4: 图片与文字对应**：每张配图内容与 S6 文字描述精确对应
- [ ] **V6.4: CSS 检查**：`.culture-image` 的 `opacity: 0.18`，`mix-blend-mode: normal`，`object-fit: contain`
- [ ] **V6.4: 多图模式**：S6 命中 N 个维度 → N 张配图
- [ ] **V6.4: 容错**：单张图片下载失败 → 仅跳过该张；全部失败 → culture-image 区域留空
- [ ] **V6.4: 零幻觉**：不能确定图片真实性的 → 不下载不展示

### 版本 A：晨曦暖色版专项检查

- [ ] `body` / `.scene` / `.left-panel` / `.closing-card` 均为 `background: #F0EDE4`
- [ ] 所有文字色为深咖啡系：`#5C5040`（主文字）/ `#8B7B6B`（副文字）
- [ ] **无 text-shadow**（暖色背景上不需要投影）
- [ ] 标题字重 `700`，正文字重 `400`
- [ ] 装饰线（divider）高度 `3px`，无发光效果
- [ ] 入场动画为 **1/3 左侧滑入**：`power3.out`，`x: -40→0`
- [ ] 开幕卡片入场动画为左侧滑入（`x: -40→0`）
- [ ] 所有卡片组件（fact-card、national-bird-badge、migration-route-card）背景 `rgba(0,0,0,0.03)` + 边框 `rgba(0,0,0,0.1)`
- [ ] info-tag 文字色为 `{{PRIMARY_HEX}}`，无 text-shadow
- [ ] threat-tag 文字色为 `{{WARNING_COLOR}}`，无 text-shadow
- [ ] radial-glow 使用黑色微光 `rgba(0,0,0,0.04)`，非白色光晕
- [ ] S7 `protection-badge` 背景 `rgba(0,0,0,0.04)` + 边框 `2px solid {{PRIMARY_HEX}}`
- [ ] S7 `conservation-status-card` 左边界 `4px solid {{WARNING_COLOR}}`
- [ ] S7 `conservation-call` 使用上下细线分隔，文字色 `{{WARNING_COLOR}}`
- [ ] SVG echo card 背景 `fill="none"`，边框 `stroke="rgba(0,0,0,0.15)"`，文字 `fill="#5C5040"`
- [ ] **剪映标注**：正片叠底（Multiply），适配明亮/杂乱生态背景
- [ ] 整体视觉呈现"翻开一本鸟类百科"的暖纸质感

### 版本 B：暮影电影版专项检查

- [ ] `body` / `.scene` / `.left-panel` / `.closing-card` 均为 `background: #000000`
- [ ] 所有文字色为纯白：`#FFFFFF`（主文字）/ `rgba(255,255,255,0.75)`（副文字）
- [ ] **所有文字层级有 `text-shadow: 0 2px 2px rgba(0,0,0,0.9)`**
- [ ] 标题字重 `900`（极粗），正文字重 `600`（中粗）
- [ ] 装饰线（divider）高度 `4px`，有 `filter: drop-shadow(0 0 5px {{PRIMARY_HEX}})` 发光
- [ ] 入场动画为**标准淡入**：`y: 35→0`，`expo.out`
- [ ] 开幕卡片入场动画为标准淡入（`y: 40→0`）
- [ ] 所有卡片组件（fact-card、national-bird-badge、migration-route-card）背景 `rgba(255,255,255,0.06)` + 边框 `rgba(255,255,255,0.15-0.2)`
- [ ] info-tag 文字色为 `{{PRIMARY_HEX}}`，有 text-shadow
- [ ] threat-tag 文字色为 `{{WARNING_COLOR}}`，有 text-shadow
- [ ] radial-glow 使用白色微光 `rgba(255,255,255,0.06)`
- [ ] S7 `protection-badge` 背景 `rgba(255,255,255,0.06)` + 边框 `2px solid {{PRIMARY_HEX}}` + `box-shadow: 0 0 12px rgba({{PRIMARY_RGB}},0.25)`
- [ ] S7 `conservation-status-card` 左边界 `4px solid {{WARNING_COLOR}}`
- [ ] S7 `conservation-call` 使用上下细线分隔，文字色 `{{WARNING_COLOR}}`，有 text-shadow
- [ ] SVG echo card 背景 `fill="rgba(255,255,255,0.06)"`，边框 `stroke="rgba(255,255,255,0.2)"`，文字 `fill="#FFFFFF"`
- [ ] **剪映标注**：滤色（Screen），适配深色/纯净/暗光背景
- [ ] 整体视觉呈现"电影字幕悬浮于暗夜"的发光电影感