## Router

react相关的路由



### react-router



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



