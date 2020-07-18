## Async and await

- callback
- promise
- async await : 现在我们主要采用这种写法

- 在小程序app, 不能用 `await` 加在 `wx.request` 前面来返回 promise object
- 需要通过 call `success(res)` 回调函数来获得

```js
import { config } from "../config/config";
class Http {
    static request({ url, data, callback, method = 'GET' }) {
        //wx.request
        wx.request({
            url: `${config.apiBaseUrl}${url}`,
            data,
            method,
            header: {
                appkey: config.appkey
            },
            success(res) {
                callback(res.data);
            }
        })
    }
}
```


