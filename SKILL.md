---
name: study-anything
description: Runs a persistent, self-evolving study system for any subject — learning ladder, top-20% study plan, curated resources, guided study sessions, one-question-at-a-time exams, and Feynman retelling — with every topic's spec, plan, log and weak points stored under this skill's topics/ directory and indexed by category and tags. Use when the user wants to learn, continue, review, be quizzed on, or explain back any subject (e.g. "我想学 X", "继续学 X", "考我 X", "用费曼法讲 X", "做个学习计划"), or asks what they have studied.
---

# Study Anything

一个可记录、可迭代、可进化的学习系统。所有学习数据都存在本 skill 目录（下称 `$SKILL`，即本文件所在目录）的 `topics/` 中，并用 git 管理。

## 启动：每次触发都先做

1. 读 `$SKILL/topics/INDEX.md` 和 `$SKILL/topics/_learner.md`。
2. 按名称、别名、tag 匹配用户说的主题：
   - **已存在**：读该主题的 `profile.md`、`weak-points.md`、`plan.md`，以及 `log.md` 最后 3 条。用一两句话告诉用户当前进度（等级、计划进度、未解决薄弱点数），再进入对应模式。
   - **不存在**：进入"新建主题"。
   - **匹配到多个**：列出候选让用户选。
3. 判断模式（用户没说清就按"下一步建议"推荐一个，并等确认）：

| 用户意图 | 模式 | 读取 |
|---|---|---|
| 学一个新东西 / 做计划 | 新建主题 | [workflows/plan.md](workflows/plan.md) |
| 找资料、推荐资源 | 资源筛选 | [workflows/resources.md](workflows/resources.md) |
| 继续学、学下一次 | 学习 | [workflows/session.md](workflows/session.md) |
| 考我、测一下 | 考官 | [workflows/exam.md](workflows/exam.md) |
| 我来讲一遍、费曼 | 费曼 | [workflows/feynman.md](workflows/feynman.md) |
| 计划不合适、复盘、调整 | 复盘 | [workflows/review.md](workflows/review.md) |
| 我学过什么 / 某类有哪些 | 查询 | 只读 `INDEX.md` 回答 |

## 推荐的学习链路

```
新建主题（阶梯 → 20% → 计划）→ 资源筛选 → 学习 → 考官
                                           ↑        ↓ 有讲不清的点
                                      复盘调整 ← 费曼
```

- 每次"学习"结束后默认进入"考官"。
- 考官中得分 ≤ 6 的知识点，建议转"费曼"。
- 每完成 3 次学习、或准备升级到下一等级时，进入"复盘"。

## 交互原则

- 默认中文。一次只做一件事：只问一个问题、只讲一个知识点，然后停下等用户。
- 不要一口气输出整份长文。计划、阶梯这类结构化内容先给摘要，确认后再写入文件。
- 解释优先用例子和类比，避免"听起来高级但没说明白"的词；必须用术语时当场解释。
- 遵循 `_learner.md` 和主题 `profile.md` 里记录的偏好。

## 记录规则（必须执行）

每个模式结束时，按顺序完成，不得省略：

1. 时间一律用 `date "+%Y-%m-%d %H:%M"` 获取，不要凭感觉写。
2. 往该主题 `log.md` **末尾追加**一条记录（格式见 [templates/log.md](templates/log.md)），历史记录不改。
3. 新发现的薄弱点写入 `weak-points.md`，已有的更新状态（规则见 [workflows/exam.md](workflows/exam.md)）。
4. 改动了 `profile.md`、`ladder.md`、`plan.md`、`resources.md` 中任何内容，在 `changelog.md` 追加：改了什么、为什么。
5. 更新 `INDEX.md` 中该主题的一行（等级、进度、最近学习日期）。
6. 发现跨主题适用的学习规律（如"先看例子再讲概念更有效"），写入 `_learner.md`。
7. 提交：`git -C "$SKILL" add -A && git -C "$SKILL" commit -m "study(<slug>): <模式> <一句话摘要>"`。只在本地提交，不要 push。

## 主题目录约定

- 目录名 `slug`：小写英文加连字符，如 `playwright`、`rust-async`、`photography-basics`。
- 新建主题时复制 `$SKILL/templates/` 下全部文件到 `$SKILL/topics/<slug>/`，再填写内容。

```
topics/<slug>/
├── profile.md      # 学习规范：目标、基础、约束、偏好、有效方法、当前等级
├── ladder.md       # 5 级学习阶梯
├── plan.md         # N 次学习计划及完成状态
├── resources.md    # 资源清单与 7 天路径
├── log.md          # 学习流水，只追加
├── weak-points.md  # 薄弱点及状态
└── changelog.md    # 规范/计划的修订记录
```

## 索引 INDEX.md

每个主题一行，新建主题时添加：

```
| 主题 | slug | 分类 | tags | 当前等级 | 计划进度 | 未解决薄弱点 | 最近学习 |
| Playwright | playwright | 编程 | e2e, testing, browser-automation | L1 | 2/10 | 3 | 2026-10-19 |
```

- 分类用大类（编程、语言、设计、商业、学科、技能、兴趣……），优先复用已有分类。
- tags 3–6 个，小写英文，优先复用已有 tag，便于"测试相关的有哪些"这类查询。
