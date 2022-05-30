220524

# 14장 전역 변수의 문제점

## 전역 변수의 문제점

- 암묵적 결함: 모든 코드가 전역 변수를 참조하고 변경할 수 있음
  -> 1. 변수의 유효범위가 크면 가독성이 나빠짐
  -> 2. 의도치 않은 상태 변화가 발생할 수 있음

- 긴 생명 주기
  -> 1. 메모리 리소스를 오랜 기간 잡아먹는다.(브라우저 상에서는 브라우저가 닫힐 때까지)
  -> 2. var는 특히 재할당이 가능하기 때문에 의도와는 다르게 값이 바뀔 수 있다.

- 스코프 체인 상 종점에 존재
  -> 변수 검색 시 가장 마지막에 검색됨

- 네임스페이스 오염
  -> 파일이 분리되어 있어도 하나의 전역 스코프 공유하기 때문에 문제 발생 가능성 있음 \*

## 전역 변수의 사용을 억제할 수 있는 방법

1. 즉시 실행 함수
   -> 모든 코드를 즉시 실행 함수로 감싸면 변수를 지역변수로 만들 수 있다.

2. 네임스페이스 객체
   -> 객체 안에 객체를 만들어 계층적으로 구성, 스코프를 줄일 수 있다.
   but, 네임스페이스 객체 자체가 전역 변수에 할당되므로 그닥.

3. 모듈 패턴 like 클래스
   변수와 함수를 모아 즉시 실행 함수로 감싸서 모듈을 만듦

- - 전역 변수의 억제 + 캡슐화

# 15장

## var

- 변수의 중복 선언 허용
- 함수 레벨 스코프(지역변수로 할당시) -> 함수 이외에선 전역변수로

## let

- 변수 중복 선언 금지 -> 같은 스코프 내 중복선언X
- 모든 코드블록을 지역스코프로 인정
- 호이스팅 발생X 처럼?! -> '선언단계', '초기화단계' 분리 -> 스코프 시작부터 초기화 이전까지 사용X
- 전역 객체(window) 프로퍼티X

## const

- 상수 선언 위해서
- const는 선언과 초기화 동시에
- 재할당X -> 원시 값 할당시 값 바뀌지 않음, 코드 가독성도 상승(의미부여)
- 객체는 값 변경 가능(참조형 데이터이기 때문에)

220525

# 8장: 제어문

## 알게된 것

> 문은 변수할당 불가능
> 식 -> 값으로 평가 할 수 있는 문 => 변수에 할당 가능!
> so, 삼항연산자는 표현식이므로 변수의 할당 가능!

## 블록문

- 0개 이상의 문을 중괄호로 묶은 것
- 블록문의 끝에는 자체적으로 종결의 의미가 있어 세미콜론을 붙이지 않음

## 조건문

- if ... else 문 -> 조건식의 평과 결과에 따라 불록문 실행, 조건이 불리언일 때 많이 사용
- switch 문 -> 표현식 평가 후 case 문으로 실행 흐름을 옮김, 표현식이 문자열이나 숫자열일 때 많이 사용

## 반복문

- for 문 -> 조건식이 거짓으로 평가될 때까지 코드 블록 반복, 반복 횟수가 정해져있을 때 많이 사용
- while 문 -> 조건식의 평가 결과가 참이면 코드 블록 반복, 반복 횟수가 정해져있지 않을 때 많이 사용

## break 문

- 코드 블록을 탈출

## continue 문

- 반복문의 코드 블록 실행을 현 지점에서 중단하고 반복문의 증감식으로 실행 흐름으 옮김

# 16장: 프로퍼티와 어트리뷰트

## 내부 슬롯, 내부 메서드

- JS의 엔진의 구현 알고리즘 설명을 위해 사용
- 직접 접근 불가능

## 프로퍼티 어트리뷰트, 프로퍼티 디스트립터 객체

- JS 엔진 -> 프로퍼티 생성 -> 프로퍼티 어트리뷰트 정의(프로퍼티의 상태): JS 엔진이 관리하는 내부 슬롯 - 직접 접근X
- 간접 접근 -> object.getOwnPropertyDescriptor(객체, 키) -> 프로퍼티 디스크립터 객체 반환(프로퍼티 어트리뷰트의 정보 제공)

## 데이터 프로퍼티

- 키, 벨류 값으로 구성
- value, writable, enumerable, configurable 프로퍼티 어트리뷰트를 가짐

## 접근자 프로퍼티

- 자체적 값X, 데이터 프로퍼티 값 읽거나 저장할 때 호출됨
- get, set, enumerable, configurable
- 데이터 프로퍼티 안에 있는 프로퍼티 -> 접근자를 통해 값을 읽거나 저장할 수 있음

=> 둘 구분 어떻게?

