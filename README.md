# 🕊️ In the Name of Birds | V7.0

> **"Capture a bird, and recover a missing piece of human civilization."**
> **Codename: `bird-science-video-generator`**

> **"拍下一只鸟，找回人类文明的一块拼图。"**

An **AI-powered cinematic short-video automation engine** built for wildlife photographers and science communicators. As someone who can't code, I built this system through Trae Agent. We are not just making educational videos — we are using AI to uncover the fragments of civilization hidden behind every bird, reminding humanity: protecting birds is protecting the source code of our own civilization.

这是一个专为生态摄影师与科普博主打造的 **AI 电影级短视频自动化生产线 (Web-based Automation Engine)**。作为一个代码小白，我通过 Trae Agent 构建了这套系统。我们不仅在做科普视频，更在通过 AI 挖掘每一只鸟背后的文明碎片，提醒人类：保护鸟类，其实是在保护人类文明的源代码。

---

## 🌟 Our Mission

We hear birdsong every day. To most, it fades into the background. We have forgotten: the nose of the Shinkansen, the wing of a stealth fighter, even a Beethoven symphony — all carry the genetic signature of birds. Every bird is a living fragment of civilization's source code, and this project is our attempt to recover it before it fades from memory.

我们每天都能听到鸟鸣，但在大多数人眼里，它们只是背景。我们忘了：人类最伟大的发明——新干线的车头、隐身战斗机的机翼、甚至是贝多芬的乐章，**全都刻着鸟类的基因。**

Through an Obsidian-inspired non-linear knowledge graph, this project orchestrates the full pipeline — semantic understanding → automated web-sourced imagery → synchronized visual styling → automated video synthesis — transforming passive viewers into active stewards of the natural world.

本项目通过 **Obsidian 式的非线性知识图谱** 逻辑，打通了 **"语义理解 → 自动联网配图 → 视觉风格化同步 → 视频自动化合成"** 的全分层闭环，让公众在惊叹于自然与文明的连接时，学会了解鸟、爱护鸟。

---

## 🎨 Dual-Theme Presets

Choose the visual theme that best matches your footage's background tone:

| Version | File | Background | Text Color | Entrance Animation | Blend Mode | Best For |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **A: Morning Light** | `index_A.html` | `#F0EDE4` Warm Paper | `#5C5040` Deep Brown | 1/3 Slide-in from left | **Multiply** | Bright / busy / light backgrounds (sky, grass, woods) |
| **B: Cinematic Dark** | `index_B.html` | `#000000` Pure Black | `#FFFFFF` Pure White | Standard fade-in | **Screen** | Dark / clean / low-light backgrounds (night, deep forest) |

用户可根据拍摄素材的背景色彩与整体基调，自由切换完美适配的视觉版本：

| 版本 | 核心文件 | 背景色 | 文字色 | 入场动画 | 剪映/Premiere 混合模式 | 适用场景 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **A: 晨曦暖色版** | `index_A.html` | `#F0EDE4` 暖黄 | `#5C5040` 深咖啡 | 1/3 左侧滑入 | **正片叠底 (Multiply)** | 明亮/杂乱/浅色背景（天空、草地、树林） |
| **B: 暮影电影版** | `index_B.html` | `#000000` 纯黑 | `#FFFFFF` 纯白 | 标准淡入 | **滤色 (Screen)** | 深色/纯净/暗光背景（夜景、深林、暗色背景） |

---

## 🎬 Demo

Using the Eurasian Hoopoe (戴胜) as an example, showcasing two output modes:

以戴胜 (Eurasian Hoopoe) 为例，展示两种输出效果：

**HyperFrames raw render output / HyperFrames 纯渲染效果：**

<video src="demo/demo_render.mp4" width="100%" controls></video>

**Final result: render + real footage + manual editing in 剪映 / 叠加实拍素材 + 剪映剪辑后的最终成品：**

> Note: This version combines the HyperFrames render with real hoopoe footage, plus manually added title cards, images, and text in 剪映. It is not a pure render output.
>
> 注：此版本在 HyperFrames 渲染的基础上，额外叠加了实拍戴胜视频素材，并在剪映中手动添加了片头图片、文案等元素，非纯渲染效果。

<video src="demo/demo_cut.mp4" width="100%" controls></video>

---

## 🚀 Quick Start

### 1. Choose a theme and layout

Pick `index_A.html` or `index_B.html` based on your footage's color tone. The left 1/3 (640px) is the smart editorial panel carrying bird and civilization data; the right 2/3 (1280px) is transparent, reserved for your real footage.

根据你的正片素材色调，选择克隆并打开 `index_A.html` 或 `index_B.html`。界面左侧 1/3 (640px) 为智能编辑面板承载鸟类文明信息，右侧 2/3 (1280px) 为透明区域，完美预留给你的实拍视频素材。

### 2. Replace template variables

Open the HTML file and replace all `{{VARIABLE}}` placeholders with your bird's data (compatible with the built-in 8-dimension civilization knowledge base).

