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
14. instanceof运算符，注意不要跟typeof运算符混淆了，instanceof是theDay是不是一个Date对象
```
var theDay = new Date(1995, 12, 17);
if (theDay instanceof Date) {
  // statements to execute
}
```
15. 运算符优先级，需要用到的时候再找吧
### 基本表达式
16. this，用来被指代当前使用的对象，需要深入理解好吧
### 数值推导
17. 数值推导，一些API还在实验中，计划加入，了解一下，Comprehensions是快速的通过一个数组生成另一个数组，挺厉害的，应该要加很多属性
18. 扩展语句,如下代码的赋值方式，确实省了一些事情，也挺好用的，还用在函数传参
```
var parts = ['shoulder', 'knees'];
var lyrics = ['head', ...parts, 'and', 'toes'];
```
```
function f(x, y, z) { }
var args = [0, 1, 2];
f(...args);
```
## 数字和日期（这几个对象里边的方法和属性，都去看看文档）
1. 在ES6中使用八进制数值0O或者0o，不然不行；在ES5中严格模式下禁止使用八进制数值
2. 假如0x后面的数字超出规定范围(0123456789ABCDEF)，那么就会提示这样的语法错误(SyntaxError)："Identifier starts immediately after numeric literal".
### Number
3. Number.isSafeInteger()
4. toExponential() 返回一个数值的科学计数法形式
5. toFixed() 返回固定位的小数，没有那么多位小数就填充0
6. toPrecision() 指定一个精度数字，返回科学计数法形式，目的是保留你想要的精度  
Number还有很多属性，自己多用用就会了
### Math
7. 和其他对象不同，不能创建一个自己的Math对象，typeof Math 返回的是 object也是有一定道理的
### Date
8. Date 对象的范围是相对距离 UTC 1970年1月1日 的前后 100,000,000 天。getTime方法返回从1970年1月1日00:00:00的毫秒数。对于比较时间比较有用，简单粗暴
9. 在下边的例子中，JSClock()函数返回了用数字时钟格式的时间：
```
function JSClock() {
  var time = new Date();
  var hour = time.getHours();
  var minute = time.getMinutes();
  var second = time.getSeconds();
  var temp = "" + ((hour > 12) ? hour - 12 : hour);
  if (hour == 0)
    temp = "12";
  temp += ((minute < 10) ? ":0" : ":") + minute;
  temp += ((second < 10) ? ":0" : ":") + second;
  temp += (hour >= 12) ? " P.M." : " A.M.";
  return temp;
}
```
## 文本格式化和字符串的使用问题（多看一下String这个类）
1. Unicode字元溢出，有了这个处理方式之后，任何字符都可以使用16进制数来进行转义
```
'\u{2F804}'
// the same with simple Unicode escapes
'\uD87E\uDC04'
```
2. 除非必要，尽量使用字符串字面量,下面这个实例，除非必要，也尽量少使用eval()函数，性能不好且保密性不好
```
const firstString = '2 + 2'; //创建一个字符串字面量
const secondString = new String('2 + 2'); // 创建一个字符串对象
typeof firstString // string
typeof secondString // object
eval(firstString); // 返回数字 4
eval(secondString); // 返回字符串 "2 + 2"
```
3. 字符串字面量是一个类数组对象
```
const hello = 'Hello, World!';
const helloLength = hello.length;
hello[0] = 'L'; // 无效，因为字符串是不变的
hello[0]; // 返回 "H"
```
4. String 中的方法match, replace, search 通过正则表达式来工作
5. 模板字符串可以使用``反勾号，里面的字符就不需要转义了，如果使用""还需要加\n\才能换行
```
console.log(`string text line 1
string text line 2`);
// "string text line 1
// string text line 2"
```
6. 现在使用模板字符串，可以使用语法糖让类似功能的实现代码更具可读性
```
const five = 5;
const ten = 10;
console.log('Fifteen is ' + (five + ten) + ' and not ' + (2 * five + ten) + '.');
// "Fifteen is 15 and not 20."
// 这是我的操作了
```
```
const five = 5;
const ten = 10;
console.log(`Fifteen is ${five + ten} and not ${2 * five + ten}.`);
// "Fifteen is 15 and not 20."
```
### 国际化
7. Intl对象， Collator, NumberFormat, 和 DateTimeFormat 对象的构造函数是Intl对象的属性.
    + DateTimeFormat 日期时间格式化
    + NumberFormat 数字格式化
    + Collator 定序 字符串按照一个什么样的方式排序，这个对象就很方便
