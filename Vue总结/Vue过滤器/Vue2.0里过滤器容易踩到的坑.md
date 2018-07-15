### Vue2.0 里过滤器容易踩到的坑

vue2.0 里，不再有自带的过滤器，需要自己定义过滤器。

定义的方法如下：

注册一个自定义过滤器，它接收两个参数：过滤器ID(过滤器名)和过滤器函数。

```js
//main.js中定义的全局过滤器
Vue.filter("filtername", function(value, 参数) {
  return (
    参数 +
    value
      .split("")
      .reverse()
      .join("")
  );
});
```
function里第一个参数value默认为使用这个过滤器的data对象内的值，在本例中是msg的值’you are mine’。 
#### 坑1：第一个参数必须为自身的值，后面可以加任意多的参数。数序颠倒就会出错。

下面来一个最常见的小例子来说明在使用vue2.0过滤器并结合v-text时遇到的其他的几个坑：

需求：在页面输出一段反转顺序的字符串。

完整代码如下：
```html
<!doctype html>
<html>
<head>
<meta charset="UTF-8">
<title>Document</title>
<style>

</style>
</head>
<script src='./vue2.js'></script>
<script>
window.onload=function(){
    //类似于自定义指令，可以用全局方法 Vue.filter() 注册一个自定义过滤器，它接收两个参数：过滤器 ID 和过滤器函数。
    Vue.filter('reverseString',function(value,myString){
        // function里第一个参数value默认为使用这个过滤器的data值，在本例中是msg的值'you are mine'。请注意：第一个参数必须为自身的值，后面可以加任意多的参数
        return myString+value.split('').reverse().join('');

    });

    new Vue({
        el:'#box',
        data:{
            msg:'you are mine'  
        }
    });
};
</script>
<body>

<div id='box'>
    <p>msg is: <br>{{msg}}</p>
    <hr>
    <p>reverse msg is: <br>{{msg|reverseString( 'Hello:' )}}</p><!-- 在vue2.0里 过滤器只能用类似函数的写法reverseString( 'I must tell you:')，括号内是参数，不同于vue1.0的用空格后加参数的写法"  msg|reverseString  'I must tell you:' " -->

    <!-- <p v-text="msg|reverseString( 'I must tell you:' )"></p>失效 -->
    <!-- v-text里用过滤器失效，原因是在vue2.0里 管道符‘|’只能用在mousetache和v-bind中 --> 
</div>

</body>
</html>
```
输出结果：
```js
msg is: 
you are mine

reverse msg is: 
Hello:enim era uoy
```
#### 坑2：在vue2.0里 过滤器只能用类似函数的写法
```js
reverseString( ‘I must tell you:’)
```
括号内是参数，不同于vue1.0的用空格后加参数的写法；

#### 坑3：v-text里用过滤器失效，原因是在vue2.0里 管道符‘|’只能用在mousetache和v-bind中。

以上只是一个简单的过滤器的用法，如果涉及到复杂的数据处理的过滤器，比如实现vue1.0里用到过滤器套过滤器的功能，个人感觉也可以用computed来代替过滤器。