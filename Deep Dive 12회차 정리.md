# 전역 변수의 문제점 & let const 키워드와 블록 레벨 스코프

## 초생
전역 변수를 반드시 사용해야할 이유를 찾지 못한다면 지역 변수를 사용해야 한다. 
왜 전역 변수를 쓰면 안되냐?
1. 모든 코드가 전역 변수를 참조하고 변경할 수 있어서 가독성이 나쁘고 상태 변경이 될 수있는 변수가 너무 많다.
2. 생명주기가 너무 길다. 그래서 메모리 낭비가 심할 수도
3. 스코프 체인 상에서 최상단에 존재하기 때문에 검색 속도가 느리다.
4. 소속을 알 수가 없다. 자바스크립트 애플리케션은 하나의 전역 스코프를 공유하는데 다른 파일 내에 동일한 이름의 전역 변수나 함수가 있다면 오류 날수도

그래서 얘를 어떻게 하면 안 쓸수 있냐?
1. 즉시 실행함수로 묶는다. 어쨋든 함수 안에 실행하면 지역변수가 되기 때문에 전역 함수로 선언 안 할 수 있다. => 근데 이거 약간 억지 아닌지
2. 객체 하나 만들어서 프로퍼티로 추가하기
3. 캡슐화해서 모듈로 묶는다. => 젤 좋은 방법같긴함

앞에서 계속 var로 선언한 건 중복 선언이 된다 어쩌고 저쩌고 있었다. 
var 로 선언시 문제점이 있기 때문이다. 
1. 중복 선언이 된다. =>사실 이게 말이 안됨
2. 함수레벨 스코프 => 사실 얘도 좀
3. 변수 호이스팅 

그래서 보안되서 나온게 let이랑 const
let은
1. 중복 선언 금지
2. 블록레벨 스코프
3. 변수 호이스팅이 일어나지 않는 것 처럼 동작 자바스크립트 엔진이 런타임 이전에 변수 선언문만 쏙쏙 골라가서 미리 이런게 있구나 알아두기 때문에 있는 건 알음 근데 초기화 단계까지 없는 것 처럼 취급하는 거임
const
1. 상수 선언하려고 있는 거 그래서 선언과 동시에 무조건 초기화를 해줘야 한다.
2. 재할당 금지
3. 재할당이 금지된거지 불변을 의미하는게 아님

## 경찬
Var 문제
- 암묵적 결함: 모든 코드가 전역 변수를 참조하고 변경할 수 있음
  -> 1. 변수의 유효범위가 크면 가독성이 나빠짐
  -> 2. 의도치 않은 상태 변화가 발생할 수 있음
- 긴 생명 주기
  -> 1. 메모리 리소스를 오랜 기간 잡아먹는다.(브라우저 상에서는 브라우저가 닫힐 때까지)
  -> 2. var는 특히 재할당이 가능하기 때문에 의도와는 다르게 값이 바뀔 수 있다.
- 스코프 체인 상 종점에 존재
  -> 변수 검색 시 가장 마지막에 검색됨
- 네임스페이스 오염
  -> 파일이 분리되어 있어도 하나의 전역 스코프 공유하기 때문에 문제 발생 가능성 있음 *

전역 변수의 안쓰려면..!
1. 즉시 실행 함수
   -> 모든 코드를 즉시 실행 함수로 감싸면 변수를 지역변수로 만들 수 있다.
2. 네임스페이스 객체
   -> 객체 안에 객체를 만들어 계층적으로 구성, 스코프를 줄일 수 있다.
   but, 네임스페이스 객체 자체가 전역 변수에 할당되므로 그닥.
3. 모듈 패턴 like 클래스
   변수와 함수를 모아 즉시 실행 함수로 감싸서 모듈을 만듦
- - 전역 변수의 억제 + 캡슐화
var
- 변수의 중복 선언 허용
- 함수 레벨 스코프(지역변수로 할당시) -> 함수 이외에선 전역변수로
let
- 변수 중복 선언 금지 -> 같은 스코프 내 중복선언X
- 모든 코드블록을 지역스코프로 인정
- 호이스팅 발생X 처럼?! -> '선언단계', '초기화단계' 분리 -> 스코프 시작부터 초기화 이전까지 사용X
- 전역 객체(window) 프로퍼티X
const
- 상수 선언 위해서
- const는 선언과 초기화 동시에
- 재할당X -> 원시 값 할당시 값 바뀌지 않음, 코드 가독성도 상승(의미부여)
- 객체는 값 변경 가능(참조형 데이터이기 때문에)

## 경택
전역 변수의 문제점

- 변수는 생성되고 값을 할당 받으면서 메모리에 저장되게 되는데 변수가 생성되어 소멸하기 까지 주기가 길다면 그만큼 메모리를 불 필요하게 오래 차지하고 있는 것이다.

전역 변수와 지역 변수

- 지역 변수는 var은 함수레벨 스코프를 따라서 함수스코프가 끝나면 소멸하고, let과 const는 블록레벨 스코프를 따라 블록스코프가 끝나면 소멸한다. (클로저의 경우 소멸하지 않는 경우도 있다.)
- 지역 변수는 함수가 호출 된 직후에 호이스팅이 일어나 함수의 코드가 실행되기 전에 선언되고 undefined가 할당된다. 함수 코드가 실행되다가 할당문을 만나면 할당이 이루어진다.

전역 변수 사용을 자제해야 하는 이유

- 전역 변수는 호출 없이 실행되고 (처음부터 메모리를 차지), 전역은 따로 종료문이 없으므로 코드가 다 끝날 때 까지 메모리를 차지하게 된다. → 긴 생명주기
- 어디서든지 참조하고 변경할 수 있어서 의도치 않게 값이 변경 될 수 있고 가독성이 나빠질 수 있다. → 암묵적 결합
- 변수를 검색 할 때 전역이 스코프 체인 상 마지막이기 때문에 검색할 때 속도가 가장 느리다.
- 파일이 분리되어 있더라도 하나의 전역 스코프를 공유한다는 자바스크립트의 문제점 때문에 의도치 않은 에러를 발생시킬 수 있다. → 네임스페이스 오염
→ 이 문제를 해결하기 위해 나온것이 ES6 문법의 module이다. ES6의 모듈은 파일 자체의 독자적인 모듈 스코프를 제공하고 그렇기 때문에 window 객체의 프로퍼티도 아니고 전역 변수가 아니다.
- 전역 변수가 아니라는 것이 다른 파일에서만 참조할 수 없다는 것인가요?
- 생명 주기가 코드 끝날 때 까지 유효한 것은 같은가요?
⇒ 변수의 스코프는 좁을 수록 좋다고 하고 전역 변수를 꼭 사용해야 할 때가 아니라면 지역 변수를 사용하도록 한다.

var의 특징(문제점)

- 중복 선언 허용
→ 같은 스코프 내에서 중복 선언을 허용한다. 중복 선언 시 초기화 문의 유무에 따라 초기화 문이 있다면 var 키워드가 없는 것 처럼 동작하고 초기화 문이 없는 변수 선언문은 무시된다.
- 함수 레벨 스코프
→ var 변수는 오직 함수의 코드 블록만을 지역 스코프로 가져 함수 외부에서 선언 할 경우 전역 변수가 된다.
- 변수 호이스팅
→ var 변수는 선언문 이전에 참조하더라도 변수 호이스팅이 일어나 에러가 나지 않는다. var 변수의 선언문은 런타임 이전에 호이스팅이 일어나 코드의 선두로 끌어 올려진 것 처럼 작동하고 undefined가 할당된다. 그 후 할당문을 만나면 값이 할당된다. ⇒ 가독성을 떨어뜨리고 오류의 여지를 남긴다.

let의 특징

- 같은 스코프 내에서 중복 선언이 금지된다.
- 블록 레벨 스코프
→ var 변수와 다르게 모든 코드 블록을 지역 스코프로 인정하는 블록 레벨 스코프를 따른다.
- 변수 호이스팅
→ let 변수는 선언 단계와 초기화 단계가 분리되어 진행되며 선언 단계는 똑같이 런타임 이전에 진행되지만 초기화 단계는 선언문을 만나면 이루어진다. 즉 초기화 이전에 (선언문을 만나기 전에) 변수를 참조하려 하면 에러가 발생하고 선언 단계와 초기화 단계 사이의 구간을 TDZ (Temporal Dead Zone) 이라 한다.
- let 전역 변수는 보이지 않는 개념적인 블록에 존재하게 된다.
→ 실행 컨텍스트에 자세히 나온다고 한다.

const의 특징

- 선언과 초기화를 같이 해야 한다.
- 재할당 금지

→ var, let 과 달리 재할당이 금지되어 있어 변수에 원시 값을 할당 해 상수로 사용할 수 있다.

(원시값은 변경 불가능 한 값이므로 const와 만나면 바꿀수 없다) 
그러나 const로 선언한 변수에 객체를 할당했을 경우 객체는 참조 타입이므로 값이 변경 가능하다. 

정리


ES6를 사용한다면 var 변수는 사용하지 않는 것이 좋고 const를 먼저 사용하고 재할당이 필요한 경우에 let으로 바꿔 사용한느 것이 좋다고 한다

## 명성
지역 변수는 함수가 호출되기 이전까지는 생성되지 않는다.
함수를 호출하지 않으면 함수 내부의 변수 선언문이 실행되지 않기 때문이다.


let키워드로 선언한 변수는 스코프 시작 지점부터 초기화 단계 시작 지점(변수 선언문)까지변수를 참조할 수 없다.
스코프의 시작지점부터 초기화 시작 지점까지 변수를 참조할 수 없는 구간을
일시적 사각지대(Temporal Dead Zone : TDZ)라고 부른다.

let 키워드로 선언한 전역 변수는 전역 객체의 프로퍼티가 아니다.
 즉 window.foo와 같이 접근할 수 없다.
let 전역 변수는 보이지 않는 개념적인 블록(전역 렉시컬 환경의 선언적 환경 레코드)내에 존재하게 된다.

TDZ로 인해 let 키워드로 선언한 변수는 변수 호이스팅이 발생하지 않는 것처럼 보인다.
let 키워드로 선언한 변수도 여전히 호이스팅이 발생하기 때문에 참조 에러가 발생한다.
(가장 가까운 변수를 찾는 점에서 지역변수를 찾고, 아직 할당문이 실행되지 않은 let 함수를 참조하였고 그에 맞는 에러메시지가 출력 됨.)

자바스크립트에서는 ES6에서 도입된 let, const를 포함해서 모든 선언을 호이스팅한다.
단 ES6에서 도입된 const,let,class를 사용한 선언문은 호이스팅이 발생되지 않은 것처럼 동작한다.

const 키워드는 재할당을 금지할 뿐 "불변"을 의미하지는 않는다.
새로운 값을 재할당 하는 것은 불가능하지만, 프로퍼티의 동적 생성,삭제, 프로퍼티 값의 변경을 통해 객체를 변경하는 것은 가능하다.
이때 객체가 변경되더라도 변수에 할당된 참조 값은 변경되지 않는다.


지역 변수의 생명 주기는 함수의 생명 주기와 일치한다.
하지만 누군가가 메모리 공간을 참조하고 있으면 해제되지 않고 확보된 상태로 남아 있게 된다.

## 클로버
변수 호이스팅은 전역변수에 한에서 실행되는 것이다. 지역변수는 함수호출시 생성, 함수 종료시 소멸됨.

선언된 지역변수는 함수가 생성한 스코프에 등록된다. 대부분의 지역변수는 함수의 종료시에 소멸되기는 하지만 예외적으로 함수가 종료 되었을때도 스코프를 참조하고 있다면 등록된 지역변수 역시 스코프가 소멸되지 않고 있으므로 소멸되지 않는다.

@@@@@@@@여기서 질문: 지역 스코프가 참조되는 예시는 무엇인가? 말이 이해가 안됨.

function name (){...code};
name(); 이렇게 호출되고 종료 됐을때 지역변수가 사라지는게 아니라

var A = function(){...let b; } 이렇게 함수가 변수에 할당되어 참조될때 지역스코프가 살아있다는 의미인가요?


호이스팅은 변수 선언이 스코프의 선두로 끌어 올려진 것처럼 동작하는 자바스크립트의 특징이다.
지역변수는 지역스코프의 맨 위 상단으로 끌어올려짐
전역변수는 전역스코프의 맨 위 상단으로 끌어올려짐


