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

### 외부 템플릿과 표현식 처리하기

다음 예제는 자바스크립트와 Kendo UI 템플릿을 사용해서 항목 목록을 보여주는 방법입니다.
```
    <script id="javascriptTemplate" type="text/x-kendo-template">
        <ul>
        # for (var i = 0; i < data.length; i++) { #
            <li>#= myCustomFunction(data[i]) #</li>
        # } #
        </ul>
    </script>
```

표현식을 사용하여 외부 템플릿을 사용하려면, 이 정의를 사용하며 값들의 배열을 받는 템플릿을 초기화하세요. 자바스크립트는 템플릿안에 for 루프를 실행하고  각 이름에 대한 HTML 리스트 항목을 생성합니다. 보조적인 전역 자바스크립트 함수는 보여지는동안 각각의 데이터를 조작하는데 사용됩니다.
```
    <div id="example"></div>

    <script id="javascriptTemplate" type="text/x-kendo-template">
        <ul>
        # for (var i = 0; i < data.length; i++) { #
            <li>#= myCustomFunction(data[i]) #</li>
        # } #
        </ul>
    </script>

    <script type="text/javascript">
        // Use a custom function inside the template. Must be defined in the global JavaScript scope.
        function myCustomFunction (str) {
            return str.replace(".", " ");
        }

        // Get the external template definition using a jQuery selector.
        var template = kendo.template($("#javascriptTemplate").html());

        // Create some dummy data.
        var data = ["Todd.Holland", "Steve.Anglin", "Burke.Ballmer"];

        var result = template(data); //Execute the template
        $("#example").html(result); //Append the result
    </script>
```

  
템플릿 표현식 내에 사용자 정의 변수를 정의한 다음 데이터 필드와 동일한 방식으로 출력 할 수 있습니다.
```
    <script id="javascriptTemplate" type="text/x-kendo-template">
        # var myCustomVariable = "foo"; #
        <p>
            #= myCustomVariable #
        </p>
      </script>
```
표현식은 HTML 주석 안에서도 실행됩니다. 
```
<!-- #alert('it is executed!')# -->
```
## 인라인 및 외부 템플릿

템플릿을 정의하기 위해서, 다음의 방식중 하나를 사용합니다.

- 인라인 템플릿 정의하기 : 자바스크립트 문자열을 사용하고 작은 템플릿에 적합합니다.
- 외부 템플릿 정의하기 : HTML 스크립트 블록을 사용합니다. 로직 또는 HTML 마크업을 포함하는 대다수의 큰 템플릿은 외부 템플릿을 사용합니다. 자바스크립트 아닌 HTML 안에 외부템플릿이 있기 때문에 디자이너들이 생성하거나 수정하기 쉽습니다. 

### 인라인 템플릿 생성하기

인라인 템플릿을 생성하기위해서 자바스크립트 문자열을 생성합니다.
```
    var templateString = "Your name is #: myName #";
    var template = kendo.template(templateString);
```

템플릿에 전달 된 데이터에 myName이라는 변수가 포함되어 있으면 템플릿이 작동합니다. 만약 인라인 템플릿이 #을 포함하고 있으면 `var templateString = '<a href="\\#index">#: myName #</a>'; ` 성정으로 이스케이프합니다. 이것은 페이지에서 보여지는 앵커태그를 생성합니다.

```
    <div id="example"></div>

    <script type="text/javascript">
        var templateString = '<a href="\\#index">#: myName #</a>';
        var template = kendo.template(templateString);

        $("#example").html(template({ myName: "Todd" }));
    </script>
```

### 외부 템플릿 생성하기

외부 템플릿은 자바스크립트가 아닌 HTML에 특별한 블록에 만들어집니다. 외부 템플릿을 정의하기 위해서 `text/x-kendo-template` 타입으로 HTML안에 스크립트 블록을 생성해야합니다.
```
    <script type="text/x-kendo-template" id="myTemplate">
        <!--Template content here-->
    </script>
```

  
JavaScript로 초기화 할 때 템플릿 내용을 선택할 수 있도록 외부 템플릿에는 항상 ID가 있어야합니다.
```
    // Extract the template content from script tag.
    var templateContent = $("#myTemplate").html();
    // Compile a template.
    var template = kendo.template(templateContent);
```
  
아래 표시된 것처럼 JavaScript가 Kendo UI 템플리트 구문으로 올바르게 형식화되어 있으면 외부 템플릿 내에서 HTML 및 JavaScript를 추가 할 수 있습니다.
```
    <script type="text/x-kendo-template" id="myTemplate">
        #if(isAdmin){#
            <li>#: name # is Admin</li>
        #}else{#
            <li>#: name # is User</li>
        #}#
    </script>
```
다음 예제는 단순한 경우를 요약한 것 입니다. 
```
    <ul id="users"></ul>

    <script type="text/x-kendo-template" id="myTemplate">
        #if(isAdmin){#
            <li>#: name # is Admin</li>
        #}else{#
            <li>#: name # is User</li>
        #}#
    </script>

    <script type="text/javascript">
        var templateContent = $("#myTemplate").html();
        var template = kendo.template(templateContent);

        //Create some dummy data
        var data = [
            { name: "John", isAdmin: false },
            { name: "Alex", isAdmin: true }
        ];

        var result = kendo.render(template, data); //render the template

        $("#users").html(result); //append the result to the page
    </script>
```

참고 : [Kendo UI 공식 Document]([https://docs.telerik.com/kendo-ui/framework/templates/overview)
