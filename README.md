# react 开发 GitHub

## 项目依赖包

```json
"dependencies": {
    "@zeit/next-css": "^1.0.1",
    "antd": "^3.13.6",
    "atob": "^2.1.2",
    "axios": "^0.18.0",
    "babel-plugin-import": "^1.11.0",
    "cross-env": "^5.2.0",
    "debug": "^4.1.1",
    "http-proxy": "^1.17.0",
    "ioredis": "^4.6.2",
    "koa": "^2.7.0",
    "koa-router": "^7.4.0",
    "koa-session": "^5.10.1",
    "lru-cache": "^5.1.1",
    "markdown-it": "^8.4.2",
    "next": "^8.0.3",
    "nprogress": "^0.2.0",
    "react": "^16.8.3",
    "react-dom": "^16.8.3",
    "react-redux": "^6.0.1",
    "redux": "^4.0.1",
    "redux-devtools-extension": "^2.13.8",
    "redux-thunk": "^2.3.0"
  }
```

## nextjs 项目的创建

- 手动创建
  - 安装 react react-dom nextjs 依赖
  - 在目录 pages 下添加页面
- create-next-app
  - `npx create-next-app <projectName>`
  - `yarn create next-app <projectName>`
  - `create-next-app <projectName>`

## nextjs 作为 koa 的中间件使用

- nextjs 自带的服务器只是处理 ssr 渲染 , 无法处理 数据接口 , 数据库连接 , session 状态
- 实际服务器需要处理 HTTP 请求 , 并根据请求数据返回相应内容 , 还需要根据域名之类的 HOST 来定位服务器

## 安装 redis 数据库

### Windows

官方没有 Windows 包 , 是由微软创建 : <https://github.com/microsoftarchive/redis/releases>

版本比较老 , 建议下载 3.0.504 稳定版

安装之后 会自动添加到 Windows 的服务中自启动 , 如果想手动启动可以执行 安装目录下的 `.\redis-server.exe .\redis.windows.conf` , 记住要指定 Windows 上的配置文件

判断 redis 服务是否启动 : 在安装目录下 `.\redis-cli.exe` 或 在任意路径(因为安装时已经添加到环境变量中了)`redis-cli`

### redis 基本使用

是基于协议的使用方式 , 启动了 redis-server 之后 , 可以使用 redis-cli 连接数据库 , 同时可以使用不同语言的 SDK 连接数据库.

- redis 数据库是 **内存数据结构存储**
- 可持久存储
- 支持多种数据结构
- 连接数据库后 , 在命令行中 `set` 是存储 , `get` 是获取
- `setex` : 给某一个 key 设置过期时间 , 例如 `setex c 10 1` 意思是 key c 的值是 1 , 在 10 秒后过期.
- `KEYs *` : 获取所有存储的 key
- `DEL <key>` : 删除某个 key

#### 给 redis 设置密码

- 打开 redis.windows.conf 的文件
- 在配置文件中找到 requirepass 后面注释的部分是密码
- 可更改 端口 port 启动另外一个 redis 服务
- 在 redis 目录下启动 `.\redis-server.exe .\redis.windows.conf`
- 连接数据库 : `redis-cli -p <port>`
- 密码认证 : `auth <password>`

#### nodejs 连接 redis 数据库

- 可以使用模块 : ioredis , `yarn add ioredis`

```js
async function test() {
  const Redis = require('ioredis')

  const redis = new Redis({
    port: 6378,
    password: 123456
  })

  await = redis.setex('c', 10, 123)
  const keys = await redis.keys('*')
  console.log(await redis.get('c'))
}
```

## nextjs 集成 antd

一些问题:

- nextjs 默认不支持 css import
- 需要根据 nextjs 提供的插件机制支持 css import
- 创建 `next.config.js` 文件 , 这是 nextjs 的整体配置文件
- 然后安装 `@zeit/next-css` , 用于加载 css

## Nextjs 基础

### nextjs 目录结构

- pages
  - 所有的文件对应一个页面 , `_app.js` 和 `_document.js` 是例外
- components
  - 公用组件
- lib
  - 非组件型的公用型代码 , 比如 utils
- static
  - 图片
- .next
- next.config.js
  - nextjs 相关配置文件

### 路由基础

#### Link

进行前端路由跳转

```js
import Link from 'next/link';

export default () =>
(  <Link href='/a'>
    <button>a</button>
  </Link>;
);
```

Link 本身没有任何标签 , 只是监听了点击事件.

#### Router 模块

手动跳转

```js
import Router from 'next/router';

export default () => {
  function gotoTestB() {
    Router.push('/test/b');
  }
  return <button onClick={gotoTestB}>a</button>;
};
```
