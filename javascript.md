# The common snippets of the javascript :blush:


#### 防反跳 / debounce

```js
const debounce = (action, delay) => {
  let timer
  return function () {
    var context = this
    var args = arguments
    clearTimeout(timer)
    timer = setTimeout(() => { action.apply(context, args) }, delay)
  }
}
```

#### 拉平数组 / flatten

```js
const flatten = arr => {
    let list = []
    const flattenFunc = arg => arg.forEach(item => Array.isArray(item) ? flattenFunc(item) : list.push(item))
    flattenFunc(arr)
    return list
}
```

#### 获取函数的返回值 / value

```js
const value = func => {
  const valueFunc = arg => typeof arg === 'function' ? valueFunc(arg()) : arg
  return valueFunc(func)
}
```

#### 动态加载javascript

```javascript
  function loadScript(url, callback){
    var script = document.createElement('script');
    script.type = 'text/javascript';

    if(script.readyState){ //IE
      script.onreadystatechange = function(){
        if(script.readyState === 'loaded' || script.readyState === 'complete'){
          script.onreadystatechange = null;
          callback()
        }
      }
    }else{ //Others
      script.onload = callback.call(this);
    }

    script.url = url;
    document.getElementsByTagName('head')[0].appendChild(script);
  }
```

> From:[The best way to load external JavaScript](https://www.nczonline.net/blog/2009/07/28/the-best-way-to-load-external-javascript/)

#### 移动端页面初始化


```javascript
  ;(function(factory){
    window.factory = factory(window, document);

    return window.factory;
  })(function(win, doc){
    var context = {
      init:function(scale){
        var html = document.documentElement;
        var width = html.clientWidth > scale ? scale : html.clientWidth;
        var dpr = window.devicePixelRatio >= 1.5 ? 2 : window.devicePixelRatio;

        //设置html的dpr和fontsize
        html.setAttribute('data-dpr', dpr);
        html.style.fontSize = width * 100 / scale + 'px';

        //设置body的宽度--可以解决微信内置浏览器里面的一个小bug
        this.setBody();
      },
      view:function(){
        return {
          w:document.documentElement.clientWidth,
          h:document.documentElement.clientHeight
        }
      },
      setBody:function(){
        var body = document.body;
        body.style.width = this.view().w + 'px';
        body.style.height = this.view().h + 'px';
      }
    }
  })
```

#### 获取随机数

```javascript
  function getRandom(min, max){
    //左开右闭
    return Math.ceil(Math.random() * (max - min + 1) + min);
  }
```

```javascript
  function getRandom(min, max){
    //左闭右开
    return Math.floor(Math.random() * (max - min + 1) + min);
  }
```

```javascript
  function getRandom(min, max){
    //闭区间
    return Math.round(Math.random() * (max - min + 1) + min, 10);
  }
```
#### 获取元素的计算之后的样式

```javascript
  function getStyle(obj, attr){
    return obj.currentStyle ? obj.currentStyle[attr] : getComputedStyle(obj, null)[attr];
  }
```
#### 判断对象的数据类型

```javascript
  function type(obj){
    return Object.prototype.toString.call(obj).match(/\s(\w+)/)[1].toLowerCase();
  }
```

#### 对象复制

```javascript
  function copy(obj, deep){
    var result = '';
    if(type(obj) !== 'object') return;
    //利用JSON的方法进行深复制和浅复制
    return result = deep ? JSON.parse(JSON.stringify(obj)) : obj;
  }
```
#### 判断网页是否在微信浏览器打开

```javascript
  function isWeChat(){
    return navigator.userAgent.toLowerCase().match(/MicroMessenger/i) === "micromessenger";
  }
```

#### 判断手机系统

```javascript
  function isApple(){
    return /ip(hone|ad|od)/i.test(navigator.userAgent.toLowerCase());
  }
```
```javascript
  function isAndroid(){
    return /android/i.test(navigator.userAgent.toLowerCase());
  }
```
#### 获取查询字符串的值

```javascript
    function getQuery(url){
      var arr = [];
      var query = {};

      url = url && url.charAt(0) === '?' ? url.slice(1) : url || location.search.slice(1);
      arr = url.split('&');

      arr.forEach(function(v){
        var a = v.split('=');
        query[a[0]] = encodeURIComponent(a[1]);
      })

      return query;
    }
```
#### 获取元素在页面中的位置

```javascript
  function getPosition(ele){
    var position = {
      left:ele.offsetLeft,
      top:ele.offsetTop
    };
    var currentParent = ele.offsetParent;

    while (currentParent !== null) {
      position.left += currentParent.offsetLeft;
      position.top += currentParent.offsetTop;
      currentParent = currentParent.offsetParent;
    }

    return position;
  }
```

```javascript
  function getPosition(ele){
    return ele.getBoundingClientRect();
  }
```
#### js仿照md5

```javascript
  function md5(){
    var str = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/';
    return str.split('').sort(function(v1,v2){
      return Math.random() > 0.5;
    }).join('').slice(0, 32);
  }
```
#### 获取星期几

```javascript
  function getDay(){
    var arr = ['星期天', '星期一', '星期二', '星期三', '星期四', '星期五', '星期六'];
    return arr[new Date().getDay()];
  }
```

#### requestAnimationFrame的兼容性处理

```javascript
  ;(function(){
    var lastTime = 0;
    var vendors = ['ms', 'moz', 'webkit', 'o'];

    for(var i = 0; i < vendors.length && !window.requestAnimationFrame; ++i){
      window.requestAnimationFrame = window[vendors[i] + 'RequestAnimationFrame'];
      window.cancelAnimationFrame = window[vendors[i] + 'CancelAnimationFrame'] ||  window[vendors[x] + 'CancelRequestAnimationFrame'];
    }

    if (!window.requestAnimationFrame) window.requestAnimationFrame = function(callback, element) {
        var currTime = new Date().getTime();
        var timeToCall = Math.max(0, 16 - (currTime - lastTime));
        var id = window.setTimeout(function() {
            callback(currTime + timeToCall);
        }, timeToCall);
        lastTime = currTime + timeToCall;
        return id;
    };
    if (!window.cancelAnimationFrame) window.cancelAnimationFrame = function(id) {
        clearTimeout(id);
    };
  })()
```
#### 数组去重

```javascript
Array.prototype.unique = function() {
  return Array.from(new Set(this));
}
```

```javascript
Array.prototype.unique = function() {
  var sortArr = this.sort();
  return sortArr.filter(function(v,i,context){
    return v != context[i+1];
  })
}
```

```javascript
Array.prototype.unique = function() {
  var result = [];
  this.forEach(function(v){
    if(result.indexOf(v) === -1){
      result.push(v);
    }
  })
  return result;
}
```

```javascript
Array.prototype.unique = function() {
  var json = {};
  var result = [];
  this.forEach(function(value){
    var type = Object.prototype.toString.call(value).match(/\s(\w+)/)[1].toLowerCase();
    if(!((type + '-'+value) in json)){
      json[type + '-'+value] = true;
      result.push(value);
    }
  })
  return result;
}
```

```javascript
Array.prototype.unique = function() {
  var sortArr = this.sort(),
    i = 0;
  for(; i < sortArr.length; i++){
    if(sortArr[i] === sortArr[i+1]){
      sortArr.splice(i,1);
      i--;
    }
  }
  return sortArr;
}
```

```javascript
Array.prototype.unique = function() {
  var sortArr = this.sort(), result = [];
  sortArr.reduce((v1,v2) => {
    if(v1 !== v2){
      result.push(v1);
    }
    return v2;
  })
  result.push(sortArr[sortArr.length - 1]);
  return result;
}
```

#### 操作className

```javascript
//操作className时候的辅助函数
function toArray(argu){
  var splitText = typeof argu === 'string' ? (argu.indexOf(' ') !== -1 ? ' ' : ',') : ' ';
  return Array.isArray(argu) ? argu : argu.split(splitText);
}
```
>说明：以下四种方法的参数的形式可以为以下几种

> * 数组：['classname1', 'classname2']
> * string
>  * 单字符串:'classname1'
>  * 空格分隔: 'classname1 classname2'
>  * 逗号分隔: 'classname1, classname2'

```javascript
HTMLElement.prototype.hasClass = function (classname) {
  let selfClass = this.className.split(' ');
      classname = toArray(classname);
  if(this.classList){
    for(let v of classname){
      if(!this.classList.contains(v)){
        return false;
      }
    }
  }else{
    for(let v of classname){
      if(selfClass.indexOf(v) === -1){
        return false;
      }
    }
  }
  return true;
}
```

```javascript
HTMLElement.prototype.addClass = function (classname) {
  return this.className = Array.from(new Set((toArray(classname).join(' ') + ' ' + this.className).split(' '))).join(' ');
}
```

```javascript
HTMLElement.prototype.addClass = function (classname) {
  classname = toArray(classname);
  classname.forEach(function(v){
    if(!this.hasClass(v)){
      this.className += ' ' + v;
    }
  }.bind(this))
  return this;
}
```

```javascript
HTMLElement.prototype.removeClass = function (classname) {
  var selfClass = Array.from(new Set(this.className.split(' ')));
      classname = toArray(classname);
  classname.forEach(function(v){
    if(selfClass.indexOf(v) !== -1){
      selfClass.splice(selfClass.indexOf(v), 1);
    }
  })
  this.className = selfClass.join(' ');
  return this;
}
```

```javascript
HTMLElement.prototype.toggleClass = function (classname) {
  classname = toArray(classname);
  classname.forEach(function(v){
    if(this.hasClass(v)){
      this.removeClass(v)
    }else{
      this.addClass(v);
    }
  }.bind(this))
}
```

#### 判断网页运行在电脑还是手机

```javascript
  //返回true是手机，否则是电脑
  const isMobile = () => {
    return ['android', 'iphone', 'symbianos', 'windows phone', 'ipad', 'ipod'].some((v) => {
      return navigator.userAgent.toLowerCase().indexOf(v) >= 0;
    })
  }
```

#### 转意html

```javascript
  const escapeHTML = (html) => {
    let htmlMap = {
      '<': "&lt;",
      '>':'&gt;',
      '&':'&amp',
      '"':'&quot;'
    };

    return html.replace(/[<>"&]/g, (char) => htmlMap[char]);
  }
```

### 操作cookie

```javascript
/*
  这里主要是一些操作cookie时候的一些工具方法
*/
class Utils {

  //第一个方法主要用于转义cookie里面的特殊字符
  encode(str){
    return String(str).replace(/[,;"\s%\\]/g, (c) => encodeURIComponent(c));
  }

  //第二个方法主要是用于对比编码的字符串进行解码的方法
  decode(str){
    return decodeURIComponent(str);
  }

  //第三个方法主要是用于判断变量是不是纯粹的javascript对象的方法
  isPlainObject(obj){
    return !!obj && Object.prototype.toString.call(obj) === '[object Object]';
  }

  //第四个方法主要是进行回退的方法
  fallback(value, fallback){
    return value == null ? fallback : value;
  }
}
export default new Utils();
```

```javascript
import util from './utils.js';
/*
  这个是操作cookie的主要的类
*/
class Cookie{

  constructor(config){
    this.defaultConfig = util.isPlainObject(config) ? config : {path: '/', domain:'', secure: false, expires: 1};
    this.defaultTime = 60 * 60 *24 * 1000;
  }

  set(key, value, options){
    //设置cookie的方法--主要有两种设置形式，key为字符串或者对象也可以是数组。当key是字符串的时候，value就是其对应的值，当key是对象的时候，则键表示cookie的名称
    //值表示cookie的值，value参数则是options设置对象，此时所有的cookie共用一个相同的选项设置对象
    //当cookie是数组的时候，设置形式如下 [{name:value, 'options':{这个对象就是对应的配置选项}},...]
    //name就是cookie的名称 value就是cookie的值  option就是这个cookie对应的选项对象

    //先判断是不是对象--是对象的话，就利用循环转换成不是对象的cookie的设置方式
    if(util.isPlainObject(key)){
      //key是对象的情况--先判断一下key.option是否存在，存在则使用这个，不存在则使用options。注意这个时候的options是设置在value上的
      value = key.option ? key.option : value;
      Object.keys(key).forEach((v) => {
        v !== 'option' && this.set(v, key[v], value);
      })
    }else if(Array.isArray(key)){
      //key是数组的情况
      key.forEach((v) => {
        this.set(v, value);
      })
    }else{
      //key是字符串的情况
      //先对options进行类型的判断
      options = util.isPlainObject(options) ? options : {expires:1}
      //然后再获取到cookie中最重要的一项设置--expires
      let expires = options.expires || this.defaultConfig.expires || 1;
      let path = options.path || this.defaultConfig.path || '/';
      let secure = options.secure || this.defaultConfig.secure || false;
      let domain = options.domain || this.defaultConfig.domain || '';
      let expiresType = typeof expires;
      if(expiresType === 'string'){
        expires = new Date(expires);
      }else if(expiresType === 'number'){
        expires = new Date(Date.now() + this.defaultTime * expires);
      }
      //然后在对expires进行标准化
      ('toGMTString' in expires) && (expires = expires.toGMTString());
      //设置cookie
      document.cookie = `${util.encode(key)}=${util.encode(value)}; path=${path}; domain=${domain}; expires=${expires}; secure=${secure}`;
    }

  }

  get(key){
    //获取cookie的方法--如果不传递参数，则默认是获取所有的cookie,以json对象的形式返回-也可以传递一个参数--获取指定名称的cookie
    let cookies = document.cookie;
    let cookieResult = {};
    let result = {};

    //浏览器客户端没有cookie，则直接返回
    if(cookies == "") return;

    cookies.split('; ').forEach((value) => {
      value.replace(/^(.+)=(.+)$/g, (a, k, v) => {
        cookieResult[k] = v;
      })
    })
    //利用参数判断返回的情况
    //这里主要分三种情况--1、key是字符串，返回对应的cookie值--2、key是数组，返回一个包含这些名称的json对象--3、key不存在，直接返回所有的cookie，json对象格式
    if(key && Array.isArray(key)){
      key.forEach((v) => {
        result[v] = cookieResult[v];
      })
    }else if(key && typeof key === 'string'){
      result = cookieResult[key];
    }else{
      result = cookieResult;
    }
    return result;
  }

  clear(key){
    //删除cookie的方法
    //分三种情况--1、key为undefined：删除所有的cookie
    //           2、key为数组：删除数组内指定的cookie
    //           3、key为字符串：删除指定名称的cookie
    let keyArr = Array.isArray(key) ? key : (key !== undefined ? [key] : Object.keys(this.get()));
    keyArr.forEach((v) => {
      this.set(v, '', {expires:-1});
    })
  }

  isabled(){
    //判断cookie是否能用的方法
    return navigator.cookieEnabled;
  }
}
export default Cookie;
```

### 函数节流

```javascript
function throttle(func, wait, options){
  //设置三个变量用于保存信息
  var context,  //保存上下文
      args, //保存参数
      result; //保存函数的返回值

  //设置一个保存定时器的timer
  var timeout = null;

  //设置上一次函数执行的时间戳
  var previous = 0;

  //设置options的默认值
  if(!options){
    options = {};
  }

  //设置执行函数
  var later = function(){
    //如果options.leading为false则每次出发回调后将previous置为0
    previous = options.leading === false ? 0 : Date.now();

    timeout = null;

    result = func.apply(context, args);

    if(!timeout){
      context = args = null;
    }
  }

  return function(){

    //先保存这次函数的执行时间
    var now = Date.now();

    //接着判断是否需要在刚刚开始的时候执行函数
    if(!previous && options.leading === false){
      //进到这里面说明就不需要
      previous = now;
    }

    //接着在获取到时间的差值
    var remaining = wait - (now - previous);  //主要比较的就是两次函数的执行时间和预先设定的时间的差值

    //保存这个函数的上下文和参数
    context = this;
    args = arguments;

    //开始根据判断条件进行函数的调用
    if(remaining < 0 || remaining > wait){
      //进入到这里就表示函数可以进行调用了
      //remaining < 0 一开始就要执行
      //remaining > wait 正常的执行条件

      if(timeout){
        //如果存在定时器，说明还有没有执行的定时器，清除掉
        clearTimeout(timeout);
        timeout = null;
      }

      //重置这次函数的执行时间，下次执行的时候需要判断
      previous = now;

      //执行函数
      result = func.apply(context, args);

      //重置变量，防止内存泄漏
      if(!timeout){
        context = args = null;
      }
    }else if(!timeout && options.trailing !== false){
      //最后一次需要出发的情况
      timeout = setTimeout(later,remaining);
    }

    //返回结果
    return result;
  }

}
```

### 函数去抖

```javascript
function debounce(func, wait, immedicate){
  /*
    参数的基本解释：
      func: function 需要进行去抖的函数
      wait： 去抖时间
      immedicate： 设置去抖函数的触发时机，设置为true则事件发生的时候立即触发。否则在事件结束wait时间之后触发
  */

  //设置几个需要用到的局部变量
  var context, //存储this
      args, //存储传递给去抖函数的参数
      timestamp, //存储每次函数触发的时间
      timeout, //存储对定时器的引用
      result; //存储原函数的返回值

      //主要就是这个函数，这个函数就是定时器调用的函数，我们需要在这个函数里面做一件十分重要的事就是判断函数触发的时机

      var later = function(){

        //首先获取时间差
        var last = Date.now() - timestamp;

        //再看一下有没有达到函数调用的时间
        if(last < wait && last >= 0){
          //重置函数调用
          timeout = setTimeout(later, wait - last);
        }else{
          //说明可以调用函数了，
          //吧timeout设置为null，以便下次判断
          timeout = null;
          //但是需要先判断一下immedicate，因为如果这个为true，则我们不需要调用了
          if(!immedicate){
            //说明不是立即调用
            result = func.apply(context, args);
            if(!timeout){
              context = args = null;
            }
          }
        }
      }

      return function(){
        //闭包的形式，方便传递参数
        context = this;
        args = arguments;

        //每次函数调用的时间
        timestamp = Date.now();

        var callNow = immedicate && !timeout; //immedicate为true且函数不是第一次调用

        if(!timeout){
          //如果能进到这里，表示的是这个函数不是第一次触发了
          //如果是第一次触发，我们需要调用定时器了
          timeout = setTimeout(later, wait);
        }
        if(callNow){
          //如果是立即调用，就直接调用func函数
          result = func.apply(context, args);
          context = args = null; //释放资源
        }
        return result;
      }
}
```

### 求数组最大值

```javascript
const arrayMax = arr => Math.max(...arr)
```

### 求数组的最小值

```javascript
const arrayMin = arr => Math.min(...arr)
```

### chunk函数

```javascript
const chunk = (arr, size) => Array.from({length: Math.ceil(arr.length / size)}, (v, i) => arr.slice(i * size, i * size + size))
```

### compact: 去除数组中值为falsey的元素

```javascript
const compact = (arr) => arr.filter(Boolean)
```

### 计算一个值在数组中出现的次数

```javascript
const countOccurrences = (arr, value) => arr.reduce((a, v) => v === value ? a + 1 : a + 0, 0)
```

### deepFlatten: 拉平数组

```javascript
const deepFlatten = (arr) => [].concat(...arr.map(v => Array.isArray(v) ? deepFlatten(v) : v))
```

### difference: 返回数组的差值

```javascript
const difference = (a, b) => {
  const s = new Set(b)
  return a.filter(x => !s.has(x))
}
```

### 删除数组中的元素，直到回调函数返回true

```javascript
const dropElements = (arr, func) => {
  while(arr.length > 0 && !func(arr[0])) {
    arr.shift()
  }
  return arr
}
```

### 返回索引是某个值的倍数的元素

```javascript
const everyNth = (arr, nth) => arr.filter((e, i) => i % nth === 0)
```

### 过滤出数组中没有重复值的元素

```javascript
const filterNoneUnique = arr => arr.filter(i => arr.indexOf(i) === arr.lastIndexOf(i))
```

### 拉平数组

```javascript
const flatten = arr => arr.reduce((a, v) => a.concat(v), [])
```

### 拉平数组(深拉平)

```javascript
const flattenDepth = (arr, depth = 1) => depth != 1 ? arr.reduce((a, v) => a.concat(Array.isArray(v) ? flattenDepth(v, depth - 1) : v), []) : arr.reduce((a, v) => a.concat(v), [])
```

### 对数组按照特定条件分组

```javascript
const groupBy = (arr, func) => arr.map(typeof func === 'function' ? func : val => val[func])
                                  .reduce((acc, val, i) => {
                                    acc[val] = (acc[val] || []).concat(arr[i])
                                    return acc
                                  }, {})
```

### 返回数组的第一个元素

```javascript
const head = arr => arr[0]
```

### 返回除数组最后一个元素之外的所有元素

```javascript
const initial = arr => arr.slice(0, -1)
```

### 初始化范围数组

```javascript
const initializeArrayWithRange = (end, start = 0) => Array.from({length: end - start}).map((v, i) => i + start)
```

### 初始化并以特定的值填充数组

```javascript
const initializeArrayWithValues = (n, value = 0) => Array(n).fill(value)
```

### 返回数组交集

```javascript
const intersection = (a, b) => {
  const s = new Set(b)
  return a.filter(x => s.has(x))
}
```

### 返回数组的最后一个元素

```javascript
const last = arr => arr[arr.length - 1]
```

### 将数组中的值映射到对象

```javascript
const mapObject = (arr, fn) => {
  const keyValue = [arr, arr.map(fn)]
  return keyValue[0].reduce((acc, val, ind) => (acc[val] = keyValue[1][ind], acc), {})
}
```

### 返回数组的第n个元素

```javascript
const nthElement = (arr, n = 0) => (n > 0 ? arr.slice(n + 1) : arr.slice(n))[0]
```

### 从对象中选取给定键的键值对

```javascript
const pick = (obj, arr) => arr.reduce((acc, curr) => (curr in obj && (acc[curr] = obj[curr]), acc), {})
```

### 从数组中筛选指定的值

```javascript
const pull = (arr, ...args) => {
  let pulled = arr.filter(v => !args.includes(v))
  arr.length = 0
  pulled.forEach(v => arr.push(v))
}
```

### 从数组中移除使给定函数返回false的元素

```javascript
const remove = (arr, func) => Array.isArray(arr) ? arr.filter(func).reduce((acc, val) => {
  arr.splice(arr.indexOf(val), 1)
  return acc.concat(val)
}, []) : []
```