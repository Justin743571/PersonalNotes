# 基础知识



## 数据类型

### 基本数据类型

#### string 

#### number

#### boolean

#### undefined

#### null



### 引用数据类型

#### Object

#### Array

#### Function







### undefined与null

在JavaScript中，`null`和`undefined`都表示某种形式的“没有值”，但它们之间存在一些区别：

1. **undefined**：
   
   - 在JavaScript中，`undefined`表示声明了但未初始化的变量，或者访问对象中不存在的属性时返回的值。
   - 当尝试访问尚未赋值的变量时，JavaScript会返回`undefined`。
   - 函数没有明确返回值时，默认返回`undefined`。
   - 例如：
     ```javascript
     let x;
     console.log(x); // 输出 undefined
     ```
   
2. **null**：
   - `null`表示“空值”或“未知值”，通常用于表示变量或对象的特定属性已经被赋值为空。
   - 如果要明确表示某个变量或对象属性是“空”的，通常会将其赋值为`null`。
   - 例如：
     ```javascript
     let y = null;
     console.log(y); // 输出 null
     ```

总之，`undefined`通常是JavaScript中默认的“没有值”的状态，而`null`是明确指定的“空值”。





## 一.操作符



#### 在JavaScript中，逻辑操作可以用于非布尔数据



```javascript
//=== 是严格相等运算符，用于比较两个值是否相等且类型也相等
// 相等运算符 == 只会比较值是否相等，而不考虑数据类型。
let x2 =1;
console.log(x2===1);
console.log(x2!==1);

//三元运算符
let points = 110;
let type =points>100? 'gold':'silver';
console.log(type);


//在JavaScript中，逻辑操作可以用于非布尔数据

//类真值
//当只要有一个值为真，结果就为真
//类假值 falsy（false）类假值有: undefined  null 0 flase '' NaN
console.log(false||'Mosh');
//它会返回Mosh 因为string类型是类真值
console.log(false||1||2);
//它会返回1 因为运算从第一个参数开始，只要它遇到第一个类真正值,它就会返回
//例子 当用户没有选择颜色，系统会默认给它一个默认颜色
let userColor = undefined ; 
let defaultColor = 'blue';
let currentColor = userColor || defaultColor;
console.log(currentColor);

//逻辑操作符优先级
let x = 2 + 3 * 4
console.log(x) //会返回 14

```



在 JavaScript 中，`&&` 和 `||` 是逻辑运算符，用于处理布尔值和表达式。它们的含义如下：

### 1. 逻辑与运算符 `&&`：

- **语法：** `expr1 && expr2`

- **含义：** 如果 `expr1` 为真（truthy），则返回 `expr2` 的值；否则返回 `expr1` 的值。

- **应用：** 常用于条件语句和表达式中，用于在第一个条件为真时执行第二个条件。

```javascript
const result = (true && "Hello, World!"); // result 将为 "Hello, World!"
```

### 2. 逻辑或运算符 `||`：

- **语法：** `expr1 || expr2`

- **含义：** 如果 `expr1` 为真（truthy），则返回 `expr1` 的值；否则返回 `expr2` 的值。

- **应用：** 常用于设置默认值或者在某个条件为假时执行备用操作。

```javascript
const defaultValue = someValue || "Default Value";
```

### 3. 短路逻辑：

- **逻辑与 (`&&`) 短路：** 如果第一个条件为假，不会执行第二个条件，直接返回第一个条件的值。

```javascript
false && console.log("This won't be printed");
```

- **逻辑或 (`||`) 短路：** 如果第一个条件为真，不会执行第二个条件，直接返回第一个条件的值。

```javascript
true || console.log("This won't be printed");
```

短路逻辑是 JavaScript 中常用的一种技巧，它能够根据第一个条件的结果决定是否执行第二个条件，从而提高代码的效率。



## 二.循环

