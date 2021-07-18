---
theme: seriph
download: true
---

# 前端工程化

吴睿

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
- 组件库和工具库
- 测试
- 自动化
- 性能
- 重构
- 微前端
- Serverless
- 参考

---

# 什么是前端工程化

<br>

提升前端效率的工作，都可以认为是前端工程化。

<!--

为什么需要前端工程化？

提升效率谁不想要呢？

-->

---

# 选型

- 稳定：不会经常有破坏性更新，向后兼容度高，更新/迁移成本低
- 易用：使用相对简单，更有可能统一技术栈，更方便不同团队间人员流动
- 生态：需要考虑支持国内外生态，如小程序端、支付和分享场景等
- 暂时不考虑魔改等情况（一般也不会出现需要魔改的情况）

<br>
<br>

<v-clicks>

- Angular：对小程序支持不佳
- React：心智负担较重，易用性不佳
- Solid、Fre 等：生态不成熟
- Vue：各方面相对不错

</v-clicks>

<br>
<br>

<div v-click class="text-2xl">

Vue + uni-app：大问题没有，小问题可能会遇上

</div>

<!--

关于 React 的心智负担问题：

1. 原本 class 组件也就是类组件是相对完整的，function 组件也就是函数组件是有相当多限制的。

2. 引入 hooks 之后，函数组件开始趋向完整，虽然仍然有一些缺失，但已经是社区里的大趋势了。

3. 但函数组件的思维方式和类组件的思维方式完全不同，文档却依然以类组件为主来做解释，这就导致了很多人可能会在使用函数组件时踩坑。

4. 所以说心智负担较重。

关于 Vue 的问题：

Vue 相对不错，那是不是意味着没有问题了呢？

主要问题出在 uni-app 上，uni-app 的表现并不是特别稳定。

uni-app 的文档看起来很完整，但往往在某些细节上阐述不清，又或是底层上实现有问题，导致开发稍微复杂一点的应用的过程中必定会遇到一些问题。

同时，开发团队也没有完全把心思放在 uni-app 上，试图打造一整个的生态，但是不知道是不是人手问题，所有相关的产品都或多或少有些坑。

但综合来看，这依然是目前较为适合我们公司内的一套技术栈，我们可以用 20% 的时间处理 80% 的问题，剩余的 20% 问题就需要我们花 80% 时间去攻坚了。

-->

---

# 规范

- 帮助开发者编写相对良好的代码，提高可读性、可维护性
- 帮助代码审查 Code Review
- 保证团队一致性，降低沟通成本，方便不同团队间人员流动

---

# 规范

- 帮助开发者编写相对良好的代码，提高可读性、可维护性
- 帮助代码审查 Code Review
- 方便不同团队间人员流动

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
  - `ESLint`：`JavaScript` / `TypeScript`
  - `Stylelint`：`CSS` / `LESS` / `SCSS`
  - `Husky` + `LintStaged` + `Commitlint`：Git 提交
- Formatter：检查（并修复）格式问题的工具
  - 目前最流行的是 `Prettier`，支持多种语言
  - 可以和 `ESLint`，`Stylelint` 等结合使用
- Linter 和 Formatter 就能处理所有规范问题吗？
  - 命名问题
  - 换行问题
  - 本地问题

<!--

命名问题：变量命名、文件命名、目录命名、项目命名

换行问题：使用 Windows 系统默认的换行可能会造成影响，一般要求使用 Unix 系统默认的换行保证跨平台可用

本地问题：是不是配置正确了来确保提交的代码没有问题

-->

---

# 组件库和工具库

---

# 测试

---

# 自动化

---

# 性能

---

# 重构

---

# 微前端

---

# Serverless

---

# 参考
