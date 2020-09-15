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
