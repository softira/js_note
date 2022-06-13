
### DOM及其基础操作
> DOM：document object model文档对象模型，提供一些属性和方法供我们操作页面中的元素

**获取DOM元素的方法**
- document.getElementById() 指定在文档中，基于元素的ID或者这个元素对象
- [context].getElementsByTagName() 在指定上下文（容器）中，通过标签名获取一组元素集合
- [context].getElementsByClassName() 在指定上下文中，通过样式类名获取一组元素集合
- documnent.getElementsByName() 在整个文档中，通过标签的NAME（NAME在表单中是用来分组的）属性值获取一组节点集合（在IE中只有表单元素的NAME才能识别，所以我们一般只应用于表单元素的处理）
- document.head/document.body/doucument.documentElement获取页面中的HEAD/BODY/HTML三个元素
- [context].querySelector([selector]) 在指定上下文中，通过选择器获取到指定的元素对象
- [context].querySelectorAll([selector]) 在指定上下文中，通过选择器获取到指定的元素集合
- querySelector/querySelectorAll 不兼容IE6~8

**JS中节点和描述节点之间关系的属性**
> 节点：Node（页面中所有的东西都是节点）
> 节点集合：NodeList (getElementsByName/querySelectorAll获取的都是节点集合)
- 元素节点（元素标签）
 + nodeType：1
 + nodeName：大写的标签名
 + nodeValue：null
- 文本节点
 + nodeType：3
 + nodeName：'#text'
 + nodeValue：文本内容
- 注释节点
 + nodeType：8
 + nodeName：'#commen'
 + nodeValue：注释内容
- 文档节点document
 + nodeType：9
 + nodeName：'#document'
 + nodeValue：null
- ......
描述这些节点之间关系的属性
- childNodes：获取所有的子节点
- children：获取所有的元素子节点（子元素标签）//但是IE6~8下，使用children会把注释也当做元素节点
- firstChild：获取第一个子节点
- lastChild：获取最后一个子节点
- firstElementChild/lastElementChild：获取第一个和最后一个元素子节点（不兼容IE6~8）
- previousSibling：获取上一个哥哥节点
- nextSibling：获取下一个弟弟节点
- previousElemwntSibling/nextElementSibking：获取哥哥和弟弟元素节点（不兼容IE6~8）
- ......
- 标准浏览器（非IE6~8）会把空格和换行当成文本节点处理
```
/*
* children：获取指定上下文中，所有的元素子节点
* @params
*  context [element object] 指定的上下文元素信息
* @return
*  [arry] 返回所有的元素子节点集合
* by team on 2021/11/17
*/
function children(context) {
 // 先获取所有的子节点
 let res = [],
   nodeList = context.childNodes;
 // 循环遍历所有子节点，找出元素子节点（nodeType === 1），存储到RES中即可
 for (var i = 0; i < nodeList.length; i++) {
  var item = nodeList[i];
  item.nodeType === 1 ? res.push(item) : null
 }
 return res;
}
```
#### 在JS中动态增删改元素
`createElement`创建元素对象
`createTextNode`创建文本对象
`appendChild`把元素添加到容器的末尾
`insertBefore`把元素添加到指定元素的前面
`cloneNode(true/false)`克隆元素或者节点//=>深克隆会连子元素一起克隆，浅克隆只克隆本身
`removeChild`移除容器中某个元素
`setAttribute/getAttribute/removeAttribute`设置获取元素的自定义属性信息（这种方式是把自定义属性放到元素结构上）
```
// 动态创建一个DIV元素对象，把其赋给BOX
let box = document.createElement('div');
box.id = 'boxActive'
// 动态创建一个文本
let text = document.createTextNode('tanshuai');
// 添加
box.appendChild(text);
document.body.appendChild(box);
// 放到指定元素前：容器.insertBefore([新元素], [指定元素])
// ========================
let box1 = document.querySelector('.box');
// 克隆第一份（深克隆）
let box2 = box1.cloneNode(ture);
// 克隆第二份（浅克隆）
let box3 = box1.cloneNode(false);
// ========================
var btnList = document.querySelectorAll('button');
for (var i = 0; i < btnList.length; i++) {
 // 设置自定义属性：元素对象.属性名 = 属性值（原理是向元素对象对应的堆内存中添加了一个属性）
 // btnList[i].myIndex = i;
 // 设置自定义属性：基于SET-ATTRIBUTE是把属性信息写到元素标签的结构上（在结构中可以看到的），并没有放到元素对象对应的堆内存中
 btnList[i].setAttribute('data-index', i);
 btnList[i].onclik = function() {
  //获取自定义属性：元素对象.属性名（原理是从堆内存中获取到对应的属性值）
  // alert(this.myIndex);
  // 基于GET_ATTRIBUTE可以把结构上存储的自定义属性值获取到
  alert(this.getAttribute('data-index'));
 }
}
```

