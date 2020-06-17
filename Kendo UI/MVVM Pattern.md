# MVVM Pattern 

## Overview

Model View ViewModel 은 개발자들을 도와주는 디자인 패턴으로 유저 인터페이스인 뷰로 부터 데이터인 모델을 분리하는 것입니다.

  
MVVM의 View-Model 부분은 View에서 해당 개체를 쉽게 사용할 수 있도록 Model에서 데이터 개체를 노출하는 역할을합니다. Kendo UI MVVM 컴포넌트는 Kendo UI 프레임워크의 레스트 와 함께 완벽하게 통합되는 MVVM 패턴의 구현입니다.

## 시작하기
1. 뷰-모델 객체를 생성함으로써 시작합니다. 뷰-모델은 뷰에서 보여질 데이터들을 나타냅니다. 뷰-모델을 선언하기 위해서 kendo.observable 함수를 사용하고 자바스크립트 객체를 전달합니다.
	```
	var viewModel = kendo.observable({
    name: "John Doe",
    displayGreeting: function() {
        var name = this.get("name");
        alert("Hello, " + name + "!!!");
	    }
	});
	```
2. 뷰를 선언합니다. View는 UI, 즉 HTML 요소 집합으로, View-Model에 바인딩됩니다.  다음 예제에서 입력 값 (텍스트)은 data-bind 속성을 통해 View-Model의 이름 필드에 바인딩됩니다. 필드가 바뀔때, input 값은 바뀐 값으로 업데이트 됩니다. 반대도 역시 가능합니다.  input의 값이 바뀔때, 필드도 업데이트 됩니다. 버튼의 click 이벤트는 data-bind 속성을 통해 뷰모델의 displayGreeting 메소드로 바인딩 되어집니다. 메소드는 유저가 버튼을 클릭할때 실행됩니다.
	```
	<div id="view">
	    <input data-bind="value: name" />
	    <button data-bind="click: displayGreeting">Display Greeting</button>
	</div>
	```
3. 뷰에서 뷰모델로 바인드합니다. kendo.bind 메소드를 호출함으로써 작업이 완료됩니다.

## 데이터-* 옵션을 세팅하기

Kendo UI MVVM 위젯의 구성 옵션 설정 이름 지정 규칙에 대한 자세한 정보는 설정 데이터 옵션의 이름 지정 규칙을 확인하세요. 

아래의 예제는 data-* 옵션을 세팅하는 방법입니다.
```
kendo.bind($("#view"), viewModel);
```

## 바인딩
  
바인딩은 DOM 요소 (또는 위젯) 속성을 View-Model의 필드 또는 메소드에 쌍으로 만듭니다. 바인딩은 양식(value:name)안에 data-bind 속성을 통해 지정됩니다. value 와 click인 두개의 바인드는 앞의 예제에서 사용되었습니다.

Kendo UI MVVM 은 source, html, attr, visible, enabled, 그외 다른 속성으로 바인딩하는 것을 지원한다. data-bind 는 바인딩의 콤마로 분리된 리스트를 포함합니다.(data-bind="value:name, visible:isNameVisible").

Kendo UI MVVM은 또한 중첩된 뷰-모델 필드로 데이터 바인딩을 하는것을 지원합니다.

```
<div data-bind="text: person.name">
</div>
<script>
var viewModel = kendo.observable({
    person: {
        name: "John Doe"
    }
});
kendo.bind($("div"), viewModel);
</script>
```

## 중요 노트

- 숫자 옵션을 문자 옵션으로 설정합니다.  일부 Kendo UI 위젯은 숫자를 나타내는 문자열 옵션을 허용하며 예를 들어 <input data-role = "maskedtextbox"data-mask = "09">와 같이 구문 분석 할 수 있습니다.  이 마스크는 숫자로 구문 분석되며 위젯은 "09"문자열 대신 초기화 방법으로 단일 9 자리를받습니다. 이와 같은 시나리오에서 위젯 옵션은 사용자 정의 MVVM 바인딩과 함께 설정되어야합니다. 

- 바인딩은 자바스크립트 코드가 아닙니다. 바인딩이 자바스크립트 코드와 비슷해보여도 아닙니다. 코드의 <div data-bind = "text : person.name.toLowerCase ()"> </ div> 청크가 유효한 Kendo UI MVVM 바인딩 선언이 아닙니다. View-Model에서 값을 View에 표시하기 전에 처리해야하는 경우 메소드를 작성하여 대신 사용해야합니다.
	```
	<div data-bind="text: person.lowerCaseName"></div>

	<script>
	var viewModel = kendo.observable({
	    person: {
	        name: "John Doe",
	        lowerCaseName: function() {
	            return this.get("name").toLowerCase();
	        }
	    }
	});
	kendo.bind($("div"), viewModel);
	</script>
	```

참조 : [Kendo UI 공식 Document](https://docs.telerik.com/kendo-ui/framework/mvvm/overview?_ga=2.9511922.670891943.1592290666-1650820140.1589955240)
