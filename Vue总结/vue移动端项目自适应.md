## vue 移动端项目自适应的相关设置
使用scss动态的将px转换成rem
```scss
//将px转换成rem的方法
@function px2rem($px) {
    $rem: 37.5px;//基于宽度为750物理像素的设计稿进行设计的
    @return ($px/$rem)+rem;
    // 在转换的时候要看设计稿是基于哪个物理分辨率下进行设计的，然后在看看这个物理像素的分辨率是属于几倍屏
}
```
man.js

```js
// The Vue build version to load with the `import` command
// (runtime-only or standalone) has been set in webpack.base.conf with an alias.
import Vue from "vue";
import App from "./App";
import router from "./router";
//引入动态设置font-size大小的js文件
import "./common/self";
Vue.config.productionTip = false;
// 定义的全局自定义指令
Vue.directive("focus", {
  bind: function(el, binding, vnode) {
    console.log(el);
    console.log("我是自定义的focus指令");
  }
});

new Vue({
  el: "#app",
  router,
  components: {
    App
  },
  template: "<App/>"
});
```

self.js

```js
//动态的设置html的font-size的大小
//获取视窗的宽度
var htmlWidth =
  document.documentElement.clientWidth || document.body.clientWidth;
//获取HTML元素
var htmlDom = document.getElementsByTagName("html")[0];
//设置HTML元素的font-size大小
if (htmlWidth > 750) {
  htmlWidth = 750;
}
htmlDom.style.fontSize = htmlWidth / 10 + "px";
```