```
var gasPrice = new Intl.NumberFormat("en-US",
                        { style: "currency", currency: "USD",
                          minimumFractionDigits: 3 });
console.log(gasPrice.format(5.259)); // $5.259
var hanDecimalRMBInChina = new Intl.NumberFormat("zh-CN-u-nu-hanidec",
                        { style: "currency", currency: "CNY" });
console.log(hanDecimalRMBInChina.format(1314.25)); // ￥ 一,三一四.二五
```
```
var names = ["Hochberg", "Hönigswald", "Holzman"];
var germanPhonebook = new Intl.Collator("de-DE-u-co-phonebk");
// as if sorting ["Hochberg", "Hoenigswald", "Holzman"]:
console.log(names.sort(germanPhonebook.compare).join(", "));
// logs "Hochberg, Hönigswald, Holzman"
```
## 正则表达式
1. 用到了括号，它在正则表达式中常用作记忆设备。即这部分所匹配的字符将会被记住以备后续使用，例如使用括号的子字符串匹配。
2. 这一段就不做笔记了，得多看几遍
3.  /Chapter (\d+)\.\d*/  小数点前的 \ 意味着这个pattern必须寻找字面字符 '.')
4. 括号中的"?:"，这种模式匹配的子字符串将不会被记住。比如，(?:\d+)匹配一次或多次数字字符，但是不能记住匹配的字符。
5. 正则表达式可以被用于 RegExp 的 exec 和 test 方法以及 String 的 match、replace、search 和 split 方法。 => JavaScript手册
```
var myArray = /d(b+)d/g.exec("cdbbdbsbz");
// 和 "cdbbdbsbz".match(/d(b+)d/g); 相似。
// 但是 "cdbbdbsbz".match(/d(b+)d/g) 输出数组 [ "dbbd" ]，
// 而 /d(b+)d/g.exec('cdbbdbsbz') 输出数组 [ "dbbd", "bb", index: 1, input: "cdbbdbsbz" ].
```
6. lastIndex开始下一个匹配的起始索引值。（这个属性只有在使用g参数时可用在 通过参数进行高级搜索 一节有详细的描述.)
7. 当发生/d(b+)d/g使用两个不同状态的正则表达式对象，lastIndex属性会得到不同的值。如果你需要访问一个正则表达式的属性，则需要创建一个对象初始化生成器，你应该首先把它赋值给一个变量。
```
var myArray = /d(b+)d/g.exec("cdbbdbsbz");
console.log("The value of lastIndex is " + /d(b+)d/g.lastIndex);
The value of lastIndex is 0
```
```
var myRe = /d(b+)d/g;
var myArray = myRe.exec("cdbbdbsbz");
console.log("The value of lastIndex is " + myRe.lastIndex);
The value of lastIndex is 5
```
8. 匹配到的替换文本中，脚本使用替代的$ 1,$ 2表示第一个和第二个括号的子字符串匹配。
```
 var re = /(\w+)\s(\w+)/;
var str = "John Smith";
var newstr = str.replace(re, "$2, $1");
console.log(newstr);
```
9. 正则表达式有六个可选参数 (flags) 允许全局和不分大小写搜索等。这些参数既可以单独使用也能以任意顺序一起使用, 并且被包含在正则表达式实例中。
    + g 全局搜索。
    + i 不区分大小写搜索。
    + m 多行搜索。
    + s 允许 . 匹配换行符。
    + u 使用unicode码的模式进行匹配。
    + y 执行“粘性(sticky)”搜索,匹配从目标字符串的当前位置开始。
