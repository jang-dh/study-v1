# JavaScript Scope

스코프는 변수의 접근성을 정의합니다.

## 자바스크립트 함수 스코프

자바스크립트에서 스코프의 두가지 타입이 있습니다.
* 로컬 스코프
* 글로벌 스코프
자바스크립트는 함수 스코프를 가지고 있습니다. 각각의 함수는 새로운 스코프를 생성합니다.
스코프는 변수들의 접근성을 정의합니다.
함수안에 정의된 변수들은 바깥의 함수로부터 접근이 가능하지 않습니다.

## 로컬 자바스크립트 변수들
자바스크립트 함수에 선언된 변수들은 함수의 로컬입니다.
로컬 변수는 함수 스코프를 갖습니다. 함수안에서만 접근이 가능합니다.
```javascript
// code here can NOT use carName  
  
function myFunction() {  
var carName = "Volvo";  
  
// code here CAN use carName  
  
}
```
로컬 변수가 그들의 함수안에서만 인식되기 때문에, 같은 이름을 같은 변수들은 다른 기능으로 사용될 수 있습니다.
로컬 변수는 함수가 시작될 때 만들어지고 함수가 끝났을때 삭제됩니다.

## 글로벌 자바스크립트 변수들
함수 바깥에 선언된 변수들은 글로벌이 됩니다.
글로벌 변수는 글로벌 스코프를 가집니다. 페이지에 모든 스크립트들과 함수들은 접근이 가능합니다.

```javascript
var carName = "Volvo";  
  
// code here can use carName  
  
function myFunction() {  
  
// code here can also use carName  
  
}
```

## 자바스크립트 변수들
자바스크립트에서 객체들과 함수들도 변수입니다.

> 스코프는 코드의 다른 부분들로 부터 변수, 객체, 그리고 함수의 접근성을 정의합니다.

## 자동적인 글로벌 
만약 선언없이 변수에 값을 할당 하였다면 자동적으로 글로벌 변수가 됩니다.
이 예제에서 `carName`은 함수내에 할당되어 있어도 글로벌 변수로 여겨집니다.
```javascript
myFunction();  
  
// code here can use carName  
  
function myFunction() {  
carName = "Volvo";  
}
```

## 엄격한 방식
모든 현대의 브라우저는 "엄격한 방식"으로 자바스크립트를 실행하는 것을 지원합니다.

> "엄격한 방식"에서는 선언되지 않은 변수들은 자동적으로 글로벌이 되지 않습니다.

## HTML에서 글로벌 변수들

자바스크립트에서 글로벌 스코프는 완전한 자바스크립트 환경입니다.
HTML에서 글로벌 스코프는 윈도우 객체입니다. 모든 글로벌 변수들은 윈도우 객체에 속해있습니다.

```javascript
var carName = "Volvo";  
  
// code here can use window.carName
```

## 경고
  
의도하지 않는 한 전역 변수를 작성하지 마세요.
글로벌 변수들은 윈도우 변수들로 다시 쓰여질수 있습니다.
어떤 윈도우 객체를 포함하고 있는 어떤 함수는 글로벌 변수와 함수들로 다시 쓰여질 수 있습니다.


## 자바스크립트 변수들의 생명주기

자바스크립트 변수의 생명주기는 정의될 때 시작합니다.
로컬 변수들은 함수가 끝났을 때 삭제됩니다.
웹 브라우져에서 글로벌 변수들은 브라우저 윈도우가 닫혔을때 삭제됩니다.

## 함수 arguments
 함수 arguments는 함수안에 로컬 변수로써 동작합니다.