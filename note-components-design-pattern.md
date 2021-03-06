---
title: note-components-design-pattern
tags: [components, pattern]
created: '2020-10-02T11:42:34.698Z'
modified: '2020-10-05T06:11:13.841Z'
---

# note-components-design-pattern

## latest

- 组件库研发方向及特色
  - [跨框架开发ui组件库(stencil)](https://zhuanlan.zhihu.com/p/41974042)
    - 开发者用起来framework-agnostic，但原作者很可能要维护多个port或bridge
  - headless ui
    - 只适合简单组件，复杂组件如table实现功能时很可能与layout密切相关
    - opinionated: ui交互或技术选型具有明显的偏向性
  - ui组件
    - dom结构(非视觉结构)、样式、行为
    - foundation + adapter

## opinionated

- ui设计
  - portal的target容器默认是组件自身或document.body
  - should we show a indeterminate for the header's checkbox if partial is selected
  - Inline Editing is a very common feature in a table, but it's highly coupled with specific ui libraries, so it won't be a part of BaseTable itself.
- 交互设计
  - should we select all the children if the parent is selected
  - how to sync the staled keys if those rows are removed
- 技术选型
  - all in js
- 参考现有ui解决方案：dom密集操作、状态数据频繁更新
- 流行typescript库很多都用的class，所以是否用class可参考现有成熟方案的选择
- 通用组件库
  - 组件库结构包括的通用的design tokens，通用的core，core可用来共享locale、theme、工具方法、类型定义
    - 具体框架会实现各自组件的生命周期、状态管理、样式交互、事件处理，这也是组件互操作的因素
    - 最好支持切换不同css框架提供的design tokens
    - 实现方式1：vanilla js组件加上胶水层可移植到其他库
    - 实现方式2：各框架的组件单独实现
    - 实现方式3：web components，或类似api的库
  - 组件库参考
    - carbon-components: a collection of reusable HTML and SCSS partials
    - carbon-components-react: components implemented using React.
      - built React first. We also support core parts of the system in vanilla JS, Angular, and Vue. 
    - 只共用样式，组件分开实现，而不是简单wrapper，因为不同框架解决状态更新、数据同步、事件等的方案不同
    - 选用已有框架的重要原因是借鉴处理状态、事件、路由等问题较成熟的解决方案
    - 最新的web components和stencil再等等看，思路是framework as compiler
      - web components本身使用浏览器标准的runtime，特别适合替代vue/react的runtime
      - web components难以替代其他框架，因为这些框架的目标不止浏览器环境，还支持native、ssr
      - 在其他框架中使用w-c组件，无需w-c框架层的依赖，这是通用组件重要的优势
      - 但在w-c中使用其他框架组件，则需组件源码加上框架runtime的依赖，并且每次导入组件都会导入一次框架层的依赖
    - stencil vs svelte
      - stencil编译到w-c，svelte还能编译到framework-less的纯js
      - stencil组件基于vdom，svelte组件会编译到js代码
      - stencil的状态管理更类似react
      - stencil的dom模版使用jsx，svelte使用的是自定义指令
      - svelte暂不支持ts
      - stencil的css基于shadow dom，且写在单读文件，svelte的css写在style块
    - 参考现有ui解决方案：dom密集操作、状态数据频繁更新
    - 流行typescript库很多都用的class，所以是否用class可参考现有成熟方案的选择
  - ref
    - https://github.com/jaywcjlove/awesome-uikit
    - [Compiler like Svelte.js or Stencil.js](https://github.com/vuejs/vue/issues/9011)

## back-garden-design-in-action

- logo: green plum
- design-system-tokens
  - text: sans serif(衬线体多用于印刷)
  - color: mineral-ui-color-palette, primary-mediumseagreen
  - bezel-less
- interaction
  - hover-color
  - click-ripple
  - loader-flower
- animation
  - flip
  - misc
    - rotate
    - unfold
    - point movement
- shape
  - point/polygon-shape-based
  - https://medium.com/google-design/you-need-a-shape-system-8d2aa9016817
- 公共api
  - variant
    - borderless
      - 部分组件提供无边框的版本，如modal
      - 也可考虑实现成dark mode的形式

## material design

### guide

- material-design-web-vanilla
  - 缺点
    - 样式与dom结构绑定了
  - 大部分组件都由js和css构成，如checkbox、dialog、drawer、list、textfield
  - 有少部分组件只有css，如button、card、elevation、layout、typography
  - 有少部分组件只有js，如animation、autoInit
- material-design-web-react
  - 每个react组件复用了material-design-web包的MDCCheckboxFoundation、MDCCheckboxAdapter、cssClasses
  - MDCCheckboxFoundation在componentDidMount中初始化
  - adapter对象包含各种setState逻辑
- ref
  - [rmwc: Foundation Adapter Implementation](https://github.com/jamesmfriedman/rmwc/issues/141)
