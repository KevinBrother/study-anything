# Playwright 修订记录

<!--
每次修改 profile / ladder / plan / resources 时追加：

## YYYY-MM-DD HH:MM

- 文件：
- 改动：
- 依据：<log 日期 / 薄弱点编号 / 用户要求>
-->

## 2026-10-20 15:54

- 文件：profile.md、ladder.md、plan.md、resources.md
- 改动：创建主题，初版学习规范、阶梯（起始 L2）、12 次计划
- 依据：用户要求。初始方案为 10 次，用户反馈组件测试、视觉回归、移动模拟都需要学（仅多语言矩阵可跳过），扩为 12 次；总时长 10→12 次经用户确认

## 2026-10-20 16:20

- 文件：resources.md、plan.md
- 改动：填充计划资源（官方文档 5 组资源，全部联网验证）；修正第 10 次源码路径（injected 已从 playwright-core 移到 packages/injected）；第 11 次更新为新版 CT 方案（experimental-ct 已移除，改为 story gallery + mount fixture）
- 依据：资源筛选模式，2026-10-20 联网验证结果
