### 1. Bash变量
变量命名规则：

1. 变量名必须以字母或下划线开头,名字中间只能由字母,数字和下划线组成
2. 变量名的长度不得超过255个字符
3. 变量名在有效的范围内必须是唯一的
4. 在bash中,变量的默认类型都是字符串型

#### 1.1 变量的分类
1. 用户自定义变量。变量自定义的

```
定义变量：等号两边不能有空格，变量名不能以数字开头，变量值里如果有空格应该用双引号括起来；
调用变量：$变量名，例如echo $x 输出x的变量值；
变量叠加：变量名="$变量名"追加内容 或 变量名=${变量名}追加内容；
set命令：查看系统下所有变量，包括环境变量，自定义变量；-u如果设定此选项后，调用未声明变量时会报错(默认没有任何提示)；
删除变量：unset 变量名(不需要加$)
```
2. 环境变量： 这种变量中主要保存的是和系统操作环境相关的数据。变量可以自定义，但是对系统生效的环境变量名和变量作用是固定的

```
环境变量和用户自定义变量的区别？
环境变量是全局变量；用户自定义变量是局部变量。
用户自定义变量只在当前的Shell中生效；环境变量在当前Shell和这个Shell的所有子Shell中生效。

#设置环境变量
export 变量名 = 变量值
或者
变量名 = 变量值
export 变量名

#查看环境变量
set：查看所有变量
env：查看环境变量

#删除环境变量
unset 变量名

#PATH环境变量(以冒号分隔)
PATH变量：系统查找命令的路径
#查看PATH环境变量
echo $PATH
#增加PATH变量的值
PATH="$PATH":/root/sh
```
3. 位置参数变量(预定义变量的一种)：这种变量主要是用来向脚本当中传递参数或数据的，变量名不能自定义，变量作用是固定的
4. 预定义变量：是Bash中已经定义好的变量，变量名不能自定义，变量作用也是固定的 