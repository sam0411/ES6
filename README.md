# ES6
ES6 Learning

## 相等运算符==。
JavaScript在设计时，有两种比较运算符：
第一种是==比较，它会自动转换数据类型再比较，很多时候，会得到非常诡异的结果；
第二种是===比较，它不会自动转换数据类型，如果数据类型不一致，返回false，如果一致，再比较。
由于JavaScript这个设计缺陷，不要使用==比较，始终坚持使用===比较。
另一个例外是NaN这个特殊的Number与所有其他值都不相等，包括它自己
唯一能判断NaN的方法是通过isNaN()函数


## null和undefined
JavaScript的设计者希望用null表示一个空的值，而undefined表示值未定义。事实证明，这并没有什么卵用，区分两者的意义不大。大多数情况下，我们都应该用null。undefined仅仅在判断函数参数是否传递的情况下有用。


## Object
JavaScript的对象是一组由键-值组成的无序集合，要获取一个对象的属性，我们用对象变量.属性名的方式：
```javascript
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
```