## Coupon Concept


- 先改一下 六宫格的函数名, `home.js`

```js
  async initAllData() {
    const themeA = await Theme.getHomeLocationA();
    const bannerB = await Banner.getHomeLocationB();
    const grid = await Category.getHomeLocationC();
    this.setData({
      themeA: themeA[0],
      bannerB,
      grid
    })
  },
```

- `category.js`

```js
import { Http } from "../utils/http";

class Category {
    static async getHomeLocationC() {
        return await Http.request({
            url: `category/grid/all`
        })
    }
}

export {
    Category
}
```

---


![](img/2020-07-30-19-51-14.png)

- create `model/Activity.js`

```js
import { Http } from "../utils/http";

class Activity {
    static locationD = 'a-2'
    static async getHomeLocationD() {
        return await Http.request({
            url: `activity/name/${Activity.locationD}`
        })
    }
}

export {
    Activity
}
```

- 同时修改 `home.js`

```js
import { config } from "../../config/config"
import { Theme } from "../../model/theme"
import { Banner } from "../../model/banner"
import { Category } from "../../model/category"
import { Activity } from "../../model/Activity"

// pages/home/home.js
Page({

  /**
   * Page initial data
   */
  data: {
    themeA: null,
    bannerB: null,
    grid: [],
    activityD: null
  },

  async onLoad(options) {
    //在这里使用 async and await 就不需要 callback function
    this.initAllData()
  },

  async initAllData() {
    const themeA = await Theme.getHomeLocationA();
    const bannerB = await Banner.getHomeLocationB();
    const grid = await Category.getHomeLocationC();
    const activityD = await Activity.getHomeLocationD();
    this.setData({
      themeA: themeA[0],
      bannerB,
      grid,
      activityD
    })
  },

```


- update `home.wxml`

```html
<!--pages/home/home.wxml-->
<view>
	<image class="top-theme" src="{{themeA.entrance_img}}" />
	<swiper
	 class="swiper"
	 indicator-dots="{{true}}"
	 indicator-active-color="#157658"
	 autoplay="{{true}}"
	 circular="{{true}}"
	>
		<block wx:for="{{bannerB.items}}">
			<swiper-item>
				<image class="swiper" src="{{item.img}}" />
			</swiper-item>
		</block>
	</swiper>

	<s-category-grid grid="{{grid}}" />

	<image class="activity" src="{{activityD.entrance_img}}" />
</view>
```


- set style `home.wxss`

```css
.activity{
    margin-top: 20rpx;
    width:100%;
    height: 310rpx;
}
```

![](img/2020-07-30-20-15-28.png)

---

## 背景颜色的设置


- 可以小程序官方文档查看 背景颜色的更改

![](img/2020-07-30-20-20-26.png)

- set `home.json`

```json
{
  "usingComponents": {
    "s-category-grid": "/components/category-grid/index"
  },
  "backgroundColor" : "#000000"
}
```

![](img/2020-07-30-20-52-43.png)

- 我们需要更改样式，让它正常显示, 同时删除默认 `app.wxss` 的样式

- 现在我们设置六宫格的 样式 `category-grid/index.wxss`

```css
/* components/category-grid/index.wxss */
.container{
    height: 320rpx;
    width: 100%;
    display:flex;
    flex-direction: row;
    align-items: center;
    justify-content: center;
    background-color: #ffffff;
}
```


- 可以通过调试 `Wxml` , 可以发现是在 page 底下

![](img/2020-07-30-20-58-11.png)


-  更改 `home.wxsss`

```css
.top-theme{
    width:100%;  /*if u can use 100%, don't use 750 rpx*/
    height: 260rpx;
    display: flex;
}

.swiper{
    width:100%;
    height: 360rpx;
}

.activity{
    margin-top: 20rpx;
    width: 100%;
    height: 310rpx;
    display: flex;
}
/* option+command+L */
```

- 如果想要小程序全局显示背景颜色，可以在 `app.wxss` 里设置

```css
/**app.wxss**/
page{
  background-color: #f5f5f5;
}
```


![](img/2020-07-30-21-02-48.png)

- 现在一切显示正常了！

























