---
order: 3
title: SDK与API介绍
groupOrder: 1
group: 快速上手
---

## sdk与API介绍
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
open.api.proxy | cfg | 通过开放平台网关调用isv自己服务器的API，参数同 [fetch](https://developer.mozilla.org/zh-CN/docs/Web/API/Fetch_API/Using_Fetch)，body 无需 stringify，用户信息携带见下 | Object | 无 | 参数与fetch相同 | 无

#### 用户信息
- ISV发起的代理请求需要设置X-Request-Auth: UserId/AES
- 网关发给目标URL会带上头部
  - X-UserId： xxxx，
  - X-UserId-Encode：AES/Base64


AES加密规则：
- AES模式AES/ECB/PKCS5Padding
- 密钥
  - 由app密钥得到utf-8编码的字符数组
  - 如果数据长度等于16，则直接作为AES密钥
  - 如果长度大于16，则取前16个字节
  - 如果小于16，则补0到16个字节
- AES得到的密文通过Base64得到字符串


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
    headers: {
        'X-Request-Auth: ': 'UserId/AES'
    },
    // body: {}
}, (res) => {
    this.setState({
        txt: JSON.stringify(res)
    });
});
```
