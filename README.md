# ES6
ES6 Learning

## JavaScript 数据类型
number：和JavaScript的number完全一致；
boolean：就是JavaScript的true或false；
string：就是JavaScript的string；
null：就是JavaScript的null；
array：就是JavaScript的Array表示方式——[]；
object：就是JavaScript的{ ... }表示方式。
undefined: 就是JavaScript的function

## 相等运算符==
JavaScript在设计时，有两种比较运算符：
第一种是==比较，它会自动转换数据类型再比较，很多时候，会得到非常诡异的结果；
第二种是===比较，它不会自动转换数据类型，如果数据类型不一致，返回false，如果一致，再比较。
由于JavaScript这个设计缺陷，不要使用==比较，始终坚持使用===比较。
另一个例外是NaN这个特殊的Number与所有其他值都不相等，包括它自己
唯一能判断NaN的方法是通过isNaN()函数


## null和undefined
JavaScript的设计者希望用null表示一个空的值，而undefined表示值未定义。事实证明，这并没有什么卵用，区分两者的意义不大。大多数情况下，我们都应该用null。undefined仅仅在判断函数参数是否传递的情况下有用。


## Object
JavaScript的对象是一组由键-值组成的无序集合，要获取一个对象的属性，我们用对象变量.属性名的方式.

由于JavaScript的对象是动态类型，你可以自由地给一个对象添加或删除属性

JavaScript的默认对象表示方式{}可以视为其他语言中的Map或Dictionary的数据结构，即一组键值对。

但是JavaScript的对象有个小问题，就是键必须是字符串。但实际上Number或者其他数据类型作为键也是非常合理的。

如果我们要检测对象是否拥有某一属性，可以用in操作符. 如果in判断一个属性存在，这个属性不一定是xiaoming的，它可能是xiaoming继承得到的. 因为toString定义在object对象中，而所有对象最终都会在原型链上指向object，所以xiaoming也拥有toString属性。

要判断一个属性是否是xiaoming自身拥有的，而不是继承得到的，可以用hasOwnProperty()方法

```javascript
	
	//Definition and accessing
	var person = {
	    name: 'Bob',
	    age: 20,
	    tags: ['js', 'web', 'mobile'],
	    city: 'Beijing',
	    hasCar: true,
	    zipcode: null
	};

	person.name; // 'Bob'
	person.zipcode; // null


	//Dynamic delete properties
	var xiaoming = {
	    name: '小明'
	};
	xiaoming.age; // undefined
	xiaoming.age = 18; // 新增一个age属性
	xiaoming.age; // 18
	delete xiaoming.age; // 删除age属性
	xiaoming.age; // undefined
	delete xiaoming['name']; // 删除name属性
	xiaoming.name; // undefined
	delete xiaoming.school; // 删除一个不存在的school属性也不会报错

	//Detect properties using in operator
	var xiaoming = {
	    name: '小明',
	    birth: 1990,
	    school: 'No.1 Middle School',
	    height: 1.70,
	    weight: 65,
	    score: null
	};
	'name' in xiaoming; // true
	'grade' in xiaoming; // false
	'toString' in xiaoming; // true

	//hasOwnProperty()
	var xiaoming = {
	    name: '小明'
	};
	xiaoming.hasOwnProperty('name'); // true
	xiaoming.hasOwnProperty('toString'); // false
```

## 多行字符串
由于多行字符串用\n写起来比较费事，所以最新的ES6标准新增了一种多行字符串的表示方法，用反引号 ` ... ` 表示
```javascript
	`这是一个
	多行
	字符串`;
```

## 模板字符串
如果有很多变量需要连接，用+号就比较麻烦。ES6新增了一种模板字符串，表示方法和上面的多行字符串一样，但是它会自动替换字符串中的变量：
```javascript
	var name = '小明';
	var age = 20;
	var message = `你好, ${name}, 你今年${age}岁了!`;
	console.log(message);
```

## 操作字符串
要获取字符串某个指定位置的字符，使用类似Array的下标操作，索引号从0开始.
需要特别注意的是，字符串是不可变的，如果对字符串的某个索引赋值，不会有任何错误，但是，也没有任何效果
```javascript
	var s = 'Hello, world!';

	s[0]; // 'H'
	s[6]; // ' '
	s[7]; // 'w'
	s[12]; // '!'
	s[13]; // undefined 超出范围的索引不会报错，但一律返回undefined

	var s = 'Test';
	s[0] = 'X';
	alert(s); // s仍然为'Test'
```
toLowerCase()把一个字符串全部变为小写
toUpperCase()把一个字符串全部变为大写
indexOf()会搜索指定字符串出现的位置
substring()返回指定索引区间的子串
```javascript
	var s = 'hello, world'
	s.substring(0, 5); // 从索引0开始到5（不包括5），返回'hello'
	s.substring(7); // 从索引7开始到结束，返回'world'

	var s = 'hello, world';
	s.indexOf('world'); // 返回7
	s.indexOf('World'); // 没有找到指定的子串，返回-1

	var s = 'Hello';
	var lower = s.toLowerCase(); // 返回'hello'并赋值给变量lower
	lower; // 'hello'

	var s = 'Hello';
	s.toUpperCase(); // 返回'HELLO'
```

## Array
JavaScript的Array可以包含任意数据类型，并通过索引来访问每个元素。

要取得Array的长度，直接访问length属性. 直接给Array的length赋一个新的值会导致Array大小的变化.

Array可以通过索引把对应的元素修改为新的值，因此，对Array的索引进行赋值会直接修改这个Array. 如果通过索引赋值时，索引超过了范围，同样会引起Array大小的变化.

```javascript
	var arr = [1, 2, 3.14, 'Hello', null, true];
	arr.length; // 6

	var arr = [1, 2, 3];
	arr.length; // 3
	arr.length = 6;
	arr; // arr变为[1, 2, 3, undefined, undefined, undefined]
	arr.length = 2;
	arr; // arr变为[1, 2]

	var arr = ['A', 'B', 'C'];
	arr[1] = 99;
	arr; // arr现在变为['A', 99, 'C']

	var arr = [1, 2, 3];
	arr[5] = 'x';
	arr; // arr变为[1, 2, 3, undefined, undefined, 'x']
```

indexOf()来搜索一个指定的元素的位置

slice()就是对应String的substring()版本，它截取Array的部分元素. 如果不给slice()传递任何参数，它就会从头到尾截取所有元素。利用这一点，我们可以很容易地复制一个Array

push()向Array的末尾添加若干元素
pop()则把Array的最后一个元素删除掉

unshift()往Array的头部添加若干元素
shift()方法则把Array的第一个元素删掉

sort()可以对当前Array进行排序，它会直接修改当前Array的元素位置，直接调用时，按照默认顺序排序
reverse()把整个Array的元素给掉个个，也就是反转

splice()方法是修改Array的“万能方法”，它可以从指定的索引开始删除若干元素，然后再从该位置添加若干元素

oncat()方法把当前的Array和另一个Array连接起来，并返回一个新的Array. concat()方法并没有修改当前Array，而是返回了一个新的Array

join()方法是一个非常实用的方法，它把当前Array的每个元素都用指定的字符串连接起来，然后返回连接后的字符串