```javascript
//遍历对象 for-in循环
//key 会依次取到 name 和 age 这两个属性名。key 表示当前属性的名称，而 person[key] 表示当前属性的值
const person ={
    name:'mosh',
    age: 30
};
//这是基本格式,每一次循环中，key都会对应person的一个属性
for(let key in person){
    console.log(key,person[key]);
}



//遍历数组 for-of
const colors=['red','green','blue'];
for(let color of colors){
    console.log(color);
}
```

break 结束循环， continue结束此次循环，进入下次循环(结束的循环中在continue后面代码不执行)

## 三.对象

#### 在JavaScript中，如果对象的键（key）与值（value）的变量名相同，可以使用简写形式，只写键的变量名即可。

#### 每一个对象都有一个构造器属性，它引用了创建该对象的构造函数。  

#### 构造函数的作用是在实例化对象时进行初始化操作

#### 在JavaScript中，对象确实可以随意创建，不需要事先定义类或构造函数。你可以直接使用对象字面量语法（`{}`）创建对象，也可以使用`new`关键字和构造函数创建对象。

#### 函数既对象

#### 数值类型遵从深复制概念，而引用类型遵从指针指向同地址的概念



构造器（Constructor）在 JavaScript 中与对象和构造函数相关。在 JavaScript 中，你可以使用构造函数创建对象。构造函数是一个用于创建和初始化对象的函数。当你使用 `new` 关键字来调用构造函数时，它会创建一个新的对象，并将该对象的 `constructor` 属性指向构造函数本身。

下面是一个简单的例子：

```javascript
// 构造函数
function Person(name, age) {
  this.name = name;
  this.age = age;
}

// 使用构造函数创建对象
var person1 = new Person('John', 25);

// 访问构造器属性
console.log(person1.constructor); // 输出：function Person(name, age) { ... }
```

在这个例子中，`Person` 是一个构造函数，它有两个参数 `name` 和 `age`，用来初始化创建的对象的属性。当你使用 `new Person('John', 25)` 创建 `person1` 对象时，`person1.constructor` 就指向了 `Person` 构造函数。

这对于识别对象的类型和了解对象的创建方式很有用。通过检查对象的 `constructor` 属性，你可以知道对象是由哪个构造函数创建的。但需要注意，这种方式并不是完全可靠的，因为该属性可以被修改。

如果你想要更深入地了解 JavaScript 中的构造函数、原型链等概念，可以进一步研究这些主题。这些概念对于理解 JavaScript 中的对象和继承机制非常重要。



### 在JavaScript中，函数就是对象

**构造函数是通过函数定义的，它用于创建特定类型的对象。对象通过构造函数创建后，会拥有 `constructor` 属性，指向用于创建它的构造函数。**

在 JavaScript 中，每个函数对象都有一个内建属性叫做 `prototype`。这个属性是一个对象，它包含了一些预定义的属性和方法。

当你创建一个函数时，JavaScript 会自动为这个函数创建一个 `prototype` 对象。这个对象包含一个叫做 `constructor` 的属性，指向该函数自身。这就是为什么在前面的例子中，我们可以通过 `person1.constructor` 来获取构造函数。

例如：

```javascript
function Person(name, age) {
  this.name = name;
  this.age = age;
}

// Person 函数的 prototype 对象
console.log(Person.prototype); // 输出：{ constructor: [Function: Person] }
```

然而，并不是每个函数都被用作构造函数。构造函数是一种特殊的函数，用于创建对象。当你使用 `new` 关键字调用一个函数时，它就成为了构造函数。构造函数的目的是初始化对象的属性，并且通过 `prototype` 对象实现了对象之间的继承关系。

所以，可以说每个函数都有一个 `prototype` 对象，但不是每个函数都是构造函数。构造函数是一种特殊用途的函数，用于创建对象。



### 值类型数据复制值,引用类型数据或对象复制引用

```javascript
let number = 10  //这里的number和下面形参number不是同一个变量

function increase(number){
    number++;
}

increase(number);
console.log(number); //结果返回10
```

