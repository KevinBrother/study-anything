# Playwright 学习阶梯

## L1 完全新手

- 需要掌握：
  - 安装 @playwright/test 并下载浏览器（npx playwright install）
  - 读懂 playwright.config.ts 的基本项（testDir、projects、use）
  - 写一个最小 test + expect 结构并运行（headed/headless）
- 常见错误：
  - 忘记 npx playwright install 导致"浏览器未安装"报错
  - 用 node 而不是 npx playwright test 运行测试
  - 改了 config 不重启 watch 模式
- 练习：
  - 在 console-ui-react 跑通现有 e2e 测试
- 通关标准：能独立跑通项目现有 e2e 并说清一个测试从启动到结束经历了什么
- （用户已越过此级：仓库已有 quality gate 并跑通过）

## L2 入门：定位与断言

- 需要掌握：
  - 熟练使用 getByRole / getByText / getByTestId 及链式 filter、nth
  - 理解"定位器优先级"：role > text > testid > css/xpath
  - web-first 断言（expect(locator).toBeVisible 等）与普通断言的区别
  - 理解 auto-waiting 的 actionability 状态机（可见/稳定/可接收事件/滚动/执行）
- 常见错误：
  - 硬编码 css/xpath 定位，UI 一改就挂
  - 用 page.waitForTimeout 代替自动等待
  - 在断言外抓取文本（await textContent）导致时序问题
  - 用 nth(0) 掩盖定位不精确
- 练习：
  - 为技能模型列表页手写 3 个定位测试
  - 故意制造 "element is not stable / intercepted" 报错并解读
- 通关标准：不看文档为任意页面写出稳定定位；能解释一条 actionability 报错的含义

## L3 熟练：工程化

- 需要掌握：
  - page.route() 拦截与网络 mock（含失败场景模拟）
  - storageState 保存与复用登录态
  - 自定义 fixture、beforeEach、tags 分组组织测试
  - 视觉回归：toHaveScreenshot、baseline 更新流程、容差配置
- 常见错误：
  - 每个测试都重新登录，拖慢整个套件
  - mock 拦截过宽（**/*）导致测试互相干扰
  - 视觉回归不锁字号/主题，CI 上因渲染差异误报
  - 在 fixture 里做本该属于测试的操作
- 练习：
  - 扩展 model-api.ts 新增失败场景
  - 搭登录态复用 fixture
  - 为一个页面加截图快照测试
- 通关标准：为项目搭好一套可复用的 e2e 基建（mock + 登录态 + fixture + 快照）

## L4 进阶：排查与 CI

- 需要掌握：
  - Trace Viewer：开启、回放、从 trace 定位失败根因
  - flaky 测试的常见根因与根治手段
  - GitLab CI：并行 workers、shard、retry、HTML reporter
  - projects 配置多浏览器 + 移动设备模拟（devices）
- 常见错误：
  - 用 retry 掩盖 flaky 而不查根因
  - CI 与本地环境差异（字体、视口、CPU 慢）导致的快照/超时问题
  - 并行测试共享状态（同一账号、同一条数据）互相污染
- 练习：
  - 用 trace 排查一个真实失败测试并写排障笔记
  - 优化 quality gate 配置（多浏览器 + 移动模拟 + 并行 + 报告）
- 通关标准：独立排查 CI 失败并根治至少一个 flaky；quality gate 在 CI 稳定通过

## L5 能独立做项目：原理与 AI 协作

- 需要掌握：
  - 三层架构：client（JSON-RPC）→ driver → 各浏览器协议（CDP/patched Firefox/WebKit）
  - 注入脚本的职责：内置选择器引擎、actionability 判定、DOM 快照
  - 组件测试（CT）：mount 机制、与 E2E 的边界
  - AI 测试工作流：AI 生成测试的审校要点、trace 喂给 AI 排查失败
- 常见错误：
  - 把 CT 当 E2E 用（或反之），测试层级混乱
  - 盲信 AI 生成的测试，不审定位器健壮性和断言充分性
  - 原理只背名词，解释不了实际报错
- 练习：
  - 读 playwright-core injected 源码并写原理笔记
  - 为一个 React 组件写 CT 测试
  - 用 AI 为新页面生成测试并人工审校入库
- 通关标准：能完整讲清 auto-waiting 全过程（含注入脚本的角色）；落地一条 AI 生成→审校→入库的测试工作流