- object.getOwnPropertyDescriptor가 반환한 디스크립토 객체 확인

## 프로퍼티 정의?

- 프로퍼티 정의할 때 프로퍼티 어트리뷰트 선택 가능! (Object.defineProperty)

  > enumerable: false => 열거X(for ...)
  > writable: false => 값 변경X
  > configurable: false => 삭제X, 재정의X

- Objec.defineProperty로 프로퍼티 정의시 일부 어트리뷰트 생략가능

## 객체 변경 방지

- 객체는 변할 수 있는 값이기 때문에 변경 방지하는 메서드가 있음!
  > 확장X(객체확장X): Object.preventExtensions: 추가 금지(2가지: 동적, defineProperty), 삭제는 가능
  > 재정의X(객체밀봉): Object.seal -> 읽기와 쓰기만 가능
  > 읽기만 가능(객체 동결): Object.isFrozen
  > 중첩객체 동결(불변 객체): 재귀적 Object.freeze

## 정리 & 배운것

- 프로퍼티는 프로퍼티 상태를 나타내는 어트리뷰트를 가지고 있고 개발자는 그것을 원하는 대로 설정 가능 => 객체를 만들 때 원하는 대로 옵션을 선택할 수 있다!
- 마치, 스타크래프트에서 커세어는 공중 공격만 가능하고, 벌쳐는 지상 공격만 가능하다. 질럿은 근거리 공격만 되고, 마린은 원거리, 공중 다됨. 게임 유닛의 속성을 다르게 만들었듯이 객체도 속성을 다르게 설정 가능하다!

220527

# 17장: 생성자 함수에 의한 객체 생성

## 객체 생성 방식

1. 객체 리터럴로 생성

- 문제
  - 동일한 프로퍼티를 가진 객체를 여러 개 생성해야하는 경우 비효율적

2. new 연산자(생성자 함수)로 생성

- 장점
  - 프로퍼티 구조가 동일한 객체를 여러 개 생성할 때 간편

## 생성자 함수와 인스턴스

> 인스턴스 생성 과정

- 생성자 함수 역할
  1. 인스턴스 생성하기 위한 템플릿 역할
  2. 인스턴스를 초기화 하는 역할(프로퍼티 추가 or 초기값 할당)
- 생성자 함수를 호출하면 암묵적으로 인스턴스 생성 후 반환

1.  인스턴스와 this 바인딩

- 빈 객체가 생성되는데 그것은 인스턴스이다.
- 인스턴스는 this에 바인딩 된다.

2. 인스턴스 초기화

- 프로퍼티 추가 및 생성

3. 인스턴스 반환

- 암묵적으로 인스턴스가 바인딩된 this를 반환

`생성자 함수 내부에서는 return 생략!`

## 내부 메서드

- 함수는 객체이고 객체의 내부슬록과 내부메서드를 가지고 있다.
- 그리고 함수는 `[[Call]]`, `[[Constructor]]]`도 추가로 가지고 있는데
- 일반 함수는 호출 가능하기 때문에 call을 항상 가지고 있고 constructor는 선택

> constructor 구분

- constructor -> 함수 선언문, 함수 표현식, 클랙스
  ```
  // 함수 선언문
  function sum(a, b) {
    return a + b;
  }
  ```
  ```
  // 함수 선언문
    function sum(a, b) {
      return a + b;
    }
  ```
- non-constructor -> 메서드, 화살표 함수
  - 프로퍼티로 정의된 함수는 메서드로 인정X(일반 함수)

> new 연산자

    - 일반 함수의 return 문이 있다면 new 연산자로 인스턴스 생성시 빈 객체 반환함
    - 생성자 함수 구분을 위해 보통 생성자 함수는 파스칼 케이스로 명명

> new.target

    - new 연선자로 생성자 함수 호출 -> new.target은 함수 자신을 가리킴
    - 일반 함수로 호출 -> new.target은 undefined
    - 활용 -> new.target으로 new 연산자와 생성자 함수로서 호출했는지 확인 후 재귀 호출로 생성자 함수로서 호출 가능

# 18장: 함수와 일급 객체

## 일급 객체란 무엇인가?!

1. 무명의 리터럴 생성
2. 변수나 자료구조에 저장 가능
3. 함수의 매개변수에 전달 가능
4. 함수의 반환값으로 사용 가능

- 함수는 일급객체!

### 함수와 일반객체와의 차이

1. 함수는 호출 가능하다.
2. 함수 고유의 프로퍼티를 갖는다.

> 함수 고유의 프로퍼티

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

5. **proto** 접근자 프로퍼티


    - 프로토타입 객체에 접근하기 위해 사용하는 접근자 프로퍼티

6. prototype 프로퍼티


    - 생성자 함수로 호출할 수 있는 함수 객체, constructor만 소유하는 프로퍼티