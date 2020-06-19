# 자바스크립트 소개

자바스크립트가 무엇을 하는지 몇가지의 예제들을 포함하고 있습니다.

## 자바스크립트는 HTML 내용을 바꿀 수 있습니다.

많은 자바스크립트 HTML 메소드 중 하나는 `getElementById()` 입니다.
이 예제는 HTML 요소 (id="demo"포함)를 찾기 위해 메소드를 사용하여 "Hello JavaScript"로 요소 내용(InnerHTML)을 변경합니다.

```javascript
document.getElementById("demo").innerHTML = "Hello JavaScript";
```

<br/>

> *자바스크립트는 "와 "" 둘다 허용합니다*

<br/>


```javascript
document.getElementById('demo').innerHTML = 'Hello JavaScript';
```


## 자바스크립트는 HTML 속성 값을 변경할 수 있습니다.

이 예제에서 자바스크립트는 \<img> 태그의 src(source) 속성의 값을 변경합니다.

## 자바스크립트는 HTML 스타일을 변경할 수 있습니다.

HTML 요소의 스타일을 변경하는 것은 HTML 속성을 변경하는 변형입니다.

```javascript
document.getElementById("demo").style.fontSize = "35px";
```

## 자바스크립트는 HTML 요소를 숨길 수 있습니다.

HTML 요소를 숨기는 것은 display 스타일을 바꿈으로써 수행될 수 있습니다.

```javascript
document.getElementById("demo").style.display = "none";
```

## 자바스크립트는 HTML 요소를 보여줄 수 있습니다.

숨겨진 HTML 요소들을 보이는 것은 display 스타일을 바꿈으로써 수행될 수 있습니다.

```javascript
document.getElementById("demo").style.display = "block";
```

참고 : [w3schools 자바스크립트 튜토리얼](https://www.w3schools.com/js/js_intro.asp)