10. 使用.exec()方法时，与'g'标志关联的行为是不同的。 （“class”和“argument”的作用相反：在.match()的情况下，字符串类（或数据类型）拥有该方法，而正则表达式只是一个参数，而在.exec()的情况下，它是拥有该方法的正则表达式，其中字符串是参数。对比str.match(re)与re.exec(str) ), 'g'标志与.exec()方法一起使用获得迭代进展。
11. m标志用于指定多行输入字符串应该被视为多个行。如果使用m标志，^和$匹配的开始或结束输入字符串中的每一行，而不是整个字符串的开始或结束。
## 数组对象
1. 括号语法被称为 "数组字面值" 或 "数组初始化器", 它比其他创建数组的方式更便捷，所以通常是首选。详细内容参见 Array literals ，就不创建新的数组对象的那个，直接加方括号。
2. 调用 arr.length 会返回数组长度，但是数组实际上包含了空的（undefined）元素。 因此在数组上使用 for...in 循环，将不会返回任何的值 ，只要数组值是空的，就无法进入循环的意思吗,但是数组值为undefined，是能够进入循环的
3. 数组长度不是整数，将会报错
```
var arr = Array(9.3);  // RangeError: Invalid array length
```
4. 注意，在数组定义时省略的元素不会在forEach遍历时被列出，但是手动赋值为undefined的元素是会被列出的
5. push,pop,unshift,shift
```
var myArray = new Array ("1", "2", "3");
myArray.unshift("4", "5"); 
// myArray becomes ["4", "5", "1", "2", "3"]
```
6. splice(index, count_to_remove, addElement1, addElement2, ...)从数组移出一些元素，（可选）并替换它们。
```
var myArray = new Array ("1", "2", "3", "4", "5");
myArray.splice(1, 3, "a", "b", "c", "d"); 
// myArray is now ["1", "a", "b", "c", "d", "5"]
// This code started at index one (or where the "2" was), 
// removed 3 elements there, and then inserted all consecutive
// elements in its place.
```
7. map(callback[, thisObject]) 在数组的每个单元项上执行callback函数，并把返回包含回调函数返回值的新数组
8. filter(callback[, thisObject])跟every(callback[, thisObject])差不多，但是前一个返回的是一个所有符合条件的数组项的新数组，后一个判断是不是所有数组项都符合这个条件，返回的是true or false；some(callback[, thisObject]) 顾名思义
9. 以上方法都带一个被称为迭代方法的的回调函数，因为他们以某种方式迭代整个数组。都有一个可选的第二参数 thisObject，如果提供了这个参数，thisObject 变成回调函数内部的 this 关键字的值。如果没有提供，例如函数在一个显示的对象上下文外被调用时，this 将引用全局对象(window).
10. 实际上在调用回调函数时传入了3个参数。第一个是当前元素项的值，第二个是它在数组中的索引，第三个是数组本身的一个引用。 JavaScript 函数忽略任何没有在参数列表中命名的参数，因此提供一个只有一个参数的回调函数是安全的，例如 alert 。----没看懂
11. reduce(callback[, initialValue])和reduceRight(callback[, initalvalue])，一个从左到右，一个从右到左。他们应该使用在那些需要把数组的元素两两递归处理，并最终计算成一个单一结果的算法。
### 数组和正则表达式
12.  RegExp.exec(), String.match() 和 String.split() 的返回值是一个数组。
### 类数组对象
13. 一些 JavaScript 对象, 例如 document.getElementsByTagName() 返回的 NodeList 或者函数内部可用的 arguments 对象，他们表面上看起来，外观和行为像数组，但是不共享他们所有的方法。例如 arguments 对象就提供一个 length 属性，但是不实现 forEach() 方法。
```
//没看太懂想要表达什么意思
function printArguments() {
  Array.prototype.forEach.call(arguments, function(item) {
    console.log(item);
  });
}
```
### 数组推导式
14. 推导式可以经常被用在那些需要调用 map() 和 filter()函数的地方，或作为一种结合这两种方式。
15. 推导式这个不是在出一个新的对象吗，回过头仔细看看
```
var numbers = [1, 2, 3, 4];
var doubled = [for (i of numbers) i * 2];
console.log(doubled); // logs 2,4,6,8
```
16. 数组推导式的输入不一定必须是数组; 迭代器和生成器 也是可以的。
```
var str = 'abcdef';
var consonantsOnlyStr = [c for (c of str) if (!(/[aeiouAEIOU]/).test(c))  ].join(''); // 'bcdf'
var interpolatedZeros = [c+'0' for (c of str) ].join(''); // 'a0b0c0d0e0f0'
//输入形式是不能保存的，所以我们要使用join()回复到一个字符串。
```
### 类型化数组
17. JavaScript typed arrays 是类数组对象（array-like object），其提供访问原始二进制数据的机制。 专门的优化将有助于JavaScript代码能够快速和容易地操纵原始二进制数据类型的数组。
18. JavaScript类型数组被分解为缓冲(Buffer)和视图(views)。视图提供了一个上下文，即数据类型、起始偏移量和元素数，这些元素将数据转换为实际类型数组。 ---- 实际的并不了解怎么操作的
19.  ArrayBuffer是一种数据类型，用于表示一个通用的、固定长度的二进制数据缓冲区。你不能直接操纵一个ArrayBuffer中的内容；你需要创建一个数组类型视图或DataView来代表特定格式的缓冲区，并从而实现读写缓冲区的内容。
20. 类型数组视图具有自描述性的名字，并且提供数据类型信息，例如Int8, Uint32, Float64等等。如一个特定类型数组视图Uint8ClampedArray. 它意味着数据元素只包含0到255的整数值。它通常用于Canvas数据处理-----下面有个表格（clamp-强化）
## 带键集合 Map和Set（weakMap和weakSet）
### 映射
#### Map对象
1. Map对象一些基本的属性方法 get、has、delete、clear
#### Object和Map对象的比较
2. Map具有更多优势，那是肯定的呀，根据大众需求封装好的专门的类，Object也可以封装出来呀
    + Object的键均为Strings类型，在Map里键可以是任意类型。
    + 必须手动计算Object的尺寸，但是可以很容易地获取使用Map的尺寸。
    + Map的遍历遵循元素的插入顺序。
    + Object有原型，所以映射中有一些缺省的键。因为重复的键值对会被覆盖的（可以用 map = Object.create(null) 回避）。
