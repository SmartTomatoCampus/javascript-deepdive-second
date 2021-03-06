#브리님

## 변수
메모리 주소에 직접 접근하는 것은 매우 위험하기 때문에 자바스크립트는 주소 직접접근을 허용하지 않는다. 

 변수는 하나의 값을 저장하기 위해 확보한 메모리 공간 자체 또는 그 메모리 공간을 식별하기 위해 붙인 이름이다. 
값의 위치를 가리키는 상징적 이름

## 식별자
코드는 컴퓨터에게 내리는 명령이지만 개발자를 위한 문서이다. 고로 개발자의 의도를 명확히 나타내는 변수명은 매우 중요하다. 
이러한 식별자는 값이 저장되어 있는 메모리주소와 매핑관계이고 이 매핑정보도 메모리에 저장된다.
>변수 이름을 식별자라고 한다.
식별자는 값이 아니라 메모리 주소를 기억하고 있다. 

## 변수 선언
1. 값을 저장하기 위한 메모리 값을 확보
2. 변수 이름과 확보한 메모리 공간의 주소를 연결

변수 선언을 위한 var 키워드

그렇다면, 확보된 메모리 공간은 비어있을까?
답은 ❌ , 확보된 메모리 공간에는 자바스크립트엔진 에 의해 undefined (원시타입 값)가 암묵적으로 할당되어 초기화된다.

즉, 자바스크립트 엔진은 변수 선언을 2단계에 걸쳐 수행한다.
1. 선언단계 : 변수 이름을 등록하여 자스엔진에 변수 존재를 알린다. 
2. 초기화단계 : 값을 저장하기 위한 메모리 공간을 확보하고 undefined 를 할당하여 초기화한다.
* 이 때 초기화란, 변수가 생성되고 최초로 값을 할당하는 것.

초기화를 안하면?
이전에 사용했던 값이 남아 있을 수도 있음 -> 이것을 쓰레기 값이라고 부름.
그렇기에 자동으로 초기화를 시켜주는 var 키워드는 이러한 위험으로부터 안전하다.

변수 이름은 어디에 등록되나?
실행컨텍스트에 등록된다. 실행컨텍스트는 자스엔진이 코드를 실행하기 위해 필요한 환경을 제공하고 관리하는 영역이다.

## 호이스팅
자스 코드는 인터프리터 방식이기 때문에 코드를 순차적으로 읽어나간다. 그렇다면 console 코드에서는 에러가 나야하는데 왜 에러가 나지 않을까?

#### 함수의 선언은 런타임(코드 실행시점) 이전에 일어난다.
소스를 실행하기 전 소스 실행 준비를 하는데 이 때 변수 선언을 포함한 모든 선언문을 소스코드에서 먼저 실행한다.(실행컨텍스트에 가져다두는것임)

이처럼, 마치 변수 선언문이 코드의 최상단으로 끌어올려진 것 처럼 보이는 현상을 호이스팅 이라고 한다.
var 뿐 아니라 let, const, function, class 키워드 모두 호이스팅 된다.

## 값 할당
위의 선언과 다르게 할당은 소스코드가 순차적으로 실행되는 시간인 런타임에 동작한다.

그렇기 때문에 선언과 할당을 한 번에 해도 실질적으로는 두 번의 선언, 할당 과정으로 나누어 실행된다.


#초생님

1. 변수란 값을 저장된 메모리 공간의 이름이다. 
2. 이런 변수에 값을 저장하는 것을 할당, 변수에 저장된 값을 읽는 것을 참조라 한다.
3. 변수 이름은 식별자라고 한다. 식별자는 메모리에 있는 값들을 구분할 수 있는 고유한 이름을 말한다. 식별자는 네이밍 규칙에 맞게 작성하여 의미있는 단어로 짓자.
4. 자바스크립트는 변수의 선언과 할당 시점이 다르다.
    자바스크립트는 런타임이전에 코드의 모든 선언문을 찾는다. 그 후에 변수의 값을 초기화 한다. 
    이와 같은 특성 때문에 변수 선언문 이전에 var 키워드로 선언된변수를 참조한다면 참조에러가 아닌 undefined 가 출력된다.
이를 변수 호이스팅 이라고 한다.
그래서 자바스크립트는 변수의 선언과 할당 시점이 다르다는 것!을 잘 기억해두면 좋을거 같읍니다

#클로버
코드가 실행될때마다 데이터의 값이 저장되는 메모리 주소가 랜덤하게 변하기 때문에 
기억하고 싶은 데이터를 재사용하기 위해 변수라는 메커니즘을 사용한다.
데이터를 정리하는 일종의 수납상자 라고 이해했다.

var의 단점으로는 재선언, 재할당이 모두 가능하여 협업에 문제점을 야기할 수 있다.
따라서 var의 사용은 지양하는 편이 좋다.

변수를 선언한 이후 값을 할당하지 않으면 확보된 메모리 공간에 undefined라는 값이 할당되어
초기화된다. 초기화 되지 않으면 다른 애플리케이션이 사용했던 값이 남아 결과에 문제가 
생길 수 있기 때문이다

