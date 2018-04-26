---
order: 3
title: qnui 升级 aop-ui
groupOrder: 1
group: 快速上手
---

# qnui 升级 aop-ui

aop-ui 是1688开放平台在阿里巴巴自身实践过两年的组件库 next 1.x 之上，集成了工作台主题之后，发布的组件库。包含isv开发过程中所需的绝大部分组件，极大提升开发效率。

## 注意
1. 由于 qnui 是基于 next0.x 搭建，aop-ui 是基于 next1.x 搭建，因此会有一些breaking change，如果跑不起来，请对照文档进行修改。（这种应该很少，应用至少是可以跑起来的）
2. 一定要把 qnui 依赖清理干净，可以先 `npm uninstall --save qnui`，然后 `aop dev`，根据报错位置来替换 

## 步骤
1. **安装 aop-ui 和 peerDependency: moment**

    `npm install --save moment`

    `npm install --save aop-ui`

2. **修改配置**
   在 custom.config.js 中修改原来的 qnui 为 aop-ui
   如果没有 custom.config.js 文件，请参考
   《just脚手架升级到aop脚手架》
   
     ![](https://img.alicdn.com/tfs/TB1xQ66nb9YBuNjy0FgXXcxcXXa-1090-758.png)

3. **引入scss文件**
    在 common/index.scss 下引入主题包
     `@import '~aop-ui/index.scss'`
    或者在其他文件中引入到工程代码里
    
     ![](https://img.alicdn.com/tfs/TB1jlH6nb9YBuNjy0FgXXcxcXXa-1246-1250.png)

4. **全局替换 qnui**
    将 qnui 替换成 aop-ui 即可，组件引用路径都不用调整，注意一定要把qnui清理干净，否则可能会有冲突

5. **启动看是否已经修改**

    `aop dev`

    ![](https://img.alicdn.com/tfs/TB1dVkOnmtYBeNjSspkXXbU8VXa-701-539.png)



