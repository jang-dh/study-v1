# Grid 

## Overview


그리드는 테이블 양식안에서 보여지는 데이터를 위한 파워풀 컨트롤이다.
  
데이터 표시 및 조작 방법을 결정하는 페이징, 정렬, 필터링, 그룹화 및 편집과 같은 데이터 작업을 실행하기위한 옵션을 제공합니다. Grid는 jQuery DataSource 컴포넌트 용 Kendo UI를 사용하여 로컬 및 원격 데이터 세트에 대한 데이터 바인딩을 지원합니다.

## 나아가서

  
지원하는 다양한 기능으로 인해 그리드는 Kendo UI 위젯 중 가장 복잡합니다. 작업을 시작하기 전에 더 큰 확신을 얻으려면 다음 개념에 익숙해 져야합니다.

+ **DataSource** -   DataSource는 중요한 Kendo UI 구성 요소 중 하나입니다. 로컬 또는 원격 데이터를 사용하기위한 추상화이며 그리드의 작동 방식을 이해하는 핵심 개념입니다.

+ **Remote CRUD operations** - 이 섹션에서는 Kendo UI DataSource의 HTTP 요청을 통해 데이터를 검색하여 원격 데이터 서비스에 제출하는 시나리오에 대해 자세히 설명합니다.

+ **Remote data binding** - 이것은 서버 필터링, 페이징 및 그리드의 다른 기능에 대한 정보를 제공합니다.

+ **Kendo UI edting functionality** - Grid를 포함한 일부 Kendo UI 위젯의 편집 기능은 Kendo UI MVVM 바인딩을 사용하여 모델에 바인딩 된 특정 편집기 요소 또는 양식으로 구현됩니다.

## Grid 초기화

Grid를 초기화 하기 위해서 아래의 두개의 방법중 하나를 사용하여야 합니다.

+ 빈 \<div> 태그 사용하기
+ HTML 테이블 사용하기

1. 빈 \<div> 태그 사용하기
	- 빈 \<div> 태그로 부터 그리드를 초기화 할때, 모든 그리드 설정이 초기화 스크립트 명령문에 제공되어집니다. 이것은 자바스크립트안에서 그리드의 레이아웃과 설정을 정의해야한다는 것을 의미합니다. 
	```
	// Define the HTML div that will contain the Grid.
    <div id="grid"></div>

    // Initialize the Grid.
    <script>

        $(document).ready(function(){
            $("#grid").kendoGrid({
                columns: [{
                    field: "FirstName",
                    title: "First Name"
                },
                {
                    field: "LastName",
                    title: "Last Name"
                }],
                dataSource: {
                    data: [{
                        FirstName: "Joe",
                        LastName: "Smith"
                    },
                    {
                        FirstName: "Jane",
                        LastName: "Smith"
                    }]
                }
            });
        });

    </script>
	```

2. HTML 테이블 사용하기

	- HTML 테이블에서 그리드를 초기화하면 일부 설정이 테이블 구조 및 요소의 HTML 속성에서 유추 될 수 있습니다. 이것은 테이블의 HTML에서 그리드의 완전한 레이아웃을 정의할수 있다는것을 의미합니다.   