```javascript

	//indexOf()
	var arr = [10, 20, '30', 'xyz'];
	arr.indexOf(10); // 元素10的索引为0
	arr.indexOf(20); // 元素20的索引为1
	arr.indexOf(30); // 元素30没有找到，返回-1
	arr.indexOf('30'); // 元素'30'的索引为2

	//slice()
	var arr = ['A', 'B', 'C', 'D', 'E', 'F', 'G'];
	arr.slice(0, 3); // 从索引0开始，到索引3结束，但不包括索引3: ['A', 'B', 'C']
	arr.slice(3); // 从索引3开始到结束: ['D', 'E', 'F', 'G']

	//slice(), copy array, compare memory location
	var arr = ['A', 'B', 'C', 'D', 'E', 'F', 'G'];
	var aCopy = arr.slice();
	aCopy; // ['A', 'B', 'C', 'D', 'E', 'F', 'G']
	aCopy === arr; // false

	//push(), pop(), to end 
	var arr = [1, 2];
	arr.push('A', 'B'); // 返回Array新的长度: 4
	arr; // [1, 2, 'A', 'B']
	arr.pop(); // pop()返回'B'
	arr; // [1, 2, 'A']
	arr.pop(); arr.pop(); arr.pop(); // 连续pop 3次
	arr; // []
	arr.pop(); // 空数组继续pop不会报错，而是返回undefined
	arr; // []

	//shift(), unshift(), to start
	var arr = [1, 2];
	arr.unshift('A', 'B'); // 返回Array新的长度: 4
	arr; // ['A', 'B', 1, 2]
	arr.shift(); // 'A'
	arr; // ['B', 1, 2]
	arr.shift(); arr.shift(); arr.shift(); // 连续shift 3次
	arr; // []
	arr.shift(); // 空数组继续shift不会报错，而是返回undefined
	arr; // []

	//sort()
	var arr = ['B', 'C', 'A'];
	arr.sort();
	arr; // ['A', 'B', 'C']

	//reverse()
	var arr = ['one', 'two', 'three'];
	arr.reverse(); 
	arr; // ['three', 'two', 'one']

	//splice()
	var arr = ['Microsoft', 'Apple', 'Yahoo', 'AOL', 'Excite', 'Oracle'];
	// 从索引2开始删除3个元素,然后再添加两个元素:
	arr.splice(2, 3, 'Google', 'Facebook'); // 返回删除的元素 ['Yahoo', 'AOL', 'Excite']
	arr; // ['Microsoft', 'Apple', 'Google', 'Facebook', 'Oracle']
	// 只删除,不添加:
	arr.splice(2, 2); // ['Google', 'Facebook']
	arr; // ['Microsoft', 'Apple', 'Oracle']
	// 只添加,不删除:
	arr.splice(2, 0, 'Google', 'Facebook'); // 返回[],因为没有删除任何元素
	arr; // ['Microsoft', 'Apple', 'Google', 'Facebook', 'Oracle']

	//concat()
	var arr = ['A', 'B', 'C'];
	var added = arr.concat([1, 2, 3]);
	added; // ['A', 'B', 'C', 1, 2, 3]
	arr; // ['A', 'B', 'C']

	//join()
	var arr = ['A', 'B', 'C', 1, 2, 3];
	arr.join('-'); // 'A-B-C-1-2-3'
```

## if statement
JavaScript把null、undefined、0、NaN和空字符串''视为false，其他值一概视为true，因此上述代码条件判断的结果是true.

## for statement
for循环的一个变体是for ... in循环，它可以把一个对象的所有属性依次循环出来

```javascript

	//for, in, key iteration
	var o = {
	    name: 'Jack',
	    age: 20,
	    city: 'Beijing'
	};
	for (var key in o) {
	    console.log(key); // 'name', 'age', 'city'
	}

	//for, in, key iteration + hasOwnProperty()
	var o = {
	    name: 'Jack',
	    age: 20,
	    city: 'Beijing'
	};
	for (var key in o) {
	    if (o.hasOwnProperty(key)) {
	        console.log(key); // 'name', 'age', 'city'
	    }
	}

	//for, in iteration + Array
	var a = ['A', 'B', 'C'];
	for (var i in a) {
	    console.log(i); // '0', '1', '2'
	    console.log(a[i]); // 'A', 'B', 'C'
	}

```

## Map
ES6规范引入了新的数据类型Map. Map是一组键值对的结构，具有极快的查找速度.

由于一个key只能对应一个value，所以，多次对一个key放入value，后面的值会把前面的值冲掉


```javascript

	//Map initialization
	var m = new Map([['Michael', 95], ['Bob', 75], ['Tracy', 85]]);
	m.get('Michael'); // 95

	//Map, set & get & delete
	var m = new Map(); // 空Map
	m.set('Adam', 67); // 添加新的key-value
	m.set('Bob', 59);
	m.has('Adam'); // 是否存在key 'Adam': true
	m.get('Adam'); // 67
	m.delete('Adam'); // 删除key 'Adam'
	m.get('Adam'); // undefined

	//Map, overwrite
	var m = new Map();
	m.set('Adam', 67);
	m.set('Adam', 88);
	m.get('Adam'); // 88
```

## Set
Set和Map类似，也是一组key的集合，但不存储value。由于key不能重复，所以，在Set中，没有重复的key.

要创建一个Set，需要提供一个Array作为输入，或者直接创建一个空Set

```javascript

	//Set initialization
	var s1 = new Set(); // 空Set
	var s2 = new Set([1, 2, 3]); // 含1, 2, 3

	//Set, duplicated element overwite
	var s = new Set([1, 2, 3, 3, '3']);
	s; // Set {1, 2, 3, "3"}

	//Set, add
	s.add(4);
	s; // Set {1, 2, 3, 4}
	s.add(4);
	s; // 仍然是 Set {1, 2, 3, 4}

	//Set, delete
	var s = new Set([1, 2, 3]);
	s; // Set {1, 2, 3}
	s.delete(3);
	s; // Set {1, 2}
```

## iterable
为了统一集合类型，ES6标准引入了新的iterable类型，Array、Map和Set都属于iterable类型。

具有iterable类型的集合可以通过新的for ... of循环来遍历。

```javascript

	//iterable, for...of
	var a = ['A', 'B', 'C'];
	var s = new Set(['A', 'B', 'C']);
	var m = new Map([[1, 'x'], [2, 'y'], [3, 'z']]);
	for (var x of a) { // 遍历Array
	    console.log(x);
	}
	for (var x of s) { // 遍历Set
	    console.log(x);
	}
	for (var x of m) { // 遍历Map
	    console.log(x[0] + '=' + x[1]);
	}

```

for ... in循环由于历史遗留问题，它遍历的实际上是对象的属性名称。一个Array数组实际上也是一个对象，它的每个元素的索引被视为一个属性。当我们手动给Array对象添加了额外的属性后，for ... in循环将带来意想不到的意外效果

```javascript

	//for...in
	var a = ['A', 'B', 'C'];
	a.name = 'Hello';
	for (var x in a) {
	    console.log(x); // '0', '1', '2', 'name'
	}

	//for...of
	var a = ['A', 'B', 'C'];
	a.name = 'Hello';
	for (var x of a) {
	    console.log(x); // 'A', 'B', 'C'
	}
```

更好的方式是直接使用iterable内置的forEach方法，它接收一个函数，每次迭代就自动回调该函数.

Set与Array类似，但Set没有索引，因此回调函数的前两个参数都是元素本身

Map的回调函数参数依次为value、key和map本身


```javascript

	//forEach...array
	var a = ['A', 'B', 'C'];
	a.forEach(function (element, index, array) {
	    // element: 指向当前元素的值
	    // index: 指向当前索引
	    // array: 指向Array对象本身
	    console.log(element + ', index = ' + index);
	});

	//forEach...set
	var s = new Set(['A', 'B', 'C']);
	s.forEach(function (element, sameElement, set) {
	    console.log(element);
	});

	//forEach..map
	var m = new Map([[1, 'x'], [2, 'y'], [3, 'z']]);
	m.forEach(function (value, key, map) {
	    console.log(value);
	});

```

## Function
JavaScript的函数也是一个对象，上述定义的abs()函数实际上是一个函数对象，而函数名abs可以视为指向该函数的变量.

```javascript

	//Function definition, #1
	function abs(x) {
	    if (x >= 0) {
	        return x;
	    } else {
	        return -x;
	    }
	}

	//Function definition, #2
	var abs = function (x) {
	    if (x >= 0) {
	        return x;
	    } else {
	        return -x;
	    }
	};

	//Checking argument, throw
	function abs(x) {
	    if (typeof x !== 'number') {
	        throw 'Not a number';
	    }
	    if (x >= 0) {
	        return x;
	    } else {
	        return -x;
	    }
	}
```

## Function ... arguments

键字arguments，它只在函数内部起作用，并且永远指向当前函数的调用者传入的所有参数。arguments类似Array但它不是一个Array.

利用arguments，你可以获得调用者传入的所有参数。也就是说，即使函数不定义任何参数，还是可以拿到参数的值

实际上arguments最常用于判断传入参数的个数。

