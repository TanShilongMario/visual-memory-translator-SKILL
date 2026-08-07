# Systems: Abstraction, Human, Color, Text, Materials

---

## ABSTRACTION_LEVEL

| Level | 保留信息量 | 说明 |
|-------|------------|------|
| `low` | ~50%–70% | 仅当用户明确要求高还原 |
| `medium` | ~30%–50% | |
| **`high`** | **~15%–30%** | **默认** |
| `extreme` | ~5%–15% | 配合 extreme abstraction / color blocks / fluted glass |

---

## Human Rendering

**Preserve**：姿态、动作、手势、身体倾斜、发型轮廓、标志性服装结构、配饰、人与环境尺度。  
**Simplify**：五官细节、皮肤写实纹理、精细衣纹、小装饰、复杂光影。  
**Do not invent**：改动作、加人、加原图没有的道具、改服装核心特征、成年人儿童化、改身份角色（除非用户明确要求）。

---

## Color System

从原图提取 3–6 色：

```text
Primary 1 / Primary 2 / Neutral / Shadow / Accent / Optional Highlight
```

允许轻微降饱和、提高统一性、形成大块关系。禁止无理由大量互补色、过度鲜艳、无理由超过 6 个主视觉色。

---

## Text System

### TEXT_MODE

```text
none | user_text | auto_poetic | auto_reflective
auto_travel_note | auto_exhibition_label | auto_minimal
```

默认：`auto_poetic`。

### Copy rules

- 与图像有关但不直接描述  
- 8–20 汉字、1–2 行优先  
- 有余味；不煽情、不鸡汤、不陈词滥调  
- 少用「远方」「时光」「岁月」「治愈」  
- 不为哲理而哲理；不虚构地点或事实  

### Typography

默认：自然手写、笔记感、纤细、松弛、大量呼吸空间。  
`exhibition_ticket` / `archive_card` / `stamp_memory` 可加少量编辑/编号字体，但与手写层级须清晰。

---

## Micro Graphics

默认数量 `1 to 3`。可用：小星号、点、路径、山形、水波、箭头、几何符号、简单植物线、简化太阳、小型印章、坐标十字。  
原则：视觉批注，不是装饰。

---

## Background & Material

```yaml
background: warm_off_white_paper
texture_strength: low
ageing: none
```

推荐：米白 / 暖白 / 象牙白 / 细纹艺术纸 / 极浅奶油。  
禁止默认：黄旧纸、羊皮纸、大颗粒污渍折痕、复古烧边。

---

## Original Image Preservation

出现在成品中时须保留：主体身份、场景关系、摄影质感、色彩气氛、核心构图。  
允许：裁切、缩放、重定主体位置、局部取景。  
不应：重绘照片区、改天气/人物/建筑/地貌/动作（除非用户要求）。

---

## Translation Scale（强约束）

大留白版式下，转译主体默认约占**一个九宫格单元**，约为转译区域 **15%–30%** 面积。  
可扩大仅当：用户明确要求 / 结构过复杂需识别 / Style 需要完整结构——仍留白优先。

---

## Transition Rules

原图与转译相邻时默认：`deckled_paper_edge`（自然撕纸、细腻、不夸张）。  

可选：`clean_cut` | `soft_fade` | `vellum_overlap` | `mask_window` | `paper_fold` | `no_visible_separator`  

避免：粗糙撕裂、强阴影、立体剪贴手账感、过度真实胶水痕迹。

---

## Output Ratio

默认：`3:4` 竖图。用户指定优先。  

用途推定（未给比例时）：Story/竖屏 `9:16`；方图 `1:1`；艺术页 `3:4`；横向编辑 `4:3` 或 `3:2`；公众号封面优先询问或用用户常用比例。  
不要为守默认而无视明确用途。
