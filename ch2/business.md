# 2. business object

- 逻辑分层

```js
  /**
   * Lifecycle function--listening when page load
   * JS 类型的约束
   * 业务逻辑
   * 数据绑定
   * view视图层 业务逻辑层 桥梁 中间层
   * mvc C controller
   * Model, Logic, Service
   * Service, Manager,  
   */
```

- create a new folder `model/theme.js`

- copy `wx.request()` from home.js to theme.js


## packaging Http Request

- theme.js

```js
//业务对象
//theme, banner, spu, sku, address, user
import { config } from "../config/config";
class Theme {
    static getHomeLocationA(callback) {
        wx.request({
            url: `${config.apiBaseUrl}theme/by/names`,    //Template string
            // url: 'http://se.7yue.pro/v1/theme/by/names?names=t-1',
            method: 'GET',
            data: {
                names: 't-1'
            },
            header: {
                appkey: config.appkey
            },
            success: (res) => {
                console.log(res);
                callback(res.data)
            }
        })
    }
}

export {
    Theme
}
```

## delete utils/util.js

- create a utils/http.js

- 对wx.request() 进行二次封装

## first time reconstruct codes

- utils/http.js

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

export {
    Http
}
```

- rebuild theme.js

```js
//业务对象
//theme, banner, spu, sku, address, user
import { Http } from "../utils/http";

class Theme {
    static getHomeLocationA(callback) {
        Http.request({
            url: `theme/by/names`,
            data: {
                names: 't-1'
            },
            callback: data => {
                callback(data)
            }
        });
    }
}

export {
    Theme
}
```

- rebuild home.js

```js
import { config } from "../../config/config"
import { Theme } from "../../model/theme"

// pages/home/home.js
Page({

  /**
   * Page initial data
   */
  data: {
    topTheme: null,
  },

  /**
   * Lifecycle function--listening when page load
   * JS 类型的约束
   * 业务逻辑
   * 数据绑定
   * view视图层 业务逻辑层 桥梁 中间层
   * mvc C controller
   * Model, Logic, Service
   * Service, Manager,  
   */
  onLoad: function (options) {
    Theme.getHomeLocationA(data => {
      this.setData({
        topTheme: data[0]
      })
    })
  },

  /**
   * Page event handler function--listening when user drop down
   */
  onPullDownRefresh: function () {

  },

  /**
   * Called when page reach bottom
   */
  onReachBottom: function () {

  },

  /**
   * Called when user click on the top right corner to share
   */
  onShareAppMessage: function () {

  }
})
```
![](img/2020-03-25-13-10-17.png)
- same result.


## 但现在代码可读性不高，每次都嵌套 callback, 还需要重构

