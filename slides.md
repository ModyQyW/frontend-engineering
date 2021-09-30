---
theme: seriph
download: true
highlighter: shiki
---

# 前端工程化

<br>

吴睿

[Repo](https://github.com/modyqyw/frontend-engineering)

Powered by [Slidev](https://sli.dev/)

<!--

大家好。这次的分享会主要想跟大家分享一下我在前端工程化这一方面的理解。这是我做业务之外的主要发力点，也算是有自己的一点见解吧。

-->

---

# 目录

- 选型
- 规范
- 测试
- 发布和部署
- 参考

<!--

整个分享会会涉及下面四个部分：选型，规范，测试，发布和部署。

这四部分的内容都是由浅到深的，目的就是想让大家在做项目的时候或多或少能用上今天所说到的东西。

-->

---

# 什么是前端工程化

<br>

提升前端效率的工作，都可以认为是前端工程化。

<!--

在正式讲述前，我们需要首先明确一个概念，那就是什么是前端工程化。

前端工程化不是什么高大上的概念，只要提升了前端开发效率，都可以认为做了前端工程化。

前面提到的四个部分，都在某些方面提升了前端开发效率，下面就来一一讲述。

-->

---

# 选型

- 现状：混乱
  - 框架/库用到了 [Taro](https://docs.taro.zone/)、[Expo](https://expo.io/)、[Vue](https://cn.vuejs.org/)、[UniApp](https://uniapp.dcloud.io/)、[WePY](https://wepyjs.gitee.io/wepy-docs/)、[MpVue](http://mpvue.com/)、[AngularJS](https://www.angularjs.net.cn/) 等，规范也各不相同
  - 项目配置（如路由、状态管理、工具类库等）没有规律
    - 每次加入项目开发都需要额外花时间去梳理适应，带来隐性的时间成本，不利于前端在不同项目间流动
  - 底层工具链用到了 [Metro](https://facebook.github.io/metro/)、[Webpack](https://webpack.docschina.org/)、[Gulp](https://www.gulpjs.com.cn/)、[VueCLI](https://cli.vuejs.org/zh/) 等
    - 错综复杂，难以维护或升级

<!--

我们先来看看选型这部分。

目前我们公司内的前端技术栈相对比较混乱，项目有使用到 Taro、Expo、Vue、UniApp、WePY、MpVue、AngularJS 这些框架或者库。

公司内的前端大部分都会 Vue，但只是基于 Vue 的就有 3 个了：UniApp、WePY、MpVue，这三个非常相似，却又在一些细节和底层实现上有差别，在开发前或者开发的时候一般都需要简单重新过一遍文档回忆一下。而另外一些框架、库和 Vue 相差比较大，如果是第一次接触不免要新学一下，之后还要在开发期间多次翻阅文档。

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

怎么统一？怎么选？

- 生态支持：生态支持要足够好，方便遇到问题的时候查找解决方案
- 学习成本低：学习使用成本低，最好有中文文档，方便扩展团队和前端流动
- 维护成本低：方便长生命周期产品后续维护
- 适合团队：当前大部分团队成员都掌握

</v-clicks>

<!--

要想处理这种混乱的情况，最有效的方法就是做统一。统一框架或者库、统一配置约定、统一底层工具链。

统一框架或者库就是说选定一个基本框架或者基本库，同时选定拓展插件、拓展库，覆盖桌面端网页、移动端网页、桌面端应用、移动端应用、多端小程序。

统一配置约定就是说不要一个项目一套配置，尽量使用约定式配置，比如统一使用 DayJS，统一使用基于文件系统的路由等等。

统一底层工具链就是不要直接用 Webpack、Rollup 之类的工具，而是使用封装好的脚手架，最好是官方提供的，比如 VueCLI 和 CreateReactApp。

那要怎么统一呢？也就是说，要选满足什么条件的呢？

第一个是要有足够的生态支持，尤其是要有国内生态的支持度，要考虑到接入微信、支付宝之类的 API，还要考虑可能要上不同平台的小程序，最好还要有活跃的社区，这样方便遇到问题尤其是国内特有问题的时候查找解决方案。

第二个是学习成本要低，最好要有中文文档，这样的话好招人，也方便前端学习了之后在不同项目间流动。

第三个是维护成本要低，方便长生命周期产品后续维护。

第四个就是要适合团队，最起码团队成员大部分都要会，而且由于学习成本比较低，不会也可以很快学会。

-->

---

# 选型

- 前端三大框架的生态相对成熟，暂时不需要去考虑新兴之秀 Svelte、Solid

|google|baidu|
|:-:|:-:|
|<img src="/google-react-vue-angular.png" alt="google-react-vue-angular.png" title="google-react-vue-angular">|<img src="/baidu-react-vue-angular.png" alt="baidu-react-vue-angular.png" title="baidu-react-vue-angular">|

总体上看，国外更关注 React，国内更关注 Vue，Angular 垫底。

Angular 对小程序支持不佳（相关项目只有一个 [angular-miniprogram](https://github.com/wszgrcy/angular-miniprogram) 而且是近期才发起的），先排除 Angular。

<!--

前端三大框架，也就是 React、Vue、Angular 这三个，生态相对成熟，我们也不需要考虑太多，直接在这三个里面选一个就好了。不要看到 Svelte、Sold 最近的讨论度比较高就想去用，它们的生态都是不如三大框架的。

这里我收集了谷歌和百度上三大框架的搜索趋势，可以从图里看出来，国外比较关注 React，国内比较关注 Vue。

国内外关注 Angular 的都比 React 和 Vue 少，再加上 Angular 对小程序的支持不是太好，相关的项目只有一个而且是近期才开始的，这里可以先排除掉 Angular。

虽然说要排除 Angular，但是 Angular 本身，包括设计、实现、体系等等，都很值得前端去学习。我建议有空一定要学习一下 Angular。

-->

---

# 选型

- React 的心智负担较重，比 Vue 难学难精，团队内也没有多少人会 React，也排除。
  - [Class Component Example](https://codesandbox.io/s/elated-snow-8z7iu)
  - [Function Component Example](https://codesandbox.io/s/w2wxl3yo0l)

<!--

再来看看 React。React 的心智负担比较重，换句话说就是思考方式比较反直觉。

下面就来看一下两个例子。

相对 Vue 来说，难学，也难精通，再加上前端团队里没有多少个会 React 的，更不要说用好了，所以把 React 也排除掉了。

-->

---

# 选型

- Vue 一直在维护更新，有问题一般都能查询到相应解决方案，学习使用成本低，中文文档完整友好，学习曲线平缓。
- 生态支持良好。
  - [UniApp](https://uniapp.dcloud.io/)：多端小程序和移动端应用
  - [Cordova](https://cordova.apache.org/) 和 [Capacitor](https://capacitorjs.com/)：移动端应用
  - [Electron](https://www.electronjs.org/)：桌面端应用
- 前端团队目前大部分人都会 Vue，不需要过多折腾。

<!--

最后也就只剩下了 Vue。

……

-->

---

# 选型

- VueCLI 提供了完整的底层工具链，也很容易扩展、维护、升级，另外也有一些社区插件、库、框架以实现约定式配置。
  - [vue-cli-plugin-auto-routing](https://github.com/ktsn/vue-cli-plugin-auto-routing) - 约定式路由
  - [VuexORM](https://vuex-orm.org/)、[Pinia](https://pinia.esm.dev/)、[Hamlem](https://harlemjs.com/)、[VuexPersistedState](https://github.com/robinvdvleuten/vuex-persistedstate) - 对 vuex 的改进尝试
  - [@vue/composition-api](https://github.com/vuejs/composition-api) - 把 Vue 3 Composition API 带到 Vue 2
  - [UnpluginVue2ScriptSetup](https://github.com/antfu/unplugin-vue2-script-setup) - 把 Vue 3 `<script setup>` 带到 Vue 2
  - [UnpluginVueComponents](https://github.com/antfu/unplugin-vue-components) - 自动导入组件
  - [UnpluginIcons](https://github.com/antfu/unplugin-icons) - 自动导入图标
  - [Nuxt](https://nuxtjs.org/)：开箱即用的 SSR、SSG 支持，还附带约定式路由等额外功能
  - [Lodash](https://lodash.com/)、[Validator](https://github.com/validatorjs/validator.js)、[DayJS](https://dayjs.gitee.io/)、[Iconify](https://iconify.design/)、[Remixicon](https://remixicon.com/)、[Axios](https://axios-http.com/)、[SWRV](https://docs-swrv.netlify.app/)、[VueQuery](https://vue-query.vercel.app/)、[TailwindCSS](https://tailwindcss.com/)，[WindiCSS](https://windicss.org/)……
- 备选 Vite，生态飞速发展中。

---

# 选型

- Vue 本身没什么缺点，但 UniApp 缺点很明显。
  - 想借助 UniApp、UniCloud 和 HBuilderX 自立生态，但官方投入和社区支持均不足，很多细节需要打磨
  - 官方指引较为混乱、分散
  - 编译存在细节缺陷，一些边缘情况编译出来不支持运行，需要人工介入

```vue
<template>
  <button
    type="button"
    class="
      flex
      text-center
      w-full
      items-center
      justify-center
    "
  >
    Reset
  </button>
</template>
```

<style>
.shiki-container {
  width: 50%;
  margin: 0 auto;
}
</style>

<!--

说完了优点，我们再来说一下缺点。

……

-->

---

# 选型

- MillCloud/boilerplate-vue2 - 桌面端网页、移动端网页，[Github](https://github.com/MillCloud/boilerplate-vue2)，[Gitee](https://gitee.com/MillCloud/boilerplate-vue2)
- MillCloud/boilerplate-uni-app-vue2 - 小程序、移动端应用，[Github](https://github.com/MillCloud/boilerplate-uni-app-vue2)，[Gitee](https://gitee.com/MillCloud/boilerplate-uni-app-vue2)
- MillCloud/boilerplate-vue3 - 桌面端网页、移动端网页，WIP，[Github](https://github.com/MillCloud/boilerplate-vue3)，[Gitee](https://gitee.com/MillCloud/boilerplate-vue3)

<!--

为了帮助更快速地做开发，我做了一些模板放到 Github 和 Gitee 上面，感兴趣的可以自己去看看。

-->

---

# 规范

- 现状：没有标准
- 目标：形成统一的标准，而且尽量严格，避免劣质代码，方便代码审查等

<v-clicks>

标准包括了什么？只考虑代码质量就足够了吗？

</v-clicks>

<!--

讲完了选型，我们再来讲讲规范相关的东西。

前面提到的约定式配置算不算规范呢？算，它更侧重于项目规范。这里要讲的规范，更侧重于代码规范。

那代码规范现在是什么情况呢？跟选型类似，代码规范也没有一个标准，可能一个项目里是严格标准，另一个项目里又是宽松标准了。

尽管有工具可以辅助我们执行这些标准，但从过往的经验来看，有工具还不够，还需要尽量严格，越是严格，出错的概率也就越小。

统一了之后，好处就在于最大限度地阻止了劣质代码的出现，代码审查之类的需要阅读源码的工作也更轻松。

但紧接着，我们还需要解决另一个问题，那就是代码规范标准都包括了什么？我们都知道代码都要正常地跑起来，所以我们的代码规范标准自然要包括代码质量。但是这样就足够了吗？

-->

---

# 规范

<v-click>

|<mdi-close mx="auto" />|<mdi-check mx="auto" />|
|:-:|:-:|

</v-click>

```ts
const page_count = 5
const shouldUpdate = true

const a = 5
const isPaginatable = a > 10
const shouldPaginatize = a > 10
```

```ts
const pageCount = 5
const shouldUpdate = true

const postCount = 5
const hasPagination = postCount > 10
const shouldPaginate = postCount > 10
```

<style>
.shiki-container {
  display: inline-flex;
  flex-direction: row;
  width: 50%;
}

.slidev-code {
  width: 100%;
}
</style>

<!--

下面是两组代码，大家可以简单地先看一下哪一边会比较好。

业界普遍认为，右边会比较好。

pageCount 和 shouldUpdate 采用了不同的命名方式，不够统一。

用 a 做命名，没有确切的含义。下面一个就是不够自然，一般我们想的是“有没有分页”，而不是“是不是可分页的”。再下面一个就是生造一个动词出来。这三个都有着语义化问题。

-->

---

# 规范

<v-clicks>

- 代码规范标准
  - 代码质量：代码能不能完成需求，代码是否低耦合，代码性能是否足够好，语义化程度等
  - 代码风格：换行，分号，逗号，空格，属性顺序等
- 执行
  - 借助工具：ESLint，Stylelint，Prettier，Markdownlint，Commitlint，Husky，LintStaged……
  - 借助人力：代码审查，处理工具无法处理的问题
  - [设计模式](https://refactoringguru.cn/design-patterns/catalog)，[谷歌工程实践文档](https://google.github.io/eng-practices/)，[Code Review 最佳实践](https://zhuanlan.zhihu.com/p/73809355)，[前端 Code Review 指北](https://blog.csdn.net/Tencent_TEG/article/details/119791977)，[@modyqyw/fabric](https://github.com/ModyQyW/fabric)

</v-clicks>

<!--

从上面的例子能得出什么结论？那就是代码规范标准除了要考虑代码质量，还要考虑代码风格。

代码质量方面，最基本的自然是代码能不能完成需求，再高追求一点那就涉及到耦合度、性能、语义化之类的问题了。

代码风格方面，包括了换行、分号、逗号、空格、属性顺序等等琐碎的内容。

我们要怎么去执行这些规范？

首先自然是借助工具，业界常用的工具有 ESLint，Stylelint，Prettier，Markdownlint，Commitlint，Husky，LintStaged 等，基本覆盖了大多数方面。

其次就是要借助人力了，也就是代码审查，Code Review。工具不能处理所有的问题，比如代码质量、语义化等等，这些大部分都是要人力分辨的。

关于 Code Review，其实可讲的还有很多，但是由于时间关系，这里就不再展开，感兴趣可以看一下链接里的内容。

还有就是，前面三个模板使用的规范是我自己整合的库，感兴趣可以自己看一下。

-->

---

# 测试

- 当构建可靠的应用时，测试在个人或团队构建新特性、重构代码、修复 bug 等工作中扮演了关键角色
- 在 web 应用领域内主要有三大类
  - 单元测试：[Jest](https://jestjs.io/zh-Hans/)、[Mocha](https://mochajs.org/)
  - 组件测试：[Testing Library](https://testing-library.com/)
  - 端到端测试：[Cypress](https://www.cypress.io/)、[Nightwatch](https://nightwatchjs.org/)、[WebdriverIO](https://webdriver.io/)

<!--

然后我们再来说说测试这部分。

测试就是为了找出代码潜在的问题，提高代码质量的，同时，它也让你在改动代码的时候更有底气。Web 应用领域里面主要有三大类：单元测试，也叫单测，还有组件测试、端到端测试。

因为我们平时做业务开发时间都比较紧，端到端测试往往没有时间做，所以尽量做一下单元测试和组件测试就可以了。

主要涉及的库已经列写在下面了，感兴趣的可以去自己学习一下，不会太复杂，这里不讲他们的用法，而是讲讲我对测试的理解。

-->

---

# 测试

1. 测试是为了找出缺陷
   - 测试应当全面，尽量覆盖有价值的边缘情况
2. 测试不应该穷尽
   - 测试案例应该具有代表性
3. 尽早测试
   - 尽早发现问题，尽早修复
4. 缺陷集群效应
   - 越复杂的模块，潜在的问题越多，要写的测试也越多
5. 不要一直使用相同的测试
   - 更新测试、交叉测试
6. 测试依赖于上下文
   - 不同的项目可能需要不同的测试策略
7. 考虑外部因素
   - 用户体验，市场需求等

<!--

首先，测试就是为了找出缺陷。不要为了不找出缺陷而去写测试，那样的话，直接不写就可以了。为了找出缺陷，测试要全面，尽量覆盖有价值的边缘情况，比如 0，正负 1，特殊字符等等。

然后就是测试不应该穷尽。拿密码来说，如果要测试穷尽，那就需要考虑密码长度，测 26 个字母、10 个数字和一些标点的所有组合，那样的话需要写多少个测试案例？要耗费多少时间和人力？投入和回报是不成正比的。所以说，测试不应该穷尽，测试案例应该具有代表性。

尽早测试这个应该很好理解，尽早测试也就能尽早发现问题，也就能尽早修复，节约不必要的成本。

缺陷集群效应就是指大部分的缺陷往往会集中在复杂的模块里，有点类似于二八原则。对于复杂的模块，我们往往要写更多的测试。

不要一直使用相同的测试是为什么呢？这就跟杀虫剂一样，杀虫剂能杀死大部分的害虫，但小部分的害虫具有抗药性，无法被杀死，小部分的缺陷可能不会被测试出来，这时候就需要更新我们的测试，有时候也可以让新的人员来做测试，也就是交叉测试，目的就是找出隐藏很深的缺陷。

测试依赖于上下文，也就是不要所有项目都用一套测试策略，举个例子来说就是，金融项目的测试往往比电子商务项目的测试更全面更细致。

最后就是测试也需要考虑外部因素，用户体验啦，市场需求啦等等。当初诺基亚的手机质量很好，没有什么缺陷，为什么就突然不行了呢？是测试不行吗？实际上是因为人们开始转向智能机了，但诺基亚还是功能机。

这些都跟库没有关系，学习库的用法之后可以考虑在实践中应用这些东西。

-->

---

# 测试

|测试驱动开发 TDD|
|:-:|
|<img src="/tdd.webp" alt="tdd.webp" title="tdd" class="mx-auto w-1/2" >|

领域驱动开发 DDD

<!--

业界里还有一种做法，那就是测试驱动开发，简称 TDD。流程就跟这张图里一样，写测试，写代码通过测试，重构，继续写测试，这么循环下去。

由于时间关系，这里就不再展开，感兴趣可以看一下参考里的内容。

-->

---

# 发布和部署

<v-clicks>

- 初始化项目
- 本地开发
- 测试
- 更新版本号
- 写改动日志
- 推送到仓库
- 构建
- 推送到服务器

祖传特色：手动操作，容易出现疏漏

减少人的干预，增加机器的参与，半自动化/自动化

</v-clicks>

<!--

最后来讲讲发布和部署。

一个传统的完整前端开发流程包括了下面的步骤，其中发布和部署就包括了更新版本号、写改动日志、推送到仓库、构建和推送到服务器。

这几个步骤往往需要人工干预，特别容易出现疏漏，比如漏了更新版本号、漏了写改动日志、构建错了等等。

怎么才能避免这种问题？我们往往会考虑减少人的干预，增加机器的参与，也就是所谓的半自动化、自动化。

-->

---

# 发布和部署

<br>

[都城二期后台管理](https://work.iscnu.net/SystemDevelopment/Duchenggo/_git/desktop-web)：release-it + 脚本

- main 分支开发
- release-it 更新版本，推送到仓库
- shell 脚本构建并部署到服务器

---

# 发布和部署

<br>

[都城一期 EPAY](https://work.iscnu.net/SystemDevelopment/Ducheng/_git/epay?path=%2F&version=GBnext&_a=contents)：release-it + 脚本

- main 分支开发
- release-it 更新版本，JavaScript 脚本更新 manifest.json，最后推送到仓库
- 手动用 HBuilderX 构建出 APK / IPA 再处理

---

# 发布和部署

<br>

[developer-examination](https://github.com/MillCloud/developer-examination)：release-it + Github Actions + Github Pages

- main 分支开发
- release-it 更新版本，推送到仓库，并同步 main 分支到 release 分支
- Github Actions 构建 release 分支，构建产物同步到 git-pages 分支
- Github Pages 部署 git-pages 分支

---

# 发布和部署

<br>

- 使用 release-it 和脚本处理版本号、改动日志和推送到仓库
- 使用脚本和服务构建并推送到服务器

<!--

developer-examination 部署演示

-->

---

# 发布和部署

|Git Flow|Github Flow|Gitlab Flow|
|:-:|:-:|:-:|
|<img src="/git-flow.png" title="Git Flow" alt="Git Flow" class="mx-auto w-2/3">|<img src="/github-flow.png" title="Github Flow" alt="Github Flow" class="mx-auto w-2/3">|<img src="/gitlab-flow.png" title="Gitlab Flow" alt="Gitlab Flow" class="mx-auto w-2/3">|

[Git 工作流程](https://www.ruanyifeng.com/blog/2015/12/git-workflow.html)

<!--

接下来我还想跟大家聊一下分支模型的事情。现在大部分仓库都是基于 Git 做代码管理的，这里就聊一下三种比较经典的工作流程，Git Flow、Github Flow 和 Gitlab Flow。

Git Flow 是最早被提出来的工作流程，你需要为不同的工作设立不同的分支，看流程示意图应该能感受到，它的优点就是清晰可控，缺点就是太过复杂了，对于小型团队来说反而可能拖慢节奏。

Github Flow 针对 Git Flow 做了基于 PR 的改进。开发的时候先从主分支拉出，修改完毕后提交 PR，最后合并到主分支。优点就是更简洁了，缺点在于对人的要求比较高，需要明确地写明 PR 做了什么工作，同时还可能需要增加一个分支用来追踪线上版本。

Gitlab Flow 结合了 Git Flow 和 Github Flow 的优点，也是我个人比较推荐使用的工作流程。在主分支外，建立起环境分支，比如 release 分支。在代码改动时，把主分支逐步合并到环境分支里。

由于时间关系，这里就不再展开，感兴趣可以看一下链接里的内容。

-->

---

# 发布和部署

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

# 展望

- Node 全栈和 Serverless - [express](https://expressjs.com/)，[koa](https://koajs.com/)，[egg](https://eggjs.org/)，[serverless](https://serverless.com/)，[midway](https://www.midwayjs.org/)，[nest](https://nestjs.com/)
- 面向现代浏览器的前端开发：[Vite](https://cn.vitejs.dev/)、[Vue 3](https://v3.cn.vuejs.org/)……
- ...

---

# 参考

- [带你入门前端工程](https://woai3c.gitee.io/introduction-to-front-end-engineering/)
- [敏捷开发入门教程](https://www.ruanyifeng.com/blog/2019/03/agile-development.html)
- [持续集成是什么](https://www.ruanyifeng.com/blog/2015/09/continuous-integration.html)
- [滴答清单时间管理方法论和实践](https://help.dida365.com/tasks)
- [搭建知识框架](https://mp.weixin.qq.com/s/YzImrD4dmNe1SjBHztOofg)
- [10x 程序员工作法](https://time.geekbang.org/column/intro/148)
- [代码整洁之道](https://weread.qq.com/web/reader/f3e322f0811e3913eg012ae9)
- [架构整洁之道](https://weread.qq.com/web/reader/480322f072021a3248038c8)
- [程序员修炼之道](https://weread.qq.com/web/reader/2cf32ec0811e3ac71g017571)
- [重构](https://weread.qq.com/web/reader/2ed32e60811e3a304g014c02)
- [代码精进之路](https://weread.qq.com/web/reader/81132f5071cc7f7a81151c9)
- [A successful Git branching model](https://nvie.com/posts/a-successful-git-branching-model/)
- [Github flow](https://docs.github.com/cn/get-started/quickstart/github-flow)
- [Introduction to GitLab Flow](https://docs.gitlab.com/ee/topics/gitlab_flow.html)
