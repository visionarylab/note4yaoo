---
title: note-style-css-in-js-dev
tags: [css-in-js, style]
created: '2020-08-07T16:13:30.609Z'
modified: '2020-09-25T05:56:45.321Z'
---

# note-style-css-in-js-dev

## guide

- why use css in js
  - 维护方便
  - all-in-js的趋势
  - 标准化theme的趋势
  - 局部样式、动态样式、主题切换
  - 技术选型时，参考知名项目或大公司项目的选择

- I feel like we’re moving out of the CSS-in-JS era into something new. We’re moving more towards:
  - Static extraction
  - Zero-runtime
  - Types
  - Platform-agnostic: atomic/tailwind output, native
- Something we could perhaps call “TSS” (Typed/Token Style Sheets)

## pieces 

- css-in-js vs sass
  - Component Driven idealogy. Your CSS also is now a component. - This is pretty cool!
  - Total styling isolation
  - Load what you need and when you needed, kinda lazy CSS
  - Theme provider, skins, modularity and dynamic - This can be achieved by other libs too
  - Server side construction of your component DOM and its style.
  - Remove the need to manually handle class names
  - Easily use javascript variables within style
  - colocate css with jsx/html
  - 参考使用css-in-js的优点

- [survey: styled-components vs SASS vs CSS, which one would win!](https://twitter.com/Ipenywis/status/1275091218905608192)
  - s-c:sass:css = 2:1:5
  - 仅8人投票

- It's funny how CSS-in-JS is controversial vs. external/extracted CSS files, but web components basically require inline CSS strings in JS. 
  - Due to the complete style isolation, you basically cannot bundle CSS to a separate file with shadow DOM in a performant way.

- The more I look at projects like tailwindcss and tachyons_css, the more I realise CSS-in-JS misses the boat(错失良机) on solving the important problems with large-scale CSS:
  - No specificity issues
  - No bloat(膨胀，过多)
  - No naming wars
  - No opinionated component-based architecture

- Wholeheartedly agree, BEM + ITCSS all the way as opposed to(相对于，而不是) sprinkling(撒在，使用少量) utility classes on top of everything. 
  - Tailwind creates a many to many maintenance problem that just makes large codebases unmaintainable. 
    - if you apply 4-7 CSS classes to style something out of let's say 100 available classes to 1000-10 000 lines of HTML, there are too many variations. 
    - If you ever want to get rid of a class it's going to be difficult, as the combinations are practically infinite.
    - Whereas if you scope CSS to a namespaced selector e.g. `.c-my-component-name` you will be able to see all instances of this component in use when you globally search your project and you have a clear route to refactoring
    - So... give it a few years and lots of team will be stuck loading Tailwind's 350kb forever because they just can't get it out of their codebase.
  - I imagine it’s popular because of CSS-in-JS.

- css in js style
  - Old way: Include this css import to get styles.
  - New way: Styles automagically added when you use the component.
  - Old way:
    - you control all your styles
  - New way:
    - those fucking styles appearing by themselves, your application contains at least 3 css-in-js libraries, some of them duplicated, your app looses half of styles during SSR, 
    - and you are looking at some AstroTurf, which ends as css.

- With our css-in-js lib(radix) and components, we have core layers and then framework-specific layers. 
  - We can build Svelte or Vue wrappers, so we're not necessarily tied to any particular framework.
  - The design tool just maps styles to components.
  - It's not inherently linked to React.

- I tend to stick to what I know that works at scale (BEM/ITCSS). But I also find that there is such a huge learning curve to BEM/ITCSS that it leads to problems in itself. Is scoped styling the answer? 
  - For a personal project, I'll generally go with BEM. For a project involving many developers and which will be used and maintained over years ? Scoped styles for sure.

- [Why write CSS-in-JS when vanilla CSS is just fine? ](https://twitter.com/saltnburnem/status/1290690315540717568)
  - The styling of a component is very linked to it's structure, so put them together.
  - The main element of reuse is the component. You won't ever need a .header CSS class when instead you'll reuse `<Header>`

## jss

## survey: css in js vs css

- ### [are there any cons to using regular CSS vs CSS-in-JS?_2018](https://twitter.com/ka11away/status/1014990019801411586)
  - css: css-in-js = 0.557: 0.443 /79votes
  - It’s depends on ur purposes. 
    - If u use dynamic generated styles (in runtime) a lot — css-in-js (styled-components) is a nice choice. 
    - If not, better use static css-in-js approach (emotion + extract, css-literal-loader) or classic

## solution-catalog-css-in-js

- treat /MIT/960Star/202007
  - https://github.com/seek-oss/treat
  - https://seek-oss.github.io/treat/
  - Themeable, statically extracted CSS‑in‑JS with near‑zero runtime.

## ref

- [The Next Era of CSS in JavaScript - From CSS-in-JS to TSS_202008](https://joebell.co.uk/blog/the-next-era-of-css-in-js)
  - More and more libraries are choosing to focus on features such as:
    - Static extraction
      - to inline critical styles and CSS files.
    - Zero-runtime
    - First-class TypeScript support
    - Design Token-driven
    - Platform-agnostic
      - outputting atomic classes or config files (e.g. Tailwind)
      - native/multi-framework support
  - It's these fundamental changes that lead me to believe we're moving into a new era; one I like to think of as TSS.
    - TSS - Typed/Token-driven Style Sheets
- [CSS-in-JS and the death of traditional CSS_202007](https://www.diogorodrigues.dev/blog/css-in-js-and-the-death-of-traditional-css)
- [CSS-in-JS: An Investigation. An introductory comparison_202007](https://t.co/y5zfBsY9IY?amp=1)
- [Tailwind just keeps exceeding all expectations. I’m about to leave CSS-in-JS and go all in on Tailwind for any new projects I do](https://twitter.com/flybayer/status/1290016656299683840)
  - It’s nothing but great.
