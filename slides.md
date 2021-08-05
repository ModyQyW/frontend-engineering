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

大家好。这次的分享会主要想跟大家分享一下我在前端工程化这一方面的理解。这是我在都城项目组里面业务之外的发力点，也算是有自己的一点见解吧。

-->

---

# 目录

- 选型
- 规范
- 测试
- 部署
- 文档
- 参考

<!--

整个分享会会涉及下面五个部分：选型，规范，测试，部署和文档。

-->

---

# 什么是前端工程化

<br>

提升前端效率的工作，都可以认为是前端工程化。

<!--

但在正式讲述前，我们需要首先明确一个问题，那就是什么才是前端工程化。

前端工程化不是什么高大上的概念，只要提升了前端开发效率，都可以认为做了前端工程化。

前面提到的五个部分，都在某些方面提升了前端开发效率，下面就来一一讲述。

-->

---

# 选型

- 现状：混乱
  - 框架/库用到了 [Taro](https://docs.taro.zone/)、[Expo](https://expo.io/)、[Vue](https://cn.vuejs.org/)、[UniApp](https://uniapp.dcloud.io/)、[WePY](https://wepyjs.gitee.io/wepy-docs/)、[MpVue](http://mpvue.com/)、[AngularJS](https://www.angularjs.net.cn/) 等
  - 项目配置（如路由、状态管理、工具类库等）没有规律
    - 每次加入项目开发都需要额外花时间去梳理，带来隐性的时间成本，不利于前端在不同项目间流动
  - 底层工具链用到了 [Metro](https://facebook.github.io/metro/)、[Webpack](https://webpack.docschina.org/)、[Gulp](https://www.gulpjs.com.cn/)、[VueCLI](https://cli.vuejs.org/zh/) 等
    - 错综复杂，难以维护或升级

<!--

我们先来看看选型这部分。

目前我们公司内的前端技术栈相对比较混乱，项目有使用到 Taro、Expo、Vue、UniApp、WePY、MpVue、AngularJS 这些框架或者库。

公司内的前端大部分都会 Vue，但只是基于 Vue 或者 Vue 的就有 3 个了：UniApp、WePY、MpVue，这三个非常相似，却又在一些细节和底层实现上有差别，在开发前一般都需要简单重新过一遍文档回忆一下。而另外一些框架、库和 Vue 相差比较大，如果是第一次接触不免要新学一下，之后还要在开发期间多次翻阅文档。

项目配置也有类似的问题，有可能项目 A 和项目 B 配置路由的风格不同，项目 A 用了 Moment 来处理时间，项目 B 却用了 DayJS 来处理时间。

这两种情况，都需要前端加入了项目之后去做梳理，会占用真正的开发时间，带来业务压力，也不利于前端在不同项目间流动。

底层工具链也有好几种，Metro、Webpack、Gulp、VueCLI 都有，我想没有人在兼顾业务开发的同时，还能用有那么多精力去维护或者升级底层的工具链吧？

-->

---

# 选型

- 目标：统一
  - 统一框架/库
  - 统一配置约定
  - 统一底层工具链

<v-clicks>

怎么选？条件是什么？

- 生态支持：生态支持要足够好，对国内生态要有足够的支持，方便遇到问题的时候查找解决方案
- 学习成本低：学习使用成本低，最好有中文文档，方便扩展团队和前端流动
- 维护成本低：方便长生命周期产品后续维护
- 适合团队：当前大部分团队成员都掌握

</v-clicks>

<!--

要想处理这种混乱的情况，最有效的方法就是做统一。统一什么呢？统一框架或者库、统一配置约定、统一底层工具链。

统一框架或者库就是说选定一个基本框架或者基本库，同时选定拓展插件、拓展库，覆盖桌面端网页、移动端网页、桌面端应用、移动端应用、多端小程序。

统一配置约定就是说不要一个项目一套配置，尽量使用约定式配置，比如统一使用 DayJS，统一使用文件系统路由等等。

统一底层工具链就是不要直接用 Webpack、Rollup 之类的工具，而是使用封装好的脚手架，最好是官方提供的，比如 VueCLI 和 CreateReactApp。

那要怎么统一呢？换而言之，要怎么选？要满足什么条件？我认为需要满足以下 5 个条件。

第一个是要有足够的生态支持，尤其是要有国内生态的支持度，这样方便遇到问题尤其是国内特有问题的时候查找解决方案。

第二个是学习成本要低，最好要有中文文档，这样的话好招人，也方便前端学习了之后在不同项目间流动。

第三个是维护成本要低，方便长生命周期产品后续维护。

第四个就是要适合团队，最起码团队成员大部分都要会，由于学习成本比较低，不会也可以很快学会。

-->

---

# 选型

- 前端三大框架的生态相对成熟，暂时不需要去考虑其它框架

|google|baidu|
|:-:|:-:|
|<img src="/google-react-vue-angular.png" alt="google-react-vue-angular.png" title="google-react-vue-angular">|<img src="/baidu-react-vue-angular.png" alt="baidu-react-vue-angular.png" title="baidu-react-vue-angular">|

谷歌显示总体上 React > Vue > Angular，百度显示总体上 Vue > React > Angular。

国内更关注 Vue，国外更关注 React。考虑到 Angular 对小程序支持不佳，先排除 Angular。

---

# 选型

- React 的心智负担较重，相对 Vue 难学难精，团队内也没有多少人会 React，也排除。
  - [class example](https://codesandbox.io/s/elated-snow-8z7iu)
  - [function example](https://codesandbox.io/s/w2wxl3yo0l)
- 最后只剩下 Vue 了。

---

# 选型

- Vue 的优点
  - 国内外对 Vue 的支持都不错，有问题一般都能查询到相应解决方案。可以用 UniApp 开发小程序和移动端应用，用 Cordova 和 Capacitor 开发移动端应用，用 Electron 开发桌面端应用。
  - 学习使用成本低，中文文档非常完整且有指导思想，学习曲线不陡峭，不用立刻接受过多的新概念。
  - VueCLI 提供了完整的底层工具链，也很容易扩展、维护、升级，另外也有一些社区插件、库、框架以实现约定式配置。
    - vue-cli-plugin-auto-routing
    - vuex-orm
    - Nuxt
  - 前端团队目前大部分人都会 Vue，不需要过多折腾。

---

# 选型

- Vue 的缺点
  - UniApp 很多细节仍需要打磨（HBuilderX 想自立生态但支持度不足，编译器存在缺陷，文档不够友好等），开发小程序、移动端应用、桌面端应用很需要用 80% 的时间解决 20% 的问题。

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
function add(a ,b ){
   return a+ b
}

function subtract(a ,  b ){
  return a - b;
}

function multiple(a  ,b ){
  return a *b
}

function divide(a,   b ){
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

- 能不能减少人的参与，增加机器的参与，减少人为因素造成的问题？

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

<!-- # 优化

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

</div> -->

<!--

在这里我不打算对所有都展开讲述，因为每一个要讲都很复杂，这里就大概讲讲重构和文档

-->

# 文档

---

# 参考

- [带你入门前端工程](https://woai3c.gitee.io/introduction-to-front-end-engineering/)
- [敏捷开发入门教程](https://www.ruanyifeng.com/blog/2019/03/agile-development.html)
- [持续集成是什么](https://www.ruanyifeng.com/blog/2015/09/continuous-integration.html)
- [useEffect 完整指南](https://overreacted.io/zh-hans/a-complete-guide-to-useeffect/)