```javascript

	//arguments
	function foo(x) {
	    console.log('x = ' + x); // 10
	    for (var i=0; i<arguments.length; i++) {
	        console.log('arg ' + i + ' = ' + arguments[i]); // 10, 20, 30
	    }
	}
	foo(10, 20, 30);

	//arguments checking
	function abs() {
	    if (arguments.length === 0) {
	        return 0;
	    }
	    var x = arguments[0];
	    return x >= 0 ? x : -x;
	}

	abs(); // 0
	abs(10); // 10
	abs(-9); // 9

	//arguments checking, ignore
	// foo(a[, b], c)
	// 接收2~3个参数，b是可选参数，如果只传2个参数，b默认为null：
	function foo(a, b, c) {
	    if (arguments.length === 2) {
	        // 实际拿到的参数是a和b，c为undefined
	        c = b; // 把b赋给c
	        b = null; // b变为默认值
	    }
	    // ...
	}
```

## Function ... reset
ES6标准引入了rest参数

rest参数只能写在最后，前面用...标识，从运行结果可知，传入的参数先绑定a、b，多余的参数以数组形式交给变量rest，所以，不再需要arguments我们就获取了全部参数

```javascript

	//Before ES6
	function foo(a, b) {
	    var i, rest = [];
	    if (arguments.length > 2) {
	        for (i = 2; i<arguments.length; i++) {
	            rest.push(arguments[i]);
	        }
	    }
	    console.log('a = ' + a);
	    console.log('b = ' + b);
	    console.log(rest);
	}

	//After ES6
	function foo(a, b, ...rest) {
	    console.log('a = ' + a);
	    console.log('b = ' + b);
	    console.log(rest);
	}

	foo(1, 2, 3, 4, 5);
	// 结果:
	// a = 1
	// b = 2
	// Array [ 3, 4, 5 ]

	foo(1);
	// 结果:
	// a = 1
	// b = undefined
	// Array []
```

## Variable Scope

如果一个变量在函数体内部申明，则该变量的作用域为整个函数体，在函数体外不可引用该变量

```javascript

	//No variable reference outside function
	function foo() {
	    var x = 1;
	    x = x + 1;
	}

	x = x + 2; // ReferenceError! 无法在函数体外引用变量x
```

由于JavaScript的函数可以嵌套，此时，内部函数可以访问外部函数定义的变量，反过来则不行

```javascript

	function foo() {
	    var x = 1;
	    function bar() {
	        var y = x + 1; // bar可以访问foo的变量x!
	    }

	    var z = y + 1; // ReferenceError! foo不可以访问bar的变量y!
	}
```

JavaScript的函数在查找变量时从自身函数定义开始，从“内”向“外”查找。如果内部函数定义了与外部函数重名的变量，则内部函数的变量将“屏蔽”外部函数的变量。

```javascript

function foo() {
    var x = 1;
    function bar() {
        var x = 'A';
        console.log('x in bar() = ' + x); // 'A'
    }
    console.log('x in foo() = ' + x); // 1
    bar();
}

foo();
```

JavaScript的函数定义有个特点，它会先扫描整个函数体的语句，把所有申明的变量“提升”到函数顶部.

```javascript

function foo() {
    var x = 'Hello, ' + y;
    console.log(x);
    var y = 'Bob';
}

foo();

```
语句var x = 'Hello, ' + y;并不报错，原因是变量y在稍后申明了。但是console.log显示Hello, undefined，说明变量y的值为undefined。这正是因为JavaScript引擎自动提升了变量y的声明，但不会提升变量y的赋值。

## Global Scope 全局作用域
不在任何函数内定义的变量就具有全局作用域。实际上，JavaScript默认有一个全局对象window，全局作用域的变量实际上被绑定到window的一个属性.

因此，直接访问全局变量course和访问window.course是完全一样的。

你可能猜到了，由于函数定义有两种方式，以变量方式var foo = function () {}定义的函数实际上也是一个全局变量，因此，顶层函数的定义也被视为一个全局变量，并绑定到window对象

我们每次直接调用的alert()函数其实也是window的一个变量

```javascript

	//window property as definition
	var course = 'Learn JavaScript';
	alert(course); // 'Learn JavaScript';
	alert(window.course); // 'Learn JavaScript';

	//window function as definition
	function foo() {
	    alert('foo');
	}
	foo(); // 直接调用foo()
	window.foo(); // 通过window.foo()调用

	//disable alert() window property
	window.alert('调用window.alert()');
	// 把alert保存到另一个变量:
	var old_alert = window.alert;
	// 给alert赋一个新函数:
	window.alert = function () {}
	alert('无法用alert()显示了!');

```

## Naming Space
全局变量会绑定到window上，不同的JavaScript文件如果使用了相同的全局变量，或者定义了相同名字的顶层函数，都会造成命名冲突，并且很难被发现。 减少冲突的一个方法是把自己的所有变量和函数全部绑定到一个全局变量中。

```javascript

	var MYAPP = {};

	// 其他变量:
	MYAPP.name = 'myapp';
	MYAPP.version = 1.0;

	// 其他函数:
	MYAPP.foo = function () {
	    return 'foo';
	};

```

## Destructing Assignment 解构赋值

从ES6开始，JavaScript引入了解构赋值，可以同时对一组变量进行赋值。

```javascript

	//Before ES6
	var array = ['hello', 'JavaScript', 'ES6'];
	var x = array[0];
	var y = array[1];
	var z = array[2];

	//After ES6
	var [x, y, z] = ['hello', 'JavaScript', 'ES6'];
	// x, y, z分别被赋值为数组对应元素:
	console.log('x = ' + x + ', y = ' + y + ', z = ' + z);

```

对数组元素进行解构赋值时，多个变量要用[...]括起来。 解构赋值还可以忽略某些元素.
```javascript
	
	//Assign array
	let [x, [y, z]] = ['hello', ['JavaScript', 'ES6']];
	x; // 'hello'
	y; // 'JavaScript'
	z; // 'ES6'

	//Assign array, ignore x y
	let [, , z] = ['hello', 'JavaScript', 'ES6']; // 忽略前两个元素，只对z赋值第三个元素
	z; // 'ES6'
```

如果需要从一个对象中取出若干属性，也可以使用解构赋值，便于快速获取对象的指定属性.
对一个对象进行解构赋值时，同样可以直接对嵌套的对象属性进行赋值，只要保证对应的层次是一致的.
如果要使用的变量名和属性名不一致，可以用: assign old & new property name
解构赋值还可以使用默认值，这样就避免了不存在的属性返回undefined的问题
```javascript
	
	//Assign object
	var person = {
	    name: '小明',
	    age: 20,
	    gender: 'male',
	    passport: 'G-12345678',
	    school: 'No.4 middle school'
	};
	var {name, age, passport} = person;
	console.log('name = ' + name + ', age = ' + age + ', passport = ' + passport);

	//Assign object, nested
	var person = {
	    name: '小明',
	    age: 20,
	    gender: 'male',
	    passport: 'G-12345678',
	    school: 'No.4 middle school',
	    address: {
	        city: 'Beijing',
	        street: 'No.1 Road',
	        zipcode: '100001'
	    }
	};
	var {name, address: {city, zip}} = person;
	name; // '小明'
	city; // 'Beijing'
	zip; // undefined, 因为属性名是zipcode而不是zip
	// 注意: address不是变量，而是为了让city和zip获得嵌套的address对象的属性:
	address; // Uncaught ReferenceError: address is not defined

	//Assign object, rename properties
	var person = {
	    name: '小明',
	    age: 20,
	    gender: 'male',
	    passport: 'G-12345678',
	    school: 'No.4 middle school'
	};

	// 把passport属性赋值给变量id:
	let {name, passport:id} = person;
	name; // '小明'
	id; // 'G-12345678'
	// 注意: passport不是变量，而是为了让变量id获得passport属性:
	passport; // Uncaught ReferenceError: passport is not defined

	//Assign object, default value
	var person = {
	    name: '小明',
	    age: 20,
	    gender: 'male',
	    passport: 'G-12345678'
	};

	// 如果person对象没有single属性，默认赋值为true:
	var {name, single=true} = person;
	name; // '小明'
	single; // true
```

