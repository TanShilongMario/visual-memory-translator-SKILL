# Visual Memory Translator / 影像转译编辑器

把照片转译成具有**当代编辑设计、艺术出版、视觉手札**气质的二次创作图像。

> **原图是现实记录，新图是记忆转译。**  
> 不是滤镜，不是风格迁移，不是把照片重新画一遍——而是决定这张照片最终应该留下什么。

---

## 这是什么

这是一个符合 [Agent Skills](https://cursor.com/docs/skills) / [agentskills.io](https://agentskills.io) 标准的 Cursor Skill 包。

Agent 会：理解原图 → 提炼视觉记忆 → 选择原图呈现方式与版式 → 抽象转译 → 建立留白 → 加入短句与微量批注 → 输出可执行的生图 / 修图指令。

**适合**：旅行记录、人像日常、城市建筑、风景、想做成「记忆页」而非滤镜图的照片。  
**不适合**：电商主图、宣传海报模板、儿童绘本风（除非你明确要求）。

---

## 安装

### 方式 A：从 GitHub 导入（推荐）

1. Cursor → **Customize** → **Rules** → **Add Rule**  
2. 选择 **Remote Rule (Github)**  
3. 填入本仓库 URL  

### 方式 B：手动放入项目

将 `visual-memory-translator/` 目录复制到：

```text
.cursor/skills/visual-memory-translator/
```

或用户全局：

```text
~/.cursor/skills/visual-memory-translator/
```

安装后在 Agent 中输入 `/visual-memory-translator`，或说「启用影像转译编辑器」。

---

## 快速使用

1. 上传一张照片  
2. 调用 Skill，例如：

```text
启用影像转译编辑器，默认模式。
```

```text
不要展示原图，极致抽象。
```

```text
用展览票模式，把这次旅行看成一次展览。
```

未指定参数时，Skill 会按图像类型智能默认（风景偏极简水彩、自拍偏胶带小图 + 线稿水彩等）。详细示例见 [`visual-memory-translator/examples.md`](visual-memory-translator/examples.md)。

---

## 仓库结构

```text
.
├── README.md
├── LICENSE
└── visual-memory-translator/          # Skill 包（文件夹名 = skill name）
    ├── SKILL.md                       # 主指令（YAML frontmatter + 核心流程）
    ├── examples.md                    # 调用示例
    └── references/                    # 按需加载的详细规范
        ├── display-and-layout.md      # 原图展示 / 版式
        ├── styles.md                  # 风格库
        ├── defaults-and-presets.md    # 默认决策与智能预设
        ├── systems.md                 # 抽象度 / 人物 / 色彩 / 文字 / 材质
        ├── parameters.md              # 完整参数 schema
        └── quality.md                 # 质量清单与失败修正
```

按需拆分是为了控制上下文：Agent 先读 `SKILL.md`，再按任务打开对应 reference。

---

## 设计原则（摘要）

| 原则 | 含义 |
|------|------|
| Reality as evidence | 原图是现实证据 |
| Translation as memory | 转译是记忆与残影 |
| Less, but precise | 少而准 |
| Whitespace is content | 留白即内容 |
| Editorial before decorative | 版式先于装饰 |
| Interpret, do not trace | 转译而非描摹 |

默认：**高抽象（约保留 15%–30% 信息）**、**极高留白**、**转译主体约占九宫格一格**、短句中文文案、暖米白纸面。

可选风格包括：极简水彩、线稿水彩、涂鸦、矢量、色块记忆、结构解构、邮票记忆、展览票、长虹玻璃、档案卡、标本页等。

---

## 兼容性

- Cursor Agent（`.cursor/skills/`）  
- 兼容目录：`.agents/skills/`、Claude / Codex skills 路径（见 Cursor 文档）  
- 面向多模态图像生成 / 编辑工作流；默认沟通语言为中文  

本 Skill 设置了 `disable-model-invocation: true`：需通过 `/visual-memory-translator` 或明确口令启用，避免上传普通照片时被误触发。

---

## 许可

MIT License — 见 [LICENSE](LICENSE)。
