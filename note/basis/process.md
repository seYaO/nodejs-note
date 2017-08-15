## 全局对象

#### 属性
- `process.argv` - 返回一个数组，成员是当前进程的所有命令行参数
- `process.env` - 返回一个对象，成员为当前Shell的环境变量，比如`process.env.HOME`
- `process.installPrefix` - 返回一个字符串，表示Node安装路径的前缀，比如`/usr/local` 相应地，Node的执行文件目录为`/usr/local/bin/node`
- `process.pid` - 返回一个数字，表示当前进程的进程号
- `process.platform` - 返回一个字符串，表示当前的操作系统，比如`Linux`
- `process.title` - 返回一个字符串，默认值为`node`，可以自定义该值
- `process.version` - 返回一个字符串，表示当前使用的Node版本，比如`v7.10.0`
- `process.stdout` - 返回一个对象，表示标准输出。该对象的`write`方法等同于`console.log`，可用在标准输出向用户显示内容
- `process.stdin` - 返回一个对象，表示标准输入
- `process.stderr` - 指向标准错误
- `process.execPath` - 返回执行当前脚本的Node二进制文件的绝对路径
- `process.execArgv` - 返回一个数组，成员是命令行下执行脚本时，在Node可执行文件与脚本文件之间的命令h行参数


### 方法
- `process.chdir()` - 切换工作目录到指定目录
- `process.cwd()` - 返回运行当前脚本的工作目录的路径
- `process.exit()` - 退出当前进程
- `process.getgid()` - 返回当前进程的组ID(数值)
- `process.getuid()` - 返回当前进程的用户ID(数值)
- `process.nextTick()` - 指定回调函数在当前执行栈的尾部、下一次Event Loop之前执行
- `process.on()` - 监听事件
- `process.setgid()` - 指定当前进程的组，可以使用数字ID，也可以使用字符串ID
- `process.setuid()` - 指定当前进程的用户，可以使用数字ID，也可以使用字符串ID
·