解构赋值在很多时候可以大大简化代码。例如，交换两个变量x和y的值，可以这么写，不再需要临时变量
```javascript
	//Exchange X Y
	var x=1, y=2;
	[x, y] = [y, x]
```

## Method

Bind a function with object
```javascript

	var xiaoming = {
	    name: '小明',
	    birth: 1990,
	    age: function () {
	        var y = new Date().getFullYear();
	        return y - this.birth;
	    }
	};

	xiaoming.age; // function xiaoming.age()
	xiaoming.age(); // 今年调用是25,明年调用就变成26了

```

'this'是一个特殊变量，它始终指向当前对象.

如果以对象的方法形式调用，比如xiaoming.age()，该函数的this指向被调用的对象，也就是xiaoming，这是符合我们预期的。

如果单独调用函数，比如getAge()，此时，该函数的this指向全局对象，也就是window。

ECMA决定，在strict模式下让函数的this指向undefined

```javascript
	
	//this, point to window, window no birth property
	function getAge() {
	    var y = new Date().getFullYear();
	    return y - this.birth;
	}

	var xiaoming = {
	    name: '小明',
	    birth: 1990,
	    age: getAge
	};

	xiaoming.age(); // 25, 正常结果
	getAge(); // NaN
```

```javascript
	
	//this, point to age, age is a function, no birth property
	var xiaoming = {
	    name: '小明',
	    birth: 1990,
	    age: function () {
	        function getAgeFromBirth() {
	            var y = new Date().getFullYear();
	            return y - this.birth;
	        }
	        return getAgeFromBirth();
	    }
	};

	xiaoming.age(); // Uncaught TypeError: Cannot read property 'birth' of undefined
```

```javascript

	//that points to this, this is xiaoming, worked
	var xiaoming = {
	    name: '小明',
	    birth: 1990,
	    age: function () {
	        var that = this; // 在方法内部一开始就捕获this
	        function getAgeFromBirth() {
	            var y = new Date().getFullYear();
	            return y - that.birth; // 用that而不是this
	        }
	        return getAgeFromBirth();
	    }
	};

	xiaoming.age(); // 25
```

## apply() & call(), control 'this' point to
apply()方法，它接收两个参数，第一个参数就是需要绑定的this变量，第二个参数是Array，表示函数本身的参数

call()方法，它接收两个参数，第一个参数就是需要绑定的this变量，第二个参数是把参数按顺序传入

对普通函数调用，我们通常把this绑定为null

```javascript

	//apply
	function getAge() {
	    var y = new Date().getFullYear();
	    return y - this.birth;
	}

	var xiaoming = {
	    name: '小明',
	    birth: 1990,
	    age: getAge
	};

	xiaoming.age(); // 25
	getAge.apply(xiaoming, []); // 25, this指向xiaoming, 参数为空

	//call vs. apply
	Math.max.apply(null, [3, 5, 4]); // 5
	Math.max.call(null, 3, 5, 4); // 5
```

```javascript

	//dynamically decrocate window function
	var count = 0;
	var oldParseInt = parseInt; // 保存原函数

	window.parseInt = function () {
	    count += 1;
	    return oldParseInt.apply(null, arguments); // 调用原函数
	};

	parseInt('10');
	parseInt('20');
	parseInt('30');
	console.log('count = ' + count); // 3
```

## Higher-order function
JavaScript的函数其实都指向某个变量。既然变量可以指向函数，函数的参数能接收变量，那么一个函数就可以接收另一个函数作为参数，这种函数就称之为高阶函数。

```javascript

	function add(x, y, f) {
	    return f(x) + f(y);
	}
	var x = add(-5, 6, Math.abs); // 11
	console.log(x);

```

## map
map()方法定义在JavaScript的Array中，我们调用Array的map()方法，传入我们自己的函数，就得到了一个新的Array作为结果.

[x1, x2, x3, x4].map(f) = [f(x1), f(x2), f(x3), f(x4)]

```javascript

	function pow(x) {
	    return x * x;
	}
	var arr = [1, 2, 3, 4, 5, 6, 7, 8, 9];
	var results = arr.map(pow); // [1, 4, 9, 16, 25, 36, 49, 64, 81]
	console.log(results);

	//convert string
	var arr = [1, 2, 3, 4, 5, 6, 7, 8, 9];
	arr.map(String); // ['1', '2', '3', '4', '5', '6', '7', '8', '9']
```

## reduce
rray的reduce()把一个函数作用在这个Array的[x1, x2, x3...]上，这个函数必须接收两个参数，reduce()把结果继续和序列的下一个元素做累积计算.

[x1, x2, x3, x4].reduce(f) = f(f(f(x1, x2), x3), x4)

```javascript

	//sum of array
	var arr = [1, 3, 5, 7, 9];
	arr.reduce(function (x, y) {
	    return x + y;
	}); // 25

	//把[1, 3, 5, 7, 9]变换成整数13579
	var arr = [1, 3, 5, 7, 9];
	arr.reduce(function (x, y) {
	    return x * 10 + y;
	}); // 13579
```

## filter
filter也用于把Array的某些元素过滤掉，然后返回剩下的元素 (elements whose filter function return true)

```javascript

	//filter out even number
	var arr = [1, 2, 4, 5, 6, 9, 10, 15];
	var r = arr.filter(function (x) {
	    return x % 2 !== 0;
	});
	r; // [1, 5, 9, 15]

	//filter out null / blank
	var arr = ['A', '', 'B', null, undefined, 'C', '  '];
	var r = arr.filter(function (s) {
	    return s && s.trim(); // 注意：IE9以下的版本没有trim()方法
	});
	r; // ['A', 'B', 'C']

```

filter()接收的回调函数，其实可以有多个参数。通常我们仅使用第一个参数，表示Array的某个元素。回调函数还可以接收另外两个参数，表示元素的位置和数组本身.

```javascript

	var arr = ['A', 'B', 'C'];
	var r = arr.filter(function (element, index, self) {
	    console.log(element); // 依次打印'A', 'B', 'C'
	    console.log(index); // 依次打印0, 1, 2
	    console.log(self); // self就是变量arr
	    return true;
	});

```

## sort
Array的sort()方法就是用于排序的. Array的sort()方法默认把所有元素先转换为String再排序.

sort()方法会直接对Array进行修改，它返回的结果仍是当前Array

```javascript

	//sort number
	var arr = [10, 20, 1, 2];
	arr.sort(function (x, y) {
	    if (x < y) {
	        return -1;
	    }
	    if (x > y) {
	        return 1;
	    }
	    return 0;
	});
	console.log(arr); // [1, 2, 10, 20]

	//sort by alphabet, ignore case
	var arr = ['Google', 'apple', 'Microsoft'];
	arr.sort(function (s1, s2) {
	    x1 = s1.toUpperCase();
	    x2 = s2.toUpperCase();
	    if (x1 < x2) {
	        return -1;
	    }
	    if (x1 > x2) {
	        return 1;
	    }
	    return 0;
	}); // ['apple', 'Google', 'Microsoft']

	//same array after sort
	var a1 = ['B', 'A', 'C'];
	var a2 = a1.sort();
	a1; // ['A', 'B', 'C']
	a2; // ['A', 'B', 'C']
	a1 === a2; // true, a1和a2是同一对象

```

## 闭包（Closure）

闭包就是携带状态的函数，并且它的状态可以完全对外隐藏起来. 闭包还可以把多参数的函数变成单参数的函数.

闭包每次调用都会返回一个新的函数，即使传入相同的参数

返回闭包时牢记的一点就是：返回函数不要引用任何循环变量，或者后续会发生变化的变量

如果一定要引用循环变量怎么办？方法是再创建一个函数，用该函数的参数绑定循环变量当前的值，无论该循环变量后续如何更改，已绑定到函数参数的值不变

```javascript

	// return function, execute when function called
	function lazy_sum(arr) {
	    var sum = function () {
	        return arr.reduce(function (x, y) {
	            return x + y;
	        });
	    }
	    return sum;
	}
	var f = lazy_sum([1, 2, 3, 4, 5]);
	console.log(f());

	// return new function everytime, even same parameter
	var f1 = lazy_sum([1, 2, 3, 4, 5]);
	var f2 = lazy_sum([1, 2, 3, 4, 5]);
	f1 === f2; // false
```

