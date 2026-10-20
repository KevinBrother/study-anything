# Playwright 学习规范

- slug：playwright
- 分类：编程
- tags：playwright, e2e, testing, browser-automation, react
- 别名：playwright 测试、E2E 测试、端到端测试
- 创建日期：2026-10-20

## 目标

- 为什么学：AI 开发后的产品测试——为 console-ui-react 写/维护 Playwright E2E 测试，作为 CI 质量门禁；同时理解内部原理，便于排查 flaky 和审校 AI 生成的测试
- 成功标准（可检验）：
  1. 能独立为任意页面写出稳定（无 sleep、不 flaky）的 E2E 测试
  2. 搭好可复用的 e2e 基建（登录态复用、mock、fixture）
  3. CI 上的 quality gate 配置经过优化（并行、retry、报告）并能独立排障
  4. 能讲清三层架构与 auto-waiting 的完整过程
  5. 落地一条 AI 生成测试 → 人工审校 → 入库的工作流
- 截止日期：两周内学完，约 2026-11-02

## 基础

- 已有相关经验：前端开发，React/TS 熟练；console-ui-react 仓库已有 e2e 目录、网络 mock（e2e/mocks/model-api.ts）和 Playwright quality gate；对 Playwright 内部原理感兴趣（主动问过架构）
- 起始等级：L2

## 约束与预算

- 频率：每周约 6 次（用户原话"每周三到四次甚至更多"，为两周学完 12 次需约 6 次/周）
- 总时长：12 次 × 2 小时（已确认；原提议 10 次，因用户要求纳入组件测试/视觉回归/移动模拟扩为 12 次）
- 学习环境/版本：console-ui-react 项目（React + TS，GitLab CI）；Playwright 版本以项目 package.json 为准（待学习时确认）

## 前提与风险

- console-ui-react 可本地运行（已确认，日常开发中）
- CI 的 GitLab runner 能跑浏览器（已确认——quality gate 已提交并验证过）
- 项目 e2e 现有代码可作为学习素材（已确认）
- 风险：两周节奏较密，如进度落后优先保证第 1-8 次核心内容，第 9-12 次可顺延

## 偏好

- 学习方式：官方文档为主 + 边学边在本项目 e2e 动手，视频作为补充（用户确认）
- 讲解方式：中文；例子和类比优先；术语当场解释；结合项目真实代码

## 有效方法

<!-- 复盘和费曼中验证有效的方法，格式：- YYYY-MM-DD：方法（依据） -->

## 当前等级

- L2（2026-10-20）
