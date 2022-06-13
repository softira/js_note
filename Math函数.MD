
### Math
> 数学函数：但是它不是一个函数，它是一个对象，对象中存储了很多操作数字的属性方法，因此被称为数学函数
```
console.log(typeof Math); //=>"object"
console.dir(Math);//=>{
  PI: 3.141592653589793
  abs:function(){[native code]},
  ...
}
/*
 *Math.PI;
 *Math.abs();
 */
```
### Math中常用的属性和方法
1.Math.abs([number value])
> 获取绝对值（绝对值永远是正数或者零），传递的值不是数字类型，会基于Number()转换为数字类型再处理
2.Math.ceil/floor([number value])
> 把一个数向上取整/向下取整
3.Math.round([number value])
> 四舍五入
4.Math.max/min([val1],[val2]...)
> 获取一堆数中的最大/小值
5.Math.sqrt/pow([number value])/pow([number value], [多少次幂])
> sqrt：开平方
> pow：计算一个数的多少次幂//Math.pow(2, 10)==>1024
6.Math.random()
> 获取0~1之间的随机小数
扩展：获取[n~m]之间的随机整数
> 包含n和m
```
Math.round(Math.random()*(m-n)+n)
```

