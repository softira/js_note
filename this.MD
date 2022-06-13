
### this
> 函数执行的主体：谁把函数执行的，那么执行主体就是谁
1. 给元素的某个事件绑定方法，当事件触发方法执行的时候，方法中的this是当前操作的元素本身
2. 如何确定执行主体（this）是谁？当方法执行的时候，我们看方法前面是否有点，没有点this是window（在严格模式下没有点this是undefined）；有点，点前面是谁this就是谁；
3. 在构造函数模式执行中，函数体中的this是当前类的实例
```
var name = 'ts';
function fn(){
  console.log(this.name);
}
var obj = {
  name: 'soft',
  fn:fn
};
obj.fn();//=>this:obj
fn();//=>this:windo（非严格模式，严格模式下是undefined）
(function(){
  //自执行函数中的this是window或undefined
})();
```
```
ary._proto_._proto_.hasOwnProperty();//hasOwnProperty()方法中的this是ary._proto_._proto_
// ===================
let obj = {
  fn:(function(n){
    //把自执行函数执行的返回结果赋值给fn
    //this:window
    return function(){
      //=>fn等于这个返回的小函数
      //this:obj
    };
  })(10)
};
obj.fn();
// ======================
function fn(){
  //this:window
  console.log(this)
}
document.body.onclick = function(){
  //this:document.body
  fn();
}
//===========================
var name = 'ts';
var obj = {
  name:'soft',
  prop:{
    getName: function(){
      return this.name;
    }
  }
};
console.log(obj.prop.getName());//=>return obj.prop.Name;=>undefined
var test = obj.prop.getName;
console.log(test());//=>return window.name;=>'ts'
//=========================
var name = 'ts';
var soft = {
  name:"soft",
  show:function(){
    console.log(this.name);
  },
  wait:function(){
    var fun = this.show;
    fun();
  }
};
soft.wait();//=>'ts'
//======================
var num = 10;
var obj = {num:20};
obj.fn = (function(num){
  this.num = num*3;
  num++;
  return function(n){
    this.num += n;
    num++;
    console.log(num);
  }
})(obj.num);
var fn = obj.fn;
fn(5);//=>22
obj.fn(10);//=>23
console.log(num,obj.num);//=>65 30
```

**this = xxx会报错，我们不能给THIS手动赋值**

> 每一个函数（普通函数/构造函数/内置类）都是Function这个内置类的实例，所以：函数._proto_===Function.prototype，函数可以直接调取Function原型上的方法
```
//Function.prototype => function anonymous(){}
/*
 * call / apply / bind 
 *    原型上提供的三个公有属性方法
 *    每一个函数都可以调用这个方法执行
 *    这些方法都是用来改变函数中的THIS指向的
 */
function fn(){}
fn.call();//=>fn函数基于原型链找到Function.prototype上的call方法，并且让其执行（执行的是call方法：方法中的this是fn）
fn.call.call();//=>fn.call就是Function.prototype上的call方法，也是一个函数，只要是函数就能用原型上的方法，所以可以继续调用call来执行

Function.prototype.call = function $1(){
  //...
}
/*
 * fn.call => $1
 * fn.call() => $1() this:fn
 * fn.call.call() => $1.call() => 继续让call执行，this:$1

 * 实例.方法()：都是找到原型上的内置方法，让内置方法先执行（只不过执行的时候做了一些事情会对实例产生改变，而这也是这些内置方法的作用），内置方法中的THIS一般都是当前操作的实例
 */
```

`call`方法
> 语法：函数.call([context],[params1],...)
函数基于原型链找到Function.prototype.call这个方法，并且把它执行，
在call方法执行的时候完成了一些功能
- 让当前函数执行
- 把函数中的THIS指向改为第一个传递给CAll的实参
- 把传递给CALL其余的实参当做参数信息传递给当前函数
如果执行CALL一个实参都没有传递，非严格模式下是让函数中的THIS指向WINDOW，严格模式下指向的是UNDEFINED

```
window.name = 'WINDOW';
let obj = {name: 'OBJ'};
let fn = function() {
  cosole.log(this.name);
};
fn(); //=>'WINDOW' this:window
fn.call(obj);//=>'OBJ' this:obj
//===================
function fn1(){console.log(1);}
function fn2(){console.log(2);}
.fn1.call(fn2);//=>1
.fn1.call.call(fn2);//=>2;
Function.prototype.call(fn1);//=>没有任何输出结果
Function.prototype.call.call(fn1);//=>1
//一个CALL是让左边函数执行（this是传递的参数）；多个call是让最后传参的函数执行（this是window/undefined）
```

`apply`方法
> 和call方法一样，都是把函数执行，并且改变里面的this关键字，唯一的区别是传递给函数参数的方式不同
> - call是一个个传
- apply是按照数组传参
```
let obj = {name:'OBJ'};
let fn = function(n,m){
  console.log(this.name);
};
fn.call(obj,10,20);
fn.apply(obj,[10,20]);
```

`bind`方法
> 和caa/apply一样，也是用来改变函数中的this关键字的，只不过基于bind改变this，当前方法并没有被执行
```
let obj = {name:'OBJ'};
let fn = function(n,m){
  console.log(this.name);
};
document.body.onclick = fn;//=>当事件触发，fn中的this:body
document.body.onclick = fn.call(obj);//=>基于call/apply这样处理，不是把fn绑定给事件，而是把fn执行后的结果绑定给事件
document.body.onclick = functin(){
  fn.call(obj);
}
docment.body.onclick = fn.bind(obj);
```

### THIS和面向对象的另外一种深入理解
```
/*
function sum(){
  //ARGUMENTS：内置的实参集合（箭头函数中没有），不是数组是类数组（它不是数组的实例，不能直接使用数组的方法arguments._proto_===Object.prototype)
  //let arg = Array.prototype.slice.call(arguments, 0);
  let arg = [].slice.call(arguments, 0);
  return eval(arg.join('+'));
}
let total = sum(1,2,3,4);
*/

//=>ARG：存储传递的实参信息（数组）
//=>eval：把字符串转换为JS表达式执行
let sum = (...arg) => eval(arg.join('+'));
let total = sum(1,2,3,4);
```