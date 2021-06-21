## 获取post请求

`koa2中获取请求的方式跟node中http模块相似`

### 利用ajax发送post请求

#### 用原生的js写ajax请求：

```javascript
let url="http://localhost:6330"
let msg={
	name:this.name
}
const xhr=new XMLHttpRequest()
xhr.open("POST",url,true)
xhr.onreadystatechange=function(){ //监听事件并获取返回值
    console.log(xhr.status);//获取状态码
    console.log(xhr.readyState);//监听请求是否发送成功 成功发送会打印4
    console.log(xhr.responseText);//获取返回值
}
xhr.send(JSON.stringify(msg))//发送请求
```

### koa2获取post请求

跟原生的node不同， koa2把req对象跟res对象都封装在了Context中所以koa2获取方式如下：

```javascript
const Koa = require("koa");
const app = new Koa();
let po = ''
app.use(async(ctx) => {
    ctx.set("Access-Control-Allow-Origin", "*");
    console.log(ctx.method);
    let ni = await pi(ctx)//调用下面封装的函数
    console.log(ni);//打印post请求的参数
    ctx.body = "返回" + ni
})
async function pi(ctx) {//封装获取post参数
    return new Promise((resolve, reject) => {//实例化一个Promise对象
        try {
            ctx.req.on("data", (data) => {
                // console.log(data.toString());
                po = data.toString()
            })
            ctx.req.on("end", () => {
                resolve(po)
            })
        } catch {
            reject(error)
        }
    })

}
app.listen(6330, () => {
    console.log('连接成功，端口号：6330');
})
```

