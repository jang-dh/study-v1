# CRUD 데이터 작업

Kendo UI DataSource 컴포넌트는 CRUD(생성,읽기,수정,삭제) 데이터 작업을 완전히 지원합니다.

그러니 일부 유저 인터페이스 또는  그리드, 리스트뷰와 같은 다른 Kendo UI 위젯과 반드시 결합되어야 합니다. 아래의 예제는 샘플로 그리드를 사용했지만 설정은 다른 위젯 또는 시나리오를 적용합니다. 

## Transport 설정하기

DataSource 컴포넌트는 로컬 데이터 또는 원격 데이터와 같이 작업할 수 있습니다. 두경우 모두 CRUD 작업은 DataSource의 `transport` 설정에 의해 관리됩니다. `transport`는 미리 정의 된 기능을 실행하거나 특정 이벤트에서 미리 정의 된 URL을 요청하도록 구성 할 수있는 JavaScript 객체입니다.

## 스키마 설정하기

DataSource의 스키마는 여러 데이터 연결 작업을 담당합니다. 

스키마 설정은 다음 필드 및 필드 유형을 정의합니다. 

- `schema.model.fields`에 데이터 필드 타입은 올바른 정렬 및 필터링이 가능하고 숫자 데이터의 숫자 텍스트 상자와 같은 기본 필드 편집기의 사용법이 수정됩니다. 로컬 또는 원격 데이터 시나리오 모두에 대해 `data`를 설정해야만합니다. 모든 데이터 필드가 스트링 타입이고 수정이 불가능할때만 `data`속성은 정의하지않고 넘어갈 수 있습니다.

- `schema.model.id`에 데이터 항목의 `id` 필드는 항목들의 올바른 추가, 편집, 그리고 삭제를 보장합니다. 이 필드는 반드시 데이터 안에 있어야합니다.  로컬 또는 원격 데이터 시나리오 둘다 `id`는 반드시 설정해줘야합니다. 모든 데이터 필드가 스트링 타입이고 수정이 불가능할때만 `id` 속성은 정의하지 않고 넘어갈 수 있습니다.
	
	모델 ID로 사용되는 필드에는 새로운 아이템들을 식별하기위해 DataSource 컴포넌트에서 사용하는 기본값을 가지고 있습니다. 만약 데이터 셋에서 아이템의 값이 기본값과 같다면 그것은 새로운 아이템으로 여기집니다.  필드 유형별 기본값은 다음과 같습니다.
	```
	"string": "",
	"number": 0,
	"date": new Date(),
	"boolean": false,
	"default": ""
	```
	`schema.model.id`에 표시된 필드의 값은 실제 데이터 객체안에 `id` 이름과 함께 필드로 설정되어질 것입니다. `id` 이름을 가진 필드는 DataSource의 필드이며 타입을 위한 기본값 또는 개발자에 의해 공급된 실제데이터로부터가져온 데이터로 채워집니다.

- schema.data에 있는 `key`는 데이터 아이템들을 가리킵니다. 데이터가 객체의 보통 배열 또는 JSON으로 안나타질 때 `key`는 요구됩니다.

## 로컬 CRUD 작업 설정하기

다음 정보는 클라이언트에서 데이터를 이미 사용할 수있는 시나리오 또는 검색 및 제출을 처리해야하고 Kendo UI DataSource가 자체적으로 HTTP 요청을하지 않는 시나리오에 적용 할 수 있습니다.

### 로컬 읽기 작업

편집을 지원하지않고 Kendo UI DataSource 인스턴스를 로컬 데이터로 바인딩해야할 때 `data` 옵션을 사용합니다. 

```
var dataSource = new kendo.data.DataSource({
    data: sampleData
}
```

편집을 사용할 때, `transport` 설정을 사용해야합니다. `data` 옵션은 더이상 필요하지않습니다. `transport`의 `read` 메소드는 로컬 변수를 보내야만하고 사용자정의 AJAX 요청을 만든 후 응답을 전달할 수 있습니다. 

