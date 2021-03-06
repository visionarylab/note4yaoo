---
title: toc-lib-components-design-system
tags: [components, design-system, toc]
created: '2019-12-12T13:39:25.692Z'
modified: '2020-09-28T13:39:33.266Z'
---

# toc-lib-components-design-system

## design-system

- Ant Design  /MIT/63.7kStar/202009/ts/Alibaba
  - https://github.com/ant-design/ant-design
  - https://ant.design/
  - An enterprise-class UI design language and React UI library.
  - 主要由阿里蚂蚁金服研发，antd严重依赖自研的基础组件rc-xxx
  - https://github.com/ant-design/ant-design-mobile
    - A configurable Mobile UI specification and React-based implementation.
  - https://github.com/ant-design/ant-design-pro
    - An out-of-box UI solution for applications as a React boilerplate.
  - ref
    - https://github.com/vueComponent/ant-design-vue
    - https://github.com/NG-ZORRO/ng-zorro-antd
    - https://github.com/taejs/ant-design-vanilla
- Material Design  /MIT/13.6kStar/201912/Google
  - https://material.io/design/
  - https://github.com/material-components/material-components-web
  - https://github.com/material-components/material-components-android
  - Material is an adaptable system of guidelines, components, and tools
- Bootstrap  /MIT/138kStar/202001/Twitter
  - https://github.com/twbs/bootstrap
  - https://getbootstrap.com/docs/4.4/getting-started/introduction/
  - popular framework for building responsive, mobile-first sites
- Fluent Design  /MIT/9.5kStar/202009/Microsoft
  - https://github.com/microsoft/fluentui
    - moved from https://github.com/OfficeDev/office-ui-fabric-react
  - https://www.microsoft.com/design/fluent/#/
  - https://developer.microsoft.com/en-us/fabric/#/components
  - React-based front-end framework for building experiences for Office
- Lightning Design System  /BSD/3kStar/202009/Salesforce
  - https://github.com/salesforce-ux/design-system
  - https://www.lightningdesignsystem.com/design-tokens/
  - https://www.lightningdesignsystem.com/
  - https://react.lightningdesignsystem.com/
  - Component blueprints are framework agnostic, accessible HTML and CSS
  - SLDS is a pure CSS framework that you can use with any front-end development framework
- Carbon Design System  /Apache2.0/3.5kStar/202009/IBM
  - https://github.com/carbon-design-system/carbon
  - https://www.carbondesignsystem.com/
  - https://github.com/carbon-design-system/carbon/tree/master/packages/components
    - a collection of re-usable HTML and SCSS partials for building products.
  - https://github.com/carbon-design-system/carbon/tree/master/packages/react
    - A collection of Carbon Components implemented using React.
  - https://github.com/carbon-design-system/carbon-custom-elements
    - a variant of Carbon Design System with Custom Elements v1 and Shadow DOM v1 specs.
  - carbon组件库的核心core不依赖视图层框架，然后再为各种视图开发单独的组件包，core使用了handlebars模版引擎来生成组件html
  - The design system is built React first. We also support core parts of the system in vanilla JS, Angular, and Vue. 
  - js组件和react组件只共用 `settings.prefix` 及css样式文件，此外不相关
  - ref
    - https://www.ibm.com/design/language/
    - http://react.carbondesignsystem.com/?path=/story/buttons--default
    - https://ics-design-system.us-east.mybluemix.net/ 
- Primer Design System  /MIT/580Star/201912/Github
  - https://github.com/primer/components
  - https://primer.style/components
  - React components which implement GitHub's Primer Design System    
  - 提供单独的scss样式文件
- Base Design  /MIT/2kStar/201908/Uber
  - https://github.com/uber-web/baseui
  - https://baseweb.design/
  - A React Component library implementing the Base design language
  - 主要有uber支持，组件的第三方依赖较多
- Atlassian Design  /Apache2.0/72Star/202001
  - https://bitbucket.org/atlassian/atlaskit-mk-2/src/master/
  - https://atlassian.design/
  - https://atlaskit.atlassian.com/
  - https://atlaskit.atlassian.com/docs/guides/component-design
  - Atlassian's official UI library, on the Atlassian Design Guidelines
- Polaris Design System  /MIT/3000Star/202001
  - https://github.com/Shopify/polaris-react
  - https://polaris.shopify.com/components/get-started
  - https://polaris.shopify.com/design/colors
  - Our design system helps us work together to build a great experience for all of Shopify’s merchants
- Storybook Design System  /MIT/456Star/201912
  - https://github.com/storybookjs/design-system
  - https://storybook-design-system.netlify.com/
  - https://www.learnstorybook.com/design-systems-for-developers/
  - a reusable component library that helps Storybook build UIs faster
- Pivotal UI  /MIT/612Star/201908
  - https://github.com/pivotal-cf/pivotal-ui
  - https://styleguide.pivotal.io/
  - Pivotal's design system & component library
- Garden /Apache2.0/794Star/202009
  - https://github.com/zendeskgarden/react-components
  - https://garden.zendesk.com/
  - The source of truth for tools, standards, and best practices when building products at Zendesk.
