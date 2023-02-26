# Dart 문법

Dart 문법을 확인하고 싶으면 [해당 사이트](https://dartpad.dev/?)를 추천드립니다.

# 1. Dart 언어의 특징

1. main() 함수로 시작된다.
2. 어디서나 변수 선언 및 사용이 가능하다.
3. 모든 변수가 객체(Object) 입니다.
    1. 함수, 숫자, null 모두 객체로 취급
4. 자료형에 엄격한 언어이지만 dynamic 자료형으로 여러 자료형를 사용도 가능합니다.
5. List<String> 같은 제네릭 타입 허용
6. Dart는 Java와 다르게 public, protect 같은 접근 지정자가 없습니다.
    1. 대신 `_` 을 붙여 DartPage 단위로 접근이 가능합니다. 
    2. ex : _function()
7. Null safety를 지원합니다.
    1. 모든 데이터 타입은 null을 허용하지 않습니다.
    2. 데이터 타입 뒤에 `?`을 추가하여 null을 허용하도록 선언할 수 있습니다.
8. 명령어는 세미콜론 `;` 로 끝납니다.

# 2. Dart의 기초 문법

## 2.1 주석 및 콘솔 출력

```dart
// 주석
/*
주석
*/
print("dart는 print로 콘솔을 출력합니다");
```

## 2.1 변수 선언(자료형)

```dart
void main() {
	// 정수
	int number1 = 17;
	print(number1);
	int number2 = 20 ~/ 4; //나누기
	print(number2); // 5
	int number3 = 20 % 4; //나머지
	print(number3); // 0
	
	// 실수
	double pi = 3.14;
	print(pi); //3.14

	// 문자
	string name = "황태현"
	
	// 참 / 거짓
	bool visible = true;
	print(visible); //true
	
	// 배열
	List array = [1, 2, 3];
	print(array);
	print(array[1]);

	// 제네릭 리스트
	List<int> numberArr = [1, 2, 3];
	
	// 맵 Map Key:value
	Map my = {'name': '황태현', 'age': '28'};
	print(my); // {'name': '황태현', 'age': '28'};

	// 동적 변수
	dynamic all = "모든 값 가능";
	print(all.runtimeType); // String
	all = 1; // 에러 발생 안함
	print(all.runtimeType); // int
	print(all); // 1
} 
```

## 2.2 변수 선언(var)

자료형을 지정하지 않고 var 타입으로 변수를 선언할 수 있습니다.
다만 초기화 한 값이 데이터 타입이 되고 null일 경우 dynamic 처럼 변수가 변경됩니다.

```dart
void main() {
	var a = 1;
  var b = null;
  a = "test"; // a는 int 타입이라 에러 발생
  b = "test";
}
```

## 2.3 final, const

둘 다 한번 선언 뒤 값을 변경할 수 없습니다.

다만 const는 상수를 정의할 수 있어서 런타임에서 정의되는 값을 설정이 불가능합니다.

```dart
void main() {
  final DateTime now = DateTime.now(); // 정상 작동
  const DateTime now = DateTime.now(); // 에러 발생
}
```

## 2.4 nullable & non-nullable

기본적으로 타입이 있는 변수는 non-nullable이며 null 타입을 허용하지 않습니다.
하지만 타입 뒤에 `?` 을 쓰면 null 타입을 허용하게 변경이 가능합니다.

```dart
void main() {
  String name = null; // null 타입이 허용되지 않으므로 에러가 발생한다.
  String? name1 = null;
}
```

## 2.5 타입 확인 및 검사

변수.runtimeType로 타입을 확인 할 수 있고 is로 타입을 검사할 수 있습니다.

```dart
var a = 1;
var b = "1";

print(a.runtimeType); // int
print(b.runtimeType); // String
print(a is int); // true
print(b is int); // false
```

## 2.6 표현식

Dart도 표현식을 사용하여 변수에 삽입이 가능합니다.

```dart
void main() {
  String name = '황태현';
  num age = 28;
  print('$name은 ${age}살 입니다'); //홍길동은 21살 입니다
  print('$name은 ${DateTime.now().year - age + 1}년에 태어났습니다'); //홍길동은 2002년에 태어났습니다
}
```

## 2.7 enum

다른 프로그램 언어와 똑같이 열거형도 지원합니다.

```dart
enum BoardType { notice, free, undefined }

// BAD
// board 모델에서 string타입의 type 변수를 사용할경우

if (board.type == "notice") {
   ...
} else if (board.Type == "free") {
  .....
} else {
....
}

// GOOD
// enum 형식으로 type 변수를 사용할경우 
if (board.type == BoardType.notice) {
...
} else  if (board.type == BoardType.free) {
...
} else {
...
}
```

## 2.8 함수

```dart
void main() {
  print(addNumbers(1, 2, 3));
  print(addNumbers(1, 2)); // 매개변수가 3개인데 인수를 2개 넣어서 에러가 발생
  print(optionalParameter(1, 2)); // 매개변수가 3개인데 인수를 2개 넣어서 에러가 발생
	print(namedParameter(x:1, z:2,  y:1,)); // 인수를 이름으로 넣을 수 있다.
}

addNumbers(int x, int y, int z) {
  return x + y + z;
}

// []안에 optional parameter을 선언할 수 있다.
// 이때 초기값을 설정해 줘야 합니다.
optionalParameter(int x, [int y = 0, int z = 0]) {
  return x + y + z;
}

// 매개변수에 이름을 설정할 수 있다.
namedParameter({
  required int x,
  required int y,
  required int z,
}) {
  return x + y - z;
}

// 바로 return이 되는 경우 화살표로 한줄로 사용이 가능하다.
namedParameter1({
  required int x,
  required int y,
  required int z,
}) => x + y - z;

```

## 2.9 typedef

```dart
void main() {
	// 1. 변수 선언의 타입처럼 typedef를 선언
	// 2. 이름은 변수 명 짓듯 지으면 된다.
  // 3. 초기화 하는 값은 함수이다.
  Operation operation = add;
	
	// 4. res는 add 함수를 실행하는 것과 같은 동작이다.
	// 5. 그러므로 함수에 있는 매개변수를 그대로 따라야 한다.
  int res = operation(1, 2, 3);
  print(res);
  
  operation = sub;
	// 6. 이제는 sub 함수를 실행하는 것과 같은 동작을 한다.
  int res1 = operation(1, 2, 3);
  print(res1);
}
typedef Operation = int Function(int x, int y, int z);

int add (int x, int y, int z) => x + y + z;
int sub (int x, int y, int z) => x - y - z;
```

위의 설명을 읽어도 솔직히 어따 써야할지 막막할거 같습니다.
이래 아래에 유용하게 사용하는 코드를 확인해보겠습니다.

```dart
void main() {
  print(calculate(1, 2, add));
  print(calculate(1, 2, sub));
}

typedef Operation = int Function(int x, int y);
int calculate(int x, int y, Operation operation) {
  return operation(x, y);
}
int add(int x, int y) => x + y;
int sub(int x, int y) => x - y;
```

콜