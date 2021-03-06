---
layout: post
title:  "基于typeScript和iview开发项目"
categories: share
---
##### 1、概述
采用iView作为UI组件，typeScript写后台。
包含的主要功能有：
- 载体管理
- 容器管理
- 商品管理
- 用户管理
##### 2、具体实现
###### 2.1 入口文件（index.html、index.tsx）
```
<!--index.html-->
<!DOCTYPE html>
<html lang="en">

<head>
    <title>后台管理系统</title>
</head>

<body>
    <div id="app"></div>
</body>

</html>
```
```
//index.tsx
import Vue, { CreateElement } from 'vue'
import VueRouter from 'vue-router'

import iView from 'iview'
import * as _promise from 'bluebird'
window['Promise'] = _promise

Vue.use(VueRouter)
Vue.use(iView)

import 'iview/dist/styles/iview.css'
import './assets/css/style.styl'
import AppComponent from './components/app/app.component'
import store from './stores/store'
import routes from './routes'
const router = new VueRouter({
  routes
})

new Vue({
  el: '#app',
  data: store,
  router,
  render(h: CreateElement) {
    return (
      <AppComponent />
    )
  }
})
```
###### 2.2 <a href="http://v1.iviewui.com">iView</a>（这里主要使用了表单组件和表格组件）

1. layout布局
<br>顶部导航+侧边栏 


1. Input 输入框
```
<template>
    <i-input :value.sync="value" placeholder="请输入..." style="width: 300px"></i-input>
</template>
<script>
    export default {
        data () {
            return {
                value: ''
            }
        }
    }
</script>

```
2.Table 表格
```
<template>
    <i-table :columns="columns1" :data="data1"></i-table>
</template>
<script>
    export default {
        data () {
            return {
                columns1: [
                    {
                        title: '姓名',
                        key: 'name'
                    },
                    {
                        title: '年龄',
                        key: 'age'
                    },
                    {
                        title: '地址',
                        key: 'address'
                    }
                ],
                data1: [
                    {
                        name: '王小明',
                        age: 18,
                        address: '北京市朝阳区芍药居'
                    },
                    {
                        name: '张小刚',
                        age: 25,
                        address: '北京市海淀区西二旗'
                    },
                    {
                        name: '李小红',
                        age: 30,
                        address: '上海市浦东新区世纪大道'
                    },
                    {
                        name: '周小伟',
                        age: 26,
                        address: '深圳市南山区深南大道'
                    }
                ]
            }
        }
    }
</script>
```
3. Message 全局提示
<br>轻量级的信息反馈组件，在顶部居中显示，并自动消失。
```
<template>
    <i-button type="primary" @click="info">显示普通提醒</i-button>
</template>
<script>
    export default {
        methods: {
            info () {
                this.$Message.info('这是一条普通的提醒');
            }
        }
    }
</script>
```
###### 2.3组件写法（xx.component.tsx）
```
import Vue, { CreateElement } from 'vue'
import { Component, Watch, Prop } from 'vue-property-decorator'

import { ColumnOption, ColumnRenderParams } from 'iview'

import store from '../../stores/store'

import commonService from '../../services/common.service'

import './xx.component.styl'

//组件的写法
@Component
export default class SkusComponent extends Vue {
  //<template></template>
  render(h: CreateElement) {
    return (
      <div skus-component>
        <!--这里是html视图代码-->
        <i-input type="text" value={this.message.name} placeholder = '填写名称' on-input={(val: string) => this.message.name = val} />
      <div>
      )
  }
  //data直接定义
  message: any = {
    name: '',
    sex: '',
    age: null,
  }
  //methods直接定义
  foo(){
      
  }
  //computed计算属性
  get valName() {
     return computedVal;
  }
  //数据传递
  @Prop({default: 0})
   count: number
  //观察属性
  @Watch('doll')
  dollChange() {

  }
  //生命钩子
  created() {
    
  }
```
nativeOnClick{()=>{//javascript代码}}