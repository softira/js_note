### UI组件库
> 有结构、样式、功能的库，里面提供很多开发中常用的组件，开发中直接把组件调取过来使用即可。
> - bootstrap（经常配合JQ一起使用）：支持响应式布局开发（栅格系统）
> - vue：vue element/iview
> - react：antd
> - EasyUI/AmazeUI ...
### JSON格式的数据
> 我们基于AJAX等其他方式从服务器获取的数据结果一般都是JSON格式或者XML格式
> - JSON格式的字符串
- JSON格式的对象
```
//=>普通对象
let obj = {
  name: "ts"
};
//=>JSON格式对象（其实就是把属性名用双引号包起来）
obj = {
  "name":"ts"
};
//=>JSON格式的字符串
let str = '{"name":"ts"}';
```
把JSON格式的字符串转换为对象：window.JSON.parse
```
let str = '{"name":"ts"}';
let obj = JSON.parse(str);
```
把对象转换为JSON格式字符串：JSON.stringify

