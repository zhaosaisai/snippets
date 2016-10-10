# The fields of the package.json file :blush:

#### :heartbeat: package.json

```javascript
  {
    "name":包的名称，必须滴，毕竟每件东西都有名字。(没有是无法install的),
    "version":版本号，必须滴，没有是无法install的,
    "description":对你的包的简单描述，随便写，尽量符合你的包的特点,
    "keywords":关键字，便于search,
    "homepage":项目的主页，可选的，有最好写上，方便别人查看和装逼,
    "bugs":{
      //是一个对象，下面的两种方式可全写或其一，就是用来别人反馈你的bug的
      "url":提交bug的url,
      "email":提交bug的email
    },
    "license":许可证，告诉别人，他有什么权力，他有什么限制。如果你使用的是通用的许可证，直接写一个名字即可。用的是复杂的，可提供一个对象。如下：
    "licenses" : [
      { "type" : "MyLicense",
         "url" : "http://github.com/owner/project/path/to/license"
      }
    ],
    "author":作者，你自己,
    "contributors":数组，谁给你的项目做了贡献，就把谁加进去，别让人家骂你,
    "person":{
      //提供详细信息的，可提供下面三个字段
      "name":就是名字,
      "url":本尊对应的url,
      "email":本尊的email
    },
    "files":数组，包含项目中的文件。受 .npmignore 文件的影响,
    "main":指定包的入口文件的名称，就是别人直接使用你的包的名称的时候，程序会从这个字段指定的文件开始运行。相对于根目录的文件路径,
    "bin":挺牛掰的一个玩意，可以是一个命令到文件名称的映射,也可以是一个字符串，那么这时候可执行文件的名称就是包的名称,
    "man":单一的文件名称或者是一个包含文件名称的数组，主要用于让man程序使用,
    "directories":{
      "lib":我们的库文件夹放在什么地方,
      "bin":指定bin字段的位置，前提是你没有指定bin属性，否则无效,
      "man":当前模块man文档的位置,
      "doc":文档，一般是md文件
    },
    "repository":{
      //指定你的代码存放的位置
      "type":存放代码的工具，比如git，svn,
      "url":代码存放位置的url，以github为例，可能是下面这种形式:http://github.com/seeyou404/snippets.git
    },
    "scripts":{
      //这个字段比较高大上，主要用于简写npm命令的，也可以理解成，给你的命令定义一些别名，刻意直接通过npm run 命令名进行运行
    },
    "config":{
      //配置npm包中的一些命令，可以通过npm_package_config_名称来获取
    },
    "dependencies":{
      //用于定义项目开发时所依赖的模块，基本形式如下：
      "模块名称":一个表示范围的版本号或者是一个git url
    },
    "peerDependencies":{
      //如果一个模块只能够依赖另一个模块的摸个版本运行，那么，我们需要在这里指定，此时，当用户安装的时候，如果安装的时候不符合版本约定，那么就是提醒用户
    },
    "bundledDependencies":数组，指定一组包名，会在发布的时候打包进去，也可以写成bundleDependencies,
    "optionalDependencies":指定可选的依赖，啥意思呢，就是一个依赖可用可不用，安装成功就使用，在安装失败的时候npm也能够继续初始化，这里的包会覆盖掉同名的dependencies里面同名的项,
    "engines":{
      //指明一些程序的版本，比如node，npm
      "node":">=4.1.2 <6.0.0"
    },
    "engineStrict":一个非常不建议使用的属性，知道有它就好了,
    "os":指定我们的包所能够运行的操作系统,
    "cpu":指定我们的包运行的cpu架构,
    "preferGlobal":如果你的包希望全局安装使用，把它设置为true，那么当用户局部安装的时候，会给出一个警告,
    "private":把包设置成私有的，npm不会发布它,
    "publishConfig":发布的时候使用的配置集合
}
```
> [参考](http://mujiang.info/translation/npmjs/files/package.json.html)

#### :heartbeat: 版本号解释

```javascript
  {
    "version":必须和指定的version一致,
    ">version":必须比指定的version的版本大,
    ">=version":大于或等于指定的version,
    "<version":必须小于指定的version版本,
    "<=version":小于或等于指定的版本,
    "~version":不改变大版本号和次要版本号的所有版本,
    "1.3.x":1.3.0，1.3.1等大版本号是1次要版本号是3的所有版本,
    "version1 || version2":几个里面选一个,
    "version1-version2":相当于>=version1 <=version2,

}
```
#### :heartbeat: 实例参考:npm的package.json文件

```javascript
{
  "version": "3.10.9",
  "name": "npm",
  "description": "a package manager for JavaScript",
  "keywords": [
    "install",
    "modules",
    "package manager",
    "package.json"
  ],
  "preferGlobal": true,
  "config": {
    "publishtest": false
  },
  "homepage": "https://docs.npmjs.com/",
  "author": "Isaac Z. Schlueter <i@izs.me> (http://blog.izs.me)",
  "repository": {
    "type": "git",
    "url": "https://github.com/npm/npm"
  },
  "bugs": {
    "url": "https://github.com/npm/npm/issues"
  },
  "directories": {
    "bin": "./bin",
    "doc": "./doc",
    "lib": "./lib",
    "man": "./man"
  },
  "main": "./lib/npm.js",
  "bin": "./bin/npm-cli.js",
  "dependencies": {
    "abbrev": "~1.0.9",
    "ansicolors": "~0.3.2",
    "ansistyles": "~0.1.3",
    "aproba": "~1.0.4",
    "archy": "~1.0.0",
    "asap": "~2.0.5",
    "chownr": "~1.0.1",
    "cmd-shim": "~2.0.2",
    "columnify": "~1.5.4",
    "config-chain": "~1.1.11",
    "dezalgo": "~1.0.3",
    "editor": "~1.0.0",
    "fs-vacuum": "~1.2.9",
    "fs-write-stream-atomic": "~1.0.8",
    "fstream": "~1.0.10",
    "fstream-npm": "~1.2.0",
    "glob": "~7.1.0",
    "graceful-fs": "~4.1.9",
    "has-unicode": "~2.0.1",
    "hosted-git-info": "~2.1.5",
    "iferr": "~0.1.5",
    "inflight": "~1.0.5",
    "inherits": "~2.0.3",
    "ini": "~1.3.4",
    "init-package-json": "~1.9.4",
    "lockfile": "~1.0.2",
    "lodash._baseuniq": "~4.6.0",
    "lodash.clonedeep": "~4.5.0",
    "lodash.union": "~4.6.0",
    "lodash.uniq": "~4.5.0",
    "lodash.without": "~4.4.0",
    "mkdirp": "~0.5.1",
    "node-gyp": "~3.4.0",
    "nopt": "~3.0.6",
    "normalize-git-url": "~3.0.2",
    "normalize-package-data": "~2.3.5",
    "npm-cache-filename": "~1.0.2",
    "npm-install-checks": "~3.0.0",
    "npm-package-arg": "~4.2.0",
    "npm-registry-client": "~7.2.1",
    "npm-user-validate": "~0.1.5",
    "npmlog": "~4.0.0",
    "once": "~1.4.0",
    "opener": "~1.4.2",
    "osenv": "~0.1.3",
    "path-is-inside": "~1.0.2",
    "read": "~1.0.7",
    "read-cmd-shim": "~1.0.1",
    "read-installed": "~4.0.3",
    "read-package-json": "~2.0.4",
    "read-package-tree": "~5.1.5",
    "readable-stream": "~2.1.5",
    "realize-package-specifier": "~3.0.3",
    "request": "~2.75.0",
    "retry": "~0.10.0",
    "rimraf": "~2.5.4",
    "semver": "~5.3.0",
    "sha": "~2.0.1",
    "slide": "~1.1.6",
    "sorted-object": "~2.0.1",
    "strip-ansi": "~3.0.1",
    "tar": "~2.2.1",
    "text-table": "~0.2.0",
    "uid-number": "0.0.6",
    "umask": "~1.1.0",
    "unique-filename": "~1.1.0",
    "unpipe": "~1.0.0",
    "validate-npm-package-name": "~2.2.2",
    "which": "~1.2.11",
    "wrappy": "~1.0.2",
    "write-file-atomic": "~1.2.0"
  },
  "bundleDependencies": [
    "abbrev",
    "ansi-regex",
    "ansicolors",
    "ansistyles",
    "aproba",
    "archy",
    "asap",
    "chownr",
    "cmd-shim",
    "columnify",
    "config-chain",
    "debuglog",
    "dezalgo",
    "editor",
    "fs-vacuum",
    "fs-write-stream-atomic",
    "fstream",
    "fstream-npm",
    "glob",
    "graceful-fs",
    "has-unicode",
    "hosted-git-info",
    "iferr",
    "imurmurhash",
    "inflight",
    "inherits",
    "ini",
    "init-package-json",
    "lockfile",
    "lodash._baseindexof",
    "lodash._baseuniq",
    "lodash._bindcallback",
    "lodash._cacheindexof",
    "lodash._createcache",
    "lodash._getnative",
    "lodash.clonedeep",
    "lodash.restparam",
    "lodash.union",
    "lodash.uniq",
    "lodash.without",
    "mkdirp",
    "node-gyp",
    "nopt",
    "normalize-git-url",
    "normalize-package-data",
    "npm-cache-filename",
    "npm-install-checks",
    "npm-package-arg",
    "npm-registry-client",
    "npm-user-validate",
    "npmlog",
    "once",
    "opener",
    "osenv",
    "path-is-inside",
    "read",
    "read-cmd-shim",
    "read-installed",
    "read-package-json",
    "read-package-tree",
    "readable-stream",
    "readdir-scoped-modules",
    "realize-package-specifier",
    "request",
    "retry",
    "rimraf",
    "semver",
    "sha",
    "slide",
    "sorted-object",
    "strip-ansi",
    "tar",
    "text-table",
    "uid-number",
    "umask",
    "unique-filename",
    "unpipe",
    "validate-npm-package-license",
    "validate-npm-package-name",
    "which",
    "wrappy",
    "write-file-atomic"
  ],
  "devDependencies": {
    "deep-equal": "~1.0.1",
    "marked": "~0.3.6",
    "marked-man": "~0.1.5",
    "npm-registry-couchapp": "~2.6.12",
    "npm-registry-mock": "~1.0.1",
    "require-inject": "~1.4.0",
    "sprintf-js": "~1.0.3",
    "standard": "~6.0.8",
    "tacks": "~1.2.2",
    "tap": "~7.1.2"
  },
  "scripts": {
    "dumpconf": "env | grep npm | sort | uniq",
    "prepublish": "node bin/npm-cli.js prune --prefix=. --no-global && rimraf test/*/*/node_modules && make doc-clean && make -j4 doc",
    "preversion": "bash scripts/update-authors.sh && git add AUTHORS && git commit -m \"update AUTHORS\" || true",
    "tap": "tap --reporter=classic --timeout 300",
    "tap-cover": "tap --coverage --reporter=classic --timeout 600",
    "test": "standard && npm run test-tap",
    "test-coverage": "npm run tap-cover -- \"test/tap/*.js\" \"test/network/*.js\"",
    "test-tap": "npm run tap -- \"test/tap/*.js\"",
    "test-node": "\"$NODE\" \"node_modules/.bin/tap\" --timeout 240 \"test/tap/*.js\" \"test/network/*.js\""
  },
  "license": "Artistic-2.0"
}
```
>[From](https://github.com/npm/npm/blob/master/package.json)
