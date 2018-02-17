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