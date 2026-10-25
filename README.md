# 英语学习人工智能

面向**英语专业四级（TEM-4）口语考试**的思辨口语陪练 Skill（可开源）。AI 逐轮出思辨话题（Topic）并给出一正一反两句纯英文参考句型，用户口头作答后，AI 逐字转写、输出适配专四口语的改写并点评，再提供【继续】（深度追问）与【重新回答】（重答重评）两个选项，循环推进训练。

---

## 1. 项目解决什么问题

很多英语专业学生在备考 **TEM-4 口语**的“话题陈述 / 观点阐述”环节时，普遍面临三个问题：

1. **没人陪练**：找不到即时反馈的对象，练完不知道对错、无从改进。
2. **中式英语难自纠**：说话常出现中文直译语序、中式搭配、缺主语句、逻辑跳接等"Chinglish"，自己往往察觉不到。
3. **缺思辨框架**：面对一个话题不知从何说起，缺少可复用的"肯定 / 否定"立论句型，难以组织层次分明的口头表达。

本项目把"**出题 → 口头作答 → 逐字转写 → 针对中式英语改写 → 点评 → 追问**"做成一套可循环的陪练流程，帮用户在真实作答中逐轮暴露并修正中式英语、理顺口语逻辑、提升用词地道度，从而在考场上更自信、更流畅地完成话题陈述。

---

## 2. 主要功能

- **逐轮出题陪练**：每轮先给出纯英文 `Topic`，再给出 `Affirmative`（肯定立场）与 `Negative`（否定立场）两句地道、可套用的参考句型作为"脚手架"，随后等待用户作答。
- **【我的原句】**：忠实转写用户口述的英文，保留原始表达、不美化、不纠正，让用户清楚看到自己的真实产出。
- **【优化句】**：仅输出 **1 版**适配专四口语的改写；优先修正中式英语（中文直译语序、中式搭配、逻辑断层、母语负迁移），拒绝浅层同义词替换，核心改动内容加粗，句式口语自然、不过度书面化。
- **【简短点评】**：点明本次具体的中式英语问题，并从逻辑、句式、用词地道度三方面给出简短评价。
- **双分支推进**：用户输入【继续】→ 基于当前话题做一次深度追问，开启新一轮作答；输入【重新回答】→ 不换话题，等待再次作答并重新转写 / 优化 / 点评，直到用户输入【继续】。
- **内置话题库**：覆盖教育、科技、环境、社交媒体、工作与职业、健康与生活、消费、家庭等类别，可直接选用，也可仿照生成同风格新话题。
- **灵活边界**：可切换到全新话题或随时结束训练。

---

## 3. 安装方法

本 Skill 是**纯提示词流程**，不包含任何脚本，因此"安装"就是把技能目录放入 Agent 能加载的 Skill 根目录。

1. 复制或移动整个技能目录 `英语学习人工智能/`（内含 `SKILL.md` 与 `agents/`）到你的 Skill 根目录，例如：
   - 本地 Agent 的 `workspace/.user_skills/`，或
   - 你使用的 Agent / 项目约定的 `skills` 目录。
2. 放置后，技能即可被加载，无需安装任何 Python 依赖。
3. 本 Skill **暂不支持**：网页抓取、PDF、图形界面；也不做整篇范文写作、逐词翻译、孤立语法单项讲解。

> 技术说明：开放 Skill 格式要求 frontmatter 的 `name` 为小写连字符标识，因此 `SKILL.md` 中 `name` 为 `english-learning-ai`（调用时即 `$english-learning-ai`）；中文名 `英语学习人工智能` 保留为目录名与 `agents/openai.yaml` 的 `display_name`。

---

## 4. 使用方法

1. 安装（见上文第 3 节）后，对 AI 说"开始专四口语思辨陪练"，或直接描述想练的话题方向，即可进入训练。
2. AI 会输出 `Topic` + `Affirmative` / `Negative` 两句参考句型，等待你作答。
3. 你用口头英文作答（可打字，也可口述转写）。
4. AI 输出【我的原句】→【优化句】→【简短点评】，随后给出【继续】、【重新回答】两个选项：
   - 输入 **【继续】**：基于当前话题深度追问，开启新一轮作答；
   - 输入 **【重新回答】**：不换话题，再次作答并重新转写 / 优化 / 点评，直到你输入【继续】。
5. 可随时输入"换一个话题"切换全新题目，或"结束 / 不练了"收尾训练。

### 每轮流程（输入 → 输出）

```
第 1 步  出题：AI 输出 Topic（纯英文）+ Affirmative/Negative 两句参考句型，等待用户作答
第 2 步  反馈：用户作答后，AI 依次输出
             ①【我的原句】逐字转写用户口述英文（不改写、忠实原话）
             ②【优化句】仅 1 版适配专四口语的改写，优先修正中式英语，核心改动加粗
             ③【简短点评】点明本次中式英语问题，并评价逻辑 / 句式 / 用词地道度
第 3 步  选项：AI 给出 【继续】、【重新回答】
             输入【继续】   → 基于当前话题深度追问，开启新一轮作答
             输入【重新回答】→ 不换话题，等待再次作答并重新转写/优化/点评，直到用户输入【继续】
```

---

## 5. 输入输出示例

### 出题（AI）

```
Topic: University students should work part-time while studying.
Affirmative: Part-time work gives students practical skills and financial independence.
Negative: Working part-time can distract students from their academic priorities.
```

### 输入（用户口头作答，含典型中式英语）

> I think student work part-time is very good. Because can get many experience and can earn money. Also can open my eye.

### 输出（AI 反馈）

```
①【我的原句】
I think student work part-time is very good. Because can get many experience and can earn money. Also can open my eye.

②【优化句】
I think it's good for students to work part-time, because it helps them gain valuable experience and earn some money. It can also **open their eyes** to the real world.

③【简短点评】
本句中式英语集中在三点：主句缺主语（Because can get… 应为 it helps them…）、搭配错误（experience 不能用 many，open my eye 应为 open one's eyes）、句子之间靠 And/Also 硬连导致逻辑跳接。优化后补全主语、修正搭配并加了 to the real world 收尾，句式口语自然、不书面化。

【继续】   【重新回答】
```

### 推进（用户输入 → AI 响应）

```
用户：继续
AI  ：Topic: If part-time work is worthwhile, how can students balance it with their academic priorities?
      Affirmative: With a clear schedule, students can protect study time while still gaining work experience.
      Negative: Juggling both often means sacrificing sleep or coursework in the busiest weeks.
      ...（等待新一轮作答）
```

---

## 目录结构

```
英语学习人工智能/
├── SKILL.md              # 技能定义：流程、改写标准、点评要求、话题库、示例
└── agents/
    └── openai.yaml       # 开放格式元数据（展示名、简介、默认提示语）
```

---

## 改写标准（优化句）

- 仅出 **1 版**，适配专四口语、适配口头表达（不书面化、不堆砌大词）。
- 优先修正中式英语：中文直译语序、中式搭配、逻辑断层、母语负迁移。
- **拒绝浅层同义词替换**；每次改动针对具体问题，核心改动内容加粗。
- 原句已很地道时只做轻量润色，并在点评中说明。

---

## 验证

已通过官方校验脚本验证技能结构：

```powershell
python scripts/quick_validate.py "英语学习人工智能"
# 输出：Skill is valid!
```
