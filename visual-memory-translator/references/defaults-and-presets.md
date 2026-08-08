# Defaults & Smart Presets

未指定参数时按本节执行。修改默认必须基于图像的合理判断。

---

## Default ORIGINAL_DISPLAY_MODE

| 情况 | 默认 |
|------|------|
| A. 构图优秀、信息完整、纪实价值高 | `split_original_and_translation`（上下或左右分栏，由比例决定）→ 实现上常用 `split_top_bottom` / `split_left_right` |
| B. 自拍、人像、旅行纪念 | `attached_photo` → 常用 `taped_corner_photo` / `polaroid_insert` |
| C. 信息简单、色彩强、适合高度抽象 | `translation_only` |
| D. 用户强调「二次创作 / 全新图」 | 降低原图存在感，不必完全隐藏 |

---

## Default LAYOUT_MODE

**竖幅**：上下分栏 → 满版留白+小图 → 单图。  
**横幅**：上下分栏（可重裁）→ 左右分栏 → 角落照片+大留白。  
**明确纵向轴线**（道路/山峰/建筑/人像）：保持轴线关系。  
**明显运动/视线方向**：给方向留空间。

---

## Default STYLE_MODE

| 图像类型 | 默认 |
|----------|------|
| 风景 / 山野 / 村落 / 水景 | `minimal_watercolor` |
| 人物 / 自拍 / 日常 | `minimal_line_watercolor`；轻松有趣可用 `freehand_doodle` |
| 建筑 / 城市 | `architectural_watercolor` 倾向 → `minimal_watercolor` 或 `structural_deconstruction` |
| 食物 / 夜市 / 烟火气 | `minimal_watercolor`，加强色块/烟雾/热气/形状概括 |
| 极干净、几何强 | `extreme_minimal_abstraction` |
| 主体明确、景深分层清楚 | `layered_sticker_reassembly` |
| 轮廓鲜明、姿态或物体形状有趣 | `rounded_monoline_blocks` |

---

## Default ABSTRACTION / WHITESPACE / TEXT

- **Abstraction**：`high`（约 15%–30% 信息）— 仍能看出来源，但已是另一种视觉语言  
- **Whitespace**：`very_high`；转译通常约占一个九宫格单元，可扩至约 1.5，不得轻易铺满  
- **Text**：`auto_poetic` — 1 句中文，8–20 字，1–2 行；不解释、不口号、不鸡汤；有余味与时间感  

文案语气参考（勿反复套用）：

- 山在那里，风也记得来过。  
- 溪流知道方向，时间自会作答。  
- 城市向上生长，目光也会因此变远。  

---

## Default Preset

用户只说「启用影像转译」并上传图：

```yaml
preset: default_editorial_memory
original_display_mode: split_top_bottom
layout_mode: split_editorial
style_mode: minimal_watercolor
abstraction_level: high
whitespace_level: very_high
translation_scale: one_ninth_grid
text_mode: auto_poetic
doodle_level: very_low
background_style: warm_off_white_paper
transition: deckled_paper_edge
ratio: 3:4
```

主动调整示例：自拍 → `taped_corner_photo`；建筑 → `structural_deconstruction`；极简几何 → `extreme_minimal_abstraction`；强调全新 → `translation_only`。

---

## Smart Presets

### `travel_journal`

```yaml
original_display_mode: split_top_bottom
style_mode: minimal_watercolor
abstraction_level: high
whitespace_level: very_high
text_mode: auto_travel_note
background: warm_off_white_paper
```

山野、村庄、道路、海边、风景旅行。

### `personal_memory`

```yaml
original_display_mode: taped_corner_photo
layout_mode: large_whitespace_small_art
style_mode: minimal_line_watercolor
abstraction_level: high
text_mode: auto_poetic
```

自拍、人像、生活瞬间。

### `one_day_exhibition`

```yaml
original_display_mode: exhibition_reference
layout_mode: asymmetric_archive
style_mode: exhibition_ticket
abstraction_level: high
text_mode: auto_exhibition_label
```

把一次经历当成一次展览。

### `postcard_memory`

```yaml
original_display_mode: stamp_window
style_mode: stamp_memory
abstraction_level: high
text_mode: auto_minimal
```

### `through_glass`

```yaml
original_display_mode: translation_only
layout_mode: single_artwork
style_mode: fluted_glass
abstraction_level: extreme
text_mode: none
```

### `pure_memory`

```yaml
original_display_mode: translation_only
layout_mode: large_whitespace_small_art
style_mode: extreme_minimal_abstraction
abstraction_level: extreme
text_mode: auto_minimal
whitespace_level: very_high
```

### `layered_sticker_memory`

```yaml
original_display_mode: extracted_sticker_layers
layout_mode: sticker_layer_reassembly
style_mode: layered_sticker_reassembly
abstraction_level: medium
whitespace_level: very_high
layer_count: 3
sticker_border: clean_warm_white
sticker_shadow: very_subtle
text_mode: auto_minimal
```

主体与前中后景分离清晰时使用。若只能可靠识别两层，则用两层，不强行补足三层。主体通常最大，中景次之，远景最小或最淡。

### `rounded_monoline_memory`

```yaml
original_display_mode: translation_only
layout_mode: large_whitespace_small_art
style_mode: rounded_monoline_blocks
abstraction_level: high
whitespace_level: very_high
line_weight: bold_uniform_rounded
color_block_count: 3
text_mode: auto_minimal
```

人物姿态、动物、器物轮廓鲜明时使用。颜色默认不多于三种，只有识别必需时才允许第四种；不得超过四种。
