# Playwright 学习资源

## 精选资源

### 1. Playwright 官方文档·核心篇

- 链接：https://playwright.dev/docs/intro 、 /docs/writing-tests 、 /docs/codegen 、 /docs/locators 、 /docs/assertions 、 /docs/actionability（intro、locators、actionability 已读内容；其余可访问）
- 适合谁 / 难度：入门，零基础到 L2
- 怎么用：第 1 次读 intro + writing-tests + codegen；第 2 次 locators；第 3 次 assertions + actionability
- 可以跳过：intro 的安装部分（项目已配好环境）
- 状态：在用

### 2. Playwright 官方文档·工程篇

- 链接：https://playwright.dev/docs/network 、 /docs/mock 、 /docs/auth 、 /docs/test-fixtures 、 /docs/test-snapshots（auth、test-snapshots 已读内容；其余可访问）
- 适合谁 / 难度：入门→进阶，L2 到 L3
- 怎么用：第 4 次 test-snapshots；第 5 次 network + mock（配合项目 e2e/mocks/model-api.ts 精读）；第 6 次 auth（先只做基础方案）；第 7 次 test-fixtures
- 可以跳过：auth 的"高级场景"里 session storage 部分（掌握基础方案后再回看）
- 状态：在用

### 3. Playwright 官方文档·调试与 CI 篇

- 链接：https://playwright.dev/docs/trace-viewer 、 /docs/ci（均已读内容）
- 适合谁 / 难度：进阶，L4
- 怎么用：第 8 次 trace-viewer（重点 Actions/Snapshots/Log/Network 标签）；第 9 次 ci 的 GitLab 章节（含 `--shard=$CI_NODE_INDEX/$CI_NODE_TOTAL` 并行示例）
- 可以跳过：ci 页中 GitHub Actions、Docker 之外其他平台的示例
- 状态：在用

### 4. Playwright 官方文档·组件测试（新版）

- 链接：https://playwright.dev/docs/test-components（已读内容）
- 适合谁 / 难度：进阶，L5
- 怎么用：第 11 次。⚠️ 这是新方案：`@playwright/experimental-ct-*` 已被移除，改为 dev server 提供 story gallery + `fixtures.mount()`；网上大部分 CT 教程是旧版，一律以这版为准
- 可以跳过：从旧实验包迁移的章节（新项目用不到）
- 状态：在用

### 5. playwright 源码 packages/injected/src

- 链接：https://github.com/microsoft/playwright/tree/main/packages/injected/src（已读内容）
- 适合谁 / 难度：深入，L5
- 怎么用：第 10 次精读 selectorEngine.ts、roleSelectorEngine.ts、injectedScript.ts、utilityScript.ts；README 一句话说明该目录是"helper sources which are injected into the page"。注意：注入脚本已从 playwright-core 移到独立的 packages/injected
- 可以跳过：recorder、webview 子目录、webAuthn、coverageScript 等与主线无关的文件
- 状态：在用

## 补充说明

- 第 9 次的 projects/devices 多环境配置、第 12 次的 AI 审校清单：官方文档无对应独立章节，由 AI 陪练讲解
- 第 12 次总复习可翻 https://playwright.dev/docs/best-practices（可访问）

## 首周路径

| 序号 | 对应计划 | 资源与章节 | 练习 | 预计用时 |
|---|---|---|---|---|
| 1 | 第 1 次 | 官方 intro（跳过安装）+ writing-tests + codegen | 跑通现有 e2e、读懂 config、codegen 录制、三种模式对比 | 2 小时 |
| 2 | 第 2 次 | /docs/locators | 技能模型列表页 3 个定位测试 + filter 练习 | 2 小时 |
| 3 | 第 3 次 | /docs/assertions + /docs/actionability | 改写等待测试、制造并解读 3 种 actionability 报错 | 2 小时 |
| 4 | 第 4 次 | /docs/test-snapshots | 页面快照测试 + --update-snapshots 流程 + 容差配置 | 2 小时 |
| 5 | 第 5 次 | /docs/network + /docs/mock + 项目 model-api.ts 精读 | 扩展一个接口报错场景测试 | 2 小时 |
| 6 | 第 6 次 | /docs/auth（基础方案） | setup 项目登录 + storageState 复用 | 2 小时 |