자바스크립트 코드는 인터프리터에 의해 한 줄씩 순차적으로 실행되므로 소스코드보다 밑에 있을때
참조에러가 뜰 것이라고 생각되어지지만 변수 선언은 소스코드가 순차적으로 실행되는 런타임 이전에
먼저 실행되기 때문에 소스코드의 위치와는 상관없이 참조가 가능하다. 변수 선언문이 코드의 맨 선두로
끌어 올려진 것처럼 동작하는 자바스크립트의 특징을 호이스팅이라 한다.
변수 선언뿐 아니라 var let 등과 같은 식별자는 모두 호이스팅 된다.

자바스크립트에서는 일반적으로 변수나 함수의 이름은 카멜케이스를 사용하고 생성자 함수,클래스의
이름은 파스칼 케이스를 사용한다. 생성자 함수란 new 연산자와 함께 호출하여 객체를 생성하는 함수를 말한다.

#명성
컴퓨터는 기억과 연산을 따로 처리한다. 저장할 때 사용하는 메모리는 메모리 셀 하나의 크기는 1바이트이며 1바이트 단위로 데이터를 저장하거나 읽어들인다.

Memory의 구성
Memory address, Memory cell, 그리고 Memory cell의 집합인Memory


Memory 주소
Memory의 크기만큼 16진수로 생성된다.
컴퓨터는 모든 데이터를 2진수로 처리한다.
따라서 메모리에 저장되는 데이터는 데이터의 종류(숫자,텍스트,이미지,동영상 등)와 상관없이 모두 2진수로 저장된다.

 값이 저장되는 위치 ?
값이 저장되는 위치는 특별히 지정되어 있는 것이 아니며, 임의의 메모리 주소에 저장된다. 그리고 그 값은 2진수로 저장된다.



 메모리 주소를 통해 값에 접근할 수 있을까? 
메모리 주소를 통해 값에 직접 접근하는 것은 매우 위험하기에 자바스크립트 엔진은 직접적인 메모리 접근을 허용하지 않는다.
또한 값이 저장되는 위치는 예측이 불가능하다. 
그렇기 때문에 프로그래밍 언어는 재사용이 필요한 값에 대해 변수라는 메커니즘을 제공한다. 
변수는 컴파일러/인터프리터에 의해 값이 저장된 메모리 공간의 주소로 치환되어 실행하면서, 안전하게 값에 접근할 수 있게 한다. 
객체,배열 같은 자료구조를 사용한다면 여러 값을 하나로 그룹화하여 하나의 값처럼 사용할 수도 있다.


 식별자와 값의 Mapping relation
식별자는 값이 저장되어 있는 메모리 주소와 매핑 관계를 맺으며 매핑에 관한 정보도 메모리에 저장된다.
중요한 점은 식별자는 값이 아니라 메모리 주소를 기억하고 있다는 점이다. 
식별자는 메모리 주소에 붙인 이름이다.
식별자는 변수,함수,클래스 등 메모리 상에 존재하는 값을 식별할 수 있는 이름은 모두 식별자라고 부른다.

 실행 컨텍스트와 호이스팅 
모든 식별자는 실행 컨텍스트에 등록된다.
실행 컨텍스트는 자바스크립트 엔진이 소스코드를 평가하고 실행하기 위해 필요한 환경을 제공하고 코드의 실행 결과를 실제로 관리하는 영역이다.
자바스크립트 엔진은 실행 컨텍스트를 통해 식별자와 스코프를 관리한다.
변수 이름과 변수 값은 실행 컨텍스트 내에 키/값 형식인 객체로 등록되어 관리된다.



 자바스크립트는 코드를 순차적으로 실행한다. 
실행문이 선언문보다 먼저 나왔을 때 참조 에러가 아닌 undefined가 출력되는 것은 변수의 선언이 런타임 이전의 평가 과정에서 먼저 실행되기 때문이다.
평과 과정에서 모든 선언문을 소스코드에서 찾아 먼저 실행된다.

자바스크립트 코드는 인터프리터에 의해 한 줄씩 순차적으로 실행된다. 


 호이스팅 
선언문이 코드의 선두로 끌어 올려진 것처럼 동작하는 자바스크립트 고유의 특징을 변수 호이스팅이라 한다.
 var,let,const,function,function*,class 키워드를 통해 선언하는 모든 식별자는 호이스팅된다.


 변수 선언과 값의 할당은 다르다 
변수 선언은 코드가 순차적으로 실행되는 시점인 런타임 이전에 먼저 실행되지만 값의 할당은 소스코드가 순차적으로 실행되는 시점인 런타임에 실행된다.
값의 할당은 변수 선언으로 초기화가 진행되어 undefined가 저장되어 있는 메모리 공간을 지우고 메모리 공간에 할당하려는 값을 새롭게 저장하는 것이 아니라 새로운 메모리 공간을 확보하고 그곳에 할당하려는 값을 저장한다.

 값의 재할당 
재할당은 현재 변수에 저장된 값을 버리고 새로운 값을 저장하는 것이다. 
재할당은 변수에 저장된 값을 다른 값으로 변경한다. 
그래서 변수라고 하는 것이다. 
값을 재할당할 수 없어서 변수에 저장된 값을 변경할 수 없다면 상수라 한다.

 가비지 컬렉터 
초기화 값 undefined나 새로운 값이 할당되고 버려진 값은 가비지 콜렉터에 의해 처리된다. 단 메모리에서 언제 해제될지는 예측할 수 없다.

