# Data Binding

## Overview

기본적으로 , jQuery를 위한 Kendo UI 그리드는 자동적으로 데이터를 바인드 해줍니다. 

그리드가 생성된 이후에 즉각적으로 DataSource는 쿼리를 보내고 데이터는 위젯에 로드됩니다. 아래와 같이 이 과정을 비활성하려면 위젯의 autoBind 옵션을 false로 설정하세요.
```
$("#grid").kendoGrid({
    autoBind: false,
    // Other configuration.
});
```

## Local Data

Kendo UI 그리드는 데이터의 로컬 배열로 바인드가 가능합니다.
그리드를 로컬 데이터로 바인드하기위해서 KendoGrid 객체의 dataSource 옵션을 설정합니다.
```
var people = [ { firstName: "John",
                 lastName: "Smith",
                 email: "john.smith@telerik.com" },
               { firstName: "Jane",
                 lastName: "Smith",
                 email: "jane.smith@telerik.com" },
               { firstName: "Josh",
                 lastName: "Davis",
                 email: "josh.davis@telerik.com" },
               { firstName: "Cindy",
                 lastName: "Jones",
                 email: "cindy.jones@telerik.com" } ];

 $("#grid").kendoGrid({
     dataSource: people
 });
```

## Remote Data

  
Kendo UI Grid는 템플릿 엔진과 내장 데이터 소스를 제공하여 데이터 바인딩 기능을 빠르게 설정하고 구현할 수 있습니다.

### Getting Started

원격 데이터를 바인드 하기위해서 dataSource 옵션을 지정합니다. 위젯 밖에서 데이터 소스를 만들수 있거나 넘길 수 있습니다. 만약 여러 위젯들이 같은 데이터 설정을 바인드 하려면 다른 위젯에서 참조할수있는 객체와 같은 데이터 소스를 만들어야합니다. 만약 그리드가 데이터로 바인드되는 유일한 아이템이면 인라인으로 만듭니다.

```
$("#grid").kendoGrid({
     dataSource: {
         transport: {
             read: "/Home/People.json"
         },
         schema: {
             data: "data"
         }
     }
});
```

###  Configuring the Data Source

그리드의 데이터 소스를 설정하기 위해서
1. 원격 끝 포인트를 제공해야합니다.
2. 데이터를 추가합니다.
3. 시각화 처리합니다.
4. row 템플릿을 설정합니다.

+ **원격 끝 포인트 제공하기**
	Kendo UI는 원격 엔드포인트를 공급하고 위젯의 dataSource를 정의함으로써 그리드와 함께 인라인으로 사용되어지는 데이터바인딩 프레임워크를 제공합니다. 

	다음 예제는 제안 된 접근 방식을 구현하는 방법을 보여줍니다.
	 -  dataSource는 새로운 Kendo UI DataSource를 생성하여 Grid의 데이터 소스로 할당합니다.
	 -  transport 는 원격 데이터 소스와 통신하는것을 정의합니다.
	 -   URL은 위젯을 바인딩하려는 데이터의 위치를 ​​가리 킵니다.
	 -   데이터에는 원격 엔드 포인트로 전송해야하는 추가 URL 파라미터가 나열됩니다.
	 - dataType은 data source가 기대되어지는 응답형식을 나타냅니다.   JSONP는 차단되지 않고 브라우저 간 요청에서 JSON을 반환하는 방법입니다.   의도적으로 브라우저를 잘못 인도하기 위해 콜백으로 JSON 응답을 래핑합니다.  그러나 포함하는 데이터를 완전히 인식하지 않으면 그렇게하지 않는 것이 좋습니다.
	 - schema는 응답의 스키마가 무엇인지 그리드에 표시합니다.
	 -   데이터는 반복 될 JSON 요소로 기능합니다.이 요소를 기반으로 Kendo UI는 Grid의 각 행을이 요소의 항목에 바인딩합니다. 서버는 데이터를 항목 배열로 리턴하므로 반복 items은 "items"입니다.
	 - model은 데이터의 구조를 나타냅니다. 이것을 사용함으로써 적절한 핸들링을 위한 데이터에 있는 각각의 필드 데이터 타입을 지정하고 또한 필요할때, 유니크한 id 필드를 명쾌하게 정의합니다.

	```
      <div id="grid">
      </div>

      <script>
        $(function() {
          $("#grid").kendoGrid({
            dataSource: {   
              transport: {   
                read: {
                  url: "https://api.flickr.com/services/feeds/photos_public.gne",
                  data: {
                    tags: "nature",
                    format: "json"
                  },
                  dataType: "jsonp", // "jsonp" is required for cross-domain requests; use "json" for same-domain requests
                  jsonp: "jsoncallback",
                }
              },
              schema: {
                data: "items",
                model: {
                  fields: {
                    published: {type: "date"}
                  }
                }
              }
            },
            height: 500,
            scrollable: true,
            selectable: true
          });
        });
      </script>   
	```
	
+ **데이터 추가하기**
이전의 예제는 자동적으로 생성된 컬럼의 그리드와 함께 데이터 항목에 각각 필드를 위한 컬럼과 렌더링합니다.   그리드에 필요한 필드 만 표시하려면 열 목록을 제공하고 서버 응답에서 항목 배열의 어떤 요소가 각 특정 항목에 표시되어야하는지 지정하세요


	다음 예제는 그리드가 응답의 필수 데이터를 표시하도록 열 배열에 field 속성을 지정하는 방법을 보여줍니다. 컬럼들은 컬럼을 위한 좀 더 유저 친화적인 해더 타이틀을 제공하는 title 속성을 가지고 있습니다.
	
	```
   <div id="grid">
    </div>

    <script>
      $(function() {
        $("#grid").kendoGrid({
          dataSource: {   
            transport: {   
              read: {
                url: "https://api.flickr.com/services/feeds/photos_public.gne",
                data: {
                  tags: "nature",
                  format: "json"
                },
                dataType: "jsonp", // "jsonp" is required for cross-domain requests; use "json" for same-domain requests
                jsonp: "jsoncallback",
              }
            },
            schema: {
              data: "items",
              model: {
                fields: {
                  published: {type: "date"}
                }
              }
            }
          },
          columns: [
            {field: "title", title: "Title"},
            {field: "published", title: "Published On"},
            {field: "media", title: "Image"}
          ],
          height: 500,
          scrollable: true,
          selectable: true
        });
      });
    </script>
	```

+ **시각화 처리하기**
	이미지 컬럼에서 이미지를 보여주는 대신에, 그리드는 자바스크립트 객체의 문자열을 렌더링하고 또한 날짜는 유저친화적인 양식으로 나타나지않습니다. 
	
	다음 예제는 이미지에 인라인 템플릿을 사용하여 위젯이 이미지 열을 표시 할 방식을 그리드에 표시하는 방법을 보여줍니다. 날짜는 컬럼의 format 옵션을 사용해서 적절하게 형식화됩니다.

	```
	 <div id="grid">
    </div>

    <script>
      $(function() {
        $("#grid").kendoGrid({
          dataSource: {   
            transport: {   
              read: {
                url: "https://api.flickr.com/services/feeds/photos_public.gne",
                data: {
                  tags: "nature",
                  format: "json"
                },
                dataType: "jsonp", // "jsonp" is required for cross-domain requests; use "json" for same-domain requests
                jsonp: "jsoncallback",
              }
            },
            schema: {
              data: "items",
              model: {
                fields: {
                  published: {type: "date"}
                }
              }
            }
          },
          columns: [
            {field: "title", title: "Title"},
            {field: "published", title: "Published On", format: "{0: MMM dd yyyy HH:mm}"},
            {field: "media", title: "Image", template: "<img height='100' src='#:data.media.m#' title='#: data.title#'/>"}
          ],
          height: 500,
          scrollable: true,
          selectable: true
        });
      });
    </script>
    ```

+ **행 템플릿 설정하기**

	그리드의 열에 대해보다 복잡한 템플릿 (예 : 단일 열의 여러 필드 값)을 표시 할 수 있으며 다른 열의 내용을 반복하여 템플릿 출력을 생성 할 수 있습니다. 이러한 시나리오에서는 하나의 템플릿 안의 모든 행의 구조를 묘사하기위하여 rowTemplate를 사용합니다. 

	다음의 예시는 추가적인 스타일들을 적용함으로써 그리드를 완전히 사용자 정의하는  방법을 보여줍니다. 템플릿의 td요소의 숫자는 그리드 정의안에 컬럼의 숫자와 일치합니다.

	
	```
    <div id="grid">
    </div>
    <script id="detailsTemplate" type="text/x-kendo-template">
        <tr class="row">
            <td>
              <div><span class="strong">Title: </span># if ( title ) { #
                  #= title #
                  # } #
      </div>
              <div><span class="strong">Username: </span>
                #= author #
      </div>
              <div><span class="strong">Published: </span>
                #= kendo.toString(new Date(published), "MMM dd yyyy HH:mm") #
      </div><div><span class="strong">Link: </span>
                <a href='#= link #' target='_blank'>Open</a>
      </div>
      </td>
            <td>
              <div>
                # $.each(tags.split(' '), function(index, data) { #
                <span class="tag">
                  #= data #
                  </span>
      </div>
                # }); #
      </div>
      </td>
            <td>
              <div class="image">
                  <img src="#= media.m #" alt="#= author #" />
      </div>
      </td>
      </tr>
    </script>
    <script>
      $(function() {
        $("#grid").kendoGrid({
          dataSource: {   
            transport: {   
              read: {
                url: "https://api.flickr.com/services/feeds/photos_public.gne",
                data: {
                  tags: "nature",
                  format: "json"
                },
                dataType: "jsonp", // "jsonp" is required for cross-domain requests; use "json" for same-domain requests
                jsonp: "jsoncallback",
              }
            },
            schema: {
              data: "items",
              model: {
                fields: {
                  published: {type: "date"}
                }
              }
            }
          },
          columns: [
            {title: "Info"},
            {title: "Tags"},
            {title: "Image"}
          ],
          rowTemplate: kendo.template($("#detailsTemplate").html()),
          height: 500,
          scrollable: true
        });
      });
    </script>
    <style>
      .row {
        margin-bottom: 20px;
        border-bottom: thin solid black;
      }

      .image {
        text-align: center;
      }

      .tag {
        font-style: italic;
      }

      .tag:hover {
        background-color: lightblue;
      }

      .strong {
        font-weight: bold;
      }
    </style>
	```

참조 : [Kendo UI 공식 Document](https://docs.telerik.com/kendo-ui/controls/data-management/grid/binding/overview)
