## [glob](https://www.npmjs.com/package/glob)

#### 简介
`glob`最早是出现在Unix系统的命令行中，是用来匹配文件路径的。如：`lib/**/*.js`匹配lib目录下所有的js文件

#### Usage
```base
  npm i glob
```

```js
  let glob = require('glob');

  // options(可选)
  glob('dest/**/*.js', options, (error, files) => {
    // files is an array of filenames.
    // If the `nonull` option is set, and nothing
    // was found, then files is ["**/*.js"]
    // er is an error object or null.
  })
```

#### 匹配规则
- `*` - 匹配0或多个任意字符
- `?` - 匹配任意字符
- `[...]` - 若字符在中括号中，则匹配。若以`!`或`^`开头，若字符不在中括号中，则匹配
- `!(pattern|pattern|pattern)`不满足括号中的所有模式则匹配
- `?(pattern|pattern|pattern)` - 满足0或1括号中的模式则匹配
- `+(pattern|pattern|pattern)` - 满足1或更多括号中的模式则匹配
- `*(a|b|c)` - 满足0或更多括号中的模式则匹配
- `@(pattern|pat*|pat?erN)` - 满足1个括号中的模式则匹配
- `**` - 跨路径匹配任意字符
