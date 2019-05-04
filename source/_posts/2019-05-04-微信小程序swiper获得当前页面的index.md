---
layout: photo
title: 微信小程序swiper获得当前页面的index
tags:
  - 小程序
date: 2019-05-04 22:23:37
categories: 小程序
photos:
---
小程序很多时候需要获取swiper当前页面的index，用于触发其他事件
<!--more-->

### swiper官方文档

|   属性   |   类型   |   默认值   |   必填   |   说明   |
| ---- | ---- | ---- | ---- | :--- |
|   indicator-dots   |   boolean   |   false   |   否   |   是否显示面板指示点   |
|   indicator-color   |   color   |   rgba(0, 0, 0, .3)   |   否   |   指示点颜色   |
|   indicator-active-color   |   color   |   #000000   |   否   |   当前选中的指示点颜色   |
|   autoplay   |   boolean   |   false   |   否   |   是否自动切换   |
|   current   |   number   |   0   |   否   | **当前所在滑块的index** |
|   interval   |   number   |   5000   |   否   |   自动切换时间间隔   |
|   duration   |   number   |   500   |   否   |   滑动动画时长   |
|   circular   |   boolean   |   false   |   否   |   是否采用衔接滑动   |
|   vertical   |   boolean   |   false   |   否   |   滑动方向是否为纵向   |
|   previous-margin   |   string   |   "0px"   |   否   |   前边距，可用于露出前一项的一小部分，接受 px 和 rpx 值   |
|   next-margin   |   string   |   "0px"   |   否   |   后边距，可用于露出后一项的一小部分，接受 px 和 rpx 值   |
|   display-multiple-items   |   number   |   1   |   否   |   同时显示的滑块数量   |
|   skip-hidden-item-layout   |   boolean   |   false   |   否   |   是否跳过未显示的滑块布局，设为 true 可优化复杂情况下的滑动性能，但会丢失隐藏状态滑块的布局信息   |
|   easing-function   |   string   |   "default"   |   否   |   指定 swiper 切换缓动动画类型   |
|   bindchange   |   eventhandle   |      |   否   |   **current 改变时会触发 change 事件，event.detail = {current, source}**   |
|   bindtransition   |   eventhandle   |      |   否   |   swiper-item 的位置发生改变时会触发 transition 事件，event.detail = {dx: dx, dy: dy}   |
|   bindanimationfinish   |   eventhandle   |      |   否   |   动画结束时会触发 animationfinish 事件，event.detail 同上   |

[参考链接](https://developers.weixin.qq.com/miniprogram/dev/component/swiper.html)

代码：index.wxml

```vue
<swiper class='sw-tu' circular="true" current="0" bindchange='onSlideChange'>
    <swiper-item class="sw-tuone" wx:for="{{img_list}}">
        <image class='sw-photo' src="{{item}}" />
    </swiper-item>
</swiper>
```
代码：index.js
```javascript
data: {
    index: 1,
    img_list:[
		'https://cn.bing.com/th?id=OHR.SkelligMichael_ZH-CN8635121409_1920x1080.jpg&rf=LaDigue_1920x1080.jpg&pid=hp',
        'https://cn.bing.com/th?id=OHR.MargaretRiverVineyards_ZH-CN8547374435_1920x1080.jpg&rf=LaDigue_1920x1080.jpg&pid=hp',
        'https://cn.bing.com/th?id=OHR.may1_ZH-CN8582006115_1920x1080.jpg&rf=LaDigue_1920x1080.jpg&pid=hp'
    ]
  },
  onSlideChange: function (e) {
    this.setData({
      index: e.detail.current + 1
    })
  },
```



