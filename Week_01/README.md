# 学习笔记  
## 第一周
>参考网址  
>>[目录文件为空报错](https://www.jianshu.com/p/40ffdd0654f4)  
[注意pull使用](https://www.cnblogs.com/alex-415/p/6912294.html)  
[整合本地仓库与远程仓库](https://blog.csdn.net/u012145252/article/details/80628451)  
#### 当在GitHub中fork了一个项目，如何建立本地仓库与远程仓库的连接  
1. 先下载项目到本地  
2. 保证对项目内容先不做更改  
3. 结合上面两个网址步骤去做  
    >1. git init //初始化仓库  
    >2. git add .(文件name) //添加文件到本地仓库  
    >3. git commit -m "first commit" //添加文件描述信息  
    >4. git remote add origin + 远程仓库地址 //链接远程仓库，创建主分支  
    >5. git pull origin master --allow-unrelated-histories// 把本地仓库的变化连接到远程仓库主分支  
    >6. git push origin master:master //把本地仓库的文件推送到远程仓库  
- [x] 课上代码消化
- [ ] 五子棋算法优化
- [ ] 前端知识架构
- [ ] 有关 JavaScript 语言是基于对象还是面向对象思考的博客
- [x] 红绿灯小结练习代码提交
- [ ] 完整看一遍 JavaScript 文档，doing
- [ ] 完整看一遍 HTML 文档
- [ ] 完整看一遍 CSS 文档
- [ ] 知识点整理

# 整理知识架构中....
基础不是夯实，还没完整的看过有关手册、文档，感觉很多东西不知道，下面是一些碎碎念  
争取9月10号之前看完第一遍完整的 JavaScript 文档，并记录下学习和思考的一些点，写一篇比较粗浅的 JavaScript 是基于对象还是面向对象的博客  
## 函数 
1. js中匿名函数的不断重复使用和声明函数的不断重复使用，性能上有差距吗？
### 函数表达式  
2. 这段代码中function必须传递fac函数名吗？  答：不一定，可以不传递函数名，其实觉得没必要这样使用
```
const factorial = function fac(n) {return n<2 ? 1 : n*fac(n-1)};
console.log(factorial(3));
``` 
### 函数作用域  和 函数堆栈
3. 注意函数作用域，与代码声明的的顺序，一般来说函数先声明，再声明变量和表达式
4. 函数本身也是对象，对象可以有方法，函数内部也可以声明方法，注意 apply() 的使用,还没看这是啥
5. 一个函数可以调用自身，以函数表达式为例
    + factorial()
    + fac()
    + argument.callee() ES5禁止在严格模式下使用此属性，不懂严格模式是啥？
6. 在不使用函数递归的情况下，用函数堆栈来解决递归问题？怎么弄
### 函数嵌套和闭包
7. 闭包函数调用不加括号怎么传参，应该说还要多理解一下----还是需要理解，去看看闭包函数的妙用可能就懂到底用来干啥了，保密操作吗？不能被试探和测试到的那种
    + inside能够保存x变量的值，每次重新调用的时候就会重新创建一次这个闭包，当不在引用此闭包函数之后，才会释放内存  
    + 因为不能直接引用，平时难以跟踪和检查
```
function outside(x) {
  function inside(y) {
      return x + y;
    }
    return inside;
  }
  fn_inside = outside(3); // 可以这样想：给一个函数，使它的值加3
  result = fn_inside(5); // returns 8
  result1 = outside(3)(5); // returns 8
```
8. 函数作用域链，只能说写函数嵌套的时候一定注意调用关系！！！
9. 函数内的命名冲突，作用域链是最近的优先级最高，相当于命名冲突变量的闭包内的优先级最高{inside, outside, 全局变量}-----大概只有巧用妙用的时候才会这样来用，最好是避免函数内部的命名冲突，有时候可能编译器不靠谱呢？？？
10. 才知道闭包是 JavaScript 最强大的特性之一，真的以为就是简单的 java 内部类似的
11. 闭包的产生：当内部函数以某一种形式被外部函数作用域访问时，一个闭包就产生了！！！！----那这样说的话，其实闭包可以很常见，但是很少使用吧
12. 越看越觉得就是 java 的内部类，保护一些特定的值的时候需要用内部类来获取的那种
13. 闭包使用的优点：安全保密，感觉没啥了
14. 闭包函数的陷阱：当闭包函数对冲突变量赋值的时候，到底是给哪个变量赋值了呢 答：就给闭包内的变量赋值，但是不能再用外部的变量，只能用闭包函数传进来的冲突变量；
### 使用arguments对象
15. 感觉可以接受，但注意只是一个“类数组对象”,确实包含length属性，但是很多数组对象的属性并不包含，更多信息详细参考 Function 一栏  
### 函数参数
16. 从ES6之后，有了默认参数个剩余参数两个概念
    1. 在 JavaScript 中函数参数的默认值是 undefined ，注意 JavaScript 中 undefined 和 null 的区别
    2. 过去一般是先判断测试参数是不是为 undefined (大概相当于分配了空间，但是没有赋值)，如果是 undefined 就传递参数值  
    3. 现在直接使用默认参数，不需要再多一步判断，且可以在函数头设置默认参数-----但是自己重新传值会不会覆盖掉，还需要去测试 答：会被覆盖掉，所以称为默认参数，hhhh
17. 剩余参数：允许将不确定的参数表示为数组
### 箭头函数
18. 相比函数表达式有更短的语法并以词法的形式绑定 --- 还需要多探索妙用
    + 更简洁的函数
    + this 的引用 --- 所以会产生挺多陷阱，注意检查
        - 在没有出现箭头函数之前 
            + 在构造函数中是一个全新的对象
            + 在严格模式下未定义----严格模式到底是啥，还是没有弄清楚
            + 在作为“对象方法”调用的函数中指向这个对象 --- 以面向对象的编程风格
            + 下面这段代码的意思领略了，但是注释有点看不懂，主要是看不懂严格模式和非严格模式的问题 --- 又看了一下，整个意思都领会错了
        - 在ES3/5中，通过把 this 赋值可以解决这一问题，好像跟微信小程序里边的_this = this赋值一样的道理
        - 创建一个约束函数可以准确将this值传递给对象方法，-----不懂啥是约束函数
        - 使用箭头函数可以准确的传递this值，会捕捉上下文闭包的this，-----会不会捕捉错误？上下文闭包this
        - 但是现在没用箭头函数其他的，类里边的this值可以在类的所属方法中正确传递，现在类和函数对待this的处理方式不一样吗
 ```
            function Person() {
              // 构造函数Person()将`this`定义为自身
              this.age = 0;

              setInterval(function growUp() {
                // 在非严格模式下，growUp()函数将`this`定义为“全局对象”，
                // 这与Person()定义的`this`不同，
                // 所以下面的语句不会起到预期的效果。
                this.age++;
              }, 1000);
            }
            var p = new Person();
```
### 预定义函数
19. 顶级的内建函数 ？？？是指非常巧妙吗，顶级
      + eval() 会对一串字符形式的 JavaScript 代码求值 ---- 只记得在原生 ajax 中接受到 data 用 eval() 处理,具体的忘记了
      + uneval() 不是标准 就看一眼，没看用处，没看懂介绍的这句话，创建一个Object的源代码字符串表示
      + inFinite() 测试数据是否为有限数
      + isNaN() 判断一个值是否为NaN ，文档说isNaN的内部强制转换规则很值得学习，ES6中有一个Number.isNaN() 可以了解一下
      + parseFloat() 函数解析字符串，返回一个浮点数
      + parseInt() 函数解析字符串，返回一个整数
      + decodeURI() 函数对之前经过 encodeURI() 函数或者类似加密风格的字符串进行解码
      + decodeURIComponent() 对之前进行过encodeURIComponent() 函数或者其他类似编码的字符串进行解码
      + encodeURI() 函数通过看不懂的一堆术语，通过以一个、两个、三个、或者四个转义序列表示字符的UTF-8编码，替换统一资源标识符(URI)的某些字符（注意：不是每个）来进行编码 => 大概意思就是通过固定的转义序列 来进行转义字符串，从而实现字符串加密 
      + encodeURIComponent() 跟encodeURI()差不多的功能,但是具体哪里不同，不知道
## 基本语法、字面量、变量声明、数据类型
### 基础
1. 并不建议省略 js 语法中的末尾分号，能够大大减少编译错误产生的可能性，ES语法规定在分句后面自动添加分号（ASI），想要了解更多，详情请参考JavaScript词法语法分析  
2. JavaScript源码被从左到右依次扫描并转换成一系列 token、控制字符、行终止符、注释、空白字符组成的输入元素，空白符指的是空格、换行符、制表符等  
3. const是声明一个块作用域的只读常量
4. 匹配的时候，感觉多行注释符用在多行注释，比单行注释符用在多行注释好一些  
5. 大部分使用ISO 8859-1 或者 Unicode编码的字符做标识符----ISO 8859-1完全没有听说过，Unicode编码感觉用过，但是不知道具体是什么
6. 变量在函数外以x = 1;的形式赋值，会产生一个全局变量，在严格模式下会出现错误，是单纯就在严格模式下产生错误码，可能哦，不加var、const、let --- 怎么个理解法，为什么会出错呢，同为全局变量，为什么这个x不一样呢
7. undefined，变量声明了但是没有赋值，一般就是默认参数为undefined，undefined在布尔环境中会被表示成false，在数值环境中会被表示成NaN,但是 null 在布尔环境中被表示成false，在数值环境中会被表示成 0 ，空值也是值，但是不知道赋值成null有没有分配空间，为什么就能解读成0呢？？有点想不通，还要多看一下null 类型和 undefined类型的异同  
8. 在ES6之前，在代码块中声明的变量，会是这个函数的内部变量，意思就是，出了这个代码块，但是只要还在这个函数，就能被引用  
   但如果在ES6中，使用let 声明的话，就能保证代码块中的变量是一个局部变量，其中的变量出了这个代码块就不能被所在函数引用
#### 变量提升
9. 变量提升就是在变量引用之后再声明变量，也不会发生异常。这里其实不应该叫变量提升吧，这是代码在被声明赋值时的顺序和一些东西，但是注意被提升的变量会被自动赋值成Undefined，所以如果这样干的话，可能会出现异常，但是不会被报错，输出就得一直是undefined
10. 所以由于使用变量提升，所以一般就将变量声明放在函数的顶部，提高代码的清晰度，也避免犯一些不必要的错误 
11. 下面是一段有意思的代码,所以闭包函数内部，重名之后，就是完全不一样的新声明的变量，离得最近的函数被引用---可以多看几遍，突然想起之前看过的说 x = 1 那个可以直接定义为全局变量，可能也是这个原理吧，会被自动找，自动给你提升一个var x；
```
/**
 * 例子1
 */
console.log(x === undefined); // true
var x = 3;


/**
 * 例子2
 */
// will return a value of undefined
var myvar = "my value";

(function() {
  console.log(myvar); // undefined
  var myvar = "local value";
})();
```
```
/**
 * 例子1
 */
var x;
console.log(x === undefined); // true
x = 3;
 
/**
 * 例子2
 */
var myvar = "my value";
 
(function() {
  var myvar;
  console.log(myvar); // undefined
  myvar = "local value";
})();
```
12. 注意！！！ES6中使用let（const）声明的变量是不会进行函数提升的，所以如果在let声明变量之前引用此变量，将会抛出引用错误（referenceError）这个变量一开始的时候就处于没被声明的状态，所以在引用的时候，会一直等待它被声明，相当于一个“暂时性死区”，时间和空气大概都已经凝固了吧
#### 函数提升
13. 对于函数来说，函数声明会被提升到顶部，但是函数表达式不会提升到顶部，函数表达式虽然相当于变量，但是提升之后会被赋值成undefined，相当于没有被声明，于是以变量形式声明的函数表达式也不能被引用
#### 全局变量
14. 实际上全局变量是全局对象的属性，网页中的全局对象就是window，所以可以通过形如window.variable的语法来访问和设置全局变量
15. 因此可以通过制定window或frame的名字，在当前window或frame 访问另一个window或frame内的声明变量，像父节点中声明变量，子节点来访问这个变量的时候，可以通过parent.XXX来引用他
#### 常量
16. 常量（constants），不可以在代码运行时重新声明，一次就一次，什么都要写清楚写明白，想清楚再写哦，不然会抛出异常，作用域的规则和let差不多
17. 在同一作用域，不能使用与变量名或函数名一致的常量名，可能说跟函数提升和变量提升也有点关系，所以说最好还是不要使用有冲突的变量名，潜藏bug的可能性很大，而且可能导致逻辑混乱
18. 对象属性被声明成常量，是不受保护的，就相当于，你还是可以修改里面的常量值，没办法给你做到原封不动，管不下也管不了，爱莫能助的感觉，数组被定义成常量也是不受保护的，还是可以任意修改常量里边的值，也不会报错  
#### 数据类型
19. 最新的ES定义了八种数据类型
    * 七种基本数据类型
        + 布尔值（Boolean）
        + null，一个表明null值的特殊关键字，因为JavaScript对大小写敏感，所以null 与 NULL 等变体完全不同！！特别注意是小写null
        + undefined，一个表明undefined的特殊关键字，undefined表示变量未定义时的属性？？？？不是声明了但是没被赋值时的属性吗？？？？？---难道之前理解的都是错误的？
        + 数字（Number），整数或者浮点数
        + 任意精度的整数（BigInt)，可以安全的存储和操作大整数，升值可以超过数字的安全整数限制-----有时间可以去看看原理
        + 字符串（String） 
        + 代表（Symbol）ES6中新添加的属性---这个不怎么了解，感觉没怎么接触过，一种实例是唯一且不可改变的数据类型
    * 以及对象（Object）----感觉Object没有全面去了解过，用也是简单的使用过一下子  
    可以通过这些数据类型，开发各种各样的数据结构，对象（Objects）和函数（function）是这门语言的另外两个基本元素，可以把对象当做存放值的一个容器，本来就是呀，将函数当做程序能够执行的一个步骤
#### 数据类型的转换
20. JavaScript是一种动态类型语言（dynamically typed language），声明变量的时候可以不用指定数据类型，而数据会在代码执行时，自动转换类型。其实一直觉得很神奇，接触了编译原理的词法分析和语法分析之后，大概JavaScript是在这个部分做了特别的细微的处理
21. 发现一个巧用，"1.1" - 0 + 22 // 23.1 这个字符串的能达到想要的结果，但是"1.1x" - 0 + 22 // NaN 所以说在涉及到含有数字以外字符来进行- 操作的时候，并不会自动识别出"1.1x"中的数值1.1，所以在特定环境下可以使用前面的转换，但是最好还是不要去这样使用，以免产生不必要的错误，还是老老实实使用parseFloat()比较稳一点
#### 字面量 (Literals)
22. 字面量是一种常量，程序运行时不可改动，就相当于const的数组类型，不被保护，但是使用了字面量就估计可以使用了
    + 数组字面量（Array Literals）
    + 布尔字面量（Boolean Literals）
    + 浮点数字面量（Floating-point Literals）
    + 整数（Integers） --- 注意这里加了个s，也没说是字面量，但const可以直接保护整数常量，可能字面量就需求不太大了吧
    + 对象字面量（Object Literals）
    + RegExp Literals
    + 字符串字面量（String Literals）
23. 数组字面量（Array Literals）
    + 基础
        - 一个封闭在方括号中的表达式列表-----表达式列表？？没看出来，例子就是单纯的字符串
        - 数组字面值也是一种对象初始化器 --- 注意是字面值，不是字面量---对象初始化器是个啥东西，没学过
        - 感觉挺不容易的，如果在顶层脚本里边用字面量创建数组，那么每次执行到包含数组字面量表达式的时候，都会对整个数组进行解释；
      另一方面，在函数中使用的数组，每一次使用的时候都会被函数创建一次
        - 数组字面量其实也是一个数组对象，其实看着就知道，赋值的时候就是按照数组那样去赋值的
    + 数组字面值中多余的逗号
        - 如果在同一行中连写两个逗号（，），就会有一个没有赋值的undefined 在这个位置
        - 如果在尾部加了一个逗号，将会被忽略
            + 在早期版本的浏览器中，尾部的逗号会产生错误，所以最好是不要加
            + 现在的浏览器版本好像鼓励添加最后一个逗号，因为当在末尾的时候加一个字面量的时候，如果不加尾部逗号，可能会被忽略，从而导致错误，所以在声明任何变量的时候，最好显式的声明一次这个变量，让代码变得更清晰，降低错误率
24. 布尔字面量 ---还不知道是什么，但是文档让我不要混淆布尔对象的真和假，与布尔基础值的true和false
25. 整数 --- 没有写成字面量，严格模式下八进制字面量必须以0O或者0o开头，不能以0开头 --- 注意哦是字面量，不是八进制数值，虽然表示了，但是还是不知道这个字面量怎么个写法，难道那一串都是一个字面量的表示方法
26. 浮点数字面量 --- 感觉就是科学计数法的简单表示方法
```
[(+|-)][digits][.digits][(E|e)[(+|-)]digits]
```
27. 对象字面量，感觉就是属性值里边可以放函数，但其实没有任何特别声明，就能直接这个就是一个对象字面量，字面量对象里边可以嵌套新的字面量对象节点，字面量的属性可以是任意字符串，包括空串，但是如果不是合法的标识符，就必须用""包括起来,访问的时候也要注意方式，不能用.的方式访问了，只能用对象属性值下标的方式访问
```
var unusualPropertyNames = {
  "": "An empty string",
  "!": "Bang!"
}
console.log(unusualPropertyNames."");   // 语法错误: Unexpected string
console.log(unusualPropertyNames[""]);  // An empty string
console.log(unusualPropertyNames.!);    // 语法错误: Unexpected token !
console.log(unusualPropertyNames["!"]); // Bang!
```
```
var foo = {a: "alpha", 2: "two"};
console.log(foo.a);    // alpha
console.log(foo[2]);   // two
//console.log(foo.2);  // SyntaxError: missing ) after argument list
//console.log(foo[a]); // ReferenceError: a is not defined
console.log(foo["a"]); // alpha
console.log(foo["2"]); // two
```
28. 在ES2015中，基于对象的设计，对象字面量扩展支持在创建时设置原型，支持super调用父级元素，支持用表达式动态的计算属性名
```
 [ 'prop_' + (() => 42)() ]: 42
```
```
var obj = {
    // __proto__
    __proto__: theProtoObj,
    // Shorthand for ‘handler: handler’
    handler,
    // Methods
    toString() {
     // Super calls
     return "d " + super.toString();
    },
    // Computed (dynamic) property names
    [ 'prop_' + (() => 42)() ]: 42
};
```
29. RegExp字面值 --- 这个是真的是字面值了，不是字面量哦，用两个正斜杠围起来的正则表达式
30. 字符串字面量 可以在字符字面值上使用类似String.length的属性
```
console.log("John's cat".length) 
// 将打印字符串中的字符个数（包括空格） 
// 结果为：10
```
31. 模板字面量，模板字符串提供了一些语法糖来操作字符串，可以在模板字符串之前添加一个tag来自定义字符串的解析过程，这个可以用来防止注入攻击，或者用来建立字符串的高级数据，抽象，比如说$这个符号，在JQuery中被种草了
```
// Basic literal string creation
`In JavaScript '\n' is a line-feed.`
// Multiline strings
`In JavaScript this is
 not legal.`
// String interpolation
var name = "Bob", time = "today";
`Hello ${name}, how are you ${time}?`
// Construct an HTTP request prefix is used to interpret the replacements and construction
POST`http://foo.org/bar?a=${a}&b=${b}
     Content-Type: application/json
     X-Credentials: ${credentials}
     { "foo": ${foo},
       "bar": ${bar}}`(myOnReadyStateChangeHandler);
```
33. 除非特别需要建立字符串对象，否则应该始终使用字符串字面值，可能是因为节省空间和处理时间吗？
#### 特殊字符
34. 特殊字符有一个表，严格模式下，不能使用八进制的转义字符，之前好像提及过，因为只能0O这种才能转义，但是Unicode应该没有这样，座椅不支持八进制的转义字符
35. 在换行之前用反斜线\，转义之后并没有换行，但是反斜线会被消除，只是说在代码编辑的时候，将一行拆成多行书写
```
var poem = 
"Roses are red,\n\
Violets are blue.\n\
Sugar is sweet,\n\
and so is foo."
console.log(poem)
//这个是能够能多行输出字符串
```
```
var str = "this string \
is broken \
across multiple\
lines."
console.log(str);   // this string is broken across multiplelines.
//这个是一行输出字符串
```
## 表达式和运算符
### 解构
1. 其实没看出来有什么大用处 --- 没用过
```
var foo = ["one", "two", "three"];
// 不使用解构
var one   = foo[0];
var two   = foo[1];
var three = foo[2];
// 使用解构
var [one, two, three] = foo;
```
2. 除0会产生infinite => 表示一个数值，无穷大 ，这个值的特点
    + writable : false
    + enumerber : false
    + configurable : false
3. x ** y 表示 x的y次方
4. 没有无符号左移    无符号右移，代表移动之后没有符号位
5. 能被转换成false的有null 、undefined、0、""、NaN
```
var a1 = "Cat" && "Dog";    // t && t returns Dog
var o5 = "Cat" || "Dog";    // t || t returns Cat
var o6 = false || "Cat";    // f || t returns Cat
var o7 = "Cat" || false;    // t || f returns Cat
```
6. 反正 ||运算 和 &&运算就跟其他语言一样，注意一下短路运算就好了，
7. delete操作符 为什么会放到这个区块呢，嘤嘤嘤？能够删除一个对象，或者一个对象的属性，或者一个数组中的某个键值，第四行的代码只有和with使用是才是合法的，从某个对象中删除一个属性，这个对象就是和with搭配的，不然也不知道到底删哪个对象的property
```
delete objectName;
delete objectName.property;
delete objectName[index];
delete property; // legal only within a with statement
```
8. 能够使用delete删除各式各样的隐式声明，但是被var声明的除外 --- 哪种叫做隐式声明呐？？？
9. 如果delete删除成功，那么那个属性的值就会变成undefined，删除成功返回true
10. 这一段挺绕的，意思是如果用delete删除了一个数组中的元素，那么这个元素在遍历数组的时候就会找不到，但是能够通过寻址返回undefined，数值未被定义。如果让这个元素存在但是值为undefined，就直接赋值好了，数组遍历循环的时候还能找到这个函数
```
var trees = new Array("redwood", "bay", "cedar", "oak", "maple");
delete trees[3];
if (3 in trees) {
  // 不会被执行
}
```
```
var trees = new Array("redwood", "bay", "cedar", "oak", "maple");
trees[3] = undefined;
if (3 in trees) {
  // this gets executed（会被执行）
}
```
11. typeof操作符 返回这个值所属的对象字符串
    + typeof null 挺有趣的
    + typeof对于属性值，返回这个属性值的类型
    + 对于方法和函数，返回function
    + 对于预定义的对象，会返回如下结果
```
typeof null; // returns "object"
```
```
typeof Date;     // returns "function"
typeof Function; // returns "function"
typeof Math;     // returns "object"
typeof Option;   // returns "function"
typeof String;   // returns "function"
```
12. void运算符，妙用：使用void运算符指明一个超文本链接，该文本是有效的，但是不会在当前文档进行加载
    + 如下创建一个超文本链接，用户点击，不会有任何效果
    + 当用户单击它时，提交一个表格
```
<a href="javascript:void(0)">Click here to do nothing</a>
```
```
<a href="javascript:void(document.form.submit())">
Click here to submit</a>
```
### 关系操作符
13. in操作符，如果所指的属性确实存在于对象中，返回true
```
// Arrays
var trees = new Array("redwood", "bay", "cedar", "oak", "maple");
0 in trees;        // returns true
3 in trees;        // returns true
6 in trees;        // returns false
"bay" in trees;    // returns false (you must specify the index number,
                   // not the value at that index)
"length" in trees; // returns true (length is an Array property)
// Predefined objects
"PI" in Math;          // returns true
var myString = new String("coral");
"length" in myString;  // returns true
// Custom objects
var mycar = {make: "Honda", model: "Accord", year: 1998};
"make" in mycar;  // returns true
"model" in mycar; // returns true
```
14. instanceof运算符，注意不要跟typeof运算符混淆了



