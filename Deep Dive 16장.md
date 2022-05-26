프로퍼티 어트리뷰트를 이해하기 위해서는 먼저 내부 슬롯과 내부 메서드의 개념에 대해 숙지해야 한다.

내부 슬롯과 내부 메서드는 자바스크립트 엔진의 구현 알고리즘을 설명하기 위해 ECMAScript 사양에서 사용하는 의사 프로퍼티와 의사 매서드다.

> 의사(pseudo) : 가짜,거짓

ECMAScript 사양에 등장하는 이중 대괄호 `([[...]])`로 감싼 이름들이 내부 슬롯과 내부 메서드다.
내부 슬롯과 내부 메서드는 자바스크립트 엔진에서 실제로 동작하지만 개발자가 직접 접근할 수 없는 메서드와 프로퍼티를 말한다.

예를 들어, 모든 객체는 `[[Prototype]]`이라는 내부 슬롯을 갖는다.
내부 슬롯은 자바스크립트 엔진의 내부 로직이므로 직접 접근할 수 없지만
`[[Prototype]]` 내부 슬롯의 경우, `__proto__`를 통해 간접적으로 접근할 수 있다.

```js
const o = {};

o.[[Prototype]] // Unexpected token '['

o.__proto__ // Object.prototype
```

#### 프로토타입 어트리뷰트와 프로퍼티 디스크립터 객체
자바스크립트 엔진은 프로퍼티를 생성할 때 프로퍼티의 상태를 나타내는 프로퍼티 어트리뷰트를 기본값으로 자동 정의한다.
프로퍼티의 상태란 프로퍼티의 값, 값의 갱신 가능 여부, 열거 가능 여부, 재정의 가능 여부를 말한다.

프로퍼티 어트리뷰트는 자바스크립트 엔진이 관리하는 내부 상태 값인 내부 슬롯인 위 4가지의 값을 말한다.

따라서 프로퍼티 어트리뷰트에 직접 접근할 수 없지만 `Object.getOwnPropertyDescriptor` 메서드를 사용하여 간접적으로 확인할 수는 있다.
`Object.getOwnPropertyDescriptor`는 첫번째 매개변수로 객체의 참조를 전달하고, 두번째 매개변수에는 프로퍼티 키를 문자열로 전달하며, 프로퍼티 디스크립터 객체를 반환한다.
`Object.getOwnPropertyDescriptor`는 하나의 프로퍼티에 대해 디스크립터 객체를 반환하지만
`Object.getOwnPropertyDescriptors`는 모든 프로퍼티의 프로퍼티 어트리뷰트 정보를 제공하는 프로퍼티 디스크립터 객체들을 반환한다.
```js
const person = {
  name: 'Lee'
}
person.age = 20;

Object.getOwnPropertyDescriptors(person)
/*
{
	name: {value: "Lee", writable: true, enumerable: true, configurable: true },
    age: {value: "Lee", writable: true, enumerable: true, configurable: true }
}
```

### 데이터 프로퍼티와 접근자 프로퍼티

프로퍼티는 데이터 프로퍼티와 접근자 프로퍼티로 구분할 수 있다.

- 데이터 프로퍼티
키와 값으로 구성된 일반적인 프로퍼티.
- 접근자 프로퍼티
자체적으로 값을 갖지 않고 다른 데이터 프로퍼티의 값을 읽거나 저장할 때 호출되는 접근자 함수로 구성된 프로퍼티다.

데이터 프로퍼티가 갖는 프로퍼티 어트리뷰트는 처음에 설명한 4가지 프로퍼티 어트리뷰트를 갖는다.

자체적으로 값을 갖지 않는 접근자 프로퍼티가 갖는 프로퍼티 어트리뷰트는 조금 상이하다.
`[[Value]]`와 `[[Writable]]` 대신 `[[Get]]` `[[Set]]` 프로퍼티 어트리뷰트가 존재한다.

