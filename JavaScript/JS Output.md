# JS 출력

## 자바스크립트는 가능성을 보여줍니다.

자바스크립트는 데이터를 여러가지 방법으로 "display" 할 수 있습니다.

* innerHTML을 사용하여 HTML 요소에 쓰기
* document.write()를 사용하여 HTML 출력에 쓰기
* window.alert()를 사용하여 경고 상자에 쓰기
* console.log()를 사용하여 브라우저 콘솔에 쓰기


## innerHTML 사용하기

HTML 요소로 접근하기 위해서 자바스크립트는 `document.getElementById(id)` 메소드를 사용합니다.
`id`속성은 HTML 요소를 정의합니다. `innerHTML` 속성은 HTML 내용을 정의합니다.

```html
<!DOCTYPE html>  
<html>  
<body>  
  
<h1>My First Web Page</h1>  
<p>My First Paragraph</p>  
  
<p id="demo"></p>  
  
<script>  
document.getElementById("demo").innerHTML  =  5  +  6;  
</script>  
  
</body>  
</html>
```

## document.write() 사용하기

테스트 목적으로 `document.write()`를 사용하는 것이 편리합니다.

```html
<!DOCTYPE html>  
<html>  
<body>  
  
<h1>My First Web Page</h1>  
<p>My first paragraph.</p>  
  
<script>  
document.write(5  +  6);  
</script>  
  
</body>  
</html>
```

<br/>

> *HTML 문서가로드 된 후 document.write()를 사용하면 기존의 모든 HTML이 삭제됩니다.*

<br>

```html
<!DOCTYPE html>  
<html>  
<body>  
  
<h1>My First Web Page</h1>  
<p>My first paragraph.</p>  
  
<button type="button"  onclick="document.write(5 + 6)">Try it</button>  
  
</body>  
</html>
```

<br/>

> *document.write() 메소드는 테스트용으로만 사용하세요*

<br/>

## window.alert() 사용하기

데이터를 보여주기위해서 경고 박스를 사용할 수 있습니다.

```html
<!DOCTYPE html>  
<html>  
<body>  
  
<h1>My First Web Page</h1>  
<p>My first paragraph.</p>  
  
<script>  
window.alert(5  +  6);  
</script>  
  
</body>  
</html>
```

`window` 키워드를 생략할 수 있습니다.

자바스크립트 안에서 윈도우 객체는 글로벌 영역의 객체입니다. 이것은 변수들, 속성들, 그리고 메소드들은 기본적으로 윈도우 객체에 속해있다는 것을 의미합니다. 이것은 또한 `window` 키워드를 지정하는것은 선택사항이라는  것을 의미합니다. 

```html
<!DOCTYPE html>  
<html>  
<body>  
  
<h1>My First Web Page</h1>  
<p>My first paragraph.</p>  
  
<script>  
alert(5  +  6);  
</script>  
  
</body>  
</html>
```


## console.log() 사용하기

디버깅할 목적으로 브라우저에 데이터를 보여주기 위해서 console.log() 메소드를 호출할 수 있습니다.

```html
<!DOCTYPE html>  
<html>  
<body>  
  
<script>  
console.log(5  +  6);  
</script>  
  
</body>  
</html>
```

## 자바스크립트 출력

자바스크립트는 출력 객체나 출력 메소드를 가지고 있지 않습니다.
자바스크립트로 부터 출력 장치를 접근할 수 없습니다.
브라우저 안에 현재 윈도우의 내용을 출력하기 위해서 `window.print()`를 호출하여 출력 할 수 있다는 점만 예외입니다. 

```html
<!DOCTYPE html>  
<html>  
<body>  
  
<button onclick="window.print()">Print this page</button>  
  
</body>  
</html>
```
참고 : [w3schools 자바스크립트 튜토리얼](https://www.w3schools.com/js/js_output.asp)