```javascript

	// return array, array contains 3 functions, each function call depends on i, when called, get value of i and output
	function count() {
	    var arr = [];
	    for (var i=1; i<=3; i++) {
	        arr.push(function () {
	            return i * i;
	        });
	    }
	    return arr;
	}
	var results = count();
	var f1 = results[0];
	var f2 = results[1];
	var f3 = results[2];
	f1();
	f2();
	f3();

	//anomynous function, execute on flight
	function count() {
	    var arr = [];
	    for (var i=1; i<=3; i++) {
	        arr.push((function (n) {
	            return function () {
	                return n * n;
	            }
	        })(i));
	    }
	    return arr;
	}

	var results = count();
	var f1 = results[0];
	var f2 = results[1];
	var f3 = results[2];

	f1(); // 1
	f2(); // 4
	f3(); // 9
```

创建一个匿名函数并立刻执行
```javascript

	(function (x) {
	    return x * x;
	})(3); // 9

```

```javascript

	//rely on x reference, create counter
	function create_counter(initial) {
	    var x = initial || 0;
	    return {
	        inc: function () {
	            x += 1;
	            return x;
	        }
	    }
	}

	var c1 = create_counter();
	c1.inc(); // 1
	c1.inc(); // 2
	c1.inc(); // 3

	var c2 = create_counter(10);
	c2.inc(); // 11
	c2.inc(); // 12
	c2.inc(); // 13
```

```javascript

	function make_pow(n) {
	    return function (x) {
	        return Math.pow(x, n);
	    }
	}

	var pow2 = make_pow(2);
	var pow3 = make_pow(3);

	console.log(pow2(5)); // 25
	console.log(pow3(7)); // 343

```

## Arrow Function

ES6标准新增了一种新的函数：Arrow Function（箭头函数): Input parameter points to output function.

箭头函数相当于匿名函数，并且简化了函数定义。箭头函数有两种格式，一种像上面的，只包含一个表达式，连{ ... }和return都省略掉了。还有一种可以包含多条语句，这时候就不能省略{ ... }和return

如果参数不是一个，就需要用括号()括起来

```javascript

	//Simple
	x => x * x

	// with return
	x => {
	    if (x > 0) {
	        return x * x;
	    }
	    else {
	        return - x * x;
	    }
	}

	// 两个参数:
	(x, y) => x * x + y * y

	// 无参数:
	() => 3.14

	// 可变参数:
	(x, y, ...rest) => {
	    var i, sum = x + y;
	    for (i=0; i<rest.length; i++) {
	        sum += rest[i];
	    }
	    return sum;
	}

	// return object
	x => ({ foo: x })
```

箭头函数看上去是匿名函数的一种简写，但实际上，箭头函数和匿名函数有个明显的区别：箭头函数内部的this是词法作用域，由上下文确定。箭头函数完全修复了this的指向，this总是指向词法作用域，也就是外层调用者obj.
```javascript

	var obj = {
	    birth: 1990,
	    getAge: function () {
	        var b = this.birth; // 1990
	        var fn = () => new Date().getFullYear() - this.birth; // this指向obj对象
	        return fn();
	    }
	};
	obj.getAge(); 

```

由于this在箭头函数中已经按照词法作用域绑定了，所以，用call()或者apply()调用箭头函数时，无法对this进行绑定，即传入的第一个参数被忽略
```javascript

	var obj = {
	    birth: 1990,
	    getAge: function (year) {
	        var b = this.birth; // 1990
	        var fn = (y) => y - this.birth; // this.birth仍是1990
	        return fn.call({birth:2000}, year);
	    }
	};
	obj.getAge(2015); // 25

```

## generator
generator（生成器）是ES6标准引入的新的数据类型。一个generator看上去像一个函数，但可以返回多次。
```javascript

	//no yield
	function foo(x) {
	    return x + x;
	}
	var r = foo(1); // 调用foo函数


	//with yield
	function* foo(x) {
	    yield x + 1;
	    yield x + 2;
	    return x + 3;
	}
	var ff = foo(3);
	ff.next();
```

直接调用一个generator和调用函数不一样，fib(5)仅仅是创建了一个generator对象，还没有去执行它。

next()方法会执行generator的代码，然后，每次遇到yield x;就返回一个对象{value: x, done: true/false}，然后“暂停”。返回的value就是yield的返回值，done表示这个generator是否已经执行结束了。如果done为true，则value就是return的返回值。

```javascript

	//no yield
	function fib(max) {
	    var
	        t,
	        a = 0,
	        b = 1,
	        arr = [0, 1];
	    while (arr.length < max) {
	        [a, b] = [b, a + b];
	        arr.push(b);
	    }
	    return arr;
	}
	console.log(fib(8));

	//with yield - while
	function* fib(max) {
	    var
	        t,
	        a = 0,
	        b = 1,
	        n = 0;
	    while (n < max) {
	        yield a;
	        [a, b] = [b, a + b];
	        n ++;
	    }
	    return;
	}
	var ff = fib(8);
	ff.next();

	//output using for of
	for (var x of fib(10)) {
	    console.log(x); // 依次输出0, 1, 1, 2, 3, ...
	}
```

## Standard Object

在JavaScript的世界里，一切都是对象。
```javascript

	typeof 123; // 'number'
	typeof NaN; // 'number'
	typeof 'str'; // 'string'
	typeof true; // 'boolean'
	typeof undefined; // 'undefined'
	typeof Math.abs; // 'function'
	typeof null; // 'object'
	typeof []; // 'object'
	typeof {}; // 'object'

```
可见，number、string、boolean、function和undefined有别于其他类型
特别注意null的类型是object，Array的类型也是object，如果我们用typeof将无法区分出null、Array和通常意义上的object

包装对象, number、boolean和string都有包装对象
```javascript

	var n = new Number(123); // 123,生成了新的包装类型
	var b = new Boolean(true); // true,生成了新的包装类型
	var s = new String('str'); // 'str',生成了新的包装类型

	typeof new Number(123); // 'object'
	new Number(123) === 123; // false

	typeof new Boolean(true); // 'object'
	new Boolean(true) === true; // false

	typeof new String('str'); // 'object'
	new String('str') === 'str'; // false
```

Number()、Boolean和String()被当做普通函数，把任何类型的数据转换为number、boolean和string类型
```javascript

	var n = Number('123'); // 123，相当于parseInt()或parseFloat()
	typeof n; // 'number'

	var b = Boolean('true'); // true
	typeof b; // 'boolean'

	var b2 = Boolean('false'); // true! 'false'字符串转换结果为true！因为它是非空字符串！
	var b3 = Boolean(''); // false

	var s = String(123.45); // '123.45'
	typeof s; // 'string'
```

有这么几条规则需要遵守：
1.不要使用new Number()、new Boolean()、new String()创建包装对象；
2.用parseInt()或parseFloat()来转换任意类型到number；
3.用String()来转换任意类型到string，或者直接调用某个对象的toString()方法；
4.通常不必把任意类型转换为boolean再判断，因为可以直接写if (myVar) {...}；
5.typeof操作符可以判断出number、boolean、string、function和undefined；
6.判断Array要使用Array.isArray(arr)；
7.判断null请使用myVar === null；
8.判断某个全局变量是否存在用typeof window.myVar === 'undefined'；
9.函数内部判断某个变量是否存在用typeof myVar === 'undefined'。

## Date
在JavaScript中，Date对象用来表示日期和时间。 

JavaScript的月份范围用整数表示是0~11，0表示一月，1表示二月……，所以要表示6月，我们传入的是5.
```javascript

	var now = new Date();
	now; // Wed Jun 24 2015 19:49:22 GMT+0800 (CST)
	now.getFullYear(); // 2015, 年份
	now.getMonth(); // 5, 月份，注意月份范围是0~11，5表示六月
	now.getDate(); // 24, 表示24号
	now.getDay(); // 3, 表示星期三
	now.getHours(); // 19, 24小时制
	now.getMinutes(); // 49, 分钟
	now.getSeconds(); // 22, 秒
	now.getMilliseconds(); // 875, 毫秒数
	now.getTime(); // 1435146562875, 以number形式表示的时间戳

	//create specified date
	var d = new Date(2015, 5, 19, 20, 15, 30, 123);
	d; // Fri Jun 19 2015 20:15:30 GMT+0800 (CST)
```