#### 获取元素样式和操作样式
```
//=>修改元素样式
[ELEMENT].style.xxx = xxx;
[ELEMENT].className = xxx;

//=>获取行内样式
[ELEMENT].style.xxx;
```

#### JS盒子模型属性
> 基于一些属性和方法，让我们能够获取到当前元素的样式信息，例如：clienWidth、offsetWidth等
> - client
>  + width / height
>  + top / left
> - offset
>  + width / height
>  + top / left
>  + parent
> - scroll
>  + width / height
>  + top / left

> 方法：window.getComputedStyle([ELEMENT],[伪类])/[ELEMENT].currentStyle
```
let box = document.getElementById('box');
//=>获取盒子可视区域的宽高（内容宽度+PADDING）
//获取结果的没有单位的（其余的盒模型属性也是）
//获取结果是整数，会四舍五入（其余的盒模型属性也是）
box.clientWidth
box.clientHeight
//获取当前页面一屏幕（可视化）区域的高度
let winW = document.documentElement.clientWidth || documemt.body.clientWidth;//兼容处理，前面那个低版本浏览器可能会不兼容
let winH = document.documentElement.clientHeight || documemt.body.clientHeight;
//=>获取盒子左边框和上边框的大小
box.clientLeft
box.clientTop
//=>在CLIENT的基础上加上border
box.offsetWidth
box.offsetHeight
//=>在没有内容溢出的情况下，获取的结果和CLIENT一样
//=>在有内容溢出的情况下，获取的结果约等于真实内容的宽高（左/上PADDING + 真实内容的宽/高）
//不同浏览器获取的结果可能不同
//设置overflow属性值对最后的结果也会产生一定的影响
box.scrollWidth
box.scrollHeight
//获取整个页面真实的高度
document.documentElement.scrollHeight || document.body.scrollHeight
//=>滚动条卷去的宽/高
box.scrollLeft
box.scrollTop
//=>offsetParent:获取它的父参照物
//父参照物查找：同一个平面中。最外层元素是所有后代元素的父参照物，而基于position：relative/absolute/fixed可以让元素脱离文档流（一个新的平面），从而改变元素的父参照物
//=>offsetLeft：距离父参照物的左偏移
//=>offsetTop：距离父参照物的上偏移
```

```
//SET-INTERVAL：设置一个定时器（TIMER代表这个定时器），每间隔INTERVAL这么久，就会把FUNCTION执行一次...直到手动清除定时器为止
let timer = setInterval([FUNCTION], [INTERVAL]);
clearInterval(timer)
```

**getComputedStyle**
> 获取当前元素所有经过浏览器计算过的样式
> - 只要元素页面中呈现出来，那么所有的样式都是经过浏览器计算的
> - 哪怕你没有设置和见过的样式也都就算了
> 在IE6~8浏览器中不兼容，需要基于currentStyle来获取
```
//=>第一个参数是操作的元素，第二个参数是元素的伪类
//=>获取的结果是CSSStyleDeclaration这个类的实例，包含了当前元素所有的样式信息
let styleObj = window.getComputedStyle([element], null);
styleObj["display"];
styleObj.display;
```