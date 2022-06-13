### 1.let/const
> ES6中新增用来创建变量和常量的

### 箭头函数及THIS问题
> ES6中新增了创建函数的方式：“箭头函数”
真实项目中是箭头函数和FUCTION这种普通函数混合使用

箭头函数简化了创建函数的代码
```
//=>箭头函数的创建都是函数表达式（变量=函数），这种模式下，不存在变量提升，函数只能创建完成后被执行（也就是创建的代码之后执行）
const fn = ([形参]) =>{
  //函数体
};
fn([实参])；

//=>形参只有一个，小括号可以不加
const fn=n=>{};

//=>函数体中只有一句话，并且是return xxx的，可以省略大括号和return等
/*
function fn(n){
  return function(m){
    return m+(++n);
  }
}
*/
const fn=n=>m=>m+(++n);
```

箭头函数中没有ARGUMENTS，但是可以基于剩余运算符获取实参集合，而且ES6中是支持给形参设置默认值的
```
let obj = {};
let fn = (context = window, ...arg) => {
  // ...arg：剩余运算符（把除第一项外的，其他传递的实参信息都存储到arg这个数组集合中）
  console.log(arg);
}
fn(obj,10,20,30);//=>context:obj arg:[10,20,30]
fn();//=>context:window arg:[]
```

箭头函数中没有自己的THIS，它里面用到的THIS，都是自己所处上下文中的THIS（真实项目中，一旦涉及THIS问题，箭头函数慎用）
```
window.name = "WINDOW";
let obj = {
  name: 'OBJ'
};
let fn = n => {
  console.log(this.name);
};
fn(10);//=>this:window
fn.call(obj, 10);//=>this:window 不是我们预期的OBJ
document.body.onclick = fn;//this:window 不是我们预期的OBJ
//===============================
window.name = "WINDOW";
let fn = n => {
  console.log(this.name);
};
let obj = {
  name: 'OBJ',
  fn: fn
};
fn(10);//=>this:window
fn.call(obj, 10);//=>this:window 不是我们预期的OBJ
document.body.onclick = fn;//this:window 不是我们预期的OBJ
obj.fn(10);//this:window 不是我们预期的OBJ
```

### 解构赋值
> 让左侧出现和右侧值相同的结构，以此快速获取到我们需要的内容
真实项目中常用的就是对数组和对象的解构赋值
```
// 数组的解构赋值
let ary = [1,2,3,4,5];
/*
let n = ary[0],
    m = ary[1],
    x = aty.slice(2);
*/
let [n,m,...x] = ary;//...x,只能出现在最后
console.log(n,m,x);//=>1 2 [3,4,5]
let [a, , b, c = 0, , , d, e = 0] = ary;
console.log(a, b, c, d, e);//=>1 3 4 undefined 0
//====================================
// 对象的解构赋值
let obj = {
  name: 'ts',
  age: 24,
  sex: 'male',
  friend: ['xt','wt']
}
//-----------------------------------
let {
  name,
  sex,
  nianling,
  friend:[,second]
} = obj;
console.log(name, sex , nianling,second);//=>'ts' 'male' undefined wt
//-----------------------------------
let {
  age: nianling,
  height = '180cm'
} = obj;
console.log(nianling, height);//=>24 "180cm"
```

### "..."的作用
- 拓展运算符（多用在解构赋值中）
- 展开运算符（多用在传递实参中）
- 剩余运算符（多用在接收实参中）

### class创建类
```
//=>ES6中类的创建
、、class创建的类，只能用new执行，不能当做普通函数执行
class Fn{
  //等价于之前的构造函数体
  constructor(){
    this.x = 100;
  }
  //直接写的方法就是加在原型上的 === Fn.prototype.getX = function(){}
  getX(){
    console.log(this.x);
  }
  //前面设置static的：把当前Fn当做普通对象设置的键值对
  static queryX(){}
}
```

### ES6中的模板字符串
```
let year = '2021',
    month = '12',
    day = '14';
//=>反引号
let res=`您好，今天是${year}年${month}月${day}日。`;
let ID = "box";
let HTML = `<ul class="list" id="${ID}">
    <li></li>
  </ul>`;
```