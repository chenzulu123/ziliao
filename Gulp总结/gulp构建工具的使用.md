## gulp 构建工具的使用

### 一、安装相关的插件

#### 1、gulp

```
npm install gulp --save-dev
```

#### 2、less 解析  插件

```
npm install gulp-less --save-dev
```

#### 3、js 压缩和混淆插件

```
npm install gulp-uglify --save-dev
```

#### 4、监控 less 变化的插件

```
npm install gulp-livereload --save-dev
```

#### 5、css 压缩插件

```
npm install gulp-clean-css --save-dev
```

#### 6、html 压缩插件

```
npm install gulp-htmlmin --save-dev
```

#### 7、js 检查插件

```
npm install gulp-jshint --save-dev
```

#### 8、文件合并插件

```
npm install gulp-concat --save-dev
```

#### 9、重命名文件

```
npm install gulp-rename --save-dev
```

#### 10、雪碧图制作插件

```
npm install gulp.spritesmith --save-dev
```

#### 11、清空文件夹

```
npm install gulp-clean --save-dev
```

#### 12、提示插件

```
npm install gulp-notify --save-dev
```

### 二、工程项目初始化

- 创建工程项目 gulp

- 进入对工程项目进行 npm 初始化

```js
npm init
```

- Gulpfile.js代码

```js
var gulp = require("gulp"),
  //less转换css
  less = require("gulp-less"),
  //当less更新是，css同步更新
  livereload = require("gulp-livereload"),
  //HTML压缩
  htmlmin = require("gulp-htmlmin"),
  //js压缩和混淆
  uglify = require("gulp-uglify"),
  //css压缩
  cleanCss = require("gulp-clean-css");
```

- 创建简单的 task 任务

```js
gulp.task("hello", function() {
  console.log("Hello this a gulp task!");
});
```

- 把 less 转换为 css 的 task

```js
gulp.task("less", function() {
  return gulp
    .src("src/less/*.less") //监控文件路径
    .pipe(less())
    .pipe(gulp.gest("src/css")) //转换后文件的输出路径
    .pipe(livereload()); //lss更新时css同步更新
});
```

-  压缩 html 文件

```js
gulp.task("html", function() {
  // 对html文件压缩的参数配置
  var options = {
    removeComments: true, //清除HTML注释
    collapseWhitespace: true, //压缩HTML
    collapseBooleanAttributes: true, //省略布尔属性的值 <input checked="true"/> ==> <input />
    removeEmptyAttributes: true, //删除所有空格作属性值 <input id="" /> ==> <input />
    removeScriptTypeAttributes: true, //删除<script>的type="text/javascript"
    removeStyleLinkTypeAttributes: true, //删除<style>和<link>的type="text/css"
    minifyJS: true, //压缩页面JS
    minifyCSS: true //压缩页面CSS
  };
  return gulp
    .src("src/html/*.html") //文件读取路径
    .pipe(htmlmin(options))
    .pipe(gulp.dest("dist/html")); //文件输出路径
});
```

- 压缩 js 文件

```js
gulp.task("js", function() {
  return gulp
    .src("src/js/*.js") //文件读取路径
    .pipe(uglify())
    .pipe(gulp.dest("dist/js")); //文件输出路径
});
```

- 压缩 css

```js
gulp.task("css", function() {
  return gulp
    .src("src/css/*.css") //文件读取路径
    .pipe(cleanCss())
    .pipe(gulp.dest("dist/css")); //文件输出路径
});
```

- gulp 监控文件变化

```js
gulp.task("auto", function() {
  gulp.watch("src/less/*.less", ["less"]);
  gulp.watch("src/html/*.html", ["html"]);
  gulp.watch("src/css/*.css", ["css"]);
  gulp.watch("src/js/*.js", ["js"]);
});
```