접근자 프로퍼티는 다른 데이터 프로퍼티에 접근하거나 값을 변경하는데 목적이 있다. 그렇기에`[[Get]]` 프로퍼티 어트리뷰트는 getter 함수를 호출하고, 호출한 결과가 **프로퍼티의 값**으로 반환되며 `[[Set]]` 프로퍼티 어트리뷰트는 데이터 프로퍼티의 값을 저장할 때 setter 함수를 호출하여 그 결과가 프로퍼티의 값으로 저장되는 프로퍼티 어트리뷰트이다.

```js
const person = {
  
  firstName: 'MyungSeong',
  lastName: 'Kim',
  get fullName() {
    return `${this.firstName} ${this.lastName}`;
  },
  set fullName(name){
  [this.firstName, this.lastName] = name.split(' ');
  }
}
// 값 저장 시 setter 함수 호출
person.fullName = 'Heegun Lee';
console.log(person);
// 값 접근 시 getter 함수 호출
console.log(person.fullName);

```


firstName,lastName 프로퍼티 값으로 Heegun, Lee가 되어야 하는데, 변경이 안됨............

> 프로토타입 prototype
프로토타입은 어떤 객체의 상위 객체의 역할을 하는 객체다.
하위 객체에게 자신의 프로퍼티와 메서드를 상속한다.
프로토타입 체인은 단방향으로 연결된다.
객체의 프로퍼티나 메서드에 접근할 때 찾는 프로퍼티나 메서드가 없다면 상위 프로토타입을 거슬러 올라가며 검색한다.

### 프로퍼티 정의

프로퍼티 정의란 새로운 프로퍼티를 추가하면서 프로퍼티 어트리뷰트를 명시적으로 정의하거나, 기존 프로퍼티의 프로퍼티 어트리뷰트를 재정의하는 것을 말한다.
`Object.defineProperty` 메서드를 사용하면 프로퍼티의 어트리뷰트를 정의할 수 있다.
인수로는 객체의 참조와 프로퍼티의 키인 문자열, 프로퍼티 디스크립터 객체를 전달한다.

```js
Object.defineProperty(person, 'fullName', { 
  get() {
    return `${this.firstName} ${this.lastName}`;
  },
  set(name){
  [this.firstName, this.lastName] = name.split(' ');
  },
  enumerable: true,
  configurable: true

```
`Object.defineProperties`를 사용하면 한번에 여러 개의 프로퍼티를 정의할 수 있다.

```js
const person = {};
Object.defineProperties(person, {
  //data property definition
  firstName: {
    value: 'ungmo',
    wriable: true,
    enumerable: true,
    configurable: true
  },
  lastName: {
    value: 'Lee',
    writable: true,
    enumerable: true,
    configurable: true
  },
  fullName: {
    get() {
      return //...
    },
    set(name) {
      // ...
    },
    enumerable: true,
    configurable: true
  }
});

person.fullName = 'Heegun Lee';
```

### 객체 변경 방지
객체 확장 금지 - `Object.preventExtensions`
- 프로퍼티 삭제, 값 읽기,쓰기만 가능(프로퍼티 추가 불가)
객체 밀봉 - `Object.seal`
- 값 읽기,쓰기만 가능
객체 동결 - `Object.freeze` 
- 프로퍼티 값 읽기만 가능

다만 위 메서드는 얕은 변경 방지로 중첩 객체까지는 영향을 주지 못한다. 객체의 중첩 객체까지 동결하여 불가능한 읽기 전용의 불변 객체를 구현하려면 객체를 값으로 갖는 모든 프로퍼티에 대해 재귀적으로 Object.freeze를 호출해야 한다.


___

> 의사(pseudo)는 가짜,거짓이라는 뜻을 가지고 있다.
하지만, 내부 슬롯과 메서드가 존재하지 않는다는 것은 아니다.
자바스크립트 엔진에서 실제로 동작하지만 개발자가 직접 접근할 수 없는 메서드와 프로퍼티를 말한다.

> **`[[Prototype]]`**
내부 슬롯은 자바스크립트 엔진의 내부 로직이므로 직접 접근할 수 없지만
`[[Prototype]]` 내부 슬롯의 경우, `__proto__`를 통해 간접적으로 접근할 수 있다.

