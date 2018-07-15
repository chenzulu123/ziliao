### gulp的最佳实践

##### 创建 package.json 文件
```js
{
  "name": "autopractice",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC",
  "dependencies": {
    "browser-sync": "^2.10.1",
    "coffee-script": "^1.10.0",
    "gulp": "^3.9.0",
    "gulp-clean": "^0.3.1",
    "gulp-coffee": "^2.3.1",
    "gulp-concat": "^2.6.0",
    "gulp-connect": "^2.3.1",
    "gulp-jade": "^1.1.0",
    "gulp-jshint": "^2.0.0",
    "gulp-less": "^3.0.5",
    "gulp-livereload": "^3.8.1",
    "gulp-minify-css": "^1.2.2",
    "gulp-plumber": "^1.0.1",
    "gulp-uglify": "^1.5.1",
    "gulp-webpack": "^1.5.0",
    "jade": "^1.11.0",
    "jshint": "^2.8.0"
  }
}
```

##### 进入文件夹以后通过 npm install 进行相关插件的下载和安装
* gulp 配置文件的内容

```js
// 导入需要的模块
var gulp = require("gulp"),
  less = require("gulp-less"),
  jade = require("gulp-jade"),
  coffee = require("gulp-coffee"),
  concat = require("gulp-concat"),
  uglify = require("gulp-uglify"),
  browserSync = require("browser-sync").create(),
  plumber = require("gulp-plumber"),
  minifyCss = require("gulp-minify-css");
```

```js
// 编译less，其中plumber是防止出错崩溃的插件
gulp.task("less", function() {
  gulp
    .src("src/less/*.less")
    .pipe(plumber())
    .pipe(less())
    .pipe(gulp.dest("dist/css"));
});
```

```js
// 编译jade
gulp.task("jade", function() {
  gulp
    .src("src/jade/*.jade")
    .pipe(plumber())
    .pipe(jade())
    .pipe(gulp.dest("public"));
});
```

```js
// 编译coffee
gulp.task("coffee", function() {
  gulp
    .src("src/coffee/*.coffee")
    .pipe(plumber())
    .pipe(coffee())
    .pipe(gulp.dest("dist/js"));
});
```

```js
// 将所有css文件连接为一个文件并压缩，存到public/css
gulp.task("concatCss", function() {
  gulp
    .src(["dist/css/*.css"])
    .pipe(concat("main.css"))
    .pipe(minifyCss())
    .pipe(gulp.dest("public/css"));
});
```

```js
// 将所有js文件连接为一个文件并压缩，存到public/js
gulp.task("concatJs", function() {
  gulp
    .src(["dist/js/*.js"])
    .pipe(concat("main.js"))
    .pipe(uglify())
    .pipe(gulp.dest("public/js"));
});
```

```js
// 默认任务
gulp.task("default", ["watch"]);
```

```js
// 监听任务
gulp.task("watch", function() {
  // 建立浏览器自动刷新服务器
  browserSync.init({
    server: {
      baseDir: "public"
    }
  });

  // 预处理
  gulp.watch("src/jade/**", ["jade"]);
  gulp.watch("src/coffee/**", ["coffee"]);
  gulp.watch("src/less/**", ["less"]);

  // 合并压缩
  gulp.watch("dist/css/*.css", ["concatCss"]);
  gulp.watch("dist/js/*.js", ["concatJs"]);

  // 自动刷新
  gulp.watch("public/**", function() {
    browserSync.reload();
  });
});
```
