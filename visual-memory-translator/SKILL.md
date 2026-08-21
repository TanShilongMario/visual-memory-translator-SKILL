---
name: visual-memory-translator
description: >-
  Reinterprets photos into editorial, artist-book memory pages, and can also
  translate a sentence or concept into a sparse editorial metaphor card. Not a
  filter, style-transfer, quote-on-photo template, or full portrait redraw.
  Analyzes what should survive, selects display/layout/style, and builds image
  prompts with high whitespace and controlled abstraction. When a photo is given
  and no style is named, first creates a 4/6/9-panel style-preview contact sheet,
  then regenerates the chosen direction from the original photo. Includes layered
  white-border stickers and rounded bold-monoline blocks. Use when the user
  invokes 影像转译, Visual Memory Translator, 视觉记忆转译, 文本转译, editorial photo
  reinterpretation, a concept/quote visual card, a holiday-limited editorial
  overlay, 纸币样张, 纸币实景, or asks to turn a photo into a memory page. Around Qixi, Christmas,
  and other CN/JP/US holidays (±1 day), may add a sparse seasonal motif unless
  the user opts out.
---

# Visual Memory Translator / 影像转译编辑器

> Version: 1.4.1
> Core principle: **原图是现实记录，新图是记忆转译。无图时，句子是概念，画面是隐喻。**

将用户照片转译为具有当代编辑设计、艺术出版、视觉手札气质的二次创作图。

**不是**：滤镜、风格迁移、普通拼贴、把照片完整重画成肖像、金句叠照片。

**是**：理解输入 → 决定该留下什么 → 重构版式与隐喻 → 留白 → 输出新作品。照片走记忆转译；句子走概念转译。

---

## When to use

- 用户说：启用影像转译 / 纸币样张 / 纸币实景 / `@VisualMemoryTranslator` / `/visual-memory-translator`
- 用户上传照片并要求做成艺术出版页、记忆页、展览票、邮票记忆等编辑设计感图像
- 用户只给一句文案、金句、概念，要求做成编辑感视觉卡 / 文本转译
- 用户指定 **纸币样张** 或 **纸币实景**：跳过预览，直达对应纪念钞构图
- 需要输出：**视觉 prompt + 图像生成/编辑指令**

### Input routing

| 输入 | 路径 |
|------|------|
| 有参考图 | `input_mode: photo` — 影像记忆转译（主路径） |
| 无图，只有句子/概念/标题 | `input_mode: text` — 文本隐喻转译，**不要**先追问必须上传图片 |
| 图 + 指定文案 | `input_mode: mixed` — 图走记忆转译，文案作画面文字，不另发明金句 |

无图且也没有可转译的句子时，再要求上传图片或给出句子。

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

**避免**：电商/旅游宣传、模板拼贴、满堂元素、花哨贴纸边框、大量文字、鸡汤、过度复古做旧、廉价手账、转译铺满、逐元素复制原图、无故堆无关物体、金句叠夜景、完整肖像重画。

默认背景：暖米白艺术纸、低纹理、无做旧。

---

## Workflow

Copy and track:

```
- [ ] 1. 判定 input_mode：photo / text / mixed
- [ ] 2. 读取用户参数；检测日期是否落在节日 ±1 天
- [ ] 3. photo 路径判断是否需要风格预览
- [ ] 4. photo 且未指定风格：先生成一张 4/6/9 格预览图并等待选择
- [ ] 5. text 路径：提炼一个隐喻，默认直出编辑卡（见 text-visual.md）
- [ ] 6. 决定 DISPLAY / LAYOUT / STYLE / 抽象度 / 节日层
- [ ] 7. 构造成品 prompt（photo 必须从原始照片重建）
- [ ] 8. 用质量清单自检；失败则按 recovery 修正重试
```

### Interaction

1. 读取明确参数 → 分析输入；能合理默认则不追问。
2. **photo 且未指定 `style_mode`**：默认生成一张 6 格（2×3）预览图，而不是直接出成品。
3. 用户可要求 4 格（2×2）或 9 格（3×3）；未说数量时用 6 格。
4. 预览图内只标 `01`–`09`，不把风格名与长说明塞进图里；在回复中逐号列出风格名和一句适配理由。
5. 用户回复编号后，**必须基于原始照片重新生成高清成品**；不得裁切、放大或二次编辑宫格中的低清单格。
6. 支持「再换一组」和「融合 02 和 05」；融合时先说明主风格与被吸收的特征，然后从原图生成。
7. 用户明确说「跳过预览 / 直接出最终图」或已指定风格（含 **纸币样张** / **纸币实景**）时，直达成品。只说「纸币」而未点名时，按当次需求选样张或实景。
8. 用户说「先别生成」时，不生成图；最多用文字给 3 个方向。
9. **text 路径默认 `preview_mode: skip`**。只有用户说「先给我几个方向」时，才出最多 4 个差异明显的隐喻方案（可文字，或 2×2 宫格）。
10. **节日限定**：用对话当天日期，窗口 ±1 天。默认 `holiday_mode: auto`（窗口内启用）；用户说「不用节日限定」则 skip。不得为过节而给单人照补出伴侣。

