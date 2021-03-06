# 함수와 일급 객체

# 경찬

## 18장: 함수와 일급 객체

### 일급 객체란 무엇인가?!

1. 무명의 리터럴 생성
2. 변수나 자료구조에 저장 가능
3. 함수의 매개변수에 전달 가능 
4. 함수의 반환값으로 사용 가능

- 함수는 일급객체!

### 함수와 일반객체와의 차이
1. 함수는 호출 가능하다.
2. 함수 고유의 프로퍼티를 갖는다.

함수 고유의 프로퍼티
  1. arguments 프로퍼티
    - 매개변수로 전달된 인수의 정보를 담고 있는 순회가능한 유사배열객체(함수 내부에서 지역변수 처럼 사용 가능)
  2. caller 프로퍼티
    - 함수 자신을 호출한 함수를 가리킴
  3. length 프로퍼티
    - 함수를 정의할 때 선언한 매개변수의 개수를 가리킴
  4. name 프로퍼티
    - 함수의 이름을 나타냄
    - 익명 함수일 때
      es5 -> 빈 배열
      es6 -> 함수 객체를 가리키는 식별자를 값으로 가짐
  5. proto 접근자 프로퍼티
    - 프로토타입 객체에 접근하기 위해 사용하는 접근자 프로퍼티
  6. prototype 프로퍼티
    - 생성자 함수로 호출할 수 있는 함수 객체, constructor만 소유하는 프로퍼티

# 경택

## 일급 객체

무명의 리터럴로 생성할 수 있다. → 런타임에 생성이 가능하다? 

객체와 동일하게 사용할 수 있으므로 값으로 취급 되며, 객체나 배열등에 저장 가능하다.

일반 객체와 같이 매개변수에 전달 할 수 있으며, 함수의 반환값으로 사용할 수도 있다.

→ 함수형 프로그래밍을 가능하게 하는 자바스크립트의 장점 중 하나

함수를 정의할 때 선언한 매개 변수는 함수 내부에서 변수와 같이 취급되며 함수 안에서 암묵적으로 매개변수가 선언되고 undefined가 할당되어 인수가 매개변수의 개수보다 적었을 때는 남은 매개변수는 undefined로 초기화 된 상태를 유지한다 . 인수가 더 많으면 무시되지만 arguments 객체의 프로퍼티로 보관된다.


⇒ arguments란?

호출 시 전달 된 인수들의 정보를 담고 있는 유사 배열 객체이며 순회 가능하다.

인수의 개수를 확정할 수 없을 때 가변 인자 함수를 구현할 때 유용하다. 

ES6 이후로는 REST 파라미터를 사용한다.

proto 접근자 프로퍼티


모든 객체는 [[prototype]] 이라는 내부 슬롯을 갖고 그것은 객체지향 프로그래밍의 상속을 구현하는 프로토타입 객체를 가르킨다.

프로토타입 내부슬롯에 직접 접근할 수 없으므로 proto 접근자 프로퍼티를 통해 간접적으로 접근할 수 있다.

프로토타입 프로퍼티는 생성자 함수로 호출 할 수 있는 함수 객체, 즉 constructor 만이 소유하는 프로퍼티다.

프로토타입 프로퍼티는 생성자 함수로 호출 될 때 생성자 함수가 생성 할 인스턴스의 프로토타입 객체를 가리킨다.

# 쑥스럽게

1. 다음과 같은 조건을 만족하는 객체를 일급 객체라한다 (함수가 대표적 일급객체)
- 무명의 리터럴로 생성할 수 있다. 즉, 런타임에 생성이 가능하다
- 변수나 자료구조(객체, 배열 등)에 저장할 수 있다.
- 함수의 매개변수에 전달할 수 있다.
- 함수의 반환값으로 사용할 수 있다.
2. 함수는 객체와 같이 함수의 매개변수에 전달할 수 있고, 반환값으로 사용할 수도 있다.(함수형 프로그래밍)
3. arguments, caller, length, name , prototype 프로퍼티는 일반 객체에는 없는 함수 객체 고유의 데이터 프로퍼티다
4. proto는 접근자 프로퍼티이며 모든 객체가 사용가능하다
5. arguments객체는 배열형태로 인자정보를 담고 있지만 배열이아닌 유사배열객체이다.
- 유사배열객체란? length프로퍼티를 가진 객체로 for문으로 순회할 수 있는 객체 배열메서드를 사용할경우 에러남
6. length 프로퍼티는 함수를 정의할 때 선언한 매개변수의 개수를 가리킨다.
7. arguments객체의 length프로퍼티는 인자의 개수를 가리키고, 함수객체의 length프로퍼티는 매개변수 개슈를 가리킨다.
8. name프로퍼티는 함수 이름을 나타내고 ES5까지는 익명함수표현식을 빈문자열로 값을 갖었지만 ES6이후 식별자를 값으로 갖게됨
9. 모든 객체는 [[prototype]]이라는 내부슬롯을 갖는다. proto프로퍼티는 [[prototype]]내부슬롯이 가리키는 프로토타입 객체에 접근하기위해 사용하는 접근자 프로퍼티다. 직접 접근은 안되지만 간접 접근만 가능하다.
10. hasOwnProperty메서드 : 인수로 전달받은 프로퍼티 키가 객체 고유의 프로퍼티 키인가 아닌가를 불리언값을 반환하는 메서드
11. prototpye 프로퍼티는 생성자 함수로 호출할수 있는 함수객체, 즉 cunstructor만이 소유하는 프로퍼티다. 일반객체와 생성자함수로 호출할 수 없는 non-constructor에는 없다
```
    const increase = function(num){
    return ++num
    }
    const decrease = function(num){
    return --num
    }
    const auxs = {increase,decrease}

    console.log(auxs); // { increase: [Function: increase], decrease: [Function: decrease] }
    console.log(increase(20)) // 21
    console.log(increase.hasOwnProperty('prototype')); // true
    console.log(auxs.hasOwnProperty('prototype')); // false
```

# 클로버

4가지 조건을 만족하는 객체를 일급 객체라 한다.
1. 무명의 리터럴로 생성할 수 있다. 즉, 런타임에 생성이 가능하다.
2. 변수나 자료구조(객체, 배열)등에 저장할 수 있다.
3. 함수의 매개변수에 전달할 수 있다. - 콜백함수
4. 함수의 반환값으로 사용할 수 있다. 

함수가 일급 객체라는 것은 함수와 객체를 동일하게 사용할 수 있다는 말이며, 객체는 값이므로 함수는 값과 동일하게 사용할 수 있다. 즉 값을 사용할 수 있는 곳(변수, 객체 프로퍼티값, 매열, 함수의 전달인자인 아규먼트, 함수 반환문 등)에 다 사용가능.
이것은 런타임 이전에 함수 객체로 평가된다.

함수 객체와 일반 객체의 가장 큰 차이점은 호출의 여부, 함수 고유의 프로퍼티를 갖는 것이다.
arguments, caller, length 등등 but proto는 접근자 프로퍼티이며 함수의 고유 프로퍼티가 아니다.
프로토타입의 프로퍼티이며 상속받아 사용할 수 있는 것이다.

프로토타입: 어떤 객체의 부모 객체의 역할을 하는 객체이다. 프로토타입은 자신의 자식 객체에게 자신의 프로퍼티와 메서드를 상속한다. 자식 객체는 프로토타입의 프로퍼티 또는 메소드를 자유롭게 사용할 수 있다. 프로토타입 체인은 단방향 링크드 리스트로 연결된 상속 구조를 말한다. 객체의 프로퍼티나 
메서드가 없다면 그 부모, 즉 프로토타입의 프로퍼티나 메소드를 확인한다.

## 함수의 프로퍼티

함수 arguments 프로퍼티 값은 arguments 객체이다. 함수 호출 시 전달된 인수들의 정보를 담고 있으며 순회 가능한 유사배열 객체이며, 함수 내부에서 지역 변수처럼 사용된다. 즉, 함수 외부에서는 참조 불가.
함수의 매개변수와 인수의 개수가 일치하지 않아도 되고 일치하지 않을시 에러메세지는 따로 뜨지 않는다.
파라미터를 선언했을때 최초 undefined값이 할당되며 함수내 지역변수로 사용된다, 아규먼트가(인자)가 적게 전달되거나 전달되지 않았을 경우도 undefined값을 유지한다. 초과된 인수는 버려지는 것이 아니라 arguments 객체 프로퍼티로 보관된다.

arguments 객체의 Symbol(Symbol.iterator) 프로퍼티는 arguments 객체를 순회 가능한 자료구조인 이터러블로 만들기 위한 프로퍼티이다. Symbol.iterator를 프로퍼티 키로 사용한 메서드를 구현하는 것에 의해 이터러블이 된다. 즉 이 프로퍼티가 순회가능한 객체를 만들어준다.

또한 arguments 객체는 length 프로퍼티가 있는 유사배열 객체이다. 배열 형태로 인자 정보를 담고있지만 실제로는 배열이 아닌 말그대로 유사 배열 객체이며 이것은 순회가능한 자료구조를 뜻할때 ES6에 이터러블이라는 개념이 나오기 전에 유사 배열로 명명되어 사용되었다. 즉 arguments객체는 유사배열이면서 이터러블이다. 말그대로 유사배열이지 실제 배열이 아니라 배열메소드 사용은 불가하다. 간접적 방법으로 사용해야함.

### caller 프로퍼티
함수 자신을 호출한 함수를 가르킨다. 자신을 호출한 함수가 없으면 null을 반환한다. 비표준 프로퍼티임.

### length 프로퍼티
함수를 정의할때 선언한 매개변수의 개수를 가리킨다. 여기서 주의할 점은 arguments 객체의 length 프로퍼티는 인자(아규먼트)의 개수를 가리키고, 함수 객체의 length 프로퍼티는 매개변수의 개수를 가리킨다.

### name 프로퍼티
함수 이름을 나타낸다. 비표준이였다가ES6부터 표준. ES6이전에는 빈 문자열을 갖고 이후부터는 함수 객체를 가리키는 식별자를 값으로 갖는다.

### proto 접근자 프로퍼티
모든 객체는 프로토타입 객체에 상속되어 있고 [[prototype]]이라는 내부 슬롯을 갖는다. 이 프로토타입 객체에 간접적으로 접근하기 위해 사용하는 접근자 프로퍼티이다. 

### hasOwnProperty 메서드
객체 고유의 프로퍼티 키일 경우 true를 반환, 상속받은 프로토타입의 키일 경우 false를 반환.

### prototype 프로퍼티
생성자 함수로 호출할 수 있는 함수 객체만이 갖는 프로퍼티. 즉 constructor만이 소유하는 프로퍼티이다.
일반 객체와 생성자 함수로 호출할 수 없는 메서드,화살표함수 같은 non-constructor에는 없는 프로퍼티이다.

이때의 메서드는 일반적으로 우리가 알고 있는 프로퍼티 값으로 사용되는 함수가 아니라 ES6의 함수 축약표현으로 표현된 함수를 말한다.

# 명성


함수를 정의할 때 선언한 매개변수는 함수 몸체 내부에서 변수와 동일하게 취급된다.
즉 함수가 호출되면 함수 몸체 내에서 암묵적으로 매개변수가 선언되고 undefined로 초기화된 인수가 할당된다.


매개변수의 개수보다 인수를 더 많이 전달했을 경우 초과된 인수는 무시된다.
초과된 인수가 버려지는게 아니고 무시된다는 이유는, 모든 인수는 암묵적으로 arguments 객체에 보관되기 때문이다.


유사 배열 객체와 이터러블
ES6에서 도입된 이터레이션 프로토콜을 준수하면 순회 가능한 자료구조인 이터러블이 된다.
이터러블의 개념이 없었던 ES5에서 arguments 객체는 유사 배열 객체로 구분되었다. 하지만 이터러블이 도입된 ES6부터 arguments 객체는 유사 배열 객체이면서 동시에 이터러블이다.

arguments 객체의 length 프로퍼티는 인자의 개수를 가리키고
함수 객체의 length 프로퍼티는 매개변수의 개수를 가리킨다.

prototype 프로퍼티
prototype 프로퍼티는 생성자 함수로 호출할 수 있는 함수 객체, 즉 constructor만이 소유하는 프로퍼티다.
일반 객체와 생성자 함수로 호출할 수 없는 non-constructor에는 prototype 프로퍼티가 없다.
