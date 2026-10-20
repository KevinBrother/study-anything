# Playwright 学习流水

<!--
只在末尾追加，不修改历史。每条格式：

## YYYY-MM-DD HH:MM｜<模式：新建/资源/学习/考官/费曼/复盘>｜<计划第几次，可选>

- 时长：<学习模式必填，按开始/结束时间计算；其他模式可留空>
- 内容：
- 产出：<文件路径或链接，可选>
- 得分：<考官模式：各题分数与平均分>
- 薄弱点：<新增 Wxxx / 改善 Wxxx>
- 备注：<用户原话复述、节奏信号等>
-->

## 2026-10-20 15:54｜新建

- 内容：确认目标（AI 开发后的产品测试，CI 质量门禁）、基础（React/TS 前端，项目已有 e2e）、偏好（官方文档 + 项目动手）；生成 5 级阶梯（起始 L2）、重点 20%（11 条）、12 次学习计划
- 产出：topics/playwright/（profile / ladder / plan / resources / weak-points / changelog）
- 备注：用户要求两周学完（约 2026-11-02），每周 3-4 次甚至更多（实际需约 6 次/周）；组件测试、视觉回归、移动模拟按用户要求纳入（计划由 10 次扩为 12 次）；多语言/时区矩阵不学（产品纯中文后台）

## 2026-10-20 16:20｜资源

- 内容：联网验证并筛选 5 组资源（官方文档核心篇/工程篇/调试与CI篇/组件测试/源码 packages/injected/src），填充 plan.md 全部 12 次的资源栏，排定首周路径（第 1-6 次）
- 产出：topics/playwright/resources.md
- 备注：两个重要发现——① CT 的 @playwright/experimental-ct-* 已移除，新方案为 story gallery + fixtures.mount()；② 注入脚本源码已从 playwright-core 移到 packages/injected/src。第 9 次 projects/devices 配置和第 12 次审校清单由 AI 陪练讲解
