# ES6
ES6 Learning

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