FIS是专为解决前端开发中自动化工具、性能优化、模块化框架、开发规范、代码部署、开发流程等问题的工具框架。

FIS是一系列提升产品质量与开发效率的工程化方案。

* 让前端团队可以快速进入角色，不用担心底层架构，性能优化等问题
* 可以减少人工管理静态资源成本和风险，全自动化优化页面性能
* 简化开发、测试、部署流程，来达到更快、更可靠、低成本的自动化项目交付

### FIS使用
#### 启动本地FIS服务器
```
# 查看相关命令使用
fis3 server -h
```
* fis3 server start：启动Fis服务器
* fis3 server stop：停止Fis服务器
* fis3 server open：打开本地fis服务器目录
* fis3 release：将项目发布到本地fis服务器目录

#### 发布项目
fis3 release -cwL：

* c
* w：监听文件变动
* L：自动加载页面
### JS模块化
MD5版本号好处：

* 线上的a.js不是同名文件覆盖。而是文件名+hash的冗余，所以可以先上线静态资源，再上线html页面，不存在间隙问题
* 遇到问题回滚版本的时候，无需回滚a.js，只须回滚页面即可
* 由于静态资源版本号是文本内容的hash，因此所有静态资源可以开启永久强缓存，只有更新了内容的文件才会缓存失效，缓存利用率大增。
* 修改静态资源后会在线上产生新的文件，一个文件对应一个版本，因此不会受到构造CDN缓存形式的攻击

#### FIS三种语言能力
* 资源定位：获取任何开发中所使用资源的线上路径
* 内容嵌入：把一个文件的内容(文件)或者base64编码(图片)嵌入到另一个文件中
* 依赖声明：在一个文本文件内标记对其他资源的依赖关系

##### 资源定位能力
* 资源定位能力：可以有效的分离开发路径与部署路径之间的关系
* 资源定位好处：资源可以发布到任何静态资源服务器的任何路径上而不用担心线上运行时找不到它们，而且代码具有很强的可移植性。

##### 内容嵌入
* 内容嵌入：可以为工程师提供诸如图片base64嵌入到css、js里，前端模板编译到js文件中，将js、css、html拆分成几个文件最后合并到一起的能力。
* 内容嵌入：可以有效的减少http请求数，提升工程的可维护性。

fis不建议用户使用内容嵌入能力作为组件化拆分的手段，因为fis扩展的依赖声明更适合组件化开发。

##### 依赖声明
按需加载资源或者资源所在的包。

依赖声明能力为工程师提供了声明依赖关系的编译接口。fis在执行编译的过程中，会扫描这些编译标记，从而建立一张**静态资源关系表**，它在编译阶段最后会被产出为一份**map.json**文件。

这份文件详细记录了项目内的静态资源id、发布后的线上路径、资源类型以及**依赖关系**和**资源打包**等信息。使用fis作为编译工具的项目，可以将这张表提交给后端或者前端框架去运行时根据组件使用情况来**按需加载资源或者资源所在的包**，从而提升前端页面运行性能。

#### 为什么要做js模块化
##### 模块化编程
* 拆分原来巨大的js文件，把独立的逻辑放到单文件里，被其他文件引用
* 把拆分后的js文件全部引入到页面上

##### 模块规范
* Commomjs

Nodejs中模块的写法，模块是同步装载的。同步装载在服务端没问题，但是在浏览器端会造成页面阻塞渲染。
* AMD

异步方式加载模块，模块的加载不影响后面语句的运行。所有依赖这个模块的语句，都定义在一个回调函数中，等到加载完成之后，这个回调函数才会运行。更适合浏览器端。

```
define() // 定义一个模块
require([module], callback) // 引用一个模块
```
##### AMD规范问题
* 原有的同步js代码要全部修改为异步调用的方式。跟原本写代码的方式不同，迁移成本大。
* RequireJS/SeaJS通过javascript运行时来支持"匿名闭包"、依赖分析和模块加载等功能。
* 依赖分析需要在javascript运行时通过正则匹配到模块的依赖关系，然后顺着依赖链，把所有需要加载的模块按顺序一一加载完毕。这样就会造成页面渲染的阻塞。

##### Mod(fis模块化解决方案)
Mod为工程化而生，提供类CommonJS开发体验。

* 开发者可以使用自然、容易理解的模块定义和调用方式
* 不需要关注模块是否异步
* 不需要改变开发者的开发行为
* Mod并不完全遵守AMD/CMD规范
* Mod严格上来讲并不是一个独立的模块化框架
* 它被设计用做前端工程化模块化方案的JS支持
* 需要和自动化工具、后端框架配合来使用
* 目的在于给工程师提供一个类似nodejs一样的开发体验，同时具备很好的线上性能

##### Mod使用
* Mod使用define来定义一个模块
* define(id, factory)：factory提供了三个参数：require,exports,module,用于模块的引用和导出
* 在开发中，我们无需关注模块定义，FIS提供自动化工具会自动化对JS进行denfine包装处理

##### Mod好处
* 通过工具自动添加define闭包，线上不需要支持匿名闭包
* 通过工具自动处理依赖，线上不需要动态处理依赖
* 通过后端模板自动插入script，线上不需要通过前端框架进行模块加载

### FIS组件化思想
#### 什么是组件化

#### 组件化的问题

#### FIS组件化思想
##### 构建解决路径问题
开发阶段：
* 使用相对路径
* 编码自然
* 符合组件化管理
* 保证复用

构建阶段：
* 替换绝对路径
* 自由合并


### 1. fis构建
```
-h, --help            print this help message
-d, --dest <path>     release output destination
-l, --lint            with lint
-w, --watch           monitor the changes of project
-L, --live            automatically reload your browser
-c, --clean           clean compile cache
-u, --unique          use unique compile caching
```
```
#-w 启用文件监听
#-d 指定打包目录
fis3 release -w
fis3 release -d
```
#### 1.1 浏览器自动刷新
```
#FIS3 支持浏览器自动刷新功能，只需要给 release 命令添加 -L 参数，通常 -w 和 -L 一起使用
fis3 release -wL
```
### fis-receiver(发布到远端机器)

### 参考文档
1. [fis-receiver：一行命令将项目部署到远程服务器](https://yq.aliyun.com/articles/36271)
2. [fis官方文档](http://fis.baidu.com/fis3/docs/beginning/debug.html)