3. 这三条提示可以帮你决定用Map还是Object：
    + 如果键在运行时才能知道，或者所有的键类型相同，所有的值类型相同，那就使用Map
    + 如果需要将原始值存储为键，则使用Map，因为Object将每个键视为字符串，不管它是一个数字值、布尔值还是任何其他原始值。
    + 如果需要对个别元素进行操作，使用Object。
#### WeakMap对象
4. 它的键被弱保持，也就是说，当其键所指对象没有其他地方引用的时候，它会被GC回收掉。
5. 与Map对象不同的是，WeakMap的键是不可枚举的。不提供列出其键的方法。列表是否存在取决于垃圾回收器的状态，是不可预知的。
6. WeakMap对象的一个用例是存储一个对象的私有数据或隐藏实施细节---因为回收机制问题吗，显得比较隐私比较安全
7. 对象内部的私有数据和方法被存储在WeakMap类型的privates变量中。所有暴露出的原型和情况都是公开的，而其他内容都是外界不可访问的，因为模块并未导出privates对象。----没看太懂
```
const privates = new WeakMap();
function Public() {
  const me = {
    // Private data goes here
  };
  privates.set(this, me);
}
Public.prototype.method = function () {
  const me = privates.get(this);
  // Do stuff with private data in `me`...
};
module.exports = Public;
```
### 集合
#### Set对象（不可重复）
8. Set对象是一组值的集合，这些值是不重复的，可以按照添加顺序来遍历。
#### 数组（Array）到集合（Set）的转换
9. 可以使用Array.from或展开操作符来完成集合到数组的转换。同样，Set的构造器接受数组作为参数，可以完成从Array到Set的转换。需要重申的是，Set对象中的值不重复，所以数组转换为集合时，所有重复值将会被删除。
```
Array.from(mySet);
[...mySet2];
mySet2 = new Set([1,2,3,4]);
```
#### Array 和 Set 的对比
10. 一般情况下，在JavaScript中使用数组来存储一组元素，而新的集合对象有这些优势：
    + 数组中用于判断元素是否存在的indexOf 函数效率低下。
    + Set对象允许根据值删除元素，而数组中必须使用基于下标的 splice 方法。
    + 数组的indexOf方法无法找到NaN值。-----注意，头一次知道还有这种说法
    + Set对象存储不重复的值，所以不需要手动处理包含重复值的情况。
#### WeakSet
11. WeakSet对象是一组对象的集合。WeakSet中的对象不重复且不可枚举。
12. 与Set对象的主要区别有：
    + WeakSets中的值必须是对象类型，不可以是别的类型 ----什么意思呀
    + WeakSet的“weak”指的是，对集合中的对象，如果不存在其他引用，那么该对象将可被垃圾回收。于是不存在一个当前可用对象组成的列表，所以WeakSets不可枚举
13. WeakSet的用例很有限，比如使用DOM元素作为键来追踪它们而不必担心内存泄漏。
#### Map的键和Set的值的等值判断
14. Map的键和Set的值的等值判断都基于same-value-zero algorithm --- 没看懂呀。
    + 判断使用与===相似的规则。
    + -0和+0相等。
    + NaN与自身相等（与===有所不同）。
## 处理对象
### 对象和属性
1. 对象中未赋值的属性的值为undefined（而不是null）。
2. 一个属性的名称如果不是一个有效的 JavaScript 标识符（例如，一个由空格或连字符，或者以数字开头的属性名），就只能通过方括号标记访问。这个标记法在属性名称是动态判定（属性名只有到运行时才能判定）时非常有用。
```
// 同时创建四个变量，用逗号分隔
var myObj = new Object(),
    str = "myString",
    rand = Math.random(),
    obj = new Object();
myObj.type              = "Dot syntax";
myObj["date created"]   = "String with space";
myObj[str]              = "String value";
myObj[rand]             = "Random Number";
myObj[obj]              = "Object";
myObj[""]               = "Even an empty string";
console.log(myObj);
//因为JavaScript中的对象只能使用String类型作为键类型。
```
3. 注意obj.hasOwnProperty(i)此方法的使用，我一般这样循环的时候，是不会去这样判断一下的
```
function showProps(obj, objName) {
  var result = "";
  for (var i in obj) {
    if (obj.hasOwnProperty(i)) {
        result += objName + "." + i + " = " + obj[i] + "\n";
    }
  }
  return result;
}
```
### 枚举一个对象所有的属性
4. 从ES5开始，主要有三种方法（感觉就是深拷贝浅拷贝的区别）
    + for...in 循环 该方法依次访问一个对象及其原型链中所有可枚举的属性。 --- 包括原型链哦
    + Object.keys(o) 该方法返回对象 o 自身包含（不包括原型中）的所有可枚举属性的名称的数组。----不包括原型哦
    + Object.getOwnPropertyNames(o) 该方法返回对象 o 自身包含（不包括原型中）的所有属性(无论是否可枚举)的名称的数组。-----？？？都不可以枚举你还要总结出来，说实话有点鬼畜
### 使用对象初始化器 --没看太懂
5. 如果一个对象是通过在顶级脚本的对象初始化器创建的，则 JavaScript 在每次遇到包含该对象字面量的表达式时都会创建对象。同样的，在函数中的初始化器在每次函数调用时也会被创建。
```
var obj = { property_1:   value_1,   // property_# 可以是一个标识符...
            2:            value_2,   // 或一个数字...
           ["property" +3]: value_3,  //  或一个可计算的key名... 
            // ...,
            "property n": value_n }; // 或一个字符串
```
6. 使用 Object.create 方法
7.  prototype 属性
8. 通过 this 引用对象
9. 定义 getters 与 setters
```
var o = {
  a: 7,
  get b() { 
    return this.a + 1;
  },
  set c(x) {
    this.a = x / 2
  }
};
console.log(o.a); // 7
console.log(o.b); // 8
o.c = 50;
console.log(o.a); // 25
```
```
//可能更能表现JavaScript语法的动态特性,但也会使代码变得难以阅读和理解。
var o = { a:0 }
Object.defineProperties(o, {
    "b": { get: function () { return this.a + 1; } },
    "c": { set: function (x) { this.a = x / 2; } }
});
o.c = 10 // Runs the setter, which assigns 10 / 2 (5) to the 'a' property
console.log(o.b) // Runs the getter, which yields a + 1 or 6
```
### 删除属性
10. 用 delete 操作符删除一个不是继承而来的属性 ---- 注意不是继承来的属性，自己的可以删，但是父节点还是动不了，删除各式各样的隐式节点，var 声明的不可以删除，但是不是用var声明的全局变量是可以通过delete删除的
```
g = 17;
delete g;
```
### 比较对象
11. 在 JavaScript 中 objects 是一种引用类型。两个独立声明的对象永远也不会相等，即使他们有相同的属性，只有在比较一个对象和这个对象的引用时，才会返回true.
```
/ 两个变量, 两个具有同样的属性、但不相同的对象
var fruit = {name: "apple"};
var fruitbear = {name: "apple"};
fruit == fruitbear // return false
fruit === fruitbear // return false
```