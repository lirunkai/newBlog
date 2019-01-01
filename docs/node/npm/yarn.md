# yarn

yarn类似npm的一种方式

## 初始化

`yarn init -y`

## 添加一个包  `yarn add package`

## 移除一个包  `yarn remove package`

## 更新一个包 `yarn upgrade package`

### 安装参数

`yarn add package` 默认安装到`dependencies` 常规依赖, 代码运行时所需要的

`--dev`    **devDependencies**     开发依赖

`--peer`   **peerDependencies**     这是“同伴依赖”，一种特殊的依赖，在发布包的时候需要

`--optional`    **optionalDependencies**   可选依赖

## 安装全部依赖  `yarn install` or `yarn`

    可选参数

    1. `--force` 强制重新下载所有包
    2. `--production` 只安装生产环境的包


## 全局安装 `yarn global add package` `yarn global upgrade`

## 缓存的修改 `yarn cache clean package` or `yarn cache clean`

### 工作区

在使用npm的过程中, 每个
