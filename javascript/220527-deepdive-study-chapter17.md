# TIL

## 객체 리터럴 방식의 문제점

직관적이지만 여러 개를 만들 경우 단순 노동을 해야 한다.. 

## 생성자 함수

일반 함수와 같이 함수를 정의하고 new 연산자와 함께 호출하면 생성자 함수로 동작.

생성자 함수에서의 this 바인딩은 생성자 함수가 미래에 생성할 인스턴스이다. 

```jsx
function Person(name) { // 생성자함수의 함수이름은 일반적으로 파스칼케이스로 한다.
  // 인스턴스 초기화 프로퍼티 추가하기 전이니까 빈객체이다. 1번 실행 -> person {}
  this.name  = name; // 2번 실행 -> this= me.name = 'lee' , you.name = 'kim' 
  this.sayHi = function () { 
    console.log(`Hi My name is ${this.name}`);
  }; 
//  this = me.sayHi = function () { 
//   console.log(`Hi My name is ${me.name}`);
//  }; 
//  this = you.sayHi = function () { 
//   console.log(`Hi My name is ${you.name}`);
//  }; 
}

const me = new Person('Lee');
const you = new Person('kim');
// 1. 생성자함수로서 호출이 되면 function 선두에서 빈 객체를 만들고
// 2. 생성한 빈 객체를 this(인스턴스)에 바인딩한다.
// 3. 기술한 코드를 실행한다, this에 프로퍼티 추가한다.
// 4. return this(인스턴스)를 한다. 절대 개발자가 return문을 따로 주면 안된다.

console.log(me); // me {name: 'lee',sayHi f}
console.log(you);
```

## this 바인딩

일반 함수로써 호출 ⇒ 전역 객체

메서드로써 호출 ⇒ 메서드를 호출한 객체

생성자 함수로써 호출 ⇒ 생성자 함수가 미래에 생성할 인스턴스

## 생성자 함수의 내부 메서드

함수는 일반 객체와 다르게 호출할 수 있기 때문에 일반 객체의 내부 슬롯과 내부 메서드는 물론, 함수로서 동작하기 위한 내부 슬롯과 [[call]], [[construct]] 같은 내부 메서드를 추가로 가지고 있다.

함수가 일반 함수로써 호출 되면 함수 객체의 내부 메서드 **[[call]]** 이 호출 되고, 

생성자 함수로 호출 되면 내부 메서드 **[[construct]]** 가 호출 된다.

**함수 = 호출가능 → [[call]]** 

**일반 함수 = 호출가능, non-constructor**

**생성자 함수 = 호출 가능, constructor**

## constructor / non-constructor 구분

constructor = 함수 선언문, 함수 표현식, 클래스 ⇒ 생성자 함수로 사용 가능 / **인스턴스 생성**

non-constructor = 메서드(ES6 축약 표현), 화살표 함수 ⇒ 생성자 함수로 사용 불가능 

**new 연산자와 함께 호출 하면 함수 내부의 [[construct]] 가 호출되며 호출 함수는 constructor 이어야 한다.**

## new.target

new.target은 new 연산자와 함께 작동하면 함수 자신을 가리키고 함께 작동하지 않았을 때는 undefined를 반환 한다.

undefined 일 경우 new 연산자와 함께 재귀 호출 해 생성자 함수로 호출하면 new 연산자와 함께 작동하지 않았을 때 에러 처리가 가능하다.
