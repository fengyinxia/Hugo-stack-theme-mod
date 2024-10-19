---
title: "React项目（仿airbnb）"
date: 2024-02-13T03:02:52+08:00
lastmod: 2024-02-13T03:02:52+08:00
description: 掘金搬运的，这项目是对 React 知识点一个全面的练习和汇总
tags:
  - 技术
categories:
  - React18
image:
slug: stack-theme-mod
---

## 项目介绍

这个项目是仿照爱彼迎（租房）官网写的一个项目，用了 React18、Router、Redux、styled-component 等技术实现，整个项目全面拥抱 Hooks 组件写法。

## 核心知识点

这次项目是对 React 知识点一个全面的练习和汇总，主要学习 React 的开发模式和编程思想，如 React 的开发流程、模式、项目架构，项目中的组件、工具的封装、抽取、复用的思想，以及学习整体代码如何组织。

1.  对于第一个 React 项目，我们的核心是对前面所学知识进行练习、实战；
2.  掌握 React 开发的流程、模式、项目架构，项目中会有很多组件、工具等封装、抽取、复用思想。
3.  最重要的是学习 React 开发的模式和编程的思想，而不是局限于我上课期间所讲的内容，并且大部分样式和布局内容需要大家课程自行完成。
4.  在这个项目过程中，我会尽量将之前所学的所有知识都运用起来，但是我们不会为了用某个知识而用某个知识。
5.  课程中会使用我服务器已经获取到的数据，一是国内的数据更好看，二是担心它数据有一天不再维护，三是我对数据已经进行了大量的整理。
6.  后续我们还会专门学习 React+TypeScript 项目实战的内容，React 本身非常的灵活，对 JavaScript 本身要求也较高，但是最重要的还是练习。

## 项目规范

项目中的开发规范和代码风格如下：

1.  文件夹、文件名称统一小写、多个单词以连接符（-）连接。
2.  JavaScript 变量名称采用小驼峰标识，常量全部使用大写字母，组件采用大驼峰。
3.  CSS 采用普通 CSS 和 styled-component 结合来编写（全局采用普通 CSS、局部采用 styled-component）。
4.  整个项目不再使用 class 组件，统一使用函数式组件，并且全面拥抱 Hooks。
5.  所有的函数式组件，为了避免不必要的渲染，全部使用 memo 进行包裹。
6.  组件内部的状态，使用 useState、useReducer；业务数据全部放在 redux 中管理。
7.  函数组件内部基本按照如下顺序编写代码：

· 组件内部 state 管理； · redux 的 hooks 代码； · 其他 hooks 相关代码（比如自定义 hooks）； · 其他逻辑代码； · 返回 JSX 代码。

8.  redux 代码规范如下：

· redux 目前我们学习了两种模式（普通和 RTK），在项目实战中尽量两个都用起来，都需要掌握； · 每个模块有自己独立的 reducer 或者 slice，之后合并在一起； · redux 中会存在共享的状态、从服务器获取到的数据状态；

9.  网络请求采用 axios

· 对 axios 进行二次封装； · 所有的模块请求会放到一个请求文件中单独管理。

10. 项目使用 AntDesign、MUI（Material UI）

· 爱彼迎本身的设计风格更多偏向于 Material UI，但是课程中也会尽量讲到 AntDesign 的使用方法； · 项目中某些 AntDesign、MUI 中的组件会被拿过来使用； · 但是多部分组件还是自己进行编写、封装、实现。 其他规范在项目中根据实际情况决定和编写。

## 创建和配置

通过 create-react-app name 创建项目。 项目配置：

- 配置项目的 icon
- 配置项目的 title
- 配置 jsconfig.json（vscode 代码提示）

通过 craco 配置别名和 less 文件： craco 部分：

1.  下载 craco
2.  创建 craco.config.js
3.  更新 scripts 中的 script

