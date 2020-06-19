# 자바스크립트는 어디에 있나

## \<script> 태그

HTML 안에서 자바스크립트 코드는 \<script> 와 \</script> 태그 사이에 삽입됩니다.

```javascript
<script>  
document.getElementById("demo").innerHTML  =  "My First JavaScript";  
</script>
```

## 자바스크립트 함수와 이벤트들

자바스크립트 함수는 자바스크립트 코드의 블록 이빈다. 이것은 호출될 때 실행되어 집니다.
예를 들어 함수는 유저가 버튼을 클릭하는 것 처럼 이벤트가 일어날 때 호출될 수 있습니다.

## \<head> 또는 \<body> 안 자바스크립트

HTML 문서에 원하는 수의 스크립트를 배치 할 수 있습니다.
스크립트는 HTML 페이지의 \<body> 또는 \<head>에 배치 할 수 있습니다. 동시에도 물론 가능합니다.

## \<head> 안의 자바스크립트

이 예제에서  HTML 페이지의 \<head> 섹션안의 자바스크립트 함수가 배치되었습니다.
함수는 버튼을 클릭할 때 호출됩니다.

```html
<!DOCTYPE html>  
<html>

<head>  
<script>  
function  myFunction() {  
document.getElementById("demo").innerHTML  =  "Paragraph changed.";  
}  
</script>  
</head>  
<body>

<h1>A Web Page</h1>  
<p id="demo">A Paragraph</p>  
<button type="button"  onclick="myFunction()">Try it</button>

</body>  
</html>
```

## \<body>안의 자바스크립트

이 예제에서 HTML 페이지의 \<body> 섹션 안에 자바스크립트가 배치 되었습니다. 
버튼을 클릭할 때 함수가 호출됩니다.

```html
<!DOCTYPE html>  
<html>  
<body>  
  
<h1>A Web Page</h1>  
<p id="demo">A Paragraph</p>  
<button type="button"  onclick="myFunction()">Try it</button>  
  
<script>  
function  myFunction() {  
document.getElementById("demo").innerHTML  =  "Paragraph changed.";  
}  
</script>  
  
</body>  
</html>
```

## 외부 자바 스크립트

스크립트는 외부 파일안에 배치할 수 있습니다.

###외부 파일 : myScript.js
```javascript
function myFunction() {  
document.getElementById("demo").innerHTML = "Paragraph changed.";  
}
```

외부 스크립트는 많은 다른 페이지들에서 같은 코드들이 사용될 때 유용합니다.
자바스크립트 파일은 .js 확장자를 갖습니다.

외부 스크립트를 사용하기 위해서 \<script> 태그의 scr(source) 속성안에 스크립트 파일의 이름을 넣어야 합니다.

```html
<script src="myScript.js"></script>
```

원하는대로 <head> 또는 <body>에 외부 스크립트 참조를 배치 할 수 있습니다.
스크립트는 <script> 태그가있는 위치에있는 것처럼 동작합니다.

<br/>

> *외부 스크립트는 \<script> 태그를 포함하지 않습니다.*

<br/>

## 외부 자바스크립트의 이점

외부 파일에 스크립트를 두는 것은 몇가지 장점이 있습니다.

* HTML과 코드를 분리합니다.
* HTML과 자바스크립트를 읽고 유지하기에 쉽습니다.
* 캐시된 자바스크립트 파일은 페이지로드 속도를 높일 수 있습니다.

몇명의 자바 스크립트 파일을 하나의 페이지에 추가하기 위해서 몇몇의 스크립트 태그를 사용하세요

```html
<script src="myScript1.js"></script>  
<script src="myScript2.js"></script>
```

## 외부 참조

외부 스크립트는 현제 웹 페이지에 완전한 URL 또는 상대경로로 참조 될 수 있습니다. 
이 예제는 스크립트를 링크하기 위해서 완전한 URL을 사용합니다.

```html
<script src="https://www.w3schools.com/js/myScript1.js"></script>
```

이 예제는 현재 웹 사이트에 지정된 폴더안에 있는 스크립트를 사용합니다. 
```html
<script src="/js/myScript1.js"></script>
```

이 예제는 현재 페이지와 같은 폴더에 있는 스크립트를 링크합니다.

```html
<script src="myScript1.js"></script>
```

참고 : [w3schools 자바스크립트 튜토리얼](https://www.w3schools.com/js/js_whereto.asp)