打开对应的 HTML 文件，将所有 `{{VARIABLE}}` 占位符替换为具体的鸟类数据（支持调用本项目内置的 8 大文明维度知识库）。

### 3. Generate narration audio (TTS)

Run the script below to generate broadcast-quality narration using the Edge TTS engine:

在本地运行以下 Python 脚本，利用 edge-tts 引擎生成高质感广播级旁白：

```bash
# Create the script
cat << 'EOF' > generate_tts.py
import asyncio
import edge_tts

async def gen():
    text = open('narration.txt', 'r', encoding='utf-8').read()
    comm = edge_tts.Communicate(text, 'zh-CN-XiaoxiaNeural', rate='-10%')
    await comm.save('narration.mp3')

if __name__ == '__main__':
    asyncio.run(gen())
EOF

# Run it
python3 generate_tts.py
```

### 4. Render with HyperFrames

Render the HTML template into a final video file using HyperFrames:

使用 HyperFrames 将 HTML 模板渲染为最终视频文件：

```bash
npx hyperframes lint
npx hyperframes render --quality draft --format mp4
```

---

## 🔗 Civilization Map: Eight Dimensions of Resonance

This project breaks free from fragmented science communication. Every bird automatically links to the following core nodes of human civilization:

本项目彻底打破碎片化科普，每只鸟类自动链接以下人类文明核心节点：

*   **【Human Technology】**: Structural color anti-counterfeiting, kingfisher beak fluid dynamics.
*   **【Human Technology / 人类科技】**: 羽毛结构色防伪、翠鸟长喙与流体力学。
*   **【Craft & Aesthetics】**: Traditional diancui (kingfisher-feather inlay), the evolution of plumage in ornament.
*   **【Craft & Aesthetics / 工艺美学】**: 传统点翠、羽饰演变。
*   **【Ancient Architecture】**: Flying eaves, swallowtail beam brackets.
*   **【Ancient Architecture / 古建筑学】**: 飞檐脊梁、燕尾枋构造。
*   **【Astronomy & Mythology】**: The Twenty-Eight Mansions, the Vermilion Bird totem.
*   **【Astronomy & Mythology / 天文神话】**: 二十八星宿、朱雀图腾。
*   **【Classical Music】**: Birdsong motifs and their thousand-year dialogue with classical composition.
*   **【Classical Music / 古典音乐】**: 鸟鸣动机与古典乐章的千年对话。
*   **【Modern Cinema】**: Avian symbolism and narrative codes on the silver screen.
*   **【Modern Cinema / 近现代电影】**: 银幕中的鸟类象征与叙事符码。
*   **【Literary Imagination】**: From the *Book of Songs* to Borges — birds as the eternal poetic eye.
*   **【Literary Imagination / 文学意象】**: 从《诗经》到博尔赫斯，鸟类作为永恒诗眼。
*   **【Ecological Sentinel】**: Birds as the ultimate indicator species of environmental health.
*   **【Ecological Sentinel / 生态哨兵】**: 鸟类作为环境健康的终极指示物种。

---

## ✉️ To Fellow Developers and Fellow Travelers

I am not a programmer — just someone who wants to be a loudspeaker for the natural world. The contest deadline has passed, but my love for nature and technology remains undimmed. To all bird lovers, creators, and developers: pull requests are deeply welcome. Together, let us build a universe where every bird sings back through the ages.

我是一个不会代码的小白，但我希望能成为自然界的一个扩音器。虽然我错过了比赛的截止日期，但我对自然与科技的热爱永不打折。欢迎所有热爱鸟类的博主和开发者一起提交 Pull Request，共同丰富这个百鸟回响的文明宇宙！

---

## Full Technical Specification

See [SKILL.md](./SKILL.md) for the complete technical specification, including:

请参阅 [SKILL.md](./SKILL.md) 了解完整的技术规范，包括：

- Layout specification & CSS variables / 布局规范与 CSS 变量
- Auto-theme color system (Chinese classical palette) / 自动主题色系统（中国古典色谱）
- Plumage color extraction protocol (13 anatomical zones) / 羽色提取铁律（13 部位逐项核对）
- GSAP animation recipes (versions A & B) / GSAP 动画配方（A/B 两版）
- Research workflow (WebSearch cross-validation) / 研究工作流（WebSearch 交叉验证）
- Zero-hallucination constraints (stamps, national birds, tech & culture imagery) / 零幻觉约束（邮票/国鸟/科技/文化配图）
- Post-Render Checklist

---

## File Structure

```
bird-science-video-generator/
├── SKILL.md              # Full technical specification (V7.0) / 完整技术规范文档
├── index_A.html          # Morning Light template / 晨曦暖色版模板
├── index_B.html          # Cinematic Dark template / 暮影电影版模板
├── demo/
│   ├── demo_render.mp4   # HyperFrames pure render demo / 纯渲染 Demo
│   └── demo_cut.mp4      # Render + real footage + 剪映 final / 叠加实拍成品
└── README.md             # This file / 本文件
```

## License

MIT