在这个代码中，虽然你在 `increase` 函数内部对 `number` 进行了增加操作，但是这个操作并不会影响函数外部的 `number`。JavaScript 中的基本数据类型（比如数字）在传递给函数时是按值传递的，也就是说函数内对参数的修改不会影响到函数外部的变量。

具体来说，在 `increase` 函数中，你传递的是 `number` 的值（10），而在函数内部对 `number` 的操作只是对函数内部的一个局部变量进行的，不会影响到函数外部的 `number`。

如果你想要在函数外部看到变化，可以考虑使用对象来传递参数，因为对象是按引用传递的。例如：

```javascript
let obj = {value:10}

function increase(obj){
    obj.value++;
}

increase(obj);
console.log(obj);//这里返回的为 11	
```

这样，通过传递对象，你可以在函数内部修改对象的属性，从而在函数外部看到变化。

### 模板语法

在JavaScript中，"模板语法"通常用于描述一种用于生成动态内容的字符串模板或模板字符串的语法。模板字符串是一种特殊的字符串，它允许你插入表达式、变量和其他内容，使字符串更加灵活和动态。下面是一些关于JavaScript模板字符串的基本语法和用法：

1. **创建模板字符串：**

   使用反引号（``）来创建模板字符串。例如：

   ```javascript
   let name = 'World';
   let greeting = `Hello, ${name}!`;
   console.log(greeting);  // 输出: Hello, World!
   ```

   在`${}`中可以包含任何JavaScript表达式，它会被求值并插入到字符串中。

2. **多行字符串：**

   模板字符串可以跨越多行，而无需使用特殊的字符（如 `\n`）。例如：

   ```javascript
   let multiLineString = `
   This is a
   multi-line
   string.
   `;
   console.log(multiLineString);
   ```

3. **标签模板字符串：**

   你可以使用标签函数对模板字符串进行处理，这允许你自定义模板字符串的解析方式。例如：

   ```javascript
   function customTag(strings, ...values) {
       console.log(strings); // 字符串数组
       console.log(values);  // 表达式结果数组
   }
   
   let a = 5;
   let b = 10;
   customTag`Sum of ${a} and ${b} is ${a + b}`;
   ```

   在这个例子中，`strings`是一个包含模板字符串的文本的数组，`values`是表达式的结果数组。

这些只是JavaScript模板字符串的一些基础，当你深入学习JavaScript时，你可能会发现更多高级用法和相关概念。如果你有具体的问题或者需要更多解释，随时告诉我，我会尽力帮助你。

## 四.数组

### 箭头函数

在JavaScript中，箭头函数是一种简洁的函数声明方式，它是ES6（ECMAScript 2015）引入的新特性之一。箭头函数提供了一种更简洁的语法来定义函数，并且在某些情况下可以更清晰地表达函数的意图。

下面是箭头函数的基本语法：

```javascript
// 无参数箭头函数
const greet = () => {
    return "Hello!";
};

// 有参数箭头函数
const double = (num) => {
    return num * 2;
};

// 如果只有一个参数，可以省略参数的括号
const triple = num => {
    return num * 3;
};

// 如果函数体只有一条语句，可以省略花括号和return关键字
const square = num => num * num;

// 如果箭头函数的函数体是一个对象字面量，则需要用小括号包裹起来，以免与函数体的花括号混淆
const getPerson = () => ({
    name: "John",
    age: 30
});
```

需要注意的是，箭头函数有一些与普通函数不同的行为：

1. **没有自己的this**：箭头函数的this值继承自外部函数作用域中的this值，而不是根据函数被调用时的上下文来确定。
2. **无法使用arguments对象**：箭头函数没有自己的arguments对象，但可以访问包含它的普通函数的arguments对象。
3. **不能作为构造函数**：箭头函数不能使用new关键字调用，因为它们没有自己的this绑定。
4. **不能用作Generator函数**：箭头函数不能使用yield关键字。

箭头函数通常在需要简洁的函数定义时非常有用，尤其是在回调函数、数组方法（如map、filter、reduce等）以及在简化代码时。



