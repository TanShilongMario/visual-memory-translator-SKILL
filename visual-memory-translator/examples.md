# Usage Examples

## Example A — 默认宫格预览

```text
启用影像转译 Skill，默认模式。
```

分析图像后生成一张 6 格（2×3）预览图。图内只标 `01`–`06`，回复中列出各风格名和适配理由，等待用户选号。

---

## Example A2 — 指定宫格数

```text
先给我 9 个差异大的风格看看。
```

```yaml
preview_mode: force
preview_count: 9
```

---

## Example A3 — 选号与融合

```text
05
融合 02 和 05，但以 05 为主。
再换一组。
```

选号或融合时都回到原始照片重新生成。「再换一组」则保留原图，更换候选风格组合。

---

## Example A4 — 跳过预览

```text
跳过预览，你来判断，直接出最终图。
```

```yaml
preview_mode: skip
```

---

## Example B — 不展示原图 + 极致抽象

```text
启用影像转译 Skill。
不要展示原图，极致抽象。
```

```yaml
original_display_mode: translation_only
style_mode: extreme_minimal_abstraction
abstraction_level: extreme
```

其他参数自动判断。

---

## Example C — 展览票

```text
用展览票模式，把这次旅行看成一次展览。
```

```yaml
style_mode: exhibition_ticket
layout_mode: asymmetric_archive
text_mode: auto_exhibition_label
```

未说明原图是否出现时，优先 `exhibition_reference`。

---

## Example D — 胶带照片

```text
用胶带把原图贴在左上角，其余你设计。
```

```yaml
original_display_mode: taped_corner_photo
photo_position: top_left
```

---

## Example E — 只推荐不生成

```text
先别做，给我推荐几个方案。
```

不生成。推荐最多 3 个差异明显方向，例如：

1. 上下分栏 + 极简水彩  
2. 胶带照片 + 极致抽象  
3. 展览票 + 档案式版面  

各用一句话说明适合原因。

---

## Example F — 自然语言参数

```text
启用影像转译编辑器。
原图用透明胶带贴在右上角。
风格选极致抽象极简。
不需要文字。
3:4。
```

## Example G — YAML

```yaml
skill: visual_memory_translator
original_display_mode: taped_corner_photo
photo_position: top_right
style_mode: extreme_minimal_abstraction
abstraction_level: extreme
text_mode: none
ratio: 3:4
```

---

## Example H — 分层贴纸记忆 / Layered Sticker Memory

```text
把人物、中景和远景分别剥离出来，做成统一白边贴纸；主体放大，保持大面积留白。
```

```text
Separate the subject, midground, and far background into white-bordered stickers. Enlarge the subject and preserve extensive whitespace.
```

```yaml
preset: layered_sticker_memory
original_display_mode: extracted_sticker_layers
layout_mode: sticker_layer_reassembly
style_mode: layered_sticker_reassembly
layer_count: 3
sticker_border_width: standard_3_to_5_percent
sticker_shadow: very_subtle
whitespace_level: very_high
```

若无法可靠拆出三层，自动降为两层，不补造遮挡内容。

---

## Example I — 圆润粗线色块 / Rounded Monoline Blocks

```text
把人物画成圆润的粗单线插画，只用三个以内的单色色块，不展示原图。
```

```text
Turn the subject into a rounded bold-monoline illustration with no more than three flat color blocks. Hide the source photo.
```

```yaml
preset: rounded_monoline_memory
original_display_mode: translation_only
layout_mode: large_whitespace_small_art
style_mode: rounded_monoline_blocks
line_weight: bold_uniform_rounded
color_block_count: 3
abstraction_level: high
whitespace_level: very_high
```

---

## Example J — 文本隐喻卡

```text
把这句话做成影像转译：所谓工作与生活的平衡，就是工作不断加码，生活负责配重。
```

```yaml
input_mode: text
preview_mode: skip
style_mode: editorial_metaphor_card
text_mode: user_text
ratio: 3:4
```

保留原句，只画一个隐喻（例如天平），不要画完整故事，不要金句叠照片。

---

## Example K — 节日限定

```text
启用影像转译。今天若是节日就带一点节日痕迹。
```

```yaml
holiday_mode: auto
```

窗口为节日 ±1 天。七夕双人照可用红线/喜鹊；单人照不加伴侣。

```text
不用节日限定。
圣诞节限定，但不要圣诞老人。
```

```yaml
holiday_mode: skip
# 或
holiday_mode: force
holiday_id: christmas
```

---

## Clarification example

信息不足且方向分歧大时：

> 这张图很适合两种方向：  
> 1. 保留原图，上下分栏做「现实 / 记忆」对照  
> 2. 不展示原图，直接做极致抽象  
> 3. 把原图缩成胶带照片放在角落  
> 你想选哪个？如果不选，我会默认用第 1 种。
