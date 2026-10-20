# Playwright 学习计划

## 重点 20%

1. Locators（getByRole 优先，链式 filter）— 决定测试可维护性，也是对 AI 最友好的写法
2. Auto-waiting + web-first 断言（actionability 状态机）— 免 sleep、测试稳定的根基
3. page.route() 网络 mock — 隔离后端测前端行为，AI 产品测试的核心手段
4. storageState 登录复用 — 测试工程第一道坎
5. Trace Viewer 失败排查 — AI 写的测试挂了以后的第一手资料
6. CI 集成（GitLab 并行/retry/reporter）— 质量门禁最后一公里
7. 三层架构与注入脚本原理 — 报错和 flaky 的根本解释
8. fixtures 测试组织 — 项目级复用
9. 视觉回归（toHaveScreenshot）— 防 AI 改坏 UI 的性价比最高的手段
10. 移动设备模拟（devices/viewport）— 响应式产品必备
11. 组件测试（Playwright CT）— 不起整页浏览器、直接挂载 React 组件测

## 暂不学

- 多语言/时区矩阵（locale × timezoneId 组合跑测试）— 产品纯中文后台，无国际化版本；出海时再加回

## 计划

### [ ] 第 1 次（L2，2 小时）

- 新核心概念：测试生命周期（config 加载 → worker 启动 → test → expect → teardown）
- 学习目标：说清一个测试从启动到结束经历了什么；会用 codegen 录制
- 练习任务：
  1. 跑通现有 e2e，逐项读懂 playwright.config（约 30 分钟）
  2. 用 codegen 录制一个页面操作，保存为测试文件（约 30 分钟）
  3. 分别用 headed / --debug / --ui 模式跑同一个测试，观察差异（约 15 分钟）
- 资源：待资源筛选
- 复盘问题：
  1. playwright.config 里 projects、testDir、use 各控制什么？
  2. 一个 test 文件从被加载到执行完经历哪几个阶段？
  3. codegen 生成的代码哪些该保留、哪些必须改写，为什么？
- 完成日期：

### [ ] 第 2 次（L2，2 小时）

- 新核心概念：定位器体系（role 优先 + 链式过滤）
- 学习目标：不看文档为任意页面写出稳定定位
- 练习任务：
  1. 官方 Locators 文档 + 在技能模型列表页实践 role 定位（约 30 分钟）
  2. 手写 3 个核心页面的定位测试（不用 codegen）（约 40 分钟）
  3. 用 filter / and / or 处理重复元素场景（约 10 分钟）
- 资源：待资源筛选
- 复盘问题：
  1. 为什么 getByRole 优先于 css/xpath？各自的失效场景是什么？
  2. filter 和 nth 分别什么场景用？nth(0) 有什么风险？
  3. 定位器报"strict mode violation"意味着什么，怎么修？
- 完成日期：

### [ ] 第 3 次（L2，2 小时）

- 新核心概念：auto-waiting 与 web-first 断言（actionability 状态机）
- 学习目标：解释任意一条 actionability 报错；把等待类测试改写为自动等待
- 练习任务：
  1. 官方 auto-waiting + assertions 文档（约 25 分钟）
  2. 把项目里一个含显式等待的测试改写为 web-first 断言（约 20 分钟）
  3. 故意制造 unstable / intercepted / not visible 三种报错并逐一解读（约 35 分钟）
- 资源：待资源筛选
- 复盘问题：
  1. click 前的 actionability 检查有哪几步？每步对应什么报错？
  2. expect(locator).toBeVisible() 和 expect(await locator.isVisible()) 的本质区别？
  3. "element is not stable" 在什么场景出现，怎么根治？
- 完成日期：

### [ ] 第 4 次（L3，2 小时）

- 新核心概念：视觉回归（toHaveScreenshot + baseline 管理）
- 学习目标：为一个页面建立截图快照测试并掌握 baseline 更新流程
- 练习任务：
  1. 官方 visual comparisons 文档 + 为一个页面加 toHaveScreenshot（约 40 分钟）
  2. 改动 UI 体验 --update-snapshots 的更新流程与 git 冲突处理（约 20 分钟）
  3. 配置 maxDiffPixelRatio / maxDiffPixels 容差（约 15 分钟）
- 资源：待资源筛选
- 复盘问题：
  1. 什么该用视觉回归、什么该用 DOM 断言？各自盲区是什么？
  2. baseline 放哪、多人协作时更新冲突怎么处理？
  3. CI 和本地渲染差异（字体、抗锯齿）导致快照误报怎么处理？
- 完成日期：

### [ ] 第 5 次（L3，2 小时）

- 新核心概念：网络拦截与 mock（page.route）
- 学习目标：能 mock 任意接口的正常/失败响应并让测试只依赖前端行为
- 练习任务：
  1. 精读 e2e/mocks/model-api.ts 现有实现（约 20 分钟）
  2. 官方 network 文档 + route 拦截练习（约 30 分钟）
  3. 新增一个接口报错（500/超时）场景的测试（约 30 分钟）
- 资源：待资源筛选
- 复盘问题：
  1. route 的 glob 匹配规则是什么？拦截过宽有什么风险？
  2. mock 数据写死会导致什么脆弱性？怎么组织 mock 数据？
  3. fulfill 和 continue/abort 各适用什么场景？
- 完成日期：

### [ ] 第 6 次（L3，2 小时）

- 新核心概念：认证与登录态复用（storageState）
- 学习目标：搭一次登录、全套测试复用的机制
- 练习任务：
  1. 官方 authentication 文档（约 20 分钟）
  2. 写一个 setup 项目执行登录并保存 storageState（约 45 分钟）
  3. 让现有测试改为复用 storageState 跑通（约 15 分钟）
- 资源：待资源筛选
- 复盘问题：
  1. storageState 里存了什么？什么时候会失效？
  2. setup 项目（dependencies）和普通测试项目的执行顺序是怎么保证的？
  3. 什么情况下必须退回"每个测试自己登录"？
- 完成日期：

### [ ] 第 7 次（L3，2 小时）

- 新核心概念：fixtures 与测试组织
- 学习目标：把公共 setup 重构为可复用的自定义 fixture
- 练习任务：
  1. 官方 test fixtures 文档（约 25 分钟）
  2. 将项目公共 setup（登录态/mock 加载等）重构为自定义 fixture（约 40 分钟）
  3. 用 tags / test.describe 分组，练习 --grep 过滤运行（约 15 分钟）
- 资源：待资源筛选
- 复盘问题：
  1. fixture 和 beforeEach 的区别？各自的适用场景？
  2. test fixture 和 worker fixture 的生命周期差异是什么？
  3. e2e 目录结构怎么组织才便于维护？
- 完成日期：

### [ ] 第 8 次（L4，2 小时）

- 新核心概念：Trace 与失败排查
- 学习目标：用 trace 独立定位一个真实失败测试的根因
- 练习任务：
  1. 开 trace 跑测试，用 show-trace 完整回放一遍（约 25 分钟）
  2. 排查项目里一个真实（或人为制造）的失败测试（约 40 分钟）
  3. 写一篇排障笔记：报错 → trace 证据 → 根因 → 修复（约 15 分钟）
- 资源：待资源筛选
- 复盘问题：
  1. trace.zip 里包含哪几类信息？分别用来回答什么问题？
  2. --debug 模式和 trace 各自适合什么排查场景？
  3. flaky 的常见根因有哪几类？各类怎么根治？
- 完成日期：

### [ ] 第 9 次（L4，2 小时）

- 新核心概念：CI 集成与 projects 多环境配置
- 学习目标：quality gate 支持多浏览器 + 移动模拟，并配好并行/报告
- 练习任务：
  1. 精读现有 GitLab quality gate 配置（约 20 分钟）
  2. 配 projects：多浏览器 + devices 移动模拟（约 40 分钟）
  3. 配 workers 并行、retries、HTML reporter（约 20 分钟）
- 资源：待资源筛选
- 复盘问题：
  1. workers 并行时测试之间靠什么隔离？哪些共享状态会出问题？
  2. retries 设置过高会掩盖什么问题？
  3. shard 是怎么把测试分到多个 runner 的？
- 完成日期：

### [ ] 第 10 次（L5，2 小时）

- 新核心概念：三层架构与注入脚本
- 学习目标：能完整讲清一条 click 指令从测试代码到浏览器的全过程
- 练习任务：
  1. 官方架构说明 + 源码目录结构阅读（约 35 分钟）
  2. 读 playwright-core 的 injected 目录（selector 引擎 / actionability）（约 30 分钟）
  3. 写原理笔记：一条指令的完整旅程（约 15 分钟）
- 资源：待资源筛选
- 复盘问题：
  1. client、driver、浏览器三层各自负责什么？靠什么协议通信？
  2. 注入脚本注入到哪里、负责哪几件事？
  3. 为什么 Playwright 必须用它自己下载的浏览器？
- 完成日期：

### [ ] 第 11 次（L5，2 小时）

- 新核心概念：组件测试（Playwright CT）
- 学习目标：为一个 React 组件写 CT 测试并明确 CT/E2E 边界
- 练习任务：
  1. 官方 component testing 文档 + 项目 CT 配置（约 40 分钟）
  2. 为一个核心 React 组件写 CT 测试（含交互与断言）（约 40 分钟）
- 资源：待资源筛选
- 复盘问题：
  1. CT 的 mount 和 E2E 打开页面有什么本质区别？
  2. 什么该用 CT 测、什么必须用 E2E 测？边界在哪？
  3. CT 测试里怎么 mock 掉组件的依赖（接口/子组件）？
- 完成日期：

### [ ] 第 12 次（L5，2 小时）

- 新核心概念：AI × 测试工作流（生成 → 审校 → 入库）
- 学习目标：落地一条 AI 生成测试的人工审校流程
- 练习任务：
  1. 用 AI 为一个新页面生成 E2E 测试，人工审校后入库（约 60 分钟）
  2. 总结一页"AI 生成测试审校清单"（定位器健壮性/断言充分性/mock 合理性）（约 20 分钟）
- 资源：待资源筛选
- 复盘问题：
  1. AI 生成的测试典型坏味道有哪几类？
  2. trace 怎么喂给 AI 才能高效定位失败原因？
  3. 回顾 12 次：哪三个概念收益最大？
- 完成日期：