宫格规则见 [references/style-preview.md](references/style-preview.md)。  
文本转译见 [references/text-visual.md](references/text-visual.md)。  
节日层见 [references/holidays.md](references/holidays.md)。

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
14. 节日薄层（若窗口命中且未 skip）  
15. 背景材质  
16. 比例  
17. 禁止项  

### Strong defaults (override only with reason)

```yaml
preset: default_editorial_memory
input_mode: auto                          # photo | text | mixed
preview_mode: auto                        # photo 未指定风格时先预览；text 默认 skip
preview_count: 6                          # 4 | 6 | 9
original_display_mode: split_top_bottom   # 或按图类型改，见 references
layout_mode: split_editorial
style_mode: auto                          # photo 先预览；text 默认 editorial_metaphor_card
abstraction_level: high                   # 保留约 15–30% 信息
whitespace_level: very_high
translation_scale: one_ninth_grid         # 大留白时转译约占一格 / 15–30% 面积
text_mode: auto_poetic                    # 8–20 字，不解释、不鸡汤
doodle_level: very_low
holiday_mode: auto                        # auto | force | skip；窗口 ±1 天
background_style: warm_off_white_paper
transition: deckled_paper_edge
ratio: 3:4
```

按图类型调整默认：自拍/人像 → `taped_corner_photo`，且转译禁止完整肖像；建筑 → 结构解构；极简几何 → `extreme_minimal_abstraction`；用户强调全新作品 → `translation_only`。完整规则见 [references/defaults-and-presets.md](references/defaults-and-presets.md)。

### Human / original / safety (hard rules)

- 人物：保留姿态动作发型服装结构；简化五官与纹理；**不得**擅自改动作、加人、加道具、儿童化。  
- **禁止完整肖像画**：人像转译不得变成可单独当肖像作品的写实水彩/线稿；五官最多 1–3 个记号。**例外**：`banknote_specimen` / `banknote_in_situ` 允许凹版雕线肖像，仍禁止照片级脸。  
- 原图出现在画面中时：可裁切缩放重组；**不得**改天气/人物/建筑/地貌（除非用户要求）。  
- 分层贴纸必须是 **2–3 张可分离的白边贴纸**，不得融成一张异形大贴纸。  
- 节日限定不得为过节而加人、改成情侣或改节日装；单人照只用低强度符号。  
- **不虚构**未提供的地点、日期、票号、经纬度、真实机构标识；概念编号可用 `NO. 001`。  
  节日层不代表照片拍摄于该日，禁止把「今天」写进伪造日期章。  

---

## Parameter cheat sheet

| 维度 | 常用值 | 详情 |
|------|--------|------|
| Input | `photo`, `text`, `mixed` | [text-visual.md](references/text-visual.md) |
| Display | `split_top_bottom`, `taped_corner_photo`, `translation_only`, … | [display-and-layout.md](references/display-and-layout.md) |
| Layout | `split_editorial`, `large_whitespace_small_art`, … | 同上 |
| Style | `banknote_specimen`, `banknote_in_situ`, `minimal_watercolor`, … | [styles.md](references/styles.md) / [banknote.md](references/banknote.md) |
| Preview | `auto` / `skip`; 4 / **6** / 9 格 | [style-preview.md](references/style-preview.md) |
| Holiday | `auto` / `force` / `skip`；±1 天 | [holidays.md](references/holidays.md) |
| Abstraction | `low` / `medium` / **`high`** / `extreme` | [systems.md](references/systems.md) |
| Text | `none`, `user_text`, `auto_poetic`, … | 同上 |
| Full schema | YAML | [parameters.md](references/parameters.md) |

智能预设：`travel_journal`, `personal_memory`, `one_day_exhibition`, `postcard_memory`, `through_glass`, `pure_memory`, `layered_sticker_memory`, `rounded_monoline_memory`, `editorial_text_card`, `banknote_specimen`, `banknote_in_situ` → [defaults-and-presets.md](references/defaults-and-presets.md)。

调用示例 → [examples.md](examples.md)。  
文本转译 → [text-visual.md](references/text-visual.md)。  
节日限定 → [holidays.md](references/holidays.md)。  
纪念纸币 → [banknote.md](references/banknote.md)。  
质量清单与失败修正 → [quality.md](references/quality.md)。

---

## Minimal invocation

```text
/visual-memory-translator
启用影像转译编辑器
@VisualMemoryTranslator
```

无其他参数且未指定风格时，先走 6 格风格预览。YAML 调用示例：

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
**不是把句子画成故事，而是决定这句话只需要一个隐喻。**
