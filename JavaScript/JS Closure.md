# JavaScript Closures

JavaScript 변수들은 로컬과 글로벌 스코프에 속해 있습니다.
글로벌 변수들은 closures를 사용하여 로컬로 만들 수 있습니다.

## 글로벌 변수
함수는 함수안에 정의된 모든 변수들을 허용합니다.
```javascript
function myFunction() {  
var a = 4;  
return a * a;  
}
```
그러나 함수는 함수 밖에서도 정의된 변수들을 허용합니다.
```javascript
var a = 4;  
function myFunction() {  
return a * a;  
}
```

마지막 예제에서 a 는 글로별 변수입니다.
웹 페이지에서, 글로벌 변수는 윈도우 객체에 속해있습니다.
글로벌 변수는 페이지안에서 모든 스크립트에 의해 사용될 수 있습니다.
첫번째 예제에서 a는 로컬 변수입니다.
로컬 변수는 정의된 함수안에서만 사용될 수 있습니다. 이것은 다른 함수들이나 스크립트 코드로부터 숨겨져 있습니다.
같은 이름을 갖는 글로벌 그리고 로컬 변수는 다른 변수입니다. 하나를 수정하면 다른 하나는 수정되지 않습니다.

> var, let, or const 없이 생성된 변수들은 함수 안에 있을지라도 항상 글로벌 변수입니다. 

## 변수 생명주기

글로벌 변수는 페이지 다른 페이지로 이동하거나 윈도우가 닫히는 경우 때 까지 살아 있습니다.
로컬 변수는 짧은 생명 주기를 가집니다. 함수가 호출 됐을때 생성이 되고 함수가 끝나면 삭제됩니다.


## 카운터 딜레마

어떤것을 카운트하기 위한 변수를 사용하고 싶고 이 카운터가 모든 함수에게 이용가능하길 원한다고 가정해봅시다.
글로벌 변수를 사용해야하고 카운터를 증가시키는 함수를 사용해야 합니다.
```javascript
// Initiate counter  
var counter = 0;  
  
// Function to increment counter  
function add() {  
counter += 1;  
}  
  
// Call add() 3 times  
add();  
add();  
add();  
  
// The counter should now be 3
```
위에 솔루션에서 문제가 생깁니다 : 페이지에 어느 코드든 add() 호출 없이 카운터를 변경할 수 있습니다.
  카운터는 add () 함수에 대해 로컬이어야하며 다른 코드가 변경하지 못하게해야합니다.
```javascript
// Initiate counter  
var counter = 0;  
  
// Function to increment counter  
function add() {  
var counter = 0;  
counter += 1;  
}  
  
// Call add() 3 times  
add();  
add();  
add();  
  
//The counter should now be 3. But it is 0
```
이것은 작동하지않습니다. 왜냐하면 로컬 카운터 대신 글로벌 카운터가 보이기 때문입니다.
함수가 리턴하도록하여 글로벌 카운터를 제거하고 로컬 카운터에 액세스 할 수 있습니다.

```javascript
// Function to increment counter  
function add() {  
var counter = 0;  
counter += 1;  
return counter;  
}  
  
// Call add() 3 times  
add();  
add();  
add();  
  
//The counter should now be 3. But it is 1.
```

이것도 동작하지않습니다. 함수가 호출될 때 마다 로컬 카운터가 초기화되기 때문입니다.
자바스크립트 inner 함수는 이 문제를 해결 할 수 있습니다.


## 자바스크립트 중첩 함수

모든 함수는 글로벌 범위에 엑세스합니다.
실제로 JavaScript에서는 모든 함수가 "above"범위에 액세스 할 수 있습니다.
자바스크립트는 중첩함수를 지원합니다. 중첩 함수는 "above"범위에 엑세스 할 수 있습니다.
예를들어 inner 함수인 plus()는 카운터 변수에 엑세스 할 수 있습니다.

```javascript
function add() {  
var counter = 0;  
function plus() {counter += 1;}  
plus();  
return counter;  
}
```

  
외부에서 plus () 함수에 도달 할 수 있으면 카운터 딜레마를 해결할 수 있습니다. 
또한 counter = 0을 한 번만 실행할 수있는 방법을 찾아야합니다. 
closure 가 필요합니다.

## 자바크스립트 closure

  
자체 호출 함수을 기억하십니까? 이 함수은 무엇을합니까?
```javascript
var add = (function () {  
var counter = 0;  
return  function () {counter += 1; return counter}  
})();  
  
add();  
add();  
add();  
  
// the counter is now 3

##  설명된 예
add 변수는 자체 호출 함수의 리턴 값이 할당되어집니다.
자체 호출 함수는 한번만 동작합니다. 카운터는 0으로 설정되고 함수 표현식을 리턴합니다.
이런 식으로 add는 함수가됩니다. "멋진"부분은 부모 범위의 카운터에 액세스 할 수 있다는 것입니다.
이것은 자바스크립트 클로져라고 부릅니다. 함수가 프라이빗  변수를 갖길 가능하게 해줍니다.
카운터는 익명 변수들의 영역으로부터 보호되어지고 add 함수만 사용하여 바뀔 수 있습니다.

> closure는 심지어 부모 함수가 끝난 후에도 부모 영역으로 엑세스하는 함수입니다.
