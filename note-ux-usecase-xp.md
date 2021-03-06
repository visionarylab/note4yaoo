---
title: note-ux-usecase-xp
tags: [pm, ux, xp]
created: '2019-11-18T12:37:41.447Z'
modified: '2020-07-14T11:30:51.404Z'
---

# note-ux-usecase-xp

## 界面类

- 数字展示不直观，可以考虑百分比进度条
- 类似medium和zhihu的图片先显示模糊轮廓再逐渐变清晰的效果如何实现
  - 基本思路：数据库存两张图片，然后用清晰替换模糊
- 缺少预览图时，自动生成文字logo图或[文字像素图](https://svelte.dev/contributors.jpg)
- 类似掘金个人资料修改界面的列表修改体验，没有excel的网格，很简洁
- div或一块组件不要全部为空，提示已完成或未开始更友好
- 少用context menu右键菜单，应用跨平台且体验尽量一致
  - 扩展鼠标的作用
  - 要做好触摸屏等无右键的适配
- ribbon menu vs text menu
  - good
    - 选项卡分类及图标，跨设备体验更友好，更一致
  - bad
    - text menu is easier to learn the shortcut
    - text menu tends to be more rigid and heirarchical
    - ribbon menu takes more space and hides deeper than text menu
    - 宽屏时代，侧边大量空白，占用了有限的垂直空间
    - 大量使用频率低的冗余菜单，从哪里进去找菜单不明确
    - 切换菜单不便
  - 建议
    - 竖向的ribbon menu
    - 自定义工具条
    - VS针对编程人员因为效率会使用快捷键，所以无需
    - Office面对的大部分是小白，所以需要简单易用的图形化操作界面。Adobe Creative Cloud系列软件面向专业设计人员，他们更倾向于使用快捷键完成操作

## 主题功能类

- bilibili
  - 回复内容可以包含类似 `01:30` 这样的时间数字，点击时间数字会直接跳转到视频指定位置

## 通用类

- 搜索记录多端同步：google、B站
