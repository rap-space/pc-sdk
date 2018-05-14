---
order: 1
title: 快速开始
groupOrder: 1
group: 快速上手
---

## Rap Cli


1688开放平台集PC与无线通用的开发工具
* [创建一个插件](#creating-an-plugin) – 如何创建一个新的插件。


## 安装
安装开发工具 https://github.com/rap-space/rap-cli/releases

Mac上安装时，需要在系统中放开权限。
![](https://img.alicdn.com/tfs/TB17WgQreSSBuNjy0FlXXbBpVXa-1348-1198.png)
![](https://img.alicdn.com/tfs/TB1bd7QreSSBuNjy0FlXXbBpVXa-1328-1128.png)

然后安装

## 快速开始

1. 授权Https
    ```
    rap cert
    ```

2. 初始化工程
    ```
    mkdir ${yourproject}
    cd ${yourproject}
    rap init
    ```
    选择 PC，起一个名字，填自己的 appkey

    ![](https://img.alicdn.com/tfs/TB1nRy4rDtYBeNjy1XdXXXXyVXa-976-516.png)


## 开始开发

开发工具会在当前路径下创建一个新的目录：${yourproject}, 在此目录下，开发工具会初始化应用骨架，应用的文件结构为：


```sh
.${yourproject}
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

### `rap dev`

在运行此命令前，请确定你绑定了如下的Host:
```sh
127.0.0.1	localhost
127.0.0.1    g.alicdn.com
```

`rap dev` 将会启动一个Dev Sever，在开发环境下构建代码。<br>

开发工具会自动在浏览器中打开[https://page.1688.com/html/isv-bridge.html?appKey=appKey&version=1.0.0](https://page.1688.com/html/isv-bridge.html?appKey=appKey&version=1.0.0) ，你可以在此预览你的插件。


当你对你的代码（JS 、CSS）做出改动后，页面将会自动刷新。如果在打包过程中有错误发生，错误信息会在控制台打印出来。


### 编码过程中的一些说明

#### 1. 最终产出的入口文件
最终产出三个入口文件会被引入到工作台沙箱中，分别是 index.js, index.css, vendor.dll.js
```
├── build
│   ├── index.css
│   ├── index.js
│   └── vendor.dll.js
```



#### 2. 能力:
官方会提供访问1688工作台能力的 SDK，在代码中通过以下形式调用

```javascript
window.bridge.call('open.api.request', {
    version: '1',
    namespace: 'com.alibaba.product',
    name: 'alibaba.product.get',
    data: {
        productID: 54321,
        webSite: '1688'
    }
}, (res) => {
    console.log(res);
});
```

**SDK的方法**

| 方法名 | 参数 | 说明 | 类型 | 默认值
| ----- | -----|-----|-----|-----
| call | name, params, cb | 调用1688工作台提供的服务, name为服务名， params是参数， cb是回调函数 | String, Object | 无

**SDK目前可调用的服务**

服务名 | 参数 | 说明 | 类型 | 默认值 | 备注 | 参考文档
----- | -----|-----|-----|----- | --- | ---
open.api.request | cfg | 调用开放平台的API，内部包含5个参数{version, namespace, name, appkey, data} | Object | 无 | 5个参数对应开放平台API的参数 | [开放平台API文档](https://open.1688.com/api/api.htm?ns=com.alibaba.product&n=alibaba.product.get&v=1&cat=product_new)
open.api.proxy | cfg | 通过开放平台网关调用isv自己服务器的API，参数同 [fetch](https://developer.mozilla.org/zh-CN/docs/Web/API/Fetch_API/Using_Fetch)，body 无需 stringify，用户信息会在 http header 中自动附加，用 userId 字段标识 | Object | 无 | 参数与fetch相同 | 无

#### 例子 ：
[开放平台API文档](https://open.1688.com/api/api.htm?ns=com.alibaba.product&n=alibaba.product.get&v=1&cat=product_new)

**API文档和参数的对照说明**

![](https://img.alicdn.com/tfs/TB12tJDrv1TBuNjy0FjXXajyXXa-960-662.png)


```javascript
window.bridge.call('open.api.request', {
    version: '1',
    namespace: 'com.alibaba.product',
    name: 'alibaba.product.get',
    data: {
        productID: 54321,
        webSite: '1688'
    }
}, (res) => {
    console.log(res);
});

window.bridge.call('open.api.proxy', {
    url: 'http://gw.open.1688.com/openapi/param2/1/system/currentTime/1323',
    method: 'GET',
    // headers: {},
    // body: {}
}, (res) => {
    this.setState({
        txt: JSON.stringify(res)
    });
});
```


## 打包与上传

### `rap build`

构建用于在生产环境中使用的代码，会执行一些代码优化，比如压缩去重等等。构建的代码将会在`/build`目录下。


### `rap archive`

上传前要进行的打包操作，会剔除掉 ./build 和 ./node_modules 目录，并打包成云构建服务可识别的格式。

**通过系统上传需要上传用该命令打包后的文件。**

## Tips

- 应用名称不要输入中文，`package.json`不支持中文的`name`字段，只能是字幕、数字、下划线、连接符的组合。


---

关于开发者工具使用中的任何问题，欢迎加群交流：

![](https://img.alicdn.com/tfs/TB1jsGahx9YBuNjy0FfXXXIsVXa-364-480.png)

如有如何开发建议和需求，欢迎钉钉联系开发者`刘甲`、`赵泰`。
