## 제어문

제어문은 조건에 따라 코드 블록을 실행하거나 반복 실행할 때 사용된다.

일반적인 코드는 위에서 아래 방향으로 순차실행되지만 제어문을 사용하면 코드의 실행 흐름을 인위적으로 제어하기에 가독성을 해칠 수 있다.

### 블록문
블록문은 0개 이상의 문을 중괄호로 묶은것으로 코드 블록 또는 블록이라고 부르기도 한다.
자바스크립트는 블록문을 하나의 실행 단위로 취급한다.
블록문은 자체 종결성을 갖기 때문에 끝에 세미콜론을 붙이지 않는다.

### 조건문
조건문의 조건식은 Boolean 값으로 평가되어야 한다.
만약 if문의 조건식이 Boolean값이 아니라면 강제 형변환으로 Boolean값으로 변환된다.
조건에 따라 단순히 값을 결정하여 변수에 할당하는 경우 if...else 문보다는 삼항 조건 연산자가 가독성이 좋다. 

### switch 문

switch문은 주어진 표현식을 평가하여 그 값과 일치하는 표현식을 갖는 case 문으로 실행 흐름을 옮긴다.
```js
const month = 11;
let monthName;
switch(month) {
  case 1: monthName = 'January';
  ...
  case 11: monthName = 'December';
  ...
  default: monthName = 'Invalid month';
}

console.log(monthName); // Invalid month
```
`Invalid month`가 출력된 이유는 break문을 사용하지 않았기 때문이다.
break를 사용하지 않으면 순서대로 진행되어 default 값이 출력된다.

```js
const month = 11;
let monthName;
switch(month) {
  case 1: monthName = 'January';
    break;
  ...
  case 11: monthName = 'December';
    break;
  ...
  default: monthName = 'Invalid month';
}

console.log(monthName); // Invalid month
```

default문에는 break 문을 생략하는 것이 일반적이다.

### 반복문

반복문은 조건식의 평가 결과가 참인 경우 코드 블록을 실행한다.

>반복문을 대체할 수 있는 다양한 기능
배열을 순회하는 forEach 메서드
객체의 프로퍼티를 열거할 때 사용하는 for ...in 문
이터러블을 순회할 수 있는 for ... of문과 같이 대체할 수 있는 기능이 많다.

### continue 문

continue 문은 반복문의 코드 블록 실행을 현 지점에서 중단하고 반복문의 증감식으로 실행 흐름을 이동시킨다. break문처럼 반복문을 탈출하지는 않는다.
```js
var string = 'Hello World';
var search = '1';
var count = 0;

// 문자열은 유사 배열이므로 for문으로 순회할 수 있다.
for (var i = 0; i < string.length; i++){
  if(string[i] !== search) continue;
  count++; // continue 문이 실행되면 이 문은 실행되지 않는다.
}

console.log(count) // 3 . 'l'이 3개이므로 3을 출력한다.
```
위 예제는 다음과 같이 사용할 수도 있다.
```js
for (var i = 0; i < string.length; i++){
  // 'l'이면 카운트 증가
  if(string[i] === search) {
    count++;
  }
}
console.log(count) // 3
```
if문 내에서 실행해야 할 코드가 길다면 들여쓰기가 한단계 더 깊어지므로 continue문을 사용하는 편이 가독성이 더 좋다.
___


> 일반적인 코드는 위에서 아래 방향으로 순차실행되지만,제어문을 사용하면 코드의 실행 흐름을 인위적으로 제어하기에 가독성을 해칠 수 있다.
조건에 따라 단순히 값을 결정하여 변수에 할당하는 경우 if...else 문보다는 삼항 조건 연산자가 가독성이 좋다는 것을 다시 상기하였다.

>**반복문을 대체할 수 있는 다양한 기능**
**배열**을 순회하는 `forEach` 메서드
**객체**의 프로퍼티를 열거할 때 사용하는 `for ...in` 문
**이터러블을 순회**할 수 있는 `for ... of문`과 같이 대체할 수 있는 기능이 많다.


> 알게 된 점
`for ... of` 문이 배열을 순회하는 것이라고 알고 있었는데, 이터러블을 순회한다는 점을 알게 되었다.
제어문을 사용하면 코드의 실행 흐름을 인위적으로 제어하기에 가독성을 해칠 수 있다는 점을 알게 되었다.

>궁금한 점
`continue` 문은 실행을 멈추지 않고 계속 진행하게 만든다고 한다. 서버에 요청을 보낼 때 뭔가 도움되지 않을까? 공부해야겠다.

