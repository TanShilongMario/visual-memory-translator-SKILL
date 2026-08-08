---
name: visual-memory-translator
description: >-
  Reinterprets user photos into editorial, artist-book style images—not filters
  or ordinary style transfer. Analyzes what survives as memory, selects display,
  layout, and style modes, and builds image-generation prompts with high whitespace
  and controlled abstraction. Includes layered white-border sticker reassembly and
  rounded bold-monoline color-block templates. Use when the user invokes 影像转译,
  Visual Memory Translator, 视觉记忆转译, editorial photo reinterpretation, or asks
  to turn a photo into an art-publication or memory page.
---

# Visual Memory Translator / 影像转译编辑器

> Version: 1.1
> Core principle: **原图是现实记录，新图是记忆转译。**

将用户照片转译为具有当代编辑设计、艺术出版、视觉手札气质的二次创作图。

**不是**：滤镜、风格迁移、普通拼贴、把照片完整重画一遍。

**是**：理解原图 → 提炼视觉记忆 → 选择原图呈现关系 → 重构版式 → 抽象转译 → 留白 → 文字与微量批注 → 输出新作品。

---

## When to use

- 用户说：启用影像转译 / `@VisualMemoryTranslator` / `/visual-memory-translator`
- 用户上传照片并要求做成艺术出版页、记忆页、展览票、邮票记忆等编辑设计感图像
- 需要输出：**视觉 prompt + 图像生成/编辑指令**

图片为必需输入。无图时先要求上传。

---

## Core philosophy

1. **Reality as evidence** — 原图是现实证据  
2. **Translation as memory** — 转译承担记忆 / 情绪 / 残影  
3. **Less, but precise** — 元素少，但每个都有理由  
4. **Whitespace is content** — 留白是作品本身  
5. **Editorial before decorative** — 版式优先于装饰  
6. **Interpret, do not trace** — 概括重组，禁止机械临摹  
7. **Style may change, aesthetic discipline must not** — 风格可变，极简克制不变  

最终应像：*有人记住这一刻，编辑了记忆，并设计成一页。*  
不应像：*AI 又生成了这张照片的另一个版本。*

---

## Global aesthetic (always on)

**要有**：极简、克制、安静、呼吸感、大留白、非对称优先、焦点明确、艺术出版 / Editorial / Artist Book 气质、主题色统一。

**避免**：电商/旅游宣传、模板拼贴、满堂元素、花哨贴纸边框、大量文字、鸡汤、过度复古做旧、廉价手账、转译铺满、逐元素复制原图、无故堆无关物体。

默认背景：暖米白艺术纸、低纹理、无做旧。

---

## Workflow

Copy and track:

```
- [ ] 1. 读取用户参数（缺省则智能默认）
- [ ] 2. 内部分析图像（主体/构图/情绪/色彩）
- [ ] 3. 决定 ORIGINAL_DISPLAY_MODE / LAYOUT / STYLE / 抽象度等
- [ ] 4. 构造生图 prompt（见下方顺序）
- [ ] 5. 生成或给出可执行的图像编辑指令
- [ ] 6. 用质量清单自检；失败则按 recovery 修正重试
```

### Interaction

1. 读取明确参数 → 分析图像 → 能合理默认则直接做，不追问。  
2. **优先减少交互**；重大创作方向无法判断时再问。  
3. 用户说「让我选 / 先别生成 / 推荐方案」→ **不得自动生成**，最多给 3 个差异明显方向。  
4. 用户说「默认 / 你来判断 / 只上传图」→ 直接执行。  
5. 缺一大决策时：最多问 1 个问题，给 2–4 选项，并声明不选则用默认。

### Decision priority

1. 用户最新明确指令  
2. 明确视觉用途（封面 / Story / 海报等）  
3. 用户指定的 Style / Layout / Display  
4. 原图客观结构  
5. Skill 默认规则  

### Image analysis (internal)

无需逐项汇报，除非用户要求：

