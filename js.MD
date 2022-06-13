### 常用浏览器
- webkit内核（V8引擎 ->JS引擎）
    + 谷歌Chrome
    + Safari
    + Opera >= V14
    + 国产浏览器
    + 手机浏览器
    + ...
- Gecko
    + 火狐Firefox
- Presto
    + Opera < V14
- Trident
    + IE
    + IE EDGE开始采用双内核（其中包括Chrome迷你）

谷歌浏览器的控制台（F12/Fn+F12）
- Elements：查看结构样式，可以修改这些内容
- Console：查看输出结果和报错信息
- Source：查看项目源码
- Network：查看当前网站所有资源的请求信息（包括和服务器传输的HTTP报文信息）、加载时间等（根据加载时间进行项目优化）
- Application：查看当前网站的数据存储和资源文件

### JS做客户端语言
> 按照相关的JS语法，去操作页面中的元素，有时还要操作浏览器里面的一些功能
- ECMAScript3/5/6...：JS的语法规范（变量、数据类型、操作语句等等）
- DOM（document object model）：文档对象模型，提供一些JS的属性和方法，用来操作页面中的DOM元素
- BOM（browser object model）：浏览器对象模型，提供一些JS的属性和方法，用来操作浏览器的

### JS中的变量 variable
> 变量：在编程语言中，变量其实就是一个名字，用来存储和代表不同的值

```

//ES3
var a = 12;
console.log(a); //=>输出的是a代表的值是12

//ES6
let b = 100;

const c = 1000;
c = 2000; //=>报错：CONST创建的变量，存储的值 不能被修改（可以理解为叫做常量）

//创建函数也相当于创建变量
funvtion fn(){}
//创建类也相当于创建变量
class A{}
//ES6的模块导入也可以创建变量
import B form './JS.js';

//Symbol创建唯一值
let n = Symbol(100);
let m = Symbol(100);
n == m;//=>false
```

### JS中的命名规范
- 严格区分大小写
```
let Text = 100;
console.log(test);//=>无法输出，因为第一个字母小写了
```
- 使用数字、字母、下划线、$，数字不能作为开头
```
let $box;//=>一般JQ获取的以$开头
let _box;//=>一般公共变量都是_开头
let 1box;//=>不可以，但是可以写box1
```
- 使用驼峰命名法：首字母小写，其余每一个有意义单词的首字母都要大写（命名尽可能语义化明显，使用英文单词）
```
//常用缩写：add/insert/vreate/new（新增）、update（修改）、delete/del/remove/rm（删除）、sel/select/query/get(查询)、info（信息）...
```
- 不能使用关键字和保留字：当下有特殊含义的是关键字，未来可能可能成为关键字的叫做保留字

### JS中常用的数据类型
- 基本数据类型
    + 数字类型number
        常规数字和NaN
    + 字符串string
        所有用单引号、双引号、反引号包起来的都是字符串
    + 布尔boolean
        true/false
    + 空对象指针null
    + 未定义undefined
- 引用数据类型
    + 对象数据类型object
        + {} 普通对象、[] 数组对象、/^$/ 正则对象、Math数学函数对象、日期对象...
        + 实例也是对象数据类型
        + 类的prototype也是对象数据类型的（Function.prototype除外，他是一个匿名空函数）
        + 函数也是对象
    + 函数数据类型
        + 普通函数
        + 类（内置类或者自定义类）

### JS中的输出语句
- console.log/dir/table...在控制台输出
    + .dir：输出一个对象的详细键值对信息//=>console.dir(console)
    + .table：把一个多维的JSON数组在控制台按照表格的方式呈现出来
- 浏览器窗口弹窗 alert/confirm/prompt =>三种方式输出的结果都必先经过toString转换为字符串，三种方式会阻断JS代码的执行，只有当窗口关掉，JS才回继续运行
    + alert：就一个确定选项
    + confirm：确定和取消
    + prompt：在confirm的基础上多了一个输入框
- document.write在页面中写入内容=>和alert一样，输出结果都是字符串

### SCRIPT标签的位置
> 经常放到BODY末尾，是为了保证页面结构加载完成才去做JS中的事情，放到头部，可能导致无法获取到需要操作的元素
```
window.onload = function () {
    //事件：当页面中的结构额内容都加载完成才会执行这里面的代码，JQ中对应的方法$(document).ready(function(){})
}
```

### JavaScript JS引擎
> 单线程 -> 模拟多线程
轮转时间片
短时间之内轮流执行多个任务的片段
1、任务1  任务2
2、切分任务1 任务2
3、随机排列这些任务片段，组成队列
4、按照这个队列顺序将任务片段送进JS进城
5、JS线程执行一个又一个的任务片段

```
var a; //变量声明
a = 3; //变量赋值
var a = 3; //变量声明并赋值
//两个部分组成
//声明变量 变量赋值
```