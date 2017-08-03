## 简介
单线程`Node.js`代理中间件，用于连接，快速和浏览器同步
`node.js`代理简单。轻松配置代理中间件连接、快速、浏览器同步等。

由流行的Nodejitsu http代理提供


## 兼容
```
http-proxy-middleware is compatible with the following servers:

connect
express
browser-sync
lite-server
grunt-contrib-connect
grunt-browser-sync
gulp-connect
gulp-webserver
```
```js
// 兼容koa2

// setup ---
// node v7.7.1
// koa v2.2.0
// koa-router v7.1.1
// koa2-connect v1.0.2
// http-proxy-middleware v0.17.4
// -------

// example
const Koa = require('koa');
const Router = require('koa-router');
const proxy = require('http-proxy-middleware');
const c2k = require('koa2-connect');
const app = new Koa();

const router = new Router();
router.get(
  '/',
  c2k(
    proxy({
      target: 'https://api.github.com/',
      changeOrigin: true
    })
  )
);

router.get(
  '*',
  c2k(
    proxy({
      target: 'https://api.github.com/',
      changeOrigin: true
    })
  )
);

app.use(router.routes());
app.listen(3000);

// `/` 代理root
// '*' 代理所有
```


## API 介绍

### Core concept

##### proxy([context,] config)
```js
var proxy = require('http-proxy-middleware');

var apiProxy = proxy('/api', {target: 'http://www.example.org'});
//                   \____/   \_____________________________/
//                     |                    |
//                   context             options

// 'apiProxy' is now ready to be used as middleware in a server.
```
- context: 确定应将哪些请求代理到目标主机
- options.target: 目标主机到代理。（协议+主机）


##### proxy(uri [,config])
```js
// shorthand syntax for the example above:
var apiProxy = proxy('http://www.example.org/api');
```


### Example (express example)
```js
// include dependencies
var express = require('express');
var proxy = require('http-proxy-middleware');

// proxy middleware options
var options = {
        target: 'http://www.example.org', // target host
        changeOrigin: true,               // needed for virtual hosted sites
        ws: true,                         // proxy websockets
        pathRewrite: {
            '^/api/old-path' : '/api/new-path',     // rewrite path
            '^/api/remove/path' : '/path'           // remove base path
        },
        router: {
            // when request.headers.host == 'dev.localhost:3000',
            // override target 'http://www.example.org' to 'http://localhost:8000'
            'dev.localhost:3000' : 'http://localhost:8000'
        }
    };

// create the proxy (without context)
var exampleProxy = proxy(options);

// mount `exampleProxy` in web server
var app = express();
    app.use('/api', exampleProxy);
    app.listen(3000);
```


### Context matching
RFC 3986路径用于上下文匹配。
```
foo://example.com:8042/over/there?name=ferret#nose
\_/   \______________/\_________/ \_________/ \__/
 |           |            |            |        |
scheme     authority       path        query   fragment
```
- 路径匹配
  - `proxy({...})` - 匹配任意路径，所有的请求都会被代理。
  - `proxy('/', {...})` - 匹配任意路径，所有的请求都会被代理。
  - `proxy('/api', {...})` - 匹配所有以/api开始的路径。
- 多重路径匹配
  - `proxy(['/api', '/ajax', '/someotherpath'], {...})`
- 通配符路径匹配 (对于细粒度控制，您可以使用通配符匹配。通过micromatch进行全局模式匹配。访问micromatch或glob更多globbing示例。)
  - `proxy('**', {...})` - 匹配任意路径，所有的请求都会被代理。
  - `proxy('**/*.html', {...})` - 匹配所有以.html结尾的任意路径。
  - `proxy('/*.html', {...})` - 直接匹配绝对路径下的路径。
  - `proxy('/api/**/*.html', {...})` - 匹配在/api路径下以.html结尾的请求。
  - `proxy(['/api/**', '/ajax/**'], {...})` - 组合多重路由模式。
  - `proxy(['/api/**', '!**/bad.json'], {...})` - 排除匹配。
- 自定义匹配 (为了完全控制，您可以提供一个自定义函数来确定哪些请求应该被代理。)
```js
/**
 * @return {Boolean}
 */
var filter = function (pathname, req) {
    return (pathname.match('^/api') && req.method === 'GET');
};

var apiProxy = proxy(filter, {target: 'http://www.example.org'})
```


### [Options](https://www.npmjs.com/package/http-proxy-middleware#options)

### 参考文档
- [npmjs](https://www.npmjs.com/package/http-proxy-middleware)
- [github](https://github.com/chimurai/http-proxy-middleware)
- [csdn](http://blog.csdn.net/xmloveth/article/details/56847456)
- [sf](https://segmentfault.com/a/1190000009821129)