```
var dataSource = new kendo.data.DataSource({
    transport: {
        read: function (e) {
            // On success.
            e.success(sampleData);
            // On failure.
            // e.error("XHR response", "status code", "error message");
        }
    }
}
```

  
read 함수 인수의 success 메소드를 실행하면 DataSource 인스턴스가 채워지고 해당 변경 이벤트가 발생합니다. `error` 메소드를 실행하면 처리할 수 있는 DataSource의 `error` 이벤트가 발생합니다. 

### 로컬 수정 작업

DataSoruce의 `update` 설정 세팅은 함수 인자로서 받아들어진 업데이트된 데이터 아이템을 처리하는 함수를 정의합니다.   기본적으로 `batch`가 비활성화되어 있고 한 번에 하나의 데이터 항목 만 업데이트 할 수있는 경우 업데이트 된 데이터 항목은 `e.data`의 오브젝트로 수신됩니다. 만약 `batch`가 활성화되어 있고 복잡한 데이터 항목들이 수정될 수 있다면, `e.data.models`에 객체 배열로 수신되어집니다. 끝에서 함수 인자의 `success` 또는 `error` 메소드가 실행되어야만 합니다.

```
var dataSource = new kendo.data.DataSource({
    transport: {
        /* the other CRUD settings are omitted for brevity */
        update: function (e) {
            // Batch is enabled.
            // var updateItems = e.data.models;
            // Batch is disabled.
            var updatedItem = e.data;

            // Save the updated item to the original datasource.
            // ...

            // On success.
            e.success();
            // On failure.
            // e.error("XHR response", "status code", "error message");
        }
    }
});
```

### 로컬 생성 작업

생성 함수는 다음의 차이점과 함께 업데이트와 비슷한 루틴을 수행합니다.

-   새로 생성된 데이터 아이템에는 `ID`가 없으므로 함수 스크립트로 추가하거나 원격 서비스에서 리턴해야합니다.
- 새롭게 생성된 데이터 아이템들은 할당된 ID와 함께 `success` 메소드를 반환해야합니다.  그렇지 않으면 DataSource 인스턴스가 잘못된 데이터로 작동하여 후속 데이터 작업이 실패 할 수 있습니다.
- `schema.data` 구성이 설정 된 경우, `success` 메소드는 `read`함수의 `success` 메소드로 보내는 객체로써 동일한 구조를 가진 객체에서 생성된 데이터 아이템을 수신합니다.

```
var dataSource = new kendo.data.DataSource({
    transport: {
        /* the other CRUD settings are omitted for brevity */
        create: function (e) {
            // Batch is disabled.
            // Generate appropriate data item ID and save the new items to the original datasource.
            e.data.my_ID_field_name = 123;
            // ...

            // On success return the new data items with IDs (assuming schema.data is NOT SET).
            e.success(e.data);

            // If schema.data IS SET (for example to "foo"), use the following syntax instead:
            // e.success({"foo": [e.data]});

            // On failure.
            // e.error("XHR response", "status code", "error message");
        }
    }
});
```

### 로컬 삭제 작업

생성과 업데이트와 유사합니다. 삭제 기능은 `e.data`안에 삭제된 아이템들을 수신합니다. 이 함수는 기존의 DataSource에서 제공된 아이템을 제거하고 `success` 또는 `error`를 반환합니다. 

```
var dataSource = new kendo.data.DataSource({
    transport: {
        /* the other CRUD settings are omitted for brevity */
        destroy: function (e) {
            // Remove items from the original datasource by using e.data.

            // On success.
            e.success();
            // On failure.
            // e.error("XHR response", "status code", "error message");
        }
    }
});
```

### 로컬 Transport 에러 처리

만약 `transport` 액션(읽기, 수정, 생성, 삭제)중 하나라도 실패를 하고 난 뒤 각자의 `trasport` 함수에 있는`e.success()` 대신 `e.error()` 실행하여 실패에 대한 정보를 DataSource 인스턴스에게 보내야한다. `error` 메소드는 AJAX 요청 객체, 상태 코드, 사용자 정의 에러메세지 파라미터를 수용한다. 

