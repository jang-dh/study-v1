# DataSource 

## Overview

Kendo UI DataSource 컴포넌트는 jQuery용 Kendo UI로 빌드 된 모든 웹 어플리케이션에서 중심적인 역할을 합니다.

## 시작하기

DataSource는 로컬 데이터(자바스크립트 객체의 배열) 또는 원격 데이터(JSON, JSONP, oData 또는 XML를 반환하는 웹 서비스)을 사용하기 위한 추상적 개념입니다.   CRUD (Create, Read, Update, Destroy) 데이터 작업을 완벽하게 지원하며 정렬, 페이징, 필터링, 그룹화 및 집계에 대한 클라이언트 측 및 서버 측 지원을 모두 제공합니다.

다음 목록에는 DataSource가 제공하는 일부 기능이 포함되어 있습니다.

- 원격의 엔드 포인트로부터 데이터의 수정
- 구조와 데이터의 타입 유지
-  원격 엔드 포인트와의 직렬화 형식 처리
- 업데이트 동기화 : 원격 엔드 포인트와의 생성, 수정, 삭제
-  원격 엔드 포인트로 업데이트하기위한 변경 사항을 포함하여 메모리 내 데이터 캐시 유지 보수
- 집계, 정렬 순서 및 페이징 계산 및 유지 관리
- 필터 표현식을 통한 query 메커니즘 제공

## 로컬 데이터로 바인딩하기

DataSource를 로컬 데이터로 바인드하기위해 자바스크립트 객체의 배열을 DataSource 인스턴트의 `data` 속성에 할당합니다. 

```
var movies = [{
    title: "Star Wars: A New Hope",
    year: 1977
}, {
    title: "Star Wars: The Empire Strikes Back",
    year: 1980
}, {
    title: "Star Wars: Return of the Jedi",
    year: 1983
}];

var localDataSource = new kendo.data.DataSource({
    data: movies
});
```

## 원격 데이터 서비스로 바인딩하기

DataSource를 원격 데이터로 바인딩 할때, 객체의 일반 배열보다 복잡하다면 컴포넌트는 웹서비스 URLs, 요청 타입, 반환 타입, 그리고 반환의 구조에 대한 정보를 요구합니다. 데이터가 요청되는 동안 제출되어질 사용자정의 파라미터가 제공되어질 수 있습니다. 

```
var dataSource = new kendo.data.DataSource({
    transport: {
        read: {
            // The remote service url.
            url: "http://api.openweathermap.org/data/2.5/find",

            // The request type.
            type: "get",

            // The data type of the returned result.
            dataType: "json",

            // The additional custom parameters sent to the remote service.
            data: {
                lat: 42.42,
                lon: 23.20,
                cnt: 10
            }
        }
    },
    // Describe the result format.
    schema: {
        // The data to which the DataSource will be bound is in the "list" field of the response.
        data: "list"
    }
});
```

## 여러 데이터 동작 모드 사용하기

 
데이터 작업의 일부가 서버와 클라이언트에서 유지 될 것으로 여전히 확인할 수 있지만 혼합 데이터 작업 모드에서 DataSource를 사용하면 원하지 않는 부작용이 발생합니다. 예를 들어, `serverPaging` 이 활성화 되있고 `serverFiltering` 이 비활성화 되어 있으면, DataSource는 현재 페이지로 부터 데이터만 필터할 것이며 유저는 기대했던 것보다 안좋은 결과를 보게 될 것입니다. 다른 시나리오에서 DataSource는 데이터 작업을 하기위해서 필요한 것 보다 더 많은 요청을 만들 수 있습니다. 

## 위젯 바인딩 하기

Kendo UI 위젯은 데이터 바인딩을 지원하고 DataSource 컴포넌트를 로컬과 원격 데이터를 위한 바인딩 소스로 사용합니다. 
다음 예제는 다른 Kendo UI 위젯 설정과 함께 인라인으로 DataSource를  생성하는 방법입니다.
```
$("#chart").kendoChart({
    title: {
        text: "Employee Sales"
    },
    dataSource: new kendo.data.DataSource({
        data: [
        {
            employee: "Joe Smith",
            sales: 2000
        },
        {
            employee: "Jane Smith",
            sales: 2250
        },
        {
            employee: "Will Roberts",
            sales: 1550
        }]
    }),
    series: [{
        type: "line",
        field: "sales",
        name: "Sales in Units"
    }],
    categoryAxis: {
        field: "employee"
    }
});
```

## DataSource 공유하기
  
다음 예제는 공유 DataSource를 작성하고 여러 Kendo UI 위젯이 동일한 데이터 콜렉션에 바인드하는 방법을 보여줍니다.   공유 DataSource를 사용하면 데이터 요청이 줄어들고 성능이 향상되며 데이터가 변경 될 때 모든 바인딩 된 위젯의 자동 동기화 새로 고침을 제공합니다.

```
var sharedDataSource = new kendo.data.DataSource({
    transport: {
        read: {
            url: "data-service.json",
            dataType: "json"
        }
    }
});

// Bind two UI widgets to the same DataSource.
$("#chart").kendoChart({
    title: {
        text: "Employee Sales"
    },
    dataSource: sharedDataSource,
    series: [{
        field: "sales",
        name: "Sales in Units"
    }],
    categoryAxis: {
        field: "employee"
    }
});

$("#grid").kendoGrid({
    dataSource: sharedDataSource,
        columns: [
        {
            field: "employee",
            title: "Employee"
        },
        {
            field: "sales",
            title: "Sales",
            template: '#= kendo.toString(sales, "N0") #'
    }]
});
```

참조: [Kendo UI 공식 Document](https://docs.telerik.com/kendo-ui/framework/datasource/overview)
