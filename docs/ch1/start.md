## create my page

- create a new folder `home` in `pages`
![](img/2020-03-09-23-24-14.png)
![](img/2020-03-09-23-25-42.png)
- main screen still point to index.js
- we can change that by modify app.json
![](img/2020-03-09-23-26-50.png)
- we can change the home's order
![](img/2020-03-09-23-28-34.png)
---
- Or: choose `Add Compilation Mode`
![](img/2020-03-09-23-29-53.png)

- now we can remove `index` and `logs`
- at the same time, 
![](img/2020-03-09-23-32-14.png)
- this error tell us that we need to remove `index` and `logs` 
  in `app.json`
---

## Note: all images are dynamic and we may adjust them

- open home.wxml
- create a `image` tag, set top-theme's styles
- click `home.wxss`

![](img/2020-03-11-16-02-20.png)
- width fills entire screen
- home.wxml  
```html
<view>
	<image class="top-theme" src="" />
</view>
```
- home.wxss
```css
.top-theme{
    width:100%;  /*if u can use 100%, don't use 750 rpx*/
    height: 260rpx;
}
/* option+command+L */
```
---


## about `appkey` 

- http://talelin.unna.com.cn