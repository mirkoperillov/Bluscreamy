## koa中使用ejs模板引擎

### 安装

使用npm安装：

```javascript
npm i koa-views

npm i ejs
```

或者使用yarn安装：

```javascript
yarn add koa-views

yarn add ejs
```

### 引入

```javascript
const views = require("koa-views");
```



### 配置模板引擎中间件  （第三方中间件）

- 创建一个views文件夹

```javascript
app.use(views('views', {//views是你创建的文件夹路径
    extension: 'ejs' //应用ejs模板引擎
}))
```

- 在views文件夹中创建一个index.ejs 内容如下跟html文件内容一样：

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    这是ejs模板引擎
</body>

</html>
```

- 运行

```javascript
app.use(async(ctx) => {
    await ctx.render("index");
})
```

### 向ejs模板中传递数据

