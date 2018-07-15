## px2rem-loader（Vue:将 px 转化为 rem，适配移动端）
### 1.下载 lib-flexible
使用的是 vue-cli+webpack，通过 npm 来安装的
```
npm i lib-flexible --save
```
### 2.引入 lib-flexible
在 main.js 中引入 lib-flexible

```js
import "lib-flexible/flexible";
```
### 3.设置 meta 标签
通过 meta 标签，设置设备宽度以及缩放比例
```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```
### 4.安装 px2rem-loader
```js
npm install px2rem-loader
```
### 5.配置 px2rem-loader
这里是重要的一步~~
在 build 文件中找到 util.js，将 px2rem-loader 添加到 cssLoaders 中，如：

```javascript
const cssLoader = {
  loader: "css-loader",
  options: {
    minimize: process.env.NODE_ENV === "production",
    sourceMap: options.sourceMap
  }
};
const px2remLoader = {
  loader: "px2rem-loader",
  options: {
    remUnit: 75//这里的75是html的font-size的大小，可以自行设置
  }
};
```
同时，在 generateLoaders 方法中添加 px2remLoader
```js
function generateLoaders(loader, loaderOptions) {
  const loaders = options.usePostCSS
    ? [cssLoader, postcssLoader, px2remLoader]
    : [cssLoader, px2remLoader];

  if (loader) {
    loaders.push({
      loader: loader + "-loader",
      options: Object.assign({}, loaderOptions, {
        sourceMap: options.sourceMap
      })
    });
  }

  if (options.extract) {
    return ExtractTextPlugin.extract({
      use: loaders,
      fallback: "vue-style-loader"
    });
  } else {
    return ["vue-style-loader"].concat(loaders);
  }
}
```

### 6.重启，一切 ok~

当配置完之后，只需要重启下服务，就自动转化为 rem 了

```js
npm run dev
```