![image.png](https://p6-xtjj-sign.byteimg.com/tos-cn-i-73owjymdk6/f92c4aa99e1a424cb041413210490ae6~tplv-73owjymdk6-jj-mark-v1:0:0:0:0:5o6Y6YeR5oqA5pyv56S-5Yy6IEAg5ZCs6Zuo6ZiB5qW85Lit:q75.awebp?rk3s=f64ab15b&x-expires=1729604083&x-signature=OvBrOETEglX7MwmcEW3uSyuIRbo%3D) 别名配置部分：

- 引入 node 里的 path 模块来获取当前文件路径，然后通过 path 中的 resolve 方法拼接路径

less 配置部分：

- 下载 less：npm i craco-less
- 通过 plugins 安装 less 库

config 中的具体代码如下：

```jsx
// craco.config.js
const path = require("path");
const cracoLessPlugin = require("craco-less");

const resolve = (pathname) => path.resolve(__dirname, pathname);

module.exports = {
  // plugins安装less
  plugins: [
    {
      plugin: cracoLessPlugin,
    },
  ],

  // webpack
  webpack: {
    alias: {
      "@": resolve("src"),
      components: resolve("src/components"),
      utils: resolve("src/utils"),
    },
  },
};
```

## 重置样式

通过 normalize.css 库以及自己手动在 reset.css 中重置样式，在 variable 中可以定制一些主题色变量，然后在 index.css 导入 reset.css 让 index.css 作为样式入口。 normalize.css：

- npm i normalize.css
- 在 index.js 中引入

reset.css：

```css
@import "./variables.less";

body,
button,
dd,
dl,
dt,
form,
h1,
h2,
h3,
h4,
h5,
h6,
hr,
input,
li,
ol,
p,
pre,
td,
textarea,
th,
ul {
  padding: 0;
  margin: 0;
}

a {
  color: @textColor;
  text-decoration: none;
}

img {
  vertical-align: top;
}

ul,
li {
  list-style: none;
}
```

variable.less：

```less
/* less -> @ ; scss -> $ */
@textColor: #484848;
@textColorSecondary: #222;
```

index.less： 全局使用：在 index.js 中引入

```less
@import "./reset.less";
```

## 配置 Router

### router 下载

需要下载 router：npm i react-router-dom。 在 index.js 中引入 HashRouter 或者 BrowserRouter 组件包裹 。

```jsx
import React, { Suspense } from "react";
import ReactDOM from "react-dom/client";
import { HashRouter } from "react-router-dom";

import App from "./App";
import "normalize.css";
import "./assets/css/index.less";

const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(
  <React.StrictMode>
    <Suspense fallback="loading...">
      <HashRouter>
        <App />
      </HashRouter>
    </Suspense>
  </React.StrictMode>
);
```

### 划分页面/配置路由

- 在 app 文件的 jsx 中划分页面结构，如 header、main、footer 等
- 在 router 的 routes 文件中配置路由映射
- 在 app 文件中需要路由的部分通过 useRoutes hook 传入映射

```jsx
import React, { memo } from "react";
import { useRoutes } from "react-router-dom";

import routes from "./router/routes";

const App = memo(() => {
  return (
    <div className="app">
      <div className="header">header</div>
      <div className="page">{useRoutes(routes)}</div>
      <div className="footer">footer</div>
    </div>
  );
});

export default App;
```

### 组件的异步加载

组件的异步加载（也称为代码分割）是 Webpack、Rollup 或其他模块打包工具的功能，这些工具允许你将你的应用分割成多个包，并在需要时动态加载它们。这样做的主要目的是优化应用的加载时间和性能，特别是当应用变得非常大时。

- 更快的加载时间：通过只加载用户首次访问时所需的代码，可以减少应用的初始化时间。
- 按需加载：用户只下载实际需要查看或交互的页面和组件的代码。
- 缓存优化：浏览器可以缓存已下载的包，用户再次访问时可以更快的加载已下载的部分。

React Router 提供了几种方式来结合使用异步加载的组件。最常见的方法是使用 React 的 React.lazy() 和 Suspense 组件。

- React.lazy()：允许你定义一个动态导入的组件。这个组件将自动处理模块的加载。
- Suspense：是一个可以让你在组件树中“等待”某些异步操作完成的组件，如加载组件。它可以用来在加载时显示一个备用的 UI（如加载指示器）。
- 为什么需要用 Suspense 包裹：

Suspense 组件提供了一个“等待”的边界，告诉 React 在这个边界内的组件树中，如果某个组件正在加载，应该如何处理。 将 Suspense 包裹在 App 组件（或任何父组件）周围，是为了在应用级别提供一个统一的加载指示器处理机制，确保所有懒加载的组件都能以一致的方式处理加载状态。

### 配置映射

navigater 组件用来重定向，映射对象包含 path、element、children 属性

```javascript
import React from "react";
import { Navigate } from "react-router-dom";

const Home = React.lazy(() => import("@/views/home"));
const Detail = React.lazy(() => import("@/views/detail"));
const Entire = React.lazy(() => import("@/views/entire"));

const routes = [
  {
    path: "/",
    element: <Navigate to="/home" />,
  },
  {
    path: "/home",
    element: <Home />,
  },
  {
    path: "/detail",
    element: <Detail />,
  },
  {
    path: "/entire",
    element: <Entire />,
  },
];

export default routes;
```

## 配置 Redux

1 .下载 redux/tookit：npm i @redux/tookit react-redux 2 .配置 store：configureStore

```jsx
import { configureStore } from "@reduxjs/toolkit";

import homeReducer from "./modules/home";
import entireReducer from "./modules/entire";

const store = configureStore({
  reducer: {
    home: homeReducer,
    entire: entireReducer,
  },
});

export default store;
```

3 .在 index.js 入口文件中引入：Provider store=store

```jsx
import React, { Suspense } from "react";
import ReactDOM from "react-dom/client";
import { HashRouter } from "react-router-dom";
import { Provider } from "react-redux";

import App from "./App";
import "normalize.css";
import "./assets/css/index.less";
import store from "./store";

const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(
  <React.StrictMode>
    <Suspense fallback="loading...">
      <Provider store={store}>
        <HashRouter>
          <App />
        </HashRouter>
      </Provider>
    </Suspense>
  </React.StrictMode>
);
```

4 .单文件 store 配置 toolkit 方式：createSlice

```jsx
// home.js

import { createSlice } from "@reduxjs/toolkit";

const homeSlice = createSlice({
  name: "home",
  initialState: {
    productList: [],
  },
  reducers: {},
});

export default homeSlice.reducer;
```

普通方式：创建 4 个文件

- constants.js：存放用的常量
- createActions.js：存放用的 action
- index.js：统一出口
- reducer.js：reducer 配置

```jsx
// index.js
import reducer from "./reducer";

export default reducer;
```

```jsx
// reducer.js
const initialState = {
  currentPage: 3,
};

function reducer(state = initialState, action) {
  switch (action.type) {
    default:
      return state;
  }
}

export default reducer;
```

## 配置 axios

下载 axios：npm i axios 在 request 的 index.js 中封装代码，在 request 的 config 中配置 baseURL 和 timeout，然后在最外层的 index.js 中统一导出。 config：

```jsx
const BASE_URL = "";
const TIMEOUT = 10000;

export { BASE_URL, TIMEOUT };
```

request -> index.js

```jsx
import axios from "axios";
import { BASE_URL, TIMEOUT } from "./config";

class DuRequest {
  constructor(baseURL, timeout = 10000) {
    this.instance = axios.create({ baseURL, timeout });

    this.instance.interceptors.response.use(
      (res) => {
        return res.data;
      },
      (err) => {
        return err;
      }
    );
  }

  request(config) {
    return this.instance.request(config);
  }

  get(config) {
    return this.request({ ...config, method: "GET" });
  }

  post(config) {
    return this.request({ ...config, method: "POST" });
  }
}

export default new DuRequest(BASE_URL, TIMEOUT);
```

最外层的 index.js

```jsx
import DuRequest from "./request";

export default DuRequest;
```

使用案例：

```jsx
import React, { memo, useState, useEffect } from "react";
import DuRequest from "@/services";

const Home = memo(() => {
  // 定义状态
  const [highScore, setHighScore] = useState([]);

  // 网络请求的代码
  useEffect(() => {
    DuRequest.get({ url: "/home/highscore" }).then((res) => {
      console.log(res);
      setHighScore(res);
    });
  }, []);

  return (
    <div>
      <h2>{highScore.title}</h2>
      <h4>{highScore.subtitle}</h4>
      <ul>
        {highScore.list?.map((item) => {
          return <li key={item.id}>{item.name}</li>;
        })}
      </ul>
    </div>
  );
});

export default Home;
```
