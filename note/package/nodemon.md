## 简介



## 基本配置
- `restartable` - 重启的命令，默认是 `rs` ，可以改成你自己喜欢的字符串。当用 `nodemon` 启动应用时，可以直接键入 `rs` 直接重启服务。除了字符串值外，还可以设置 `false` 值，这个值的意思是当 `nodemon` 影响了你自己的终端命令时，设置为 `false` 则不会在 `nodemon` 运行期间监听 `rs` 的重启命令。
- `ignore` - 忽略的文件后缀名或者文件夹，文件路径的书写用相对于 `nodemon.json` 所在位置的相对路径，下同。`nodemon` 会默认忽略一些文件，默认忽略的文件有：``.git, node_modules, bower_components, .sass-cache`，如果这些文件想要加入监控，需要重写默认忽略参数字段 ignoreRoot，比如加入：`"ignoreRoot": [".git", "bower_components", ".sass-cache"]`，然后在 `watch` 中将 `node_modules` 文件路径加入监控，那么 `node_modules` 内的文件也加入了监控了。
- `verbose` - `true` 表示输出详细启动与重启信息,`false` 表示不输出这些运行信息
- `execMap` - 运行服务的后缀名和对应的运行命令，`"js": "node --harmony"` 表示用 `nodemon` 代替 `node  --harmony` 运行 `js` 后缀文件；"" 指 www 这些没有后缀名的文件；默认的 `defaults.js` 配置文件会识别一些文件：`py: 'python',rb: 'ruby'`。
- `watch` - 监控的文件夹路径或者文件路径。
- `env` - 运行环境 `development` 是开发环境，`production` 是生产环境。`port` 是端口号。
- `ext` - 运行环境 `development` 是开发环境，`production` 是生产环境。`port` 是端口号。
  - 注：关于监控以及忽略文件修改有个顺序的问题，或者说优先级，首先 `nodemon` 会先读取 `watch` 里面需要监控的文件或文件路径，再从文件中选择监控 `ext` 中指定的后缀名，最后去掉从 `ignore` 中指定的忽略文件或文件路径。
- `legacy-watch` - `nodemon` 使用 `Chokidar` 作为底层监控系统，但是如果监控失效，或者提示没有需要监控的文件时，就需要使用轮询模式（polling mode），即设置 `legacy-watch` 为 `true`
- `colous` - 输出信息颜色标示。
- `runOnChangeOnly` - `true` 时运行 `nodemon www` 项目不会启动，只保持对文件的监控，当监控的文件有修改并保存时才会启动应用，其他没有影响。默认是 `false` 即一开始就启动应用并监控文件改动。
- `stdin` `stdout` - 这个是关于标准输入输出的设置，上文提到 `nodemon.json` 文件中的 `events` 字段可以为状态设置标准输入输出语句，如果这里设置了 `false`，标准输入输入语句就会实效。
- `events` - 这个字段表示 `nodemon` 运行到某些状态时的一些触发事件，总共有五个状态：
  - `start` - 子进程（即监控的应用）启动
  - `crash` - 子进程崩溃，不会触发 `exit`
  - `exit` - 子进程完全退出，不是非正常的崩溃
  - `restart` - 子进程重启
  - `config:update` - `nodemon`的`config`文件改变


## 使用

```js
  {
      "restartable": "rs",
      "ignore": [
          ".git",
          "node_modules/**/node_modules"
      ],
      "verbose": true,
      "execMap": {
          "": "node"
          "js": "node --harmony"
      },
      "events": {
          "restart": "osascript -e 'display notification \"App restarted due to:\n'$FILENAME'\" with title \"nodemon\"'"
      },
      "watch": [
          "test/fixtures/",
          "test/samples/"
      ],
      "env": {
          "NODE_ENV": "development",
          "PORT": "3000"
      },
      "ext": "js json",
      "legacy-watch": false
  }
```

```js
  // default options for config.options
  module.exports = {
      restartable: 'rs',
      colours: true,
      execMap: {
          py: 'python',
          rb: 'ruby',
          // more can be added here such as ls: lsc - but please ensure it's cross
          // compatible with linux, mac and windows, or make the default.js
          // dynamically append the `.cmd` for node based utilities
      },
      ignoreRoot: ['.git', 'node_modules', 'bower_components', '.sass-cache'],
      watch: ['*.*'],
      stdin: true,
      runOnChangeOnly: false,
      verbose: false,
      // 'stdout' refers to the default behaviour of a required nodemon's child,
      // but also includes stderr. If this is false, data is still dispatched via
      // nodemon.on('stdout/stderr')
      stdout: true,
  };
```


## 参考文档
- [nodemon](https://www.npmjs.com/package/nodemon)
- [gulp-nodemon](https://www.npmjs.com/package/gulp-nodemon)
- [github remy/nodemon](https://github.com/remy/nodemon)
- [document](http://www.cnblogs.com/JuFoFu/p/5140302.html)