### 1.添加元素

```javascript
const numbers = [3,4];
console.log(numbers);

//到最前面添加
numbers.unshift(1,2);


//到最后面添加
numbers.push(5,6);


//到中间添加或者删除
//用splice就可以向指定位置添加或者删除元素 
//第一个参数为想要指定哪个索引,第二参数为删除的个数，第三个参数为添加什么东西
numbers.splice(2,0,'a','b');


//join方法就是在每个数中间加字符什么的,提供一个分隔符
const numbers3 = [1,2,3,4];
const joined = numbers3.join(',');
console.log(joined); 

const message = 'This is My first Message';
//拆分后，parts 变量会成为一个数组，包含了原始消息中的每个单词
const parts = message.split(' ');
const combined3 = parts.join('-');
//结果如下 This-is-My-first-Message
//这样的一般用在URL
```

### 2.查找元素

```javascript
const numbers = [1,2,3,4,5,1,6];
//查找索引，第一参数为想要查询的数,
//可以有第二个参数，需要输入索引，然后会从该索引开始找
console.log(numbers.indexOf(1));
//查找最后一次出现的索引
numbers.lastIndexOf(1);
//includes 布尔类型 如果定值存在返回ture
console.log(numbers.includes(1));

```

### 3.箭头函数(查找对象)

```javascript
//当我们输入调用一个函数时，里面的参数也是函数时我们就可以用箭头函数语法

const courses = [
    {id:1, name:'a'},
    {id:2, name:'b'},
    {id:3, name:'c'},
];

//查找对象我们要用到find方法 这个course会返回一个对象
//查找是否有个course对象的name属性是a的
const course = courses.find(course=>course.name==='a');
console.log(course);

```

### 4.删除函数

```javascript
const numbers = [1,2,3,4,5,6,7];
console.log(numbers);

//到最前面删除
const first = numbers.shift(1,2);


//删除最后面一个元素
const last = numbers.pop();
console.log(numbers);
//返回值为删除的元素
console.log(last);


//到中间添加或者删除
//用splice就可以向指定位置添加或者删除元素 
//第一个参数为想要指定哪个索引,第二参数为删除的个数，第三个参数为添加什么东西
numbers.splice(2,1);
```

### 5.清空数组

```javascript
//方法二
numbers.length=0;

//方法三
numbers.splice(0,numbers.length);
```

### 6.组合和切割数组(拆分操作符)

```javascript
const first = [1,2,3];
const second = [4,5,6,7];

//组合数组
const combined = first.concat(second);
//使用拆分操作符更简单和清楚 ,使用拆分操作符时，每一个元素都被单独返回
const combined2 = [...first,'a',...second,'b'];

//slice()
//如果里面填两个参数则为 数组索引 切割的元素是 包左不包右
//如果里面填一个参数为索引，则为得到包括索引后面的元素
//如果不填参数则为copy所有
const slice = combined.slice(2);

//如果是组合或者切割引用数据类型
//则对象不会复制，会指向那个对象的地址
```

### 7.遍历一个数组

```javascript
const numbers = [1,2,3,4];

for(let number of numbers){
    console.log(number);
}

numbers.forEach(function(number)
{
    console.log(number);
})

//使用箭头函数

numbers.forEach((number,index)=>console.log(index,number)); 
```

### 8.数组排序

```javascript
const numbers = [2,3,4,1]
//sort方法是将数组改为字符串，然后在排序
numbers.sort();
console.log(numbers);
//reverse方法 将数组的元素排序颠倒,会创建一个新对象
numbers.reverse();
console.log(numbers);
```

### 9.检测数组的元素

