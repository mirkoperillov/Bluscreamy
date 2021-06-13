## koa常用中间件

### 一、koa-bodyparser

安装：

```javascript
npm i koa-bodyparser
```

koa-bodyparser可以把post请求的参数解析到ctx.request.body中

```javascript
const Koa = require("koa2");
const bodyParser = require("koa-bodyparser");

const app = new Koa();
app.use(bodyParser())

app.use(async(ctx) => {
    if (ctx.url === "/" && ctx.method === "GET") {
        let html = `
        <h1>发送post请求</h1>
        <form action="/" method="POST">
        <p>用户姓名：</p>
        <input type="text" name="userName" /><br/>
        <p>用户年龄：</p>
        <input type="text" name="userAge" /><br/>
        <button type="submit">发送</button>
        </form>
        `
        ctx.body = html
    } else if (ctx.url === "/" && ctx.method === "POST") {
        let bodyData = ctx.request.body;
        ctx.body = bodyData
    } else {
        ctx.body = `
            <h1>404</h1>
        `
    }

})

app.listen(6300, () => {
    console.log("连接成功，端口号：6300");
})
```