## Json
SON还定死了字符集必须是UTF-8，表示多语言就没有问题了。
为了统一解析，JSON的字符串规定必须用双引号""，Object的键也必须用双引号""。
```javascript
	var xiaoming = {
	    name: '小明',
	    age: 14,
	    gender: true,
	    height: 1.65,
	    grade: null,
	    'middle-school': '\"W3C\" Middle School',
	    skills: ['JavaScript', 'Java', 'Python', 'Lisp']
	};
	var s = JSON.stringify(xiaoming);
	console.log(s);
	JSON.stringify(xiaoming, null, '  ');
```

## Object Oriented Programing
JavaScript不区分类和实例的概念，而是通过原型（prototype）来实现面向对象编程。

JavaScript的原型链和Java的Class区别就在，它没有“Class”的概念，所有对象都是实例，所谓继承关系不过是把一个对象的原型指向另一个对象而已。
```javascript

	var Student = {
	    name: 'Robot',
	    height: 1.2,
	    run: function () {
	        console.log(this.name + ' is running...');
	    }
	};

	var xiaoming = {
	    name: '小明'
	};

	xiaoming.__proto__ = Student;

	xiaoming.name; // '小明'
	xiaoming.run(); // 小明 is running...

```

在编写JavaScript代码时，不要直接用obj.__proto__去改变一个对象的原型，并且，低版本的IE也无法使用__proto__。
Object.create()方法可以传入一个原型对象，并创建一个基于该原型的新对象，但是新对象什么属性都没有，因此，我们可以编写一个函数来创建xiaoming
```javascript

	// 原型对象:
	var Student = {
	    name: 'Robot',
	    height: 1.2,
	    run: function () {
	        console.log(this.name + ' is running...');
	    }
	};

	function createStudent(name) {
	    // 基于Student原型创建一个新对象:
	    var s = Object.create(Student);
	    // 初始化新对象:
	    s.name = name;
	    return s;
	}

	var xiaoming = createStudent('小明');
	xiaoming.run(); // 小明 is running...
	xiaoming.__proto__ === Student; // true

```

JavaScript对每个创建的对象都会设置一个原型，指向它的原型对象。

当我们用obj.xxx访问一个对象的属性时，JavaScript引擎先在当前对象上查找该属性，如果没有找到，就到其原型对象上找，如果还没有找到，就一直上溯到Object.prototype对象，最后，如果还没有找到，就只能返回undefined。

Array.prototype定义了indexOf()、shift()等方法，因此你可以在所有的Array对象上直接调用这些方法。

var arr = [1, 2, 3]; 其原型链是：arr ----> Array.prototype ----> Object.prototype ----> null

函数也是一个对象，它的原型链是：foo ----> Function.prototype ----> Object.prototype ----> null

由于Function.prototype定义了apply()等方法，因此，所有函数都可以调用apply()方法。

很容易想到，如果原型链很长，那么访问一个对象的属性就会因为花更多的时间查找而变得更慢，因此要注意不要把原型链搞得太长。

## 构造函数
除了直接用{ ... }创建一个对象外，JavaScript还可以用一种构造函数的方法来创建对象。它的用法是，先定义一个构造函数.

然后用关键字new来调用这个函数，并返回一个对象

如果不写new，这就是一个普通函数，它返回undefined。但是，如果写了new，它就变成了一个构造函数，它绑定的this指向新创建的对象，并默认返回this，也就是说，不需要在最后写return this;。

新创建的xiaoming的原型链是：

xiaoming ----> Student.prototype ----> Object.prototype ----> null

xiaoming ↘
xiaohong -→ Student.prototype ----> Object.prototype ----> null
xiaojun  ↗

xiaoming.name; // '小明'
xiaohong.name; // '小红'
xiaoming.hello; // function: Student.hello()
xiaohong.hello; // function: Student.hello()
xiaoming.hello === xiaohong.hello; // false， function different

## 原型继承 Before ES6
JavaScript的原型继承实现方式就是：
1.定义新的构造函数，并在内部用call()调用希望“继承”的构造函数，并绑定this；
2.借助中间函数F实现原型链继承，最好通过封装的inherits函数完成；
3.继续在新的构造函数的原型上定义新方法。
```javascript

	//原型链:new PrimaryStudent() ----> PrimaryStudent.prototype ----> Object.prototype ----> null
	function Student(props) {
	    this.name = props.name || 'Unnamed';
	}

	Student.prototype.hello = function () {
	    alert('Hello, ' + this.name + '!');
	}

	function PrimaryStudent(props) {
	    // 调用Student构造函数，绑定this变量:
	    Student.call(this, props);
	    this.grade = props.grade || 1;
	}

```

## Class继承 After ES6
关键字class从ES6开始正式被引入到JavaScript中。class的目的就是让定义类更简单。

```javascript
	
	//class student
	class Student {
	    constructor(name) {
	        this.name = name;
	    }

	    hello() {
	        alert('Hello, ' + this.name + '!');
	    }
	}

	//initialize Student
	var xiaoming = new Student('小明');
	xiaoming.hello();

	//extend Student
	class PrimaryStudent extends Student {
	    constructor(name, grade) {
	        super(name); // 记得用super调用父类的构造方法!
	        this.grade = grade;
	    }

	    myGrade() {
	        alert('I am at grade ' + this.grade);
	    }
	}
```
class的定义包含了构造函数constructor和定义在原型对象上的函数hello()（注意没有function关键字），这样就避免了Student.prototype.hello = function () {...}这样分散的代码。

PrimaryStudent的定义也是class关键字实现的，而extends则表示原型链对象来自Student。子类的构造函数可能会与父类不太相同，例如，PrimaryStudent需要name和grade两个参数，并且需要通过super(name)来调用父类的构造函数，否则父类的name属性无法正常初始化。

PrimaryStudent已经自动获得了父类Student的hello方法，我们又在子类中定义了新的myGrade方法。

## 安全限制 -> 浏览器的同源策略
默认情况下，JavaScript在发送AJAX请求时，URL的域名必须和当前页面完全一致。

完全一致的意思是，域名要相同（www.example.com和example.com不同），协议要相同（http和https不同），端口号要相同（默认是:80端口，它和:8080就不同）。有的浏览器口子松一点，允许端口不同，大多数浏览器都会严格遵守这个限制。

JSONP，它有个限制，只能用GET请求，并且要求返回JavaScript。这种方式跨域实际上是利用了浏览器允许跨域引用JavaScript资源：

如果浏览器支持HTML5，那么就可以一劳永逸地使用新的跨域策略：CORS了。 CORS全称Cross-Origin Resource Sharing，是HTML5规范定义的如何跨域访问资源。

## CORS
Origin表示本域，也就是浏览器当前页面的域。当JavaScript向外域（如sina.com）发起请求后，浏览器收到响应后，首先检查Access-Control-Allow-Origin是否包含本域，如果是，则此次跨域请求成功，如果不是，则请求失败，JavaScript将无法获取到响应的任何数据。

假设本域是my.com，外域是sina.com，只要响应头Access-Control-Allow-Origin为http://my.com，或者是*，本次请求就可以成功。 可见，跨域能否成功，取决于对方服务器是否愿意给你设置一个正确的Access-Control-Allow-Origin，决定权始终在对方手中。

对于PUT、DELETE以及其他类型如application/json的POST请求，在发送AJAX请求之前，浏览器会先发送一个OPTIONS请求（称为preflighted请求）到这个URL上，询问目标服务器是否接受：
	OPTIONS /path/to/resource HTTP/1.1
	Host: bar.com
	Origin: http://my.com
	Access-Control-Request-Method: POST
服务器必须响应并明确指出允许的Method：
	HTTP/1.1 200 OK
	Access-Control-Allow-Origin: http://my.com
	Access-Control-Allow-Methods: POST, GET, PUT, OPTIONS
	Access-Control-Max-Age: 86400

