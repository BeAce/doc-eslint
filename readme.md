# [ESLint](http://eslint.org/) 的使用

[ESLint](http://eslint.org/)可以作为代码审查的工具，来强制的制定一些代码规则或规范来管理、统一一个团队的代码风格。

你可以将它作为一个代码检查的工具，应用它的规则可以检测出代码中某些潜在的问题或者值得优化的代码，并且，你也可以将它作为一个代码规范的标准来养成你的书写习惯。

## 历史

[ESLint](http://eslint.org/)作为一个开源项目，是由Nicholas C. Zakas于2013年6月创建。

## 用法

[ESLint](http://eslint.org/)的用法非常简单，首先在本地初始化项目，安装`ESLint`。

```bash
npm init -y
npm install --save eslint
```

在项目根目录下建立`.eslintrc`

在这里，记录下`rc`结尾的文件是什么含义。

### rc file

> Actually rc stands for. runtime configuration.the rc files configure what software (application) and services are configured to start at runtime, therefore: runtime configuration. —— wiki

在`Linux`下，rc（runtime configuration）代表运行时配置。表示在某种运行环境下自动执行的配置文件。前端常用的例如`.babelrc`、`.jsbeautifyrc`。


在[ESLint](http://eslint.org)中最常用的就是其规则（[rule](http://eslint.org/docs/rules/))。在`.eslintrc`中写入以下规则

```json
//.eslintrc
{
  "rules": {
    "no-console": 2
  }
}

```

这条规则表示当代码中出现类似`console.log()`这种调试代码时报错。我们可以先新建一个`my.js`文件来故意写一个错误。

```js
function a() {
  console.log("fsafs");
}
a();
```

可以执行命令先来看下运行结果。

```bash
./node_modules/.bin/eslint my.js
```

**screenshot**

![eslint](https://images-manager.oss-cn-shanghai.aliyuncs.com/static/eslint/eslint.png)

> 从上图可以看出，[ESLint](http://eslint.org)给出了错误提示，并且告诉了我们代码错误的原因以及错误出现的行列数。该错误为第三行第三列的代码中出现了`console`的表达式。

在`rule`的书写方式中，看到了有`"no-console": 2`，这样的写法。其实有三个等级。

- 0 表示正确
- 1 表示警告`warning`
- 2 表示错误`error`

我们可以将其程度调节到0和1分别看下效果。

> 0的时候没有任何错误输出，1的时候出现了一个警告错误。

**screenshot**
![eslint](https://images-manager.oss-cn-shanghai.aliyuncs.com/static/eslint/eslint-warning.png)

## 规范继承
定制一个规范要在`rule`中写很多的配置项，我们可以和一些一线互联网公司遵守相同的代码规范。只需要在配置文件中加入如下代码。下面代码使用了`Google`的代码规范。

```json
//.eslintrc
{
  "extends": ["eslint-config-google"]
}
```

当然还需要安装依赖。

```bash
npm install --save-dev eslint-config-google
```

## 插件

[ESLint](http://eslint.org/)提供插件配置，例如`react`、`babel`等。

```json
//.eslintrc
{
  "plugins": [
    "react",
    "babel"
  ]
}
```

当然，也需要添加相应的依赖。

```json
{
  "eslint-plugin-babel": "^4.0.0",
  "eslint-plugin-react": "^6.9.0"
}

```

## 总结

一个团队的代码风格，以及代码规范是非常重要的。不仅仅能够让团队协作更加高效（别人能够读的懂你的代码），而且对于代码可维护性、辨识度、准确度有明显的提高。