```javascript
 //检测是否每一个数为正数
 const numbers = [1,2,3,-2,5,6]; 
 //every 方法会在检测到第一个不满足条件的元素时停止运行，并返回 false。
 //它不会再继续迭代数组的其他元素，因为已经有一个元素不满足条件，所以可以确定整个数组不满足条件,直接返回false。
 const allPositive = numbers.every(function(value){
    return value>=0;
 });
 console.log(allPositive);

 //some方法作用是检查是否数组中至少有一个元素符合这个条件
 //如果有一个满足要求他就会返回ture,搜索过程终止
 const numbers2 = [1,2,3,-2,5,6]; 
 const atLeastOnePositive = numbers.some(function(value){
    return value>=0;
 });
 console.log(allPositive);
```

### 10.筛选数组

```javascript
const numbers = [1,2,3,4,-1,-4,8];

//如果value为正数则直接返回目标元素,放到一个新的数组中
const filtered=numbers.filter(function(value){
    return value>=0;
});
```

### 11.数组映射

```javascript
const numbers = [1,2,3,4,-1,-4,8];
//filter是检测数组中每一个元素
//如果value为正数则直接返回目标元素,放到一个新的数组中
const filtered=numbers.filter(function(value){
    return value>=0;
});
//map 方法用于对数组中的每个元素应用一个函数，然后返回一个新的数组，其中包含了经过映射处理的元素。
const items =filtered.map(n=> '<li>'+n+'</li>');
//每一个元素都映射为了一个<li>标签

//join把数组变为字符串
const html='<ul>'+items.join(' ')+'</ul>';
console.log(html);

//更加简洁的写法
const numbers3 = [1,2,3,4,-1,-4,8];

const items3 = number3
    .filter(n => n>=0)
    .map(n =>({ value:n}));

    console.log(items3);
```

### 12.求合

`reduce()` 是 JavaScript 中数组的一个高阶函数，它用于对数组中的所有元素执行一个 reducer 函数（提供给 `reduce()` 的参数），将其结果汇总为单个值。该方法提供了一种累积的方式来处理数组，可以用来实现各种操作，比如求和、求积、查找最大值或最小值等。

下面是 `reduce()` 方法的基本语法：

```javascript
array.reduce(callback(accumulator, currentValue[, currentIndex[, array]])[, initialValue])
```

其中：

- `callback` 是一个函数，接受四个参数：
  - `accumulator`：累积器，存储 `reduce()` 函数的返回值，或者是上一次调用 `callback` 函数的返回值。
  - `currentValue`：当前正在处理的数组元素。
  - `currentIndex`（可选）：当前正在处理的元素的索引。
  - `array`（可选）：调用 `reduce()` 的数组。
- `initialValue`（可选）：作为第一次调用 `callback` 函数时的第一个参数 `accumulator` 的值。如果未提供 `initialValue`，则 `reduce()` 会以数组的第一个元素作为 `accumulator` 的初始值，并且从数组的第二个元素开始遍历。

下面是一个简单的求和示例：

```javascript
const numbers = [1, 2, 3, 4, 5];

const sum = numbers.reduce((accumulator, currentValue) => {
  return accumulator + currentValue;
}, 0);

console.log(sum); // 输出 15
```

在这个示例中，我们定义了一个数组 `numbers`，然后使用 `reduce()` 方法对数组中的所有元素求和。在 `reduce()` 的回调函数中，`accumulator` 初始值为 `0`，然后遍历数组中的每个元素，依次将 `accumulator` 和当前元素相加，最终得到总和 `15`。

`reduce()` 方法非常灵活，可以用来实现各种功能，例如计算数组元素的平均值、拼接字符串、将二维数组转换为一维数组等等。



## 四.函数

### 1.函数声明和函数表达式

```javascript
//在JavaScript中函数声明会被系统放到最前面
walk()
//函数声明
function walk(){
    console.log('walk');
}


//函数表达式
const run =function(){
    console.log('walk');
};
run();

```

### 2.余下操作符

```javascript
// ...args 这就是余下操作符,余下参数必须是参数的最后一个
//它允许你将任意数量的参数收集到一个名为 args 的数组中。
function sum(...args){
    //它会显示我们加进去的实参成为一个数组
    console.log(args);
    //可以用reduce求和，因为现在args是一个数组了
    args.reduce((a,b)=>a+b); 
}
console.log(sum(1,2,3,4,5,6));
```