浏览器确认服务器响应的Access-Control-Allow-Methods头确实包含将要发送的AJAX请求的Method，才会继续发送AJAX，否则，抛出一个错误。

由于以POST、PUT方式传送JSON格式的数据在REST中很常见，所以要跨域正确处理POST和PUT请求，服务器端必须正确响应OPTIONS请求。

## Promise ES6
在JavaScript的世界中，所有代码都是单线程执行的. 由于这个“缺陷”，导致JavaScript的所有网络操作，浏览器事件，都必须是异步执行。异步执行可以用回调函数实现.

Promise有各种开源实现，在ES6中被统一规范，由浏览器直接支持。

Promise最大的好处是在异步执行的流程中，把执行代码和处理结果的代码清晰地分离了
```javascript

function test(resolve, reject) {
    var timeOut = Math.random() * 2;
    console.log('set timeout to: ' + timeOut + ' seconds.');
    setTimeout(function () {
        if (timeOut < 1) {
            console.log('call resolve()...');
            resolve('200 OK');
        }
        else {
            console.log('call reject()...');
            reject('timeout in ' + timeOut + ' seconds.');
        }
    }, timeOut * 1000);
}

new Promise(test).then(function (result) {
    console.log('成功：' + result);
}).catch(function (reason) {
    console.log('失败：' + reason); 
});

```

Promise function always have resolve and reject. 
resolve->then (function(){...})
reject->catch (function(){...})

有若干个异步任务，需要先做任务1，如果成功后再做任务2，任何任务失败则不再继续并执行错误处理函数。要串行执行这样的异步任务，不用Promise需要写一层一层的嵌套代码。有了Promise，我们只需要简单地写: job1.then(job2).then(job3).catch(handleError);
```javascript
	
	// 0.5秒后返回input*input的计算结果:
	function multiply(input) {
	    return new Promise(function (resolve, reject) {
	        console.log('calculating ' + input + ' x ' + input + '...');
	        setTimeout(resolve, 500, input * input);
	    });
	}

	// 0.5秒后返回input+input的计算结果:
	function add(input) {
	    return new Promise(function (resolve, reject) {
	        console.log('calculating ' + input + ' + ' + input + '...');
	        setTimeout(resolve, 500, input + input);
	    });
	}

	var p = new Promise(function (resolve, reject) {
	    console.log('start new Promise...');
	    resolve(123);
	});

	p.then(multiply)
	 .then(add)
	 .then(multiply)
	 .then(add)
	 .then(function (result) {
	    console.log('Got value: ' + result);
	});

```

除了串行执行若干异步任务外，Promise还可以并行执行异步任务。
```javascript

	var p1 = new Promise(function (resolve, reject) {
	    setTimeout(resolve, 500, 'P1');
	});
	var p2 = new Promise(function (resolve, reject) {
	    setTimeout(resolve, 600, 'P2');
	});
	// 同时执行p1和p2，并在它们都完成后执行then:
	Promise.all([p1, p2]).then(function (results) {
	    console.log(results); // 获得一个Array: ['P1', 'P2']
	});

```

有些时候，多个异步任务是为了容错。比如，同时向两个URL读取用户的个人信息，只需要获得先返回的结果即可。
```javascript

	var p1 = new Promise(function (resolve, reject) {
	    setTimeout(resolve, 500, 'P1');
	});
	var p2 = new Promise(function (resolve, reject) {
	    setTimeout(resolve, 600, 'P2');
	});
	Promise.race([p1, p2]).then(function (result) {
	    console.log(result); // 'P1'
	});

```

## try ... catch ... finally
```javascript

	var r1, r2, s = null;
	try {
	    r1 = s.length; // 此处应产生错误
	    r2 = 100; // 该语句不会执行
	} catch (e) {
	    console.log('出错了：' + e);
	} finally {
	    console.log('finally');
	}
	console.log('r1 = ' + r1); // r1应为undefined
	console.log('r2 = ' + r2); // r2应为undefined

```

JavaScript有一个标准的Error对象表示错误，还有从Error派生的TypeError、ReferenceError等错误对象。我们在处理错误时，可以通过catch(e)捕获的变量e访问错误对象：
```javascript

	try {
	    ...
	} catch (e) {
	    if (e instanceof TypeError) {
	        alert('Type error!');
	    } else if (e instanceof Error) {
	        alert(e.message);
	    } else {
	        alert('Error: ' + e);
	    }
	}

```

程序也可以主动抛出一个错误，让执行流程直接跳转到catch块。抛出错误使用throw语句。
```javascript

	var r, n, s;
	try {
	    s = prompt('请输入一个数字');
	    n = parseInt(s);
	    if (isNaN(n)) {
	        throw new Error('输入错误');
	    }
	    // 计算平方:
	    r = n * n;
	    console.log(n + ' * ' + n + ' = ' + r);
	} catch (e) {
	    console.log('出错了：' + e);
	}

```

## 第三方库->underscore
underscore提供了一套完善的函数式编程的接口，让我们更方便地在JavaScript中实现函数式编程。

underscore会把自身绑定到唯一的全局变量_上，这也是为啥它的名字叫underscore的原因。

.map(obj, function (value, key) {...});
```javascript

	//return array
	var obj = {
	    name: 'bob',
	    school: 'No.1 middle school',
	    address: 'xueyuan road'
	};

	var upper = _.map(obj, function (value, key) {
	    
	    return value.toUpperCase();
	});

	console.log(JSON.stringify(upper)); //["BOB","NO.1 MIDDLE SCHOOL","XUEYUAN ROAD"]
```

.every([], arrow function); 当集合的所有元素都满足条件时，.every()函数返回true. 当集合是Object时，我们可以同时获得value和key
```javascript

	_.every([1, 4, 7, -3, -9], (x) => x > 0);

```

.some([], arrow function); 当集合的至少一个元素满足条件时，.some()函数返回true. 当集合是Object时，我们可以同时获得value和key
```javascript

_.some([1, 4, 7, -3, -9], (x) => x > 0);

```

```javascript

	var obj = {
	    name: 'bob',
	    school: 'No.1 middle school',
	    address: 'xueyuan road'
	};

	var r1 = _.every(obj, function (value, key) {
	    return key===key.toLowerCase()&&value==value.toLowerCase();;
	});
	var r2 = _.some(obj, function (value, key) {
	    return key===key.toLowerCase()&&value==value.toLowerCase();;
	});

	console.log('every key-value are lowercase: ' + r1 + '\nsome key-value are lowercase: ' + r2);

```

.max([]);这两个函数直接返回集合中最大的数. 只作用于value，忽略掉key
.min([]);这两个函数直接返回集合中最小的数. 只作用于value，忽略掉key
```javascript

	var arr = [3, 5, 7, 9];
	_.max(arr); // 9
	_.min(arr); // 3

	// 空集合会返回-Infinity和Infinity，所以要先判断集合不为空：
	_.max([]) //-Infinity
	_.min([]) //Infinity

	_.max({ a: 1, b: 2, c: 3 }); // 3

```

.groupBy([], function(){...}); 把集合的元素按照key归类，key由传入的函数返回
```javascript
var scores = [20, 81, 75, 40, 91, 59, 77, 66, 72, 88, 99];
var groups = _.groupBy(scores, function (x) {
    if (x < 60) {
        return 'C';
    } else if (x < 80) {
        return 'B';
    } else {
        return 'A';
    }
});
// 结果:
// {
//   A: [81, 91, 88, 99],
//   B: [75, 77, 66, 72],
//   C: [20, 40, 59]
// }

```

.shuffle([]); 用洗牌算法随机打乱一个集合
.sample([], number_of_pick_up); 则是随机选择一个或多个元素
```javascript

	// 注意每次结果都不一样：
	_.shuffle([1, 2, 3, 4, 5, 6]); // [3, 5, 4, 6, 2, 1]

	// 注意每次结果都不一样：
	// 随机选1个：
	_.sample([1, 2, 3, 4, 5, 6]); // 2

	// 随机选3个：
	_.sample([1, 2, 3, 4, 5, 6], 3); // [6, 1, 4]

```

.first([]); 取第一个元素
.last([]); 取最后一个元素
```javascript

	var arr = [2, 4, 6, 8];
	_.first(arr); // 2
	_.last(arr); // 8

```

.flatten([[]]); 接收一个Array，无论这个Array里面嵌套了多少个Array，flatten()最后都把它们变成一个一维数组
```javascript

	_.flatten([1, [2], [3, [[4], [5]]]]); // [1, 2, 3, 4, 5]

```

.zip([], []); 把两个或多个数组的所有元素按索引对齐，然后按索引合并成新数组。
```javascript

	var names = ['Adam', 'Lisa', 'Bart'];
	var scores = [85, 92, 59];
	_.zip(names, scores);
	// [['Adam', 85], ['Lisa', 92], ['Bart', 59]]

```

.unzip([[]]); 则是反过来
```javascript

	var namesAndScores = [['Adam', 85], ['Lisa', 92], ['Bart', 59]];
	_.unzip(namesAndScores);
	// [['Adam', 'Lisa', 'Bart'], [85, 92, 59]]

```

.object([], []); 名字和分数直接对应成Object
```javascript

	var names = ['Adam', 'Lisa', 'Bart'];
	var scores = [85, 92, 59];
	_.object(names, scores);
	// {Adam: 85, Lisa: 92, Bart: 59}

```

.range(-start, end, -step_length)让你快速生成一个序列
```javascript

	// 从0开始小于10:
	_.range(10); // [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

	// 从1开始小于11：
	_.range(1, 11); // [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

	// 从0开始小于30，步长5:
	_.range(0, 30, 5); // [0, 5, 10, 15, 20, 25]

	// 从0开始大于-10，步长-1:
	_.range(0, -10, -1); // [0, -1, -2, -3, -4, -5, -6, -7, -8, -9]

```

.bind(obj_function, obj); 可以帮我们把s对象直接绑定在fn()的this指针上，以后调用fn()就可以直接正常调用了
```javascript

	var s = ' Hello  ';
	var fn = _.bind(s.trim, s);
	fn();
	// 输出Hello

```

.partial(function, placeholder_parameter...)就是为一个函数创建偏函数. 创建偏函数的目的是将原函数的某些参数固定住，可以降低新函数调用的难度
```javascript

	var pow2N = _.partial(Math.pow, 2);
	pow2N(3); // 8
	pow2N(5); // 32
	pow2N(10); // 1024

	var cube = _.partial(Math.pow, _, 3);
	cube(3); // 27
	cube(5); // 125
	cube(10); // 1000

```

.memoize(function); 可以自动缓存函数计算的结果
```javascript

	var factorial = _.memoize(function(n) {
	    console.log('start calculate ' + n + '!...');
	    var s = 1, i = n;
	    while (i > 1) {
	        s = s * i;
	        i --;
	    }
	    console.log(n + '! = ' + s);
	    return s;
	});

	// 第一次调用:
	factorial(10); // 3628800
	// 注意控制台输出:
	// start calculate 10!...
	// 10! = 3628800

	// 第二次调用:
	factorial(10); // 3628800
	// 控制台没有输出

```

```javascript

	var factorial = _.memoize(function(n) {
	    console.log('start calculate ' + n + '!...');
	    if (n < 2) {
	        return 1;
	    }
	    return n * factorial(n - 1);
	});

	factorial(10); // 3628800
	// 输出结果说明factorial(1)~factorial(10)都已经缓存了:
	// start calculate 10!...
	// start calculate 9!...
	// start calculate 8!...
	// start calculate 7!...
	// start calculate 6!...
	// start calculate 5!...
	// start calculate 4!...
	// start calculate 3!...
	// start calculate 2!...
	// start calculate 1!...

	factorial(9); // 362880
	// console无输出

```

.once(function); 保证某个函数执行且仅执行一次
```javascript

	var register = _.once(function () {
	    alert('Register ok!');
	});
	register();
	register();
	register();

```

.delay(function, delay_milli, -parameter_for_function)可以让一个函数延迟执行，效果和setTimeout()是一样的，但是代码明显简单了
```javascript

	// 2秒后调用alert():
	_.delay(alert, 2000);

	var log = _.bind(console.log, console);
	_.delay(log, 2000, 'Hello,', 'world!');
	// 2秒后打印'Hello, world!':

```

.keys(obj)可以非常方便地返回一个object自身所有的key，但不包含从原型链继承下来的
```javascript

	function Student(name, age) {
	    this.name = name;
	    this.age = age;
	}

	var xiaoming = new Student('小明', 20);
	_.keys(xiaoming); // ['name', 'age']

```

.allKeys(obj)除了object自身的key，还包含从原型链继承下来的
```javascript

	function Student(name, age) {
	    this.name = name;
	    this.age = age;
	}
	Student.prototype.school = 'No.1 Middle School';
	var xiaoming = new Student('小明', 20);
	_.allKeys(xiaoming); // ['name', 'age', 'school']

```

.values(obj)返回object自身但不包含原型链继承的所有值. 没有allValues().
```javascript

	var obj = {
	    name: '小明',
	    age: 20
	};

	_.values(obj); // ['小明', 20]

```

.mapObject(obj, function (value, key) {...});
```javascript

	//return array
	var obj = {
	    name: 'bob',
	    school: 'No.1 middle school',
	    address: 'xueyuan road'
	};

	var upper = _.mapObject(obj, function (value, key) {
	    
	    return value.toUpperCase();
	});

	console.log(JSON.stringify(upper)); //{"name":"BOB","school":"NO.1 MIDDLE SCHOOL","address":"XUEYUAN ROAD"}
```

.invert(obj)把object的每个key-value来个交换，key变成value，value变成key
```javascript

	var obj = {
	    Adam: 90,
	    Lisa: 85,
	    Bart: 59
	};
	_.invert(obj); // { '59': 'Bart', '85': 'Lisa', '90': 'Adam' }

```

.extend(obj...); 把多个object的key-value合并到第一个object并返回. 如果有相同的key，后面的object的value将覆盖前面的object的value。
```javascript

	var a = {name: 'Bob', age: 20};
	_.extend(a, {age: 15}, {age: 88, city: 'Beijing'}); // {name: 'Bob', age: 88, city: 'Beijing'}
	// 变量a的内容也改变了：
	a; // {name: 'Bob', age: 88, city: 'Beijing'}

```

.extendOwn(obj...); 把多个object的key-value合并到第一个object并返回. 获取属性时忽略从原型链继承下来的属性。
```javascript

	function Student(name, age) {
	    this.name = name;
	    this.age = age;
	}
	Student.prototype.school = 'No.1 Middle School';
	var a = new Student('test01', 22);
	_.extend(a, {age: 15}, {age: 88, city: 'Beijing'}, {school: '68 High School'}); 

```

.clone(obj); 复制一个object对象. 会把原有对象的所有属性都复制到新的对象中. 
clone()是“浅复制”。所谓“浅复制”就是说，两个对象相同的key所引用的value其实是同一对象
```javascript

	var source = {
	    name: '小明',
	    age: 20,
	    skills: ['JavaScript', 'CSS', 'HTML']
	};
	var copied = _.clone(source);
	console.log(JSON.stringify(copied, null, '  ')); 

```

.isEqual(); 对两个object进行深度比较，如果内容完全相同，则返回true
```javascript

	//compare object
	var o1 = { name: 'Bob', skills: { Java: 90, JavaScript: 99 }};
	var o2 = { name: 'Bob', skills: { JavaScript: 99, Java: 90 }};
	o1 === o2; // false
	_.isEqual(o1, o2); // true

	//compare array
	var o1 = ['Bob', { skills: ['Java', 'JavaScript'] }];
	var o2 = ['Bob', { skills: ['Java', 'JavaScript'] }];
	o1 === o2; // false
	_.isEqual(o1, o2); // true

```

.chain(); 把对象包装成能进行链式调用的方法.因为每一步返回的都是包装对象，所以最后一步的结果需要调用value()获得最终结果。
```javascript

	var r = _.chain([1, 4, 9, 16, 25])
	         .map(Math.sqrt)
	         .filter(x => x % 2 === 1)
	         .value();
	console.log(r);
```