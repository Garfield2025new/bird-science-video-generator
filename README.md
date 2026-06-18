# Bird-Science-Video-Generator (V7.0)

> 鸟类科普画中画视频生成器 — Cinematic bird science PiP video generator

## 概述

将鸟类生物学知识与人类文明链接转化为专业的科普视频。左侧 1/3（640px）编辑面板承载鸟类信息，右侧 2/3（1280px）透明区域留给实拍素材。

**双版本预设**，用户可根据视频背景素材选择最合适的版本：

| 版本 | 文件 | 背景色 | 文字色 | 入场动画 | 剪映混合 |
|------|------|--------|--------|----------|----------|
| **A: 晨曦暖色版** | `index_A.html` | `#F0EDE4` 暖黄 | `#5C5040` 深咖啡 | 1/3 左侧滑入 | 正片叠底（Multiply） |
| **B: 暮影电影版** | `index_B.html` | `#000000` 纯黑 | `#FFFFFF` 纯白 | 标准淡入 | 滤色（Screen） |

## 快速开始

### 1. 选择版本

```
明亮/杂乱/浅色背景（天空、花丛、草地、树林）
  → 选择 A 版：index_A.html
  → 在剪映中：正片叠底（Multiply）

深色/纯净/暗光背景（夜景、深林、暗色背景）
  → 选择 B 版：index_B.html
  → 在剪映中：滤色（Screen）
```

### 2. 替换模板变量

打开对应的 HTML 文件，将所有 `{{VARIABLE}}` 占位符替换为实际鸟种数据。详见 [SKILL.md](./SKILL.md) 中的完整规范。

### 3. 生成视频

```bash
# 1. 生成 TTS 旁白
python3 -c "
import asyncio, edge_tts
async def gen():
    text = open('narration.txt').read()
    comm = edge_tts.Communicate(text, 'zh-CN-XiaoxiaoNeural', rate='-10%')
    await comm.save('narration.mp3')
asyncio.run(gen())
"
# 2. 转为 WAV
ffmpeg -y -i narration.mp3 -acodec pcm_s16le narration.wav

# 3. 检查与渲染
npx hyperframes lint
npx hyperframes render --quality draft --format mp4
```

## 场景结构

7 个标准场景 + 开幕卡 + 闭幕卡：

| 场景 | 内容 | 核心组件 |
|------|------|----------|
| **S0 开幕** | 封面 | 物种名 + 英文名 + 主题标签 |
| **S1 初见** | 物种介绍 | 科属标签 + 物种名 + 国鸟徽章(若有) |
| **S2 羽色** | 羽色密码 | color-swatch × 5 + 中国古典色谱名 |
| **S3 习性** | 食性与行为 | 迁徙标签 + 特有标注 + 知识点卡片 |
| **S4 巢穴** | 社交与繁殖 | 大数据展示 + 信息标签 |
| **S5 迁徙** | 迁徙/分布 | 迁徙路线卡 + 栖息地卡 + 湿地关联 |
| **S6 收束** | 文化关联 | 八维文化覆盖 + 联网搜图 |
| **S7 生态** | 保护呼吁 | 保护等级 + 种群趋势 + 威胁标签 + 呼吁文案 |
| **闭幕** | 片尾 | 物种名 + SVG 摘要卡 |

## 技术栈

- **GSAP 3.14** — 动画引擎
- **Edge-TTS** (`zh-CN-XiaoxiaoNeural`) — TTS 旁白
- **HyperFrames** — 视频渲染
- **剪映** — 后期合成（正片叠底/滤色混合模式）

## 文件说明

```
bird-science-video-generator/
├── SKILL.md         # 完整规范文档（V7.0）
├── index_A.html     # 晨曦暖色版模板（Light Mode）
├── index_B.html     # 暮影电影版模板（Dark Mode）
└── README.md        # 本文件
```

## 完整规范

请参阅 [SKILL.md](./SKILL.md) 了解：
- 布局规范与 CSS 变量
- 自动主题色系统（中国古典色谱）
- 羽色提取铁律（13 部位逐项核对）
- GSAP 动画配方（A/B 两版）
- 研究工作流（WebSearch 交叉验证）
- 零幻觉约束（邮票/国鸟/科技/文化配图）
- Post-Render Checklist

## License

MIT