```
var dataSource = new kendo.data.DataSource({
    transport: {
        read: function (e) {
            // On success.
            // e.success(sampleData);
            // On failure.
            e.error("XHR response", "status code", "error message");
        }
    },
    error: function (e) {
        // Handle error.
        alert("Status: " + e.status + "; Error message: " + e.errorThrown);
    }
});
```

### 예제

다음 예제는 이전의 정보에 기초한 완전한 구현이고 간단한 상품 데이터로 CRUD 작업을 보여줍니다. `original datasource`는 최초에 그리드를 채우는 데 사용된 `sampleData` 변수를 나타냅니다. 모든 데이터 작동들은 이 변수에서  유지되므로 다른곳에서 사용되어지거나 제출될 수 있습니다. 이 예제안에서 보통의 자바스크립트 배열대신 `ObservableArray`사용을 피하세요. Kendo UI DataSource는 제공된 보통의 배열을 래핑하고 자동적으로 `ObservableObjects`의 콜렉션으로 변형시킬 것입니다. 

```
    <style>html { font: 12px sans-serif; }</style>

    <div id="grid"></div>

    <script>
        var sampleData = [
            {ProductID: 1, ProductName: "Apple iPhone 5s", Introduced: new Date(2013, 8, 10), UnitPrice: 525, Discontinued: false, UnitsInStock: 10},
            {ProductID: 2, ProductName: "HTC One M8", Introduced: new Date(2014, 2, 25), UnitPrice: 425, Discontinued: false, UnitsInStock: 3},
            {ProductID: 3, ProductName: "Nokia 5880", Introduced: new Date(2008, 10, 2), UnitPrice: 275, Discontinued: true, UnitsInStock: 0}
        ];

        // Custom logic start.
        var sampleDataNextID = sampleData.length + 1;

        function getIndexById(id) {
            var idx,
                l = sampleData.length;

            for (var j=0; j < l; j++) {
                if (sampleData[j].ProductID == id) {
                    return j;
                }
            }
            return null;
        }

        // Custom logic end.
        $(document).ready(function () {
            var dataSource = new kendo.data.DataSource({
                transport: {
                    read: function (e) {
                        // On success.
                        e.success(sampleData);
                        // On failure.
                        //e.error("XHR response", "status code", "error message");
                    },
                    create: function (e) {
                        // Assign an ID to the new item.
                        e.data.ProductID = sampleDataNextID++;
                        // Save data item to the original datasource.
                        sampleData.push(e.data);
                        // On success.
                        e.success(e.data);
                        // On failure.
                        //e.error("XHR response", "status code", "error message");
                    },
                    update: function (e) {
                        // Locate item in original datasource and update it.
                        sampleData[getIndexById(e.data.ProductID)] = e.data;
                        // On success.
                        e.success();
                        // On failure.
                        // e.error("XHR response", "status code", "error message");
                    },
                    destroy: function (e) {
                        // Locate item in original datasource and remove it.
                        sampleData.splice(getIndexById(e.data.ProductID), 1);
                        // On success.
                        e.success();
                        // On failure.
                        // e.error("XHR response", "status code", "error message");
                    }
                },
                error: function (e) {
                    // Handle data operation error.
                    alert("Status: " + e.status + "; Error message: " + e.errorThrown);
                },
                pageSize: 10,
                batch: false,
                schema: {
                    model: {
                        id: "ProductID",
                        fields: {
                            ProductID: { editable: false, nullable: true },
                            ProductName: { validation: { required: true } },
                            Introduced: { type: "date" },
                            UnitPrice: { type: "number", validation: { required: true, min: 1} },
                            Discontinued: { type: "boolean" },
                            UnitsInStock: { type: "number", validation: { min: 0, required: true } }
                        }
                    }
                }
            });

            $("#grid").kendoGrid({
                dataSource: dataSource,
                pageable: true,
                toolbar: ["create"],
                columns: [
                    { field: "ProductName", title: "Mobile Phone" },
                    { field: "Introduced", title: "Introduced", format: "{0:yyyy/MM/dd}", width: "200px" },
                    { field: "UnitPrice", title: "Price", format: "{0:c}", width: "120px" },
                    { field: "UnitsInStock", title:"Units In Stock", width: "120px" },
                    { field: "Discontinued", width: "120px" },
                    { command: ["edit", "destroy"], title: "&nbsp;", width: "200px" }
                ],
                editable: "inline"
            });
        });
    </script>
```