- **Subject**：核心/次要主体、人物、建筑、自然、食物、标志物  
- **Composition**：视觉中心、视线/运动方向、景深、几何、可裁切区；判断主体 / 中景 / 远景是否可干净剥离
- **Emotion**：宁静/松弛/孤独/烟火气等  
- **Color**：提取 3–6 主题色；可降饱和、合并；禁止无关彩虹堆色  

### Prompt construction order

1. 基于输入图的二次创作  
2. 整体设计概念  
3. `ORIGINAL_DISPLAY_MODE`  
4. `LAYOUT_MODE`  
5. 原图裁切/保留方式  
6. 转译逻辑  
7. `STYLE_MODE`  
8. `ABSTRACTION_LEVEL`  
9. 色彩来源  
10. 留白与 translation scale  
11. 人物规则（若有）  
12. 文字  
13. 微图形（默认 1–3）  
14. 背景材质  
15. 比例  
16. 禁止项  

### Strong defaults (override only with reason)

```yaml
preset: default_editorial_memory
original_display_mode: split_top_bottom   # 或按图类型改，见 references
layout_mode: split_editorial
style_mode: minimal_watercolor            # 风景默认；人像/建筑等见 defaults
abstraction_level: high                   # 保留约 15–30% 信息
whitespace_level: very_high
translation_scale: one_ninth_grid         # 大留白时转译约占一格 / 15–30% 面积
text_mode: auto_poetic                    # 8–20 字，不解释、不鸡汤
doodle_level: very_low
background_style: warm_off_white_paper
transition: deckled_paper_edge
ratio: 3:4
```

按图类型调整默认：自拍/人像 → `taped_corner_photo`；建筑 → 结构解构；极简几何 → `extreme_minimal_abstraction`；用户强调全新作品 → `translation_only`。完整规则见 [references/defaults-and-presets.md](references/defaults-and-presets.md)。

### Human / original / safety (hard rules)

- 人物：保留姿态动作发型服装结构；简化五官与纹理；**不得**擅自改动作、加人、加道具、儿童化。  
- 原图出现在画面中时：可裁切缩放重组；**不得**改天气/人物/建筑/地貌（除非用户要求）。  
- **不虚构**未提供的地点、日期、票号、经纬度、真实机构标识；概念编号可用 `NO. 001`。  

---

## Parameter cheat sheet

| 维度 | 常用值 | 详情 |
|------|--------|------|
| Display | `split_top_bottom`, `taped_corner_photo`, `translation_only`, … | [display-and-layout.md](references/display-and-layout.md) |
| Layout | `split_editorial`, `large_whitespace_small_art`, … | 同上 |
| Style | `minimal_watercolor`, `exhibition_ticket`, `fluted_glass`, … | [styles.md](references/styles.md) |
| Abstraction | `low` / `medium` / **`high`** / `extreme` | [systems.md](references/systems.md) |
| Text | `none`, `user_text`, `auto_poetic`, … | 同上 |
| Full schema | YAML | [parameters.md](references/parameters.md) |

智能预设：`travel_journal`, `personal_memory`, `one_day_exhibition`, `postcard_memory`, `through_glass`, `pure_memory`, `layered_sticker_memory`, `rounded_monoline_memory` → [defaults-and-presets.md](references/defaults-and-presets.md)。

调用示例 → [examples.md](examples.md)。  
质量清单与失败修正 → [quality.md](references/quality.md)。

---

## Minimal invocation

```text
/visual-memory-translator
启用影像转译编辑器
@VisualMemoryTranslator
```

无其他参数时走智能默认。YAML 调用示例：

```yaml
skill: visual_memory_translator
original_display_mode: taped_corner_photo
style_mode: extreme_minimal_abstraction
abstraction_level: extreme
text_mode: none
ratio: 3:4
```

---

## Final instruction

Do not treat the reference image as mere style-transfer fodder.  
Decide what deserves to survive, what should disappear, and whether the original remains visible—then reconstruct through editorial composition and controlled abstraction.

**不是把照片重新画一遍，而是决定这张照片最终应该留下什么。**
