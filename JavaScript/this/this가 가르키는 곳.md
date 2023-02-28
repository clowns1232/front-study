# this가 가르키는 곳

this는 자신이 속한 객체 또는 자신이 생성할 인스턴스를 가리키는 자기 참조 변수입니다.

자바스크립트의 this는 함수를 호출할 때, `함수가 어떻게 호출되는지에 따라 this가 바인딩할 객체가 동적으로 정해집니다.`

# 1. 일반함수 호출

```jsx
// 함수 선언식
function funcDeclaration () {
	console.dir(this);
}
funcDeclaration(); // window or global

// 함수 표현식
const funcExpressions = () => {
	console.dir(this);
}
funcExpressions(); // window or global
```

# 2. 메서드 호출

메서드를 호출하면 기본적으로 this는 해당 메서드를 의미합니다.

단, **메서드가 화살표 함수**로 작성되었을 경우, 화살표 함수의 this는 상위 컨텍스트의 this를 계승받기 때문에 this가 **전역객체**에 바인딩 된다.

```jsx
const obj = {
	foo: function() {
		console.log('foo this:', this);
	},
	bar() {
		console.log('bar this:', this);
	},
	baz: () => {
		console.log('baz this:', this);
	},
}

obj.foo(); // obj
obj.bar(); // obj
obj.baz(); // window
```

# 3. 내부함수 호출

내부함수는 내부함수가 일반함수, 메소드, 콜백함수 내부 어디에서 선언되었든 상관없이 this가 **전역객체**에 바인딩 된다.

단, 내부함수의 this가 전역객체를 **바인딩하지 않도록 하는 방법**이 있다. (아래 코드 참고)

```jsx
const obj = {
	foo: function() {
		function fooInner() {
			console.log('fooInner this:', this);
		}

		fooInner();
	},

	// that 변수에 bar 메서드의 this를 할당하여 사용함으로써
	// 내부함수의 this가 전역객체를 바인딩하지 않도록 한다.
	bar: function() {
		const that = this;
		function barInner() {
			console.log('barInner this:', that);
		}
	
		barInner();
	},

	// 화살표함수의 this는 상위 컨텍스트의 this를 계승받기 때문에,
  // baz 메서드의 this를 바인딩 한다.
	baz: function() {
		const bazInner = () => {
			console.log('bazInner this:', this);
		}
		
		bazInner();
	}
}

obj.foo(); // window
obj.bar(); // obj
obj.baz(); // obj
```

# 4. 콜백함수 호출

콜백함수를 호출하면 **제어권을 가지는 함수가 this를 무엇으로 바인딩 할지 결정**한다.

```jsx
const obj = {
	foo: function() {
		setTimeout(() => {
			console.log('foo setTimeout this:', this);
		}, 1000);
	}
}

obj.foo(); // foo setTimeout this: window
```

# 5. **apply/call/bind 호출**

`call`은 함수를 호출하며 **첫 번째 인자로 전달하는 값에 this를 바인딩** 한다.

`apply`는 함수를 호출하며 **첫 번째 인자로 전달하는 값에 this를 바인딩** 한다.

인자는 배열 형태로 전달하며, 실제 배열이 전달되는 것이 아니고 **배열의 요소들이 전달**된다

`bind`는 **첫 번째 인자로 전달하는 값에 this를 바인딩** 하며, 새로운 함수를 반환한다.

```jsx
function foo(num1, num2) {
	console.log(this.name, num1 + num2);
}

const person = {
	name: 'cho',
};

foo.call(person, 1, 2); // cho, 3
foo.apply(person, [1, 2]); // cho, 3

const newFoo = foo.bind(person);
newFoo(1, 2); // cho, 3
```

# 6. 화살표 함수

메서드 호출에서 설명을 했듯이 화살표 함수는 this가 없으므로 상위 스코프에 this를 가르키고 있습니다. 

```jsx
// 전역 스코프에 정의되있으므로, this가 전역 객체를 가리킨다.
const foo = () => {
	console.log(this);
}

foo(); // window

// foo 메서드의 스코프에 정의되있으므로, this가 foo 메서드의 this를 가리킨다.
const obj = {
	foo: function() {
		const fooInner = () => {
			console.log(this);
		}

		fooInner();
	}
};

obj.foo(); // obj
```