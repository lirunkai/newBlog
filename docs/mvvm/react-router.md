## Router

react相关的路由

### react-router-dom

安装

`yarn add react-router-dom`

使用

```react
import React from "react";
import { BrowserRouter as Router, Route, Link } from "react-router-dom";

function Index() {
  return <h2>Home</h2>;
}

function About() {
  return <h2>About</h2>;
}

function Users() {
  return <h2>Users</h2>;
}

function AppRouter() {
  return (
    <Router>
      <div>
        <nav>
          <ul>
            <li>
              <Link to="/">Home</Link>
            </li>
            <li>
              <Link to="/about/">About</Link>
            </li>
            <li>
              <Link to="/users/">Users</Link>
            </li>
          </ul>
        </nav>

        <Route path="/" exact component={Index} />
        <Route path="/about/" component={About} />
        <Route path="/users/" component={Users} />
      </div>
    </Router>
  );
}

export default AppRouter;


```

**match参数获取**

`params` `url` `isExact` `path`

**跳转**

`props.history.push('/')`

**Redirect** 重定向

**Link**

**NavLink** 可以修改Link的样式

**BrowserRouter** 提供一个Provider

**Route** 配置展示的route

**Switch** 检索到第一个匹配的route进行展示
 
**HashRouter**

**withRouter(component)** 传入的props有修改组件会重新渲染

### react-router-config

#### renderRoutes(routes, extraProps={}, switchProps={})

根据routes渲染Route

源码很简单

```react
import React from "react";
import { Switch, Route } from "react-router";

function renderRoutes(routes, extraProps = {}, switchProps = {}) {
  return routes ? (
    <Switch {...switchProps}>
      {routes.map((route, i) => (
        <Route
          key={route.key || i}
          path={route.path}
          exact={route.exact}
          strict={route.strict}
          render={props =>
            route.render ? (
              route.render({ ...props, ...extraProps, route: route })
            ) : (
              <route.component {...props} {...extraProps} route={route} />
            )
          }
        />
      ))}
    </Switch>
  ) : null;
}

export default renderRoutes;
```

#### matchRoutes(routes, pathname, branch=[])

根据pathname检索routes, 如果有则返回.

源码

```react

import { matchPath, Router } from "react-router";

function matchRoutes(routes, pathname, /*not public API*/ branch = []) {
  routes.some(route => {
    const match = route.path
      ? matchPath(pathname, route)
      : branch.length
        ? branch[branch.length - 1].match // use parent match
        : Router.computeRootMatch(pathname); // use default "root" match

    if (match) {
      branch.push({ route, match });

      if (route.routes) {
        matchRoutes(route.routes, pathname, branch);
      }
    }

    return match;
  });

  return branch;
}

export default matchRoutes;
```