## 원격 CRUD 작업 설정하기

다음 정보는 Kendo UI DataSource에서 작성된 HTTP 요청을 통해 데이터를 검색하여 원격 데이터 서비스에 제출해야하는 시나리오에 적용 할 수 있습니다.

원격 데이터 CRUD 작업은 읽기,수정,생성, 삭제 액션을 수행하기 위해서 서버 코드에 의존합니다. 클라이언트 함수를 구성하는 것 대신에 DataSource의 전송은 원격 서비스 URL과 데이터를 송수신해야하는 예상 형식을 정의합니다. 이론적으로 로컬 데이터를 사용한 이전의 예제와 마찬가지로 `transprot` 함수로 원격 CRUD 작업을 사용할 수 있습니다.  그러나 이것은 드물게 요구되어집니다. 

CRUD 작업 설정의 각각 (읽기,수정,생성,삭제)은 다음과 같이 적절하게 설정해야하는 보통 `transport` 세팅을 제공합니다.

- 클라이언트의 요청 타입은 `get` 또는 `post`가 될 수 있습니다.
- 추가적인 옵션 데이터 파라미터는 필요하에 서버로 보내질 수 있습니다.
- 클라이언트의 요청 그리고 기대된 서버의 반환인 `dataType`은 `json`,`jsonp`,`odata` 등이 될 수 있습니다.
	
### 원격 읽기 작업

DataSource `transport`에 의해 정의된 `read` 서비스는 JSON, JSONP, XML, 또는 oDATA 형식의 데이터를 반환합니다. 기본적으로 기대되어지는 형식은 JSON 입니다. 만약 응답이 객체의 보통 배열이 아니라면 응답의 구조와 데이터가 어딨는지 묘사할 스키마를 정의해야합니다. 

다음 예제는 `read` transport 구성을 사용합니다. 가정된 서버 응답은 객체의 노멀한 JSON 배열입니다.
```
/* Server response:

[{
    "ProductID": 1,
    "ProductName": "Bananas"
},{
    "ProductID": 2,
    "ProductName": "Pijamas"
}]

*/

var dataSource = new kendo.data.DataSource({
    transport: {
        read: {
            url: "service/products/read/",
            type: "post",
            dataType: "json"
        }
    }
});
```
  
다음 예제는 응답 구조가 더 복잡하여 스키마를 사용해야하는 이전 버전의 수정 된 버전입니다. 정의된 `itemCount`는 서버 페이징을 사용하면 일반적으로 반환된 아이템 수와 일치하지 않습니다. 서버 응답은 오직 현재페이지의 아이템만 포함합니다. 그러나 아이템의 전체의 수에 대한 정보를 제공하여 필요하에 올바른 페이지 인터페이스를 생성할 수 있습니다. 

```
/*Server response:

{
    "itemCount": 10,
    "items": [{
        "ProductID": 1,
        "ProductName": "Bananas"
    },{
        "ProductID": 2,
        "ProductName": "Pijamas"
    }]
}

*/

var dataSource = new kendo.data.DataSource({
    transport: {
        read: {
            url: "service/products/read/",
            type: "post",
            dataType: "json"
        }
    },
    schema: {
        data: "items",
        total: "itemCount"
    },
    serverPaging: true
});
```

