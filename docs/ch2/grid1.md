# LinUI Grid 组件分类六宫格

- 我们准备开始写一个自定义组件
- create `components/category-grid`
  - create `index`, 在小程序里，会同时新建4个文件

![](img/2020-07-26-01-22-17.png)

- `app.json` 是全局控制 components

```json
{
  "pages": [
    "pages/home/home"
  ],
  "window": {
    "backgroundTextStyle": "light",
    "navigationBarBackgroundColor": "#fff",
    "navigationBarTitleText": "WeChat",
    "navigationBarTextStyle": "black"
  },
  "style": "v2",
  "sitemapLocation": "sitemap.json",
  "usingComponents": {
    "l-grid": "/miniprogram_npm/lin-ui/grid/index",
    "l-grid-item": "/miniprogram_npm/lin-ui/grid-item/index"
  }
}
```

- update `index.wxml`

```html
<view class="container">
	<l-grid>
		<block wx:for="{{}}">
			<l-grid-item>
				<view>
					<image src="{{}}" />
					<text>{{}}</text>
				</view>
			</l-grid-item>
		</block>
	</l-grid>
</view>
```



- create `model/category.js`

```js
class Category {
    static async getGridCategory() {
        return await Http.request({
            url: `category/grid/all`
        })
    }
}

export {
    Category
}
```

- update `home.js`

