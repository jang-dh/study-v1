# Templates

## Overview

Kendo UI 템플릿은 Kendo UI 툴킷 내에서 사용하기 쉬운 고성능 JavaScript 템플릿 엔진을 제공합니다.

템플릿은 자바스크립트 데이터와 자동적으로 합쳐질 수 있는 HTML 청크를 생성하는 방법을 제공합니다. 템플릿은 자바스크립트안에서 전통적인 HTML 문자열 작성을 대신합니다.   JavaScript의 전통적인 HTML 문자열 작성을 대체합니다. Kendo UI 템플릿은 일반적인 UI (사용자 인터페이스) 렌더링 시나리오에 필요한 필수 템플릿 기능을 제공하는 데 중점을두고 있으며 기능 과잉 성능에 중점을 둡니다.  Kendo UI 템플릿은 향상된 성능을 위한 편리한 syntax sugar를 교환하여 다른 템플릿 자바스크립트 라이브러리와 구별됩니다.

## 템플릿 문법

Kendo UI 템플릿은 해쉬 템플릿이라고 불리는 간단한 템플릿 문법을 사용합니다. 이 구문에서 # (해시) 기호는 템플릿을 실행할 때 데이터로 대체되어야하는 템플릿의 영역을 표시하는 데 사용됩니다.   # 문자는 템플릿 내에서 사용자 정의 JavaScript 코드의 시작과 끝을 나타내는 데에도 사용됩니다.

해시 구문을 사용하려면 다음 방법 중 하나를 사용하세요
 - HTML로써 값을 렌더링하기 : #= #
 - HTML 인코딩을 사용하여 값을  표기 : #:#
 - 임의의 자바스크립트 코드 실행하기 : # if (true) { # ... non-script content here ... # } 

## 해쉬 문자
-   템플릿에 리터럴 # 문자가 포함되어 있으며 이는 바인딩 표현식의 일부가 아니며 스크립트 코드 마커가 아닌 경우 해당 문자를 이스케이프해야합니다. 그렇지 않으면 템플릿 컴파일 오류가 발생합니다. 예를 들어 #을 하이퍼링크 URL 또는 CSS 컬러 값으로 사용되면 이런일이 발생할 수 있습니다. 자바스크립트 문자열의 #은  \\\\ #를 통해 이스케이프되고 외부 HTML 스크립트 템플릿의 #은  \\ #를 통해 이스케이프됩니다.
-   템플릿에 중첩 된 템플릿의 바인딩 표현식의 일부인 # 문자가 포함 된 경우이 문자도 이스케이프되어야합니다. 이러한 방식으로 문자는 외부 템플리트에서 무시되지만 내부 템플리트에서 올바르게 처리됩니다.

### 행 값 렌더링하기

템플릿에서 값을 그대로 렌더링하려면 다음 예제를 사용하십시오. 데이터로 렌더링 할 준비가 된 컴파일 된 인라인 템플릿을 만듭니다.

```
    var template = kendo.template("<div id='box'>#= firstName #</div>");
```

다음의 예제는 어플리케이션에서 템플릿을 사용하는 모습을 보여줍니다.

```
   <div id="example"></div>
    <script>
        var template = kendo.template("<div id='box'>#= firstName #</div>");
        var data = { firstName: "Todd" }; //A value in JavaScript/JSON
        var result = template(data); /Pass the data to the compiled template
        $("#example").html(result); //display the result
    </script>
```

### HTML 인코더 값 렌더링하기

다음 예제는 템플릿을 통해 템플릿에서 인코딩 된 HTML 값을 렌더링하여 인코딩을 자동으로 처리하는 방법을 보여줍니다.
```
   var template = kendo.template("<div id='box'>#: firstName #</div>");
```

다음 예제는 템플릿이 사용되고 데이터에서 HTML 없이 출력하는 과정을 보여줍니다.

```
    <div id="example"></div>
    <script>
        var template = kendo.template("<div id='box'>#: firstName #</div>");
        var data = { firstName: "<b>Todd</b>" }; //Data with HTML tags
        var result = template(data); //Pass the data to the compiled template
        $("#example").html(result); // display the following string result ("<b>Todd</b>")
    </script>
```

다음 예제는 HTML 인코딩이 사용되지 않았을 경우 출력을 보여줍니다.

```
    <div id="example"></div>
    <script>
        var template = kendo.template("<div id='box'>#= firstName #</div>");
        var data = { firstName: "<b>Todd</b>" }; //Data with HTML tags
        var result = template(data); //Pass the data to the compiled template
        $("#example").html(result); //display "Todd" in a bold font weight
    </script>
```

### 외부 템플릿과 표현식 다루기

다음의 예제는

참고 : [Kendo UI 공식 Document]([https://docs.telerik.com/kendo-ui/framework/templates/overview)
