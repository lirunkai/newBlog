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

在使用npm的过程中, 每个项目都会根据自己的依赖生成自己的`node_modules`.

比如使用工作区之前, 我们的结构是这样的

```
-- workDir

  -- workDirA

    -- node_modules

    -- package.json

  -- workDirB

    -- node_modules

    -- package.json

```

使用工作区之后

```
-- workDir

  --node_modules

  --package.json

  -- workDirA

    -- package.json

  -- workDirB

    -- package.json

```

#### 使用工作区

在根目录下`yarn init`， 然后添加`private: true`到`package.json`内.

添加工作区 添加`workspaces: ['workDirA', 'workDirB']`， 这里我们添加了两个工作区 `workDirA`， `workDirB`

之后如果在`workDirA`或者`workDirB`里添加依赖 `yarn add package`, 不变的是`package.json`里的内容还会添加, 但是不在`workDirA`里生成`node_modules`了, 在根目录内生成了`node_modules`.
