# The common snippets of the css :blush:

## 布局篇

#### :heartbeat: 样式重置

```css
html {
    font-family: sans-serif;
    /* 1 */
    line-height: 1.15;
    /* 2 */
    -ms-text-size-adjust: 100%;
    /* 3 */
    -webkit-text-size-adjust: 100%;
    /* 3 */
}

body {
    margin: 0;
}

article,
aside,
footer,
header,
nav,
section {
    display: block;
}

h1 {
    font-size: 2em;
    margin: 0.67em 0;
}

figcaption,
figure,
main {
    /* 1 */
    display: block;
}

figure {
    margin: 1em 40px;
}

hr {
    box-sizing: content-box;
    /* 1 */
    height: 0;
    /* 1 */
    overflow: visible;
    /* 2 */
}

pre {
    font-family: monospace, monospace;
    /* 1 */
    font-size: 1em;
    /* 2 */
}

a {
    background-color: transparent;
    /* 1 */
    -webkit-text-decoration-skip: objects;
    /* 2 */
}

a:active,
a:hover {
    outline-width: 0;
}

abbr[title] {
    border-bottom: none;
    /* 1 */
    text-decoration: underline;
    /* 2 */
    text-decoration: underline dotted;
    /* 2 */
}

b,
strong {
    font-weight: inherit;
}

b,
strong {
    font-weight: bolder;
}

code,
kbd,
samp {
    font-family: monospace, monospace;
    /* 1 */
    font-size: 1em;
    /* 2 */
}

dfn {
    font-style: italic;
}

mark {
    background-color: #ff0;
    color: #000;
}

small {
    font-size: 80%;
}

sub,
sup {
    font-size: 75%;
    line-height: 0;
    position: relative;
    vertical-align: baseline;
}

sub {
    bottom: -0.25em;
}

sup {
    top: -0.5em;
}

audio,
video {
    display: inline-block;
}

audio:not([controls]) {
    display: none;
    height: 0;
}

img {
    border-style: none;
}

svg:not(:root) {
    overflow: hidden;
}

button,
input,
optgroup,
select,
textarea {
    font-family: sans-serif;
    /* 1 */
    font-size: 100%;
    /* 1 */
    line-height: 1.15;
    /* 1 */
    margin: 0;
    /* 2 */
}

button,
input {
    /* 1 */
    overflow: visible;
}

button,
select {
    /* 1 */
    text-transform: none;
}

button,
html [type="button"],
/* 1 */

[type="reset"],
[type="submit"] {
    -webkit-appearance: button;
    /* 2 */
}

button::-moz-focus-inner,
[type="button"]::-moz-focus-inner,
[type="reset"]::-moz-focus-inner,
[type="submit"]::-moz-focus-inner {
    border-style: none;
    padding: 0;
}

button:-moz-focusring,
[type="button"]:-moz-focusring,
[type="reset"]:-moz-focusring,
[type="submit"]:-moz-focusring {
    outline: 1px dotted ButtonText;
}

fieldset {
    border: 1px solid #c0c0c0;
    margin: 0 2px;
    padding: 0.35em 0.625em 0.75em;
}

legend {
    box-sizing: border-box;
    /* 1 */
    color: inherit;
    /* 2 */
    display: table;
    /* 1 */
    max-width: 100%;
    /* 1 */
    padding: 0;
    /* 3 */
    white-space: normal;
    /* 1 */
}

progress {
    display: inline-block;
    /* 1 */
    vertical-align: baseline;
    /* 2 */
}

textarea {
    overflow: auto;
}

[type="checkbox"],
[type="radio"] {
    box-sizing: border-box;
    /* 1 */
    padding: 0;
    /* 2 */
}

[type="number"]::-webkit-inner-spin-button,
[type="number"]::-webkit-outer-spin-button {
    height: auto;
}

[type="search"] {
    -webkit-appearance: textfield;
    /* 1 */
    outline-offset: -2px;
    /* 2 */
}

[type="search"]::-webkit-search-cancel-button,
[type="search"]::-webkit-search-decoration {
    -webkit-appearance: none;
}

::-webkit-file-upload-button {
    -webkit-appearance: button;
    /* 1 */
    font: inherit;
    /* 2 */
}

details,
/* 1 */
menu {
    display: block;
}

summary {
    display: list-item;
}

canvas {
    display: inline-block;
}

template {
    display: none;
}

[hidden] {
    display: none;
}
```
> 参考[normalize.css](https://github.com/necolas/normalize.css)

#### :heartbeat: 垂直居中

```css
  /*知道宽高*/
  .verticalCenter{
    width: 100px;
    height: 100px;
    position: absolute;
    top: 50%;
    left: 50%;
    margin-top: -50px;
    margin-left: -50px;
  }
```

```css
  /*不知道宽高--使用transform*/
  .verticalCenter{
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
  }
```

```css
  /*不知道宽高--使用flex布局*/
  .verticalCenterContainer{
    display: flex;
    justify-content: center;
    align-items: center;
  }
```

#### :heartbeat: 消除表格默认的间隔
```css
  table{
    border-collapse: collapse;
  }
```

#### :heartbeat: 表格列宽自适应
```css
  table td{
    white-space: nowrap;
  }
```

#### :heartbeat: 盒子的阴影

```css
  /*一边阴影*/
  .boxShadow {
    width: 100px;
    height: 100px;
    background-color: red;
    position: relative;
  }

  .boxShadow:after {
    content: '';
    width: 5px;
    height: 90px;
    position: absolute;
    left: 0px;
    top: 10px;
    background-color: green;
    box-shadow: 0px 0px 5px 5px green;
    z-index: -1;
  }
```

```css
  /*两边阴影*/
  .boxShadow{
    width: 100px;
    height: 100px;
    background-color: red;
    box-shadow: 5px 5px 5px green;
  }
```


```css
  /*三边阴影*/
  .boxShadow {
    width: 100px;
    height: 100px;
    background-color: red;
    box-shadow: 5px 5px 5px green;
    position: relative;
  }

.boxShadow:after {
    content: '';
    width: 5px;
    height: 90px;
    position: absolute;
    left: 0px;
    top: 10px;
    background-color: green;
    box-shadow: 0px 0px 5px 5px green;
    z-index: -1;
  }
```


```css
  /*四边阴影*/
  .boxShadow{
    width: 100px;
    height: 100px;
    background-color: red;
    box-shadow: 0px 0px 5px green;
  }
```
#### :heartbeat: 盒子内部阴影

```css
  .boxshadow{
    box-shadow: inset 0 0 5px #ccc;
  }
```
#### :heartbeat: 清除浮动

```css
  .clearfix{
    width:100px;
    height:100px;
    overflow:hidden;
  }
```

```css
  .clearfix:after{
    content:"";
    display: block;
    width:0;
    height:0;
    line-height: 0;
    visibility: hidden;
    clear: both;
  }
```

```css
  .clearfix:after{
    content: "";
    display: table;
    clear: both;
  }
```

#### :heartbeat: 定义文本选择样式

```css
  ::-webkit-selection, ::-moz-selection, ::selection{
    background-color:red;
  }
```


#### :heartbeat: 长文本换行

```css
  .wrap{
    white-space: pre;
    word-wrap: break-word;
  }
```

#### :heartbeat: 设置透明度

```css
  .opacity{
    opacity:0.5;
    filter:alpha(opacity=50);
  }
```
#### :heartbeat: css设置背景全屏

```css
  html{
    background: url() no-repeat center center fixed;
    background-size: cover;
  }
```

#### :heartbeat: css3渐变模板

```css
  .gradient{
    background:#bca321;
    background-image:linear-gradient(top, #000, #fff);
    background-image:-o-linear-gradient(top, #000, #fff);
    background-image:-moz-linear-gradient(top, #000, #fff);
    background-image:-ms-linear-gradient(top, #000, #fff);
    background-image:-webkit-linear-gradient(top, #000, #fff);
    background-image:-webkit-gradient(linear, left top, from(#000), to(#fff));
  }
```
#### :heartbeat: @font-face模板

```css
  @font-face{
     font-family: 'custormFont';
     src: url('webfont.eot'); /* IE9 Compat Modes */
     src: url('webfont.eot?#iefix') format('embedded-opentype'), /* IE6-IE8 */
     url('webfont.woff') format('woff'), /* Modern Browsers */
     url('webfont.ttf')  format('truetype'), /* Safari, Android, iOS */
     url('webfont.svg#svgFontName') format('svg'); /* Legacy iOS */
  }
  body{
    font-family: 'custormFont', 'Arial', '微软雅黑';
  }
```

#### :heartbeat: 隔行变色

```css
  table tr:nth-child(even){
    background-color:#ccc;
  }
  table tr:nth-child(odd){
    background-color:#eee;
  }
```

#### :heartbeat: 首字突出显示

```css
  div::first-letter{
    float: left;
    color:#000;
    font-size:3em;
    margin:5px 0 0 5px;
  }
```

#### :heartbeat: 兼容设置最小高度

```css
  .minHeight{
    min-height:300px;
    height:auto !important;
    height:300px;
  }
```
#### :heartbeat: 不同的链接显示
```css
  a[href^="http://"]{
    padding-left:20px;
    background:url();
  }
  a[href$=".pdf"]{
    padding-left:20px;
    background:url();
  }
  a[href$=".ppt"]{
    padding-left:20px;
    background:url();
  }
```

#### :heartbeat: 禁用移动端的选择高亮显示

```css
  body{
    user-select: none;
    -webkit-touch-callout: none;
    -webkit-user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
  }
```