- gov.uk Design System  /MIT/290Star/201912
  - https://github.com/alphagov/govuk-frontend
  - https://design-system.service.gov.uk/
  - build a user interface for government platforms and services    
  - https://github.com/govau/design-system-components
  - https://github.com/alphagov/govuk-design-system
- United States Web Design System(uswds)  /CC01.0/5400Star/201912
  - https://github.com/uswds/uswds
  - https://designsystem.digital.gov/
  - visual style guide for U. S. federal government websites.
  - https://design.va.gov/
    - VA.gov is built on top of VA's design system (VADS). 
    - VADS is based on the US Web Design System
- Photon Design System  /MPL2.0/206Star/201909/Firefox
  - https://github.com/FirefoxUX/photon
  - https://design.firefox.com/photon/
  - build modern, intuitive, delightful experiences
- Clarity Design System  /MIT/5500Star/201912/Vmware
  - https://github.com/vmware/clarity/
  - https://clarity.design/
  - UX guidelines, HTML/CSS framework, and Angular components working together to craft exceptional experiences
- Reach UI Philosophy
  - https://gist.github.com/ryanflorence/e5c794e6093d16a69fa88d2112a292f7
  - accessible, composable
- design-system-deprecated
  - Mineral UI  /Apache2.0/500Star/201912/CATechnologies
    - https://github.com/mineral-ui/mineral-ui
    - https://mineral-ui.netlify.com/
  - [Nachos by Trello](https://design.trello.com/)
- design-system-guidelines
  - Airbnb Cereal
    - https://airbnb.design/cereal/
    - https://airbnb.design/building-a-visual-language/
  - https://spectrum.adobe.com/
  - https://styleguide.mailchimp.com/
  - https://ux.mailchimp.com/patterns/color
  - https://design.ubuntu.com/web/
  - Apple Design
    - https://developer.apple.com/design/
    - https://developer.apple.com/design/resources/
    - https://developer.apple.com/design/human-interface-guidelines/ios/overview/themes/
  - https://designsystem.quickbooks.com/
  - https://marvelapp.com/styleguide/overview/code-guidelines
  - https://www.audi.com/ci/en/intro/brand-appearance.html
  - https://feelix.myob.com/#/Design%20patterns
  - https://design-system.futurelearn.com/
  - https://bradfrost.com/blog/post/atomic-web-design/
  - https://spotify.design/
  - design-style
    - flat
    - motion-blur
  - Adele
    - https://adele.uxpin.com/
    - repository of publicly available design systems and pattern libraries
  - Figma
    - https://www.designsystems.com/
    - A Figma publication for design systems designers and developers
  - uxpin
    - https://www.uxpin.com/create-design-system-guide/create-ui-inventory-for-design-system
  - https://design.lyft.com/
  - http://plasma.guide/
- misc
  - https://github.com/appbaseio/designkit
    - Design kit for appbaseio ecosystem
    - not active
  - https://github.com/alexpate/awesome-design-systems
  - https://github.com/miukimiu/design-systems
  - https://github.com/CMSgov/design-system
  - https://github.com/auth0/cosmos
  - https://ether.thescenery.co/
  - https://sproutsocial.com/seeds/
  - https://palette.artsy.net/
  - https://www.duetds.com/
    - a set of organized tools, patterns and practices that work as the foundation
  - https://www.predix-ui.com
    - Our user interface components enable you to easily create Industrial web applications
  - https://www.astrouxds.com/
    - Astro Space UX Design System enables developers to build rich space app experiences
  - https://github.com/razvangeangu/cho-design-system
    - design system based on stencil
  - Solid  /MIT/115Star/202001/BuzzFeed
    - https://github.com/buzzfeed/solid
    - https://solid.buzzfeed.com/
    - Solid is BuzzFeed's functional CSS framework and styleguide.
    - Solid uses immutable, atomic CSS classes to rapidly prototype and develop features
  - Workday Canvas Design System  /Apache2.0/74Star/202001
    - https://github.com/workday/canvas-kit
    - https://design.workday.com/guidelines
  - Pluralsight Design System  /Apache2.0/158Star/202001
    - https://github.com/pluralsight/design-system
    - https://design-system.pluralsight.com/
  - Predix Design System
    - https://www.predix-ui.com/#/about/introduction
  - Morningstar Design System
    - https://designsystem.morningstar.com/
    - v2 is using web components; v3 will use vue
  - ServiceNow Design System
    - http://designsystem.servicenow.com/#!/
  - Eva Design System
    - https://eva.design/
    - https://akveo.github.io/nebular/docs/design-system/eva-design-system-intro
    - implemented for angular and react native
  - Evergreen Design System  /MIT/9000Star/202001
    - https://github.com/segmentio/evergreen
    - https://evergreen.segment.com/
  - https://github.com/artsy/palette
    - a collection of primitive, product-agnostic elements that help encapsulate Artsy's look and feel at base level
  - https://github.com/seek-oss/braid-design-system
    - 基于treat这个css-in-js解决方案实现的 Themeable design system for the SEEK Group
