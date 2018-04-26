---
order: 2
title: Just脚手架升级到aop脚手架
groupOrder: 1
group: 快速上手
---

# Just脚手架升级到aop脚手架

## 步骤
1. 如果没安装 aop-cli, 请先安装 aop-cli。

    > 要求 Node >= 7，可以使用 [nvm](https://github.com/creationix/nvm) 解决机器上多 node 版本共存的问题。

2. `npm install aop-cli -g`

    aop-cli 是由开放平台出品的专门为isv开发者提供的脚手架工具，暂时提供3个命令
    1. `aop init myapp` 初始化工程目录和示例代码
    2. `aop dev` 启动开发
    3. `aop build` 打包代码

3. 修改 package.json
   ![](media/15223215602907/15223219359947.jpg)

4. 在工程目录下添加 custom.config.js，并写入如下内容

    ```javascript
    // webpack 自定义配置文件，请勿删除！
    module.exports = function (webpack, context) {
        return {
            loaders: {}, // 配置loader 
            plugins: [], // 插件
            uglify: true, // 是否压缩
            externals: {
                'react': 'var window.React',
                'react-dom': 'var window.ReactDOM'
            }, // 需要从外部CND引入的JS包
            polyfill: false, // 打包是否包括 polyfill
            dll: ['qnui', 'react-router'], // 是否启动DllPlugin
            proxy: {} // 配置代理
        }
    }
    ```
    ![](media/15223215602907/15223998782123.jpg)


5. 执行 `aop cert`，安装 https 证书
6. 执行 `aop dev`，会直接打开宿主环境页面。
![](media/15223215602907/15223233170658.jpg)

7. 开始开发吧！
<br>
<br>


---

**有任何问题，请加钉钉群 21738069 
联系 @赵泰 @刘甲**

![](media/15223215602907/15223247965174.jpg)