> **4가지의 프로토타입 어트리뷰트**
`[[Value]]` `[[Writable]]` `[[Enumerable]]` `[[Configurable]]` 
자바스크립트 엔진은 프로퍼티를 생성할 때 프로퍼티의 상태를 나타내는
프로퍼티 어트리뷰트를 기본값으로 자동 정의한다.
프로퍼티의 상태란
프로퍼티의 값 `[[Value]]`
값의 갱신 가능 여부 `[[Writable]]`
열거 가능 여부 `[[Enumerable]]`
재정의 가능 여부 `[[Configurable]]`을 말한다.

> **데이터 프로퍼티와 접근자 프로퍼티**
프로퍼티는 데이터 프로퍼티와 접근자 프로퍼티로 구분할 수 있다.
- 데이터 프로퍼티
키와 값으로 구성된 일반적인 프로퍼티.
- 접근자 프로퍼티
자체적으로 값을 갖지 않고 다른 데이터 프로퍼티의 값을 읽거나 저장할 때 호출되는 접근자 함수로 구성된 프로퍼티다.

> getter // setter
자체적으로 값을 갖지 않는 접근자 프로퍼티가 갖는 프로퍼티 어트리뷰트는 조금 상이하다.
`[[Value]]`와 `[[Writable]]` 대신 `[[Get]]` `[[Set]]` 프로퍼티 어트리뷰트가 존재한다.
접근자 프로퍼티는 다른 데이터 프로퍼티에 접근하거나 값을 변경하는데 목적이 있다. 그렇기에`[[Get]]` 프로퍼티 어트리뷰트는 getter 함수를 호출하고, 호출한 결과가 **프로퍼티의 값**으로 반환되며 `[[Set]]` 프로퍼티 어트리뷰트는 데이터 프로퍼티의 값을 저장할 때 setter 함수를 호출하여 그 결과가 프로퍼티의 값으로 저장되는 프로퍼티 어트리뷰트이다.

> getter // setter 함수
접근자 프로퍼티가 반환하는 `setter` 함수를 통해 새로운 값을 저장한다면 setter 함수가 호출되며, 접근자 프로퍼티가 반환하는 `getter` 함수를 통해  값에 접근한다면 getter 함수가 호출된다.


> **프로토타입 prototype**
프로토타입은 어떤 객체의 상위 객체의 역할을 하는 객체다.
하위 객체에게 자신의 프로퍼티와 메서드를 상속한다.
프로토타입 체인은 단방향으로 연결된다.
객체의 프로퍼티나 메서드에 접근할 때 찾는 프로퍼티나 메서드가 없다면 상위 프로토타입을 거슬러 올라가며 검색한다.


> **프로퍼티 정의**
프로퍼티 정의란 새로운 프로퍼티를 추가하면서 프로퍼티 어트리뷰트를 명시적으로 정의하거나, 기존 프로퍼티의 프로퍼티 어트리뷰트를 재정의하는 것을 말한다.
`Object.defineProperty` 메서드를 사용하면 프로퍼티의 어트리뷰트를 정의할 수 있다.
인수로는 객체의 참조와 프로퍼티의 키인 문자열, 프로퍼티 디스크립터 객체를 전달한다.

> **객체 변경 방지**
객체 확장 금지 - `Object.preventExtensions`
- 프로퍼티 삭제, 값 읽기,쓰기만 가능(프로퍼티 추가 불가)
객체 밀봉 - `Object.seal`
- 값 읽기,쓰기만 가능
객체 동결 - `Object.freeze`
- 프로퍼티 값 읽기만 가능
다만 위 메서드는 얕은 변경 방지로 중첩 객체까지는 영향을 주지 못한다. 객체의 중첩 객체까지 동결하여 불가능한 읽기 전용의 불변 객체를 구현하려면 객체를 값으로 갖는 모든 프로퍼티에 대해 재귀적으로 Object.freeze를 호출해야 한다.
