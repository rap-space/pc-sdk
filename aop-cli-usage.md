---
order: 1
title: Aop Cli
groupOrder: 1
group: 快速上手
---

## Aop Cli

Create ISV Plugin with no build configuration.

精于心，简于形。不需书写任何webpack配置文件，即可创建完整的ISV插件。
* [创建一个插件](#creating-an-plugin) – 如何创建一个新的插件。


## 安装
安装开发工具 `aop-cli`

```sh
npm i -g aop-cli
```

## 快速开始

```sh
aop cert
aop init myApp
cd myApp
aop dev
```

## 创建一个新的插件

**你本机的Node版本必须 >= `7.10.1`**。你能够利用 [nvm](https://github.com/creationix/nvm#installation) (macOS/Linux) 或 [nvm-windows](https://github.com/coreybutler/nvm-windows#node-version-manager-nvm-for-windows) 来快速切换Node版本。

创建一个新的插件，运行命令:

```sh
aop cert
aop init myApp
cd myApp
aop dev

````

开发工具会在当前路径下创建一个新的目录：myApp, 在此目录下，开发工具会初始化应用骨架，应用的文件结构为：


```sh
.myApp
├── README.md
├── build
│   └── vendor.dll.js
├── build.sh
├── common
│   └── index.scss
├── custom.config.js
├── example
│   └── index.html
├── index.js
├── layout
│   ├── components
│   │   ├── Main
│   │   │   ├── index.jsx
│   │   │   └── index.scss
│   │   └── theme
│   │       ├── navigation-dark.scss
│   │       └── navigation-light.scss
│   ├── index.jsx
│   └── index.scss
├── package.json
├── page
│   ├── page1
│   │   ├── components
│   │   │   └── card
│   │   │       ├── index.jsx
│   │   │       └── index.scss
│   │   └── index.js
│   └── page2
│       ├── components
│       │   └── form
│       │       ├── index.jsx
│       │       └── index.scss
│       └── index.js
└── routes.jsx

```


新插件初始化成功后，你就可以愉快地开发和构建了：

### `aop cert`

安装HTTPS证书，解决证书信任问题，安装过程中可能需要输入用户密码。


### `aop dev`

在运行此命令前，请确定你绑定了如下的Host:
```sh
127.0.0.1	localhost
127.0.0.1    g.alicdn.com
```

`aop dev` 将会启动一个Dev Sever，在开发环境下构建代码。<br>

开发工具会自动在浏览器中打开[https://page.1688.com/html/isv-bridge.html?appKey=appKey&version=1.0.0](https://page.1688.com/html/isv-bridge.html?appKey=appKey&version=1.0.0) ，你可以在此预览你的插件。

当你对你的代码（JS 、CSS）做出改动后，页面将会自动刷新。如果在打包过程中有错误发生，错误信息会在控制台打印出来。


### `aop build`

构建用于在生产环境中使用的代码，会执行一些代码优化，比如压缩去重等等。构建的代码将会在`/build`目录下。


## Tips 

- 应用名称不要输入中文，`package.json`不支持中文的`name`字段，只能是字幕、数字、下划线、连接符的组合。


---

使用中遇到任何问题，欢迎加群交流：

![](https://img.alicdn.com/tfs/TB1jsGahx9YBuNjy0FfXXXIsVXa-364-480.png)

如有如何开发建议和需求，欢迎钉钉联系开发者`刘甲`、`赵泰`。