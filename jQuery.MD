### jQuery
> 一款操作DOM的类库：它里面封装了大量的方法，基于这些方法我们可以快速的进行DOM操作和项目开发

JQ的三大版本
- v1.xxx 第一代版本
  第一代版本的特点：大而全，方法是兼容所有浏览器的（包括IE6），住要应用于需要考虑兼容的PC端项目中
- v2.xxx 第二代版本
  主要是为了移动端的开发准备的，不再兼容低版本浏览器（例如IE8及以下），配合出现的还有jQuery mobile等UI库。但是，第二版本在移动端方面的处理不如zepto.js
- v3.xxx 第三代版本
  也不再兼容IE低版本浏览器了，它从性能等方面都比之前的强，但主流框架已经是angular/vue/react了，已经不再是基于操作DOM的思想开发了

```
/*
 * $([function])：等待页面中所有的DOM结构加载完成才会执行这个方法
 * => $(document).ready([function])
 */
$(function(){

});
```

#### JQ中常用的方法
```
//=>1.获取DOM元素
//操作方法：JQ选择器
$([selector],[context])
//节点之间关系的属性:用JQ选择器获取的元素，我们设置变量名的时候一般以$开始
let $box = $('.box')
$box.prev();
$box.next();
...
//=>2.DOM增删改
$('body').append(str);
$('body').html(str);
//$('body').html()不传参是获取BODY中的HTML内容
...
//=>3.操作自定义属性
//=>4.操作CSS样式（盒子模型属性）
```

除了操作DOM，JQ中还提供了有助于项目开发的方法
```
//=>事件处理
//$元素.on([event type],[function])
//$元素.off([event type],[function])
.$box.on('click',function(){})
//=>AJAX请求处理
$.ajax({
  url:'jons/product.json',
  method:'GET',
  async:false,
  dataType:'json',
  success:result=>{
    //result：当请求成功执行success函数，result就是从服务器获取的结果
    _DATA=result;
  }
});

```