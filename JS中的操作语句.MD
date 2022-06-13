### JS中的操作语句：判断、循环

#### 判断
> 条件成立做什么？不成立做什么？
- if/else in/else
- 三元运算符
- switch case

1. if/else

```
if(条件){
    条件成立执行
}else if(条件2){
    条件2成立执行
}
...
else{
    以上条件都不成立
}

//////////////////
let a = 10;
a >= 10 ? console.log('ff') : console.log('hh');//=>'ff'
//如果处理的事情比较多，我们用括号包起来，每一件事情用逗号分隔
//如果不需要处理事情，可以使用null/undefined占位
a > 0 && a < 20 ? (a ++, console.log(a)) : null;

//////////////////
//每一种case情况的比较用的都是===“绝对相等”，项目中为了保证业务的严禁，推荐使用===
let a = '5';
switch (a) {
    case 1:
        console.log('ff');
        break;
    case 5:
        console.log('hh');
        break;
    case 10:
        console.log('xx');
        break;
    default:
        console.log('jj');
}//=>jj

```

#### 循环
> 重复做某些事情就是循环
- for循环
- for in循环
- for of循环（ES6新增）
- while
- do while循环

```
/* 
 * 1.创建循环初始值
 * 2.设置（验证）循环执行的条件
 * 3.条件成立执行循环体中的内容
 * 4.当前循环结束，执行步长累计操作
 */
for(let i = 0;i < 5;i ++){
    console.log(i);
}

//循环体中的两个关键词
//continue：结束当前这轮循环
//break：强制结束整个循环（break后面的代码也不再执行）
for(var i = 0;i < 10;i ++){
    if(i >= 2){
        i += 2;
        continue
    }
    if(i >= 6){
        i --;
        break;
    }
    i ++;
    console.log(i);//=>1 
}
console.log(i); //=>11

```

> for in 循环：用来循环遍历对象中的键值对的（continue和break同样适用）
```
var obj = {
    name: 'ts',
    age: 20,
    sex: 'male',
    3: 12,
    1: 'lang'
}
for(var key in obj){
    //每次循环key变量储存的值：当前对象的属性名
    //获取属性值：obj[属性名]=>obj[key]   obj.key/obj['key']
    //for in在遍历的时候，优先循环数字属性名（从小到大）
    console.log(key);//=>1 3 'name' 'age' 'sex'
    console.log(obj[key]);//=>'lang' 12 'ts' 20 'male'
}
```