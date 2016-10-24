# The common snippets of the nodejs :blush:

#### path基本方法

```javascript
const path = require('path');

//规范化字符串
path.normalize('github.com//seeyou404/../index');
//=>'github.com/index'
path.normalize('github.com//seeyou404/./index/..//route');
//=>'github.com/seeyou404/route'

//连接路径--参数必须是字符串
path.join('seeyou404', 'index', 'vevdor');
//=>'seeyou404/index/vevdor'
path.join('seeyou404', 'index', '../', 'vevdor');
//=>'seeyou404/vevdor'

//将相对路径转换成绝对路径
path.resolve('seeyou404', 'index');
//=> 当前文件的绝对路径/seeyoy404/index
path.resolve('seeyou404', 'index', '/js', '../');
//=> /
path.resolve('seeyou404', 'index', './js', '../');
//=> 当前文件的绝对路径/seeyoy404/index

//将两个绝对路径转换成相对路径--参数必须是绝对路径--相对路径会先转换成绝对路径
path.relative('/seeyou404', '/seeyou404/index');
//=> index
path.relative('/seeyou404', '/index');
//=> ../index

// 获取文件所在的路径--获取最后一个路径分割符前的地址
path.dirname('./index/index.js');
//=> ./index
path.dirname('./index/js');
//=> ./index

// 获取文件的后缀
path.extname('./index/index.js');
//=> .js
path.extname('./index/js');
//=> ''

// 获取文件的名称
path.basename('./index/index.js');
//=> index.js
path.basename('./index/index.js', '.js');
//=> index
path.basename('./index/index.js', 'dex.js');
//=> in
path.extname('./index/js');
//=> ''
```