HTML 테이블은 일반적으로 접근성 및 검색 엔진 최적화를 개선하는 데이터로 이미 채워져 있으며 JavaScript가 비활성화되어 있거나 페이지에 JavaScript 오류가 있어도 사용자에게 데이터가 표시되도록합니다.

	- HTML 테이블로 부터 그리드를 초기화 할때, 위젯은 Kendo UI DataSource 인스턴스를 사용합니다. 셀의 내용은 추출되고 아래방법으로 DataSource가 채워집니다.

		1.  해더셀의 내용 또는 해더셀의 data-field 속성들로 부터 DataSource에 있는 데이터 필드의 네임들은 만들어집니다.
		2. 데이터필드의 네임들은 유요한 자바스크립트 식별자여야 합니다. 그러므로, data-field 속성을 사용하길 추천합니다. 그렇지않으면 해더의 셀 내용은 아래의 요구사항을 만나게 됩니다.
			- 공간이 없어야함
			- 특수문자가 없어야함 
			- 첫번째 문자는 문자여야합니다.

  
	- HTML 테이블에서 Grid를 작성하지만 DataSource가 전송 및 원격 조작을 사용하도록 구성된 경우,  테이블이 이미 채워져 있어도 초기그리드 상태에 대한 원격 요청이 수행됩니다. 이 행동은 설계에 의해서 정의 되어졌고 그리드의 MVC wrapper를 사용할때를 제외하고 피할 수 없습니다. 

  
	 -	기존 테이블에서 그리드를 만들면 그리드는 HTML 특성을 통해 정의 할 수있는 다음과 같은 열 설정을 제공합니다. 컬럼의 너비 스타일을 제외하고, 모든 속성들은 \<th> 요소에 적용 되어야만 합니다.

		 - id 속성은 컬럼의 id에 정의합니다.
		 - data-field 속성은 데이터 필드의 네임에 정의합니다.
		 -  각 <\col> 요소에 적용될 때 width 스타일은 열의 너비를 설정합니다.
		 - data-type 속성은 데이터타입을 정의합니다.
		 - data-template 속성은 컬럼 템플릿을 설정합니다.
		 - data-menu 속성은 컬럼 메뉴를 활성화 또는 비활성화합니다.
		 - data-sortable 속성은 정렬을 활성화 또는 비활성화합니다.
		 - data-filterable 속성은 필터링을 활성화 또는 비활성화합니다.
		 - data-groupable 속성은 그룹핑을 활성화 또는 비활성화합니다.
		 - data-index 속성은 열에 대한 0부터 시작하는 숫자 표시기를 정의합니다.

	- \<table> 태그에 있는 HTML 속성들을 통해서 다른 컬럼의 관계된 설정을 정의하는 것은 불가능합니다.  만약 설정을 사용해야만 한다면 위에 속성 설정들을 넘기고 그리드의 자바스크립트 초기화 명령문에서 모든 설정들을 포함시키세요. 선언적인 위젯 초기화를 사용할때 data-columns 속성을 통해서 컬럼 속성을 설정해야하는 것에 주의세요

  
	- 이전 예제와 다음 예제에서 알 수 있듯이 Grid의 클라이언트 객체는 첫 번째 경우 <div>에, 두 번째 경우에는 <table>에 연결됩니다. 그러나 그리드의 생성된 HTML output은 위젯의 설정에 완전히 의존되고 위젯을 초기화되는 방식에 관계없이 항상 동일합니다. 

	```
	    // Define the HTML table with rows, columns, and data.
    <table id="grid">
        <colgroup>
            <col />
            <col style="width:100px" />
        </colgroup>
        <thead>
            <tr>
                <th data-field="title" data-filterable="false">Title</th>
                <th data-field="year" data-type="number" data-template="<strong>#=year#</strong>">Year</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>Star Wars: A New Hope</td>
                <td>1977</td>
            </tr>
            <tr>
                <td>Star Wars: The Empire Strikes Back</td>
                <td>1980</td>
            </tr>
        </tbody>
    </table>

    // Initialize the Grid.
    <script>

        $(document).ready(function(){
          $("#grid").kendoGrid({
            sortable: true,
            filterable: true
          });
        });

    </script>
	```


## 기존 인스턴스 참조

기존의 그리드 인스턴스를 참조하기 위해서

1. jQuery.data() 메소드를 사용하세요.
2.  참조가 설정되면 Grid API를 사용하여 동작을 제어하십시오.
```
var grid = $("#grid").data("kendoGrid");
```

참조 : [Kendo UI 공식 Document](https://docs.telerik.com/kendo-ui/controls/data-management/grid/overview)
