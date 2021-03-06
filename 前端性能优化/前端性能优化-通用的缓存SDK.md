特别注意：本地host配置级别，没有浏览器配置的级别高。

### 本地存储
#### SessionStorage临时存储神器
优点：临时存储神器。关闭页面标签时自动回收，不可以跨页面交互(在同一个浏览器中的多个页面中无法同时访问)。

缺点：因为是临时的，所以不能存储持久化的数据。
#### Cookie兼容性最好的本地存储
优点：兼容性最好，几乎所有的浏览器都支持。

缺点：大小有限制、而且每次发送请求，请求头里会带着Cookie一起发过去，现在基本大多数登录的合法性验证都是用cookie验证的。
#### Localstorage
优点：兼容性中等，操作简单，就是key-value形式，几乎现代的浏览器都支持。

### 高性能Dom
#### 重排(回流-Reflow)和重绘(repaint)
对于DOM结构中的各个元素都有自己的盒子模型，这些都需要浏览器根据各种样式来计算并根据计算结果将元素放到它该出现的位置，这个过程称之为`reflow`。

当各种盒子的位置、大小以及其他属性，例如颜色、字体大小等都确定下来后，浏览器于是便把这些元素都按照各自的特性绘制了一遍，于是页面的内容出现了，这个过程称之为`repaint`。
#### 触发Reflow和repaint

* DOM元素的添加、修改(内容)、删除会触发Reflow和repaint
* 仅修改DOM元素的字体颜色，只触发repaint，因为不需要调整布局

特别注意：**回流一定触发重绘，但是重绘不一定触发回流。**

触发重绘：
* 改变字体
* 增加或者移除样式表
* 内容变化(比如用户在input框中输入文字)
* 激活CSS伪类，比如:hover
* 脚本操作DOM
* 计算offsetWidth和offsetHeight属性
* 设置style属性的值