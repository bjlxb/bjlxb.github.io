---
layout: photo
title: iview框架中i-table数据处理
tags:
  - 前端
date: 2021-04-12 15:11:36
categories: 前端
photos:
---
iview 框架中 i-table组件对某个单元格进行单独处理！
<!--more-->

## 1. 需求
后端接口数据为10或20，在前端渲染的时候，对其进行相应处理，显示的是文字状态。

## 2. 问题
项目开发使用了iview 框架的 i-table组件，数据渲染都是组件自动进行的，很难对单个单元格进行处理。

## 3. 解决方案
使用 `render` 看一下解决方案代码吧
`template`部分

```vue
<template>
	<i-table border :columns="columns0" :data="data0"></i-table>
</template>
```

`data`部分

```javascript
    export default {
        components: {Table, Button},
        data () {
            return {
                columns0: [
                    {
                        title: "id",
                        key: "id",
                    },
                    {
                        title: "所属平台",
                        key: "module",
                    },
                    {
                        title: "运行状态",
                        key: "is_run",
                        render: (h, params) => {
                            return h('div', [
                            h('span', {
                                style: {
                                }
                            }, params.row.is_run == '10'?'运行':'不运行'),
                            ])
                        }
                    },
                    {
                        title: "请求方式",
                        key: "method",
                    },
                    {
                        title: "接口描述",
                        key: "remark",
                    },
                    {
                        title:"操作",
                        key:"action",
                        // width:200,
                        align:"center",
                        render: (h, params) => {
                            return h("div", [
                                h(
                                    "Button",
                                    {
                                        props: {
                                            type:"success",
                                            size:"default"
                                        },
                                        style: {
                                        },
                                        on: {
                                            click: () => {
                                                this.detail_mission(params.row.id);
                                            }
                                        }
                                    },
                                    "详情"
                                )
                            ]);
                        }
                    }
                ],
                data0: [{id: 1, module: "baomojing", is_run: "10", method: "12112", remark: "123"}]
            }
        }
}
```

`核心代码：`

```javascript
//三元表达式
params.row.is_run == '10'?'运行':'不运行'
```

