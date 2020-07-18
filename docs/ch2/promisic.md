## 使用LinUI promisic

- [具体文档](https://doc.mini.talelin.com/function/)

- create `wechat_miniapp/utils/util.js`

- [利用ui库，来实现转换promise, 不过其实现在微信已经支持转换promise](https://course.talelin.com/lin/sleeve/4%20%E8%AF%BE%E7%A8%8B%E8%B5%84%E6%96%99.html#promisic)

```js
const promisic = function (func) {
    return function (params = {}) {
        return new Promise((resolve, reject) => {
            const args = Object.assign(params, {
                success: (res) => {
                    resolve(res);
                },
                fail: (error) => {
                    reject(error);
                }
            });
            func(args);
        });
    };
};

export {
    promisic
}
```

- `/utils/http.js`

```js
import { config } from "../config/config";
import { promisic } from "./util";
class Http {
    static async request({ url, data, callback, method = 'GET' }) {
        //wx.request
        await promisic(wx.request)({
            url: `${config.apiBaseUrl}${url}`,
            data,
            method,
            header: {
                appkey: config.appkey
            }
            //这里用 promisic API 封装成 promise, 就不需要success() 函数

            // , success(res) {
            //     callback(res.data);
            // }
        })
    }
}

//wx.request, 把它当作参数传进来，不能加(), 否则是调用
// promisic(wx.request)({
//     url: '',
//     data: data,

// })
//这里把一个函数传递进另一个函数
//动态类型 非常常见， python


export {
    Http
}
```