---
theme: seriph
download: true
---

# 前端工程化

<br>

吴睿

[Repo](https://github.com/modyqyw/frontend-engineering)

Powered by [Slidev](https://sli.dev/)

<!--

是什么

为什么

怎么做
-->

---

# 目录

- 什么是前端工程化
- 选型
- 规范
- 测试
- 部署
- 优化
- 参考

---

# 什么是前端工程化

<br>

提升前端效率的工作，都可以认为是前端工程化。

<!--

为什么需要前端工程化？

不如反问，为什么不需要前端工程化？提升效率谁不想要呢？

-->

---

# 选型

- 为什么要做选型：统一技术栈和工具链
- 选型原则：
  - 稳定：不会经常有破坏性更新，向后兼容度高，更新/迁移成本低
  - 易用：使用相对简单，更有可能统一技术栈，更方便不同团队间人员流动
  - 生态：需要考虑支持国内外生态，如小程序端、支付和分享场景等
- 暂时不考虑魔改等情况（一般也不会出现需要魔改的情况）

<br>

<v-clicks>

- Angular：对小程序支持不佳
- React：心智负担较重，易用性不佳，见 [class example](https://codesandbox.io/s/elated-snow-8z7iu) 和 [function example](https://codesandbox.io/s/w2wxl3yo0l)
- Solid、Fre 等：生态不成熟
- Vue：各方面相对不错

</v-clicks>

<br>

<div v-click class="text-xl">

Vue + uni-app：vue-cli 完整工具链，大问题没有，小问题可能会遇上

不要在中大型项目里使用 Vite，其生态仍需要发展

</div>

<!--

关于 React 的心智负担问题：

1. 原本 class 组件也就是类组件相对完整，function 组件也就是函数组件有相当多限制。引入 hooks 之后，函数组件开始趋向完整，虽然仍然有一些缺失，但已经是社区里的大趋势了。
2. 函数组件的思维方式和类组件的思维方式完全不同，文档却依然以类组件为主来做解释，这就导致了很多人可能会在使用函数组件时踩坑。所以说心智负担较重。
3. 演示 class 和 function component 的例子。

当然，我仍然鼓励大家去学习 React 的思想，毕竟 Vue 也有很多地方是受了 React 的启发。

关于 Vue 的好处：

1. Vue + uni-app 的组合支持桌面端网页（使用 Vue）、桌面端应用（使用 vue-cli-plugin-electron）、移动端网页（使用 Vue）、移动端应用（使用 uni-app）、小程序（使用 uni-app）
2. 从原生到 Vue 是渐进式的，对比 React 和 Angular，中文文档非常完整且有指导思想，学习曲线不陡峭，不用接受过多的新概念

Vue 相对不错，主要问题出在 uni-app 上，uni-app 的表现并不是特别稳定。

1. uni-app 的文档看起来很完整，但往往在某些细节上阐述不清，又或是底层上实现有问题，导致开发稍微复杂一点的应用的过程中必定会遇到一些问题，目前只建议用 uni-app 开发小程序和移动端应用。
2. 同时，开发团队也没有完全把心思放在 uni-app 上，试图打造一整个的生态，但是不知道是不是人手问题，所有相关的产品都或多或少有些坑。

综合来看，这依然是目前较为适合的技术栈，我们可以用 20% 的时间处理 80% 的问题，剩余的 20% 问题就需要我们花 80% 时间去攻坚了。

-->

---

# 规范

- 帮助开发者编写相对良好的代码，提高可读性、可维护性，也能帮助代码审查 Code Review
- 统一代码风格、代码样式、组件库、工具库等，保证团队一致性，降低沟通成本，方便不同团队间人员流动

---

# 规范

- 帮助开发者编写相对良好的代码，提高可读性、可维护性，也能帮助代码审查 Code Review
- 统一代码风格、代码样式、组件库、工具库等，保证团队一致性，降低沟通成本，方便不同团队间人员流动

<br>

```ts
function add(a, b) {
  return a + b;
}

function subtract(a, b) {
  return a - b;
}

function multiple(a, b) {
  return a * b;
}

function divide(a, b) {
  return a / b;
}
```

```ts
function AdD(a ,b ){
   return a+ b
}

function SubTracT(a ,  b ){
  return a - b;
}

function mUltIple(a  ,b ){
  return a *b
}

function diVide(a,   b ){
  return a  / b;
}
```

<style>
.slidev-code {
  display: inline-block;
  width: 50%;
}
</style>

---

# 规范

- Linter
  - 检查（并修复）潜在错误的工具
  - ESLint：JavaScript / TypeScript
  - Stylelint：CSS / LESS / SCSS
  - Husky + LintStaged + Commitlint：Git 提交
- Formatter：检查（并修复）格式问题的工具
  - 目前最流行的是 Prettier，支持多种语言
  - 可以和 ESLint，Stylelint 等结合使用
- Linter 和 Formatter 就能处理所有规范问题吗？
  - 命名问题
  - 换行问题
  - 本地问题

<div v-click class="text-xl">

一个边探索边更新的解决方案 [@modyqyw/fabric](https://github.com/modyqyw/fabric)

</div>

<!--

命名问题：变量命名、文件命名、目录命名、项目命名

换行问题：使用 Windows 系统默认的换行可能会造成影响，一般要求使用 Unix 系统默认的换行保证跨平台可用

本地问题：是不是配置正确了来确保提交的代码没有问题

-->

---

# 测试

- 当构建可靠的应用时，测试在个人或团队构建新特性、重构代码、修复 bug 等工作中扮演了关键角色
- 在 web 应用领域内主要有三大类
  - 单元测试：Jest、Mocha
  - 组件测试：Testing Library
  - 端到端测试：Cypress

<!--

在这里我不打算展开讲述，因为司内项目一般没有预留时间给开发写测试代码，但是在做组件库、工具库之类的时候，测试往往是必不可少的，感兴趣的可以去自己学习一下

-->

---

# 部署

|Git Flow|Github Flow|Gitlab Flow|
|:-:|:-:|:-:|
|<img src="/git-flow.png" title="Git Flow" alt="Git Flow">|<img src="/github-flow.png" title="Github Flow" alt="Github Flow">|<img src="/gitlab-flow.png" title="Gitlab Flow" alt="Gitlab Flow">|

<!--

在正式讲部署前，先来讲讲分支模型

或多或少有一些变种，比如使用 dev-[人名] 或 dev-[功能] 做开发分支等，但总体基本都是三个 Flow 之一。

-->

---

# 部署

- 传统部署：手动完成所有操作，包括提交、推送、构建、重启服务等

<v-clicks>

- 能不能减少人的参与，增加机器的参与，降低人为因素造成的问题？

</v-clicks>

---

# 部署

- [都城二期后台管理](https://work.iscnu.net/SystemDevelopment/Duchenggo/_git/desktop-web)（vue）：release-it + 脚本
- main 分支开发 -> 提交 -> 调用 release-it 更新版本 -> shell 脚本部署到测试服务器/正式服务器

<br>

- [developer-examination](https://github.com/MillCloud/developer-examination)（vite + react）：release-it + github actions + github pages，少量手动操作
- main 分支开发 -> 提交 -> 调用 release-it 更新版本 -> 同步 main 分支到 release 分支 -> 触发 github actions 自动构建并部署

<br>

- [next-mine-sweeper-demo](https://github.com/ModyQyW/next-mine-sweeper-demo)（next）：release-it + vercel，少量手动操作
- main 分支开发 -> 提交 -> 调用 release-it 更新版本 -> 同步 main 分支到 release 分支 -> 触发 vercel 自动构建并部署

<div v-click class="text-xl">

自动化/半自动化套路：

使用 release-it 处理版本

使用脚本 / 服务（vercel / netlify / azure devops pipelines / ...）构建并部署

</div>

<!--

部署演示

-->

---

# 部署

<br>

半自动化/自动化部署还会涉及到敏捷开发、持续集成、持续交付和持续部署等概念

|敏捷开发|持续集成|
|:-:|:-:|
|![敏捷开发](/agile-development.jpg)|![持续集成](/continuous-integration.png)|

<!--

概念拓展：敏捷开发，持续集成 Continuous Integration，持续交付 Continuous Delivery 和持续部署 Continuous Deployment

敏捷开发 = 迭代开发 + 增量开发。迭代开发将一个大任务，分解成多次连续的开发，本质就是逐步改进，每次迭代都是一个完整的软件开发周期，必须按照软件工程的方法论，进行正规的流程管理。增量开发，指的是软件的每个版本，都会新增一个用户可以感知的完整功能，可用于划分迭代。

持续集成：频繁地将代码集成到主分支，一般一天多次，让产品可以快速高质迭代

持续交付：频繁地将软件的新版本，交付给质量团队或者用户，以供评审

持续部署：即持续交付的下一步，指的是代码通过评审以后，自动部署到生产环境

-->

---

# 优化

- 借助工具来帮助优化
- 代码优化
  - 规范
  - 分析：lighthouse
  - 监控：sentry
  - 重构：《重构：改善既有代码的设计》
- 项目优化
  - 完善文档：markdown，是什么、为什么、怎么做、谁负责、谁来做、做多久
  - 微前端：qiankun，微前端有必要吗
  - 全栈：MERN、MEVN 的可能性
  - Serverless：Amazon Web Service、Google Cloud、阿里云、腾讯云，我们是不是真的需要全套云服务

<div v-click class="text-xl">

数据结构和算法、设计模式、架构

</div>

<!--

在这里我不打算对所有都展开讲述，因为每一个要讲都很复杂，这里就大概讲讲重构和文档

-->

---

# 参考

- [带你入门前端工程](https://woai3c.gitee.io/introduction-to-front-end-engineering/)
- [敏捷开发入门教程](https://www.ruanyifeng.com/blog/2019/03/agile-development.html)
- [持续集成是什么](https://www.ruanyifeng.com/blog/2015/09/continuous-integration.html)
- [useEffect 完整指南](https://overreacted.io/zh-hans/a-complete-guide-to-useeffect/)