만약 서버코드에서 에러가 발생하면 서버 응답은 클라이언트 측 DataSource 인스턴스를 알려줄 수 있습니다. 

### 원격 수정 작업

`update` 서비스는 수정된 데이터 아이템을 기대하고 성공적인 저장 기능의 확인으로써 같은 아이템을 반환합니다. 텅 빈 응답은 또한 유효한 성공적인 응답으로써 다뤄집니다. 만약 `schema.data`가 설정되고 서버의 응답이 비어 있지않다면, 서버응답은 `read`요청의 응답인 같은 구조를 가져야합니다. 

다음 예제는 `schema.data`가 없는 경우를 보여줍니다.
```
/*Client POST request:

ProductID: 1
ProductName: "Fresh yellow bananas"

Server response:

[{
    "ProductID": 1,
    "ProductName": "Fresh yellow bananas"
}]

*/

var dataSource = new kendo.data.DataSource({
    transport: {
        /* the other CRUD settings are omitted for brevity */
        update: {
            url: "service/products/update/",
            type: "post"
        }
    }
});
```
다음 예제는 `schema.data`가 있는 경우를 보여줍니다.

```
/*Client POST request:

ProductID: 1
ProductName: "Fresh yellow bananas"

Server response:

{
    "items": [{
        "ProductID": 1,
        "ProductName": "Fresh yellow bananas"
    }]
}

*/

var dataSource = new kendo.data.DataSource({
    transport: {
        /* The other CRUD settings are omitted for brevity. */
        update: {
            url: "service/products/update/",
            type: "post"
        }
    },
    schema: {
        data: "items"
    }
});
```

### 원격 생성 작업

  
`creat` 액션은 새로 작성된 데이터 항목에 ID가 없다는 점에서 현저한 차이점을 가지고 `update`와 유사한 루틴을 수행하므로 서버 측에 지정되고 원격 서비스에 의해 리턴되어야합니다. 만약 `schema.data`가 설정 되었다면 서버 응답은 `read` 요청의 응답으로 같은 구조를 가질 것 입니다. 

다음 예제는 `schema.data`가 없는 경우를 보여줍니다.
```
/*Client POST request:

ProductName: "Fresh yellow bananas"

Server response:

[{
    "ProductID": 1,
    "ProductName": "Fresh yellow bananas"
}]

*/

var dataSource = new kendo.data.DataSource({
    transport: {
        /* The other CRUD settings are omitted for brevity */
        create: {
            url: "service/products/create/",
            type: "post"
        }
    }
});
```

`schema.data` 있는경우
```
/*Client POST request:

ProductName: "Fresh yellow bananas"

Server response:

{
    "items": [{
        "ProductID": 1,
        "ProductName": "Fresh yellow bananas"
    }]
}

*/

var dataSource = new kendo.data.DataSource({
    transport: {
        /* The other CRUD settings are omitted for brevity. */
        create: {
            url: "service/products/create/",
            type: "post"
        }
    },
    schema: {
        data: "items"
    }
});
```

### 원격 삭제 작업

`destroy` 액션은 삭제되어진 데이터 아이템 또는 해당 ID만 제출합니다. 기대되어지는 응답은 `update` 액션과 유사합니다. 비어질 수 있거나 같은 데이터 아이템을 포함할 수 있습니다. 

```
/*Client POST request:

ProductID: 1
ProductName: "Fresh yellow bananas"

Server response:

[{
    "ProductID": 1,
    "ProductName": "Fresh yellow bananas"
}]

*/

var dataSource = new kendo.data.DataSource({
    transport: {
        /* the other CRUD settings are omitted for brevity */
        destroy: {
            url: "service/products/destroy/",
            type: "post"
        }
    }
});
```

### 원격 Transport 에러 처리

