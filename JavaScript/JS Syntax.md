# 자바스크립트 문법

JavaScript 구문은 일련의 규칙이며 JavaScript 프로그램 구성 방법입니다.
```javascript
var x, y, z; // How to declare variables  
x = 5; y = 6; // How to assign values  
z = x + y; // How to compute values
```

## 자바스크립트 값

자바 스크립트 문법은 값의 두가지 타입으로 정의됩니다 : 고정된 값 그리고 변하는 값
고정된 값은 literals 라 불린다. 변하는 값은 variables라 불립니다.

## 자바스크립트 Literals

고정값을 쓰는데 가장 중요한 룰 

숫자는 소수 또는 소수 없이 쓰입니다.
```
10.50  
  
1001
```
문자는 더블 또는 싱글 quotes로 묶여 텍스트형으로 쓰여집니다.
```
"John Doe"  
  
'John Doe'
```

## 자바스크립트 Variables

프로그래밍 언어에서 variables는 저장된 값으로 사용되어집니다.
자바스크립트는 변수를 선언하는데 `var` 키워드를 사용합니다.
equal 사인은 variables에 값을 할당하는데 사용되어집니다.
예제에서 x는 별수로써 정의되이진다. 그 후에 x는 값 6으로 할당됩니다.

```javascript
var x;  
  
x = 6;
```

## 자바스크립트 연산자
자바스크립트는 값을 계산하는데 연산자( `+ - * /` )를 사용합니다.
```
(5 + 6) * 10
```
자바스크립트는 변수에 값을 할당할 때 `=`를 사용합니다.
```
var x, y;  
x = 5;  
y = 6;
```

## 자바스크립트 표현식

표현식은 값을 계산하는 값, 변수 그리고 연산자의 결합입니다.
계산은 평가라고 불립니다.
예를들어, 5*10은 50으로 계산합니다.
```
5 * 10
```

표현식은 물론 변수값도 포함합니다.
```
x * 10
```

값은 숫자와 문자 같은 다양한 타입이 될수 있습니다.
예를 들어, "John" + " " + "Doe" 는 "John Doe"로 나타납니다.
```
"John" + " " + "Doe"
```

## 자바스크립트 키워드
자바스크립트 키워드는 수행되는 액션을 식별하기위해서 사용되어집니다.
`var` 키워드는 브라우저에 변수를 작성하도록 지시합니다.
```javascript
var x, y;  
x = 5 + 6;  
y = x * 10;
```

## 자바스크립트 명령어
모든 자바스크립트 명령문이 "실행"되지는 않습니다.
더블 슬래시(`//`)  뒤 또는 `/* ... */` 사이의 코드는 주석으로 간주됩니다.
명령어는 무시되고 실행되지않게됩니다.
```javascript
var x = 5; // I will be executed  
  
// var x = 6; I will NOT be executed
```

## 자바스크립트 식별자

식별자는 이름입니다.
자바스크립트에서 식별자는 변수의 이름(그리고 키워드, 그리고 함수, 그리고 라벨)으로 사용됩니다.
이름 규칙은 대다수의 프로그래밍 언어와 같습니다.
자바스크립트에서 변수의 첫번째는 문자 또는 `_` 또는 `$`만 가능합니다.
후속 문자는 문자, 숫자, 밑줄 또는 달러 기호 일 수 있습니다.

> *숫자는 첫번째 문자로 오면 안됩니다.*
> *이런 방법으로  자바스크립트는 식별자를 숫자와 쉽게 구별이 가능합니다.*

## 자바는 대소문자를 구별합니다.

모든 자바스크립트 식별자는 대소문자를 구별합니다.
`lastName` 그리고 `lastname`의 변수들은 두개의 다른 변수입니다.
```javascript
var lastname, lastName;  
lastName = "Doe";  
lastname = "Peterson";
```

## 자바스크립트와 케멜 케이스

역사적으로 프로그래머들은 여러 단어를 하나의 변수 이름으로 결합하는 다른 방법들로 사용해 왔습니다.

**Hyphens :**
firs-name, last-name, master-card, inter-city

**Underscore :**
first_name, last_name, master_card, inter_city

**Upper Camel Case(Pascal Case) :**
FirstName, LastName, MasterCard, InterCity

**Lower Camel Case :**
자바스크립트 프로그래머들은 첫번째 문자를 소문자로 사용하는 camel case를 사용하는 경향이 있습니다. 
firstName, lastName, masterCard, interCity

## 자바스크립트 문자 셋

자바스크립트는 유니코드 문자 셋을 사용합니다.
유니코드는 세계의 모든 문자, 문장 부호 및 기호를 (거의) 다룹니다.

참고 : [w3schools 자바스크립트 튜토리얼](https://www.w3schools.com/js/js_syntax.asp)
