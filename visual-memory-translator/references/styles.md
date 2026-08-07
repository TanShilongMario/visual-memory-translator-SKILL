# STYLE_MODE Library

所有 Style 是「表达插件」，**不能**覆盖全局美学（极简、克制、留白、编辑感）。

---

## `minimal_watercolor` — 极简水彩

透明水彩、淡墨、轻微纸张颗粒、水迹、干/湿边、局部渗透、低密度线稿；色彩来自原图。转译主体不能成为完整风景画。

## `minimal_line_watercolor` — 极简线稿水彩

更强调线条、色彩更少、人物轮廓更清楚。适合人像与动作。

## `freehand_doodle` — 极简自由涂鸦

自由线、轻微不完美、断线、重复线、小范围马克笔/彩铅；维持高级编辑感。禁止儿童涂鸦页。

## `minimal_vector` — 现代极简矢量

几何轮廓、纯色块、3–6 色、清晰边缘、大量负空间。禁止复杂渐变与信息图式堆砌。

## `single_line_sketch` — 单线速写

单线或极少线、连续轮廓、高度概括、几乎无填色、强留白。

## `extreme_minimal_abstraction` — 极致抽象极简

信息压缩到约 5%–15%。仅保留轮廓/路径/一两个色块/光影/动作/颜色记忆。允许第一眼抽象、第二眼发现原图关系。

## `memory_color_blocks` — 色块记忆

大色块、软边界、极少线条。例：山=灰绿块，天空=蓝留白，人=深色轮廓，夕阳=暖黄点。

## `structural_deconstruction` — 结构解构

提炼建筑轮廓、透视、道路、网格、轴线。适合城市/建筑/室内/产品。

## `stamp_memory` — 邮票记忆

**把一次经历变成可以寄出的记忆。** 齿孔、小型主体、极简邮戳、日期/地点/编号。未知信息不得虚构；可用抽象编号。

## `exhibition_ticket` — 旅行展览票

**把一次经历当成一场只发生一次的展览。** 展览标题、票据结构、小图、编号、展签短句。未知地点/日期不得虚构；可用 `UNTITLED JOURNEY` / `FIELD NOTE` / `MEMORY STUDY` / `ONE-DAY EXHIBITION` 等。

## `fluted_glass` — 长虹玻璃

垂直折射、条带、模糊、拉伸；色彩分离但不艳丽；轮廓可隐约辨认。是材料介质后的记忆，不是滤镜。

## `archive_card` — 档案卡

编号、小图、简短说明、视觉标记、大量留白。禁止虚构经纬度/精确时间/真实档案号（除非用户提供）。

## `specimen_sheet` — 标本页

拆出关键元素排列。适合食物/花草/器物/细节。元素 3–7 个以内。

## `map_note` — 地图札记

路径、行进方向、道路、河流、山体。默认概念地图，非 GIS 精确（除非用户要求）。

## `commemorative_cover` — 纪念封

首日封/纪念信封语言：邮戳、日期框、小型插图。未知信息不得虚构。

---

## Future Style Extension Contract

新 Style 至少定义：

```yaml
style_id:
style_name:
concept:
medium:
line_language:
color_language:
edge_behavior:
texture:
human_rendering:
typography:
micro_graphics:
whitespace_behavior:
avoid:
```

示例：

```yaml
style_id: minimal_watercolor
style_name: 极简水彩
concept: 现实被时间稀释之后留下的透明视觉残影
medium: 透明水彩 + 少量墨线
line_language: 细、断续、低密度
color_language: 原图提取 3-6 色，低饱和
edge_behavior: 晕染、干边、自然消失
texture: 细腻水彩纸
human_rendering: 简练轮廓 + 少量淡色
typography: 自然中文手写
micro_graphics: 1-3 个极简笔记符号
whitespace_behavior: 极高
avoid: 完整水彩风景画、儿童绘本感
```