var 키워드로 작성한 전역변수는 전역객체의 프로퍼티 값이다.
전역객체: 전역객체는 코드가 실행되기 이전 단계에 자바스크립트 엔진에 의해 어떤 객체보다도 먼저 생성되는 특수한 객체이다. 전역객체는 브라우저 환경에서는 window, 서버 환경에서는 global 객체를 의미한다. 이렇게 환경에 따라 전역객체를 가리키는 식별자가 다양했지만 ES11에서 globalThis로 통일되었다.

전역변수의 단점

암묵적 결합: 재선언 재할당 될 수 있기 때문에 코드의 손상의 위험도가 높아짐

긴 생명주기: 전역변수는 전역객체와 수명이 같기 때문에 메모리 리소스 비용이 커진다.
스코프 체인 상에서 종점에 존재: 참조시에 가장 마지막 순서이기 때문에 속도가 느려진다.

네임스페이스 오염: 파일이 분리되어 있더라도 전역 스코프를 공유한다. 따라서 전역변수의 이름이 겹칠경우 오류가 생길 수 있음.

---
전역변수 사용 억제방법: 즉시 실행함수로 모든 코드롤 감싸기, 네임스페이스 역할을 할 객체를 생성하고 전역변수처럼 사용하고 싶은 변수를 프로퍼티로 추가하기, 모듈패턴 사용하기, ES6 모듈 사용

모듈패턴: 모듈패턴은 관련이 있는 변수와 함수를 모아 즉시 실행함수로 감싸 하나의 모듈을 만드는 것. 캡슐화 구현 가능.
캡슐화: 프로퍼티와 메서드를 하나로 묶는 것.

==> 객체랑 비슷하다고 이해

ES6 모듈: 이것을 사용하면 전역변수를 사용할 수 없다. 파일자체의 독자적인 모듈 스코프를 제공하기 때문. 브라우저 호환성이 좋지 않아 아직은 잘 사용되지 않음. Webpack등의 모듈 번들러를 사용하는 것이 일반적.
var 키워드로 선언된 변수는 오직 함수의 코드 블록만을 지역스코프로 인정한다. 때문에 if문 같은 코드블록 내에서 같은 이름으로 변수가 선언되면 덮어 씌어진다.

var는 재할당 재선언 불가능 함수 레벨 스코프를 지원함, 호이스팅 가능
let은 재선언 불가능 재할당 가능 블록 레벨 스코프 지원, 호이스팅 불가
const는 재선언 재할당 불가능 블록 레벨 스코프 지원, 호이스팅 불가

let이 호이스팅 불가능한 이유는 var는 런타임 이전에 선언과 초기화된 값의 할당 단계가 함께 일어나기 때문에 호이스팅이 가능하지만 let 키워드는 선언 단계와 초기화 단계가 분리되어 진행되기 때문이다.
선언은 런타임 이전에 실행되지만 초기화 값으로 할당 되는 것은 변수 선언문을 만났을때 실행되기 때문이다. 때문에 변수 선언문을 읽기 전에 let 변수를 참조하려고 하면 참조 에러가 난다.

이렇게 let 키워드로 선언한 변수가, 변수 선언문을 만나기 전까지의 구간을 변수를 참조 할 수 없다는 의미의 일시적 사각지대(TDZ)라고 부른다. 이러한 이유때문에 변수 호이스팅이 불가능 한 것처럼 보이는거지 사실은 호이스팅이 되기는 한다.

var 키워드로 선언한 전역변수, 전역함수, 선언하지 않은 변수에 값을 할당한 암묵적 전역은 전역객체 window의 프로퍼티가 된다. 따라서 위의 값을 참조할때는 window가 생략된 것으로 볼 수 있다.

원시값과 상수를 언뜻 생각하면 둘 다 바꿀 수 없는 값. 이렇게 오해하기 쉽지만 원시 값은 말 그대로 변경 불가능 한 값이고, 상수는 재할당이 불가능한거지 재할당만 하지않으면 값을 변경 할 수 있다.
예로 상수에 객체를 할당하면 재할당 없이 객체의 프로퍼티를 변경 할 수 있기때문에 상수에 객체를 할당할 경우 값을 변경할 수 있다.

var는 불확실성이 너무 커서 사용안하는 것이 좋고, let은 재할당하는 경우에만 사용하며 웬만해서는 const를 쓰는것이 좋다.
오늘  일이 생겨서  참여를 못할거 같습니다. 대신 어제 못한 정리본 올립니다.

