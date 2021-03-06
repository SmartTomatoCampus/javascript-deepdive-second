# 객체 리터럴

## 김명성
프로퍼티 값이 함수일 경우 일반 함수와 구분하기 위해 메서드라 부른다.
=> 하지만 ES6 사양에서 메서드는 메서드 축약 표현으로 정의된 함수만을 의미하는 것으로 변경됨.
객체는 객체의 상태를 나타내는 값과 프로퍼티를 참조하고 조작하는 동작을 모두 포함할 수 있어 상태와 동작을 하나의 단위로 구조화할 수 있어 유용하다.
객체 리터럴의 중괄호는 코드 블록을 의미하지 않는다.
객체 리터럴은 자바스크립트의 유연함과 강력함을 대표하는 객체 생성 방식이다.
프로퍼티 키에 문자열,심벌 값 외의 값을 사용하면 암묵적 타입 변환으로 문자열이 된다.
예약어 또한 프로퍼티 키로 사용할 수 있으나 권장하지 않는다.
메서드 내부에서 사용한 this 키워드는 객체 자신을 가리키는 참조 변수다.
마침표 프로퍼티 접근 연산자 또는 대괄호 프로퍼티 접근 연산자의 좌측에는 객체로 평가되는 표현식을 기술한다.
객체에 존재하지 않는 프로퍼티에 접근하면 error가 아닌 undefined를 반환한다.
존재하지 않는 프로퍼티에 값을 할당하면 프로퍼티가 동적으로 생성되어 추가되고 프로퍼티 값이 할당된다.
ES6 메서드 축약 표현으로 정의한 메서드는 프로퍼티에 할당한 함수와 다르게 동작한다.
=> 인스턴스를 생성할 수 없는 non-constructor이며 prototype 생성이 불가하며 자신을 바인딩한 객체를 가리키는 내부 슬롯 [[HomeObject]]를 갖게 되어 super 키워드를 사용할 수 있게 된다.
super 키워드는 프로토타입 체인 상위에 있는 메서드를 사용할 수 있게 한다.

## 초생
1. 지금까지 객체 선언할 때 쓴건 객체 리터럴임
2. 객체는 프로터피와 메서드의 집합
3. 식별자 네이밍에 따르지 않는 프로퍼티키는 따옴표로 선언 가능
4. 프로퍼티 키도 문자열과 symbol만 되는데 이외의 타입일 경우 문자열로 타입변환
5. 프로퍼티 삭제할 때 delete object.props

## 클로버
자바스크립트는 객체 기반의 프로그래밍 언어이다. 자바스크립트를 구성하는 원시 값을 제외한 나머지 값(함수, 배열, 정규 표현식 등)은 모두 객체다.

원시 타입은 단 하나의 값만 나타내며, 변경 불가능 한 값이다.
객체 타입은 다양한 타입의 값을 하나의 단위로 구성한 복합적인 값이고, 변경 가능한 값이다.
객체는 객체의 상태를 나타내는 값, 프로퍼티와 프로퍼티를 참조하고 조작할 수 있는 메서드로 구성된 집합체이다. 

인스턴스: 인스턴스란 클래스에 의해 생성되어 메모리에 저장된 실체를 말한다. 객체지향 프로그래밍에서는 객체는 클래스와 인스턴스를 포함한 개념이다. 클래스는 인스턴스를 생성하기 위한 템플릿의 역할을 한다. 인스턴스는 객체가 메모리에 저장되어 실제로 존재하는 것에 초점을 맞춘 용어이다. 메모리에 저장되어 있는 객체의 값을 인스턴스라 하는 것이라 이해.

객체 리터럴인 중괄호는 코드 블록의 중괄호랑 다르다. 객체 리터럴은 값으로 평가되는 표현식이며 따라서 객체 중괄호 뒤에는 세미콜론을 붙인다.

프로퍼티 키는 빈 문자열을 포함하는 모든 문자열 또는 심벌 값을 쓸 수 있는데 식별자 네이밍 규칙을 따르지 않는 이름에는 반드시 따음표를 사용해서 묶어줘야 한다. 빈 문자열을 프로퍼티 키로 사용해도 에러가 발생하지 않는다.

객체에 존재하지 않는 프로퍼티에 접근하면 참조에러가 아니라 undefined를 반환한다.

ES6에서는 메서드를 정의할때 function 키워드를 생략한 축약 표현을 사용할 수 있다.
