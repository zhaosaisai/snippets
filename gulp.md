# The common snippets of the gulp :blush:

#### :heartbeat: gulp-sass：编译sass

```javascript
// 基本使用
const gulp = require('gulp');
const sass = require('gulp-sass');

gulp.task('sass', () => {
  return gulp.src('./sass/**/*.scss')
      .pipe(sass().on('error', sass.logError))
      .pipe(gulp.dest('./css'))
})


gulp.task('default', ['sass']);
```
```javascript
  //指明输出的格式
const gulp = require('gulp');
const sass = require('gulp-sass');

gulp.task('sass', () => {
  return gulp.src('./sass/**/*.scss')
        //outputStyle指明输出格式：compressed,
        .pipe(sass({outputStyle:'compressed'}).on('error', sass.logError))
        .pipe(gulp.dest('./css'))
})


gulp.task('default', ['sass']);

```

#### :heartbeat: gulp-sourcemaps：生成sourcemaps

```javascript
const gulp = require('gulp');
const sass = require('gulp-sass');
const sourcemaps = require('gulp-sourcemaps');

gulp.task('sass', () => {
  return gulp.src('./sass/**/*.scss')
      //先调用init
      .pipe(sourcemaps.init())
      .pipe(sass().on('error', sass.logError))
      //调用write()-无参数，sourcemap在源文件中
      .pipe(sourcemaps.write())
      .pipe(gulp.dest('./css'))
})


gulp.task('default', ['sass']);

```

```javascript
const gulp = require('gulp');
const sass = require('gulp-sass');
const sourcemaps = require('gulp-sourcemaps');

gulp.task('sass', () => {
  return gulp.src('./sass/**/*.scss')
      .pipe(sourcemaps.init())
      .pipe(sass().on('error', sass.logError))
      //传递一个路径--存放sourcemaps文件
      .pipe(sourcemaps.write('./sassmaps'))
      .pipe(gulp.dest('./css'))
})


gulp.task('default', ['sass']);

```
#### :heartbeat: gulp-uglify：压缩js文件

```javascript
// 基本使用
const gulp = require('gulp');
const uglify = require('gulp-uglify');

gulp.task('uglify', () => {
  return gulp.src('./src/**/*.js')
      .pipe(uglify())
      .pipe(gulp.dest('./js'))
})

gulp.task('default', ['uglify']);

```

```javascript
//添加错误处理
const gulp = require('gulp');
const uglify = require('gulp-uglify');

gulp.task('uglify', () => {
  return gulp.src('./src/**/*.js')
        .pipe(uglify())
        .pipe(gulp.dest('./js'))
        .on('error', (err) => {
          console.error('the error happening', err.toString());
        })
})

gulp.task('default', ['uglify']);

```

```javascript
//结合pump使用
const gulp = require('gulp');
const uglify = require('gulp-uglify');
const pump = require('pump');

gulp.task('uglify', (cb) => {
  pump([
    gulp.src('./src/**/*.js'),
    uglify(),
    gulp.dest('./js')
  ],cb)
})

gulp.task('default', ['uglify']);

```
#### :heartbeat: gulp-imagemin：压缩图片
```javascript
const gulp = require('gulp');
const imagemin = require('gulp-imagemin');

gulp.task('imagemin', () => {
  return gulp.src('./images/*.*')
         .pipe(imagemin({
           progressive:true
         }))
         .pipe(gulp.dest('./dist/images'))

})

gulp.task('default', ['imagemin']);
```
#### :heartbeat: gulp-babel：编译es6

```javascript
//转换成普通的es5 有的特性不能转换
const gulp = require('gulp');
const babel = require('gulp-babel');

gulp.task('babel', () => {
  return gulp.src('./src/**/*.js')
         .pipe(babel({
           presets:['es2015']
         }))
         .pipe(gulp.dest('./js'));
})

gulp.task('default', ['babel']);
```

```javascript
//可以使用generator特性
const gulp = require('gulp');
const babel = require('gulp-babel');

gulp.task('babel', () => {
  return gulp.src('./src/**/*.js')
         .pipe(babel({
           plugins:['transform-runtime']
         }))
         .pipe(gulp.dest('./js'));
})

gulp.task('default', ['babel']);

```

#### :heartbeat: gulp结合browser-sync自动刷新