만약 `transport` 액션중(읽기,수정,생성, 삭제) 하나라도 실패하고 에러가 발생하면, 처리하기위해서 다음과 같은 방법중 하나를 사용합니다.
- 보통의 에러는 텅빈 응답과 HTTP 상태 코드를 통해 반환 할 수 있습니다.
- 사용자 정의 에러는 200 GTTP 상태코드로 반환될 수 있고 에러 메세지는 응답 또는 `schema.errors`안에 정의된 어떤 다른 필드안에 `errors` 필드로 할당 될 수 있습니다. 

`erro` 이벤트 가 발생되어 질 때,  DataSource는 서버응답의 일부 일수 있는 어떤 데이터 아이템도 처리하지 않습니다.  예를 들어 만약 수정 액션이 편집 충돌로 실패하고 데이터는 서버로부터 재설정을 필요로 할 때, 에러 핸들러 안에 있는 DataSource의 `read` 메소드를 호출합니다. 에러 메세지와 함께 새로운 데이터를 같이 보내는 것은 새로운 값과 함께 DataSource에 채워질 수 없습니다.

다음 예제는 보통의 에러를 보여줍니다.
```
/*Server response:

HTTP status code: 401 Unathorized
Response body: empty

*/
var dataSource = new kendo.data.DataSource({
    /* The other CRUD settings are omitted for brevity. */
    error: function (e) {
        /* The e event argument will represent the following object:

        {
            errorThrown: "Unauthorized",
            sender: {... the Kendo UI DataSource instance ...}
            status: "error"
            xhr: {... the Ajax request object ...}
        }

        */
        alert("Status: " + e.status + "; Error message: " + e.errorThrown);
    }
});
```

다음 예제는 사용자 정의 예제를 보여줍니다.
```
/*Server response:

HTTP status code: 200 OK
Response body: { "errors": ["foo", "bar"] }

*/
var dataSource = new kendo.data.DataSource({
    /* The other CRUD settings are omitted for brevity. */
    error: function (e) {
        /* The e event argument will represent the following object:

        {
            errorThrown: "custom error",
            errors: ["foo", "bar"]
            sender: {... the Kendo UI DataSource instance ...}
            status: "customerror"
            xhr: null
        }

        */
        alert("Errors: " + e.errors.join("; "));
    }
});
```

## 싱글 요청으로 모든 아이템 제출하기

사용자정의 transport를 사용할 때, 생성, 수정, 삭제 작업은 단일 배치 로 `transport.submit` 함수의 의해서 다뤄질 것 입니다. 함수로 `trasport.read`를 정의하도록 요구되어집니다. `transport.create`, `transport.update` 그리고 `transport.delete` 작동은 이러한 경우엔 실행되지않을 겁니다.

```
<script>
    var dataSource = new kendo.data.DataSource({
        transport: {
            read:  function(options){
                $.ajax({
                    url: "https://demos.telerik.com/kendo-ui/service/products",
                    dataType: "jsonp",
                    success: function(result) {
                        options.success(result);
                    },
                    error: function(result) {
                        options.error(result);
                    }
                });
            },
            submit: function(e) {
                var data = e.data;
                console.log(data);

                // Send batch update to desired URL, then notify success/error.

                e.success(data.updated,"update");
                e.success(data.created,"create");
                e.success(data.destroyed,"destroy");
                e.error(null, "customerror", "custom error");
            }
        },
        batch: true,
        pageSize: 20,
        schema: {
            model: {
            id: "ProductID",
            fields: {
                ProductID: { editable: false, nullable: true },
                ProductName: { validation: { required: true } },
                UnitPrice: { type: "number", validation: { required: true, min: 1} },
                Discontinued: { type: "boolean" },
                UnitsInStock: { type: "number", validation: { min: 0, required: true } }
            }
        }
    }
});

dataSource.read().then(function(){
    var productOne = dataSource.at(1),
        productTwo = dataSource.at(2);

    productOne.set("UnitPrice",42);
    productTwo.set("UnitPrice",42);
    dataSource.sync();
});
</script>
```


참조 : [Kendo UI 공식 Document](https://docs.telerik.com/kendo-ui/framework/datasource/crud#sample-projects-and-examples)
