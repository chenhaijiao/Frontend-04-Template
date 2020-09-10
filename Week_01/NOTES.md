## 总结一下
1. 看完的JavaScript指南，感觉proxy代理部分还不明白，还有字面量那部分不太清楚，bind，call，apply这些个方法也还不知道
2. 现在准备读一下underscore源码，看看还有js问题没有被泛读到
## 查漏补缺
### Symbol
1. 
```
const symbol1 = Symbol();
const symbol2 = Symbol(42);
const symbol3 = Symbol('foo');
console.log(typeof symbol1);
// expected output: "symbol"
console.log(symbol2 === 42);
// expected output: false
console.log(symbol3.toString());
// expected output: "Symbol(foo)"
console.log(Symbol('foo') === Symbol('foo'));
// expected output: false
```