# Usage Examples

## Example A — 默认

```text
启用影像转译 Skill，默认模式。
```

直接分析图像并执行默认策略。

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

## Clarification example

信息不足且方向分歧大时：

> 这张图很适合两种方向：  
> 1. 保留原图，上下分栏做「现实 / 记忆」对照  
> 2. 不展示原图，直接做极致抽象  
> 3. 把原图缩成胶带照片放在角落  
> 你想选哪个？如果不选，我会默认用第 1 种。