### 3.参数默认值

```javascript
//新版本设置默认值直接在形参后面加值
//注意，我们给中间设了默认值，也的给后面设置默认值
function interest (principal,rate=3.5 ,year=5){
    //老版本默认值设置
    rate = rate||3.5;
    year = year||5;

    return principal*rate/100*year;
}
console.log(interest(10000,3.5,5));
```

### 4.setter和getter

```javascript
const person = {

    firstName :'Mosh',
    lastName : 'Hamedani',
    //
    get fullName(){
        return `${person.firstName} ${person.lastName}`
    },
    set fullName(value){
        const parts =value.split(' ');
        this.firstName = parts[0];
        this.lastName = parts[1];
     }
};


person.fullName = 'John Smith';

console.log(person);
```

### 5.this关键字

```javascript
//this在这个回调函数当中时，这个回调函数是个正则函数，它不是这个对象里的方法了，this指向的是全局对象

//处理方法我们需要引用第二个参数，把this值向这个方法对象
const video = {
    title : 'a',
    tags :['a','b','c'],
    showTags(){
        this.tags.forEach(function(tag){
            console.log(this.title,tag);
        },this);
    }
};
// 但是并不是每个JavaScript中的方法都可以输入特定的this参数



//如何改变一个函数this指向


//方法一:我们可以在对象方法的里面定义一个常量，把this赋给它，可以在回调函数里面用
const video2 = {
    title : 'a',
    tags :['a','b','c'],
    showTags(){
        //中继变量
        const self = this;
        this.tags.forEach(function(tag){
            console.log(self.title,tag);
        },this);
    }
};

//重点 使用箭头函数就可以解决,箭头函数从它的容器函数中继承了this的值
const video4 = {
    title : 'a',
    tags :['a','b','c'],
    showTags(){
        this.tags.forEach(tag =>{
            console.log(this.title,tag);
        },);
    }
};
```

# 面向对象



#### 在 JavaScript 中，当使用 `const` 声明一个引用类型（例如对象或数组）时，该引用的地址是不可变的，但是引用类型本身的内容是可变的。换句话说，你不能重新分配一个 `const` 声明的引用，但是你可以改变该引用指向的对象的属性或数组的元素。



#### 在JavaScript中，创建对象有三种方法，对象操作符，工厂函数，构造函数



#### 对象操作符创建对象不是一种复制对象的好方法



#### 闭包





### 1.抽象

```javascript
//抽象就是在对象里面的某些属性或者方法不希望被外部调用,隐藏细节

//我们可以使用到 本地变量私有成员局部变量 他们只能在这个函数中使用

function circle (radius){
    this.radius = radius;
    let defaultLocation = { x:0 , y:0};

    let computeOptimumLocation = function (factor) {
        //...
    }

    this.draw  = function(){
        computeOptimumLocation(0.1);
        //调用内部属性还是需要调用tihs
        this.radius
    }
}
const circle = new circle(10);
```

### 类

```javascript
//在新版本中有一种创建对象和继承关系的新方法 classes



class Circle{
    //在类中建立的constructor里面的属性和方法是放在实例成员里面的
    constructor(radius){
        this.raduis = radius;
        this.move = function(){
            console.log('move');
        }
    }
    //没用constructor的属性和方法是放在它的父类里的
    draw(){
        console.log('draw');
    }
}

const c = new Circle(1);
```







## 继承

#### 原型可以理解为一个对象的父母

#### 在JavaScript中，没有类的概念，继承我们需要用到原型继承



#### 所有用Circle构造函数创建的circle对象，都有同一个原型

#### 所有使用数组构造函数创建的数组，都有同一个原型





#### 实例对象与原型对象之间可以互相访问属性和方法



#### 当你重设了原型对象，也需要重设构造器



#### 在JavaScript中，没有类的概念，class关键字，这个的本质上是个函数，它更好的组织创建对象

























