# Basic Usage

## 로컬 데이터 생성하기

다음 예제는 로컬 데이터를 위한 DataSource를 생성하는 방법을 보여줍니다.
```
    var movies = [
            { title: "Star Wars: A New Hope", year: 1977 },
            { title: "Star Wars: The Empire Strikes Back", year: 1980 },
            { title: "Star Wars: Return of the Jedi", year: 1983 }
    ];

    var localDataSource = new kendo.data.DataSource({ data: movies });
```
예제의 `localDataSource` 변수는 `movies` 배열의 메모리 내 캐시를 나타내도록 초기화 된 DataSource입니다. 그러나 `movies` 배열로 나타난 데이터는 `.read()` 함수가 호출되기전까지는 DataSource 안에 로드되지않습니다.
```
localDataSource.read();
```
  
데이터 소스가 Kendo UI 위젯 또는 차트에 바인드 될 때 명시 적 호출이 필요하지 않을 수 있습니다. 위젯의 기본 설정은 관련된 DataSource로 자동적으로 설정됩니다.

## 원격 데이터 소스 생성하기

원격 데이터를 위한 DataSource를 생성하는 과정은 로컬 데이터를 위한 DataSource를 생성하는 방법과는 몇가지가 다릅니다.
-  `transport`  하나 또는 모든 CRUD (만들기, 읽기, 업데이트, 삭제) 데이터 작업에 대한 프로토콜, 엔드 포인트의 URL 및 직렬화 형식을 식별해야합니다. 
- 옵션으로 요청 함수를 원격 엔드포인트의 형식으로 marshals하는  `parameterMap`이 사용되지길 요구됩니다.
-   선택적으로 집계 계산, 필터 정의 및 그룹화, 페이징 및 정렬과 같은 기능을 지원하기 위해 서버 조작을 사용하도록 구성됩니다.

다음 예제는 원격 엔드포인트로 부터 데이터를 위한 DataSource 생성 방법을 보여줍니다.
```
    var remoteDataSource = new kendo.data.DataSource({
        type: "odata",
        transport: {
            read: "http://odata.netflix.com/Catalog/Titles"
        }
    });
```

  
이 예제의 `remoteDataSource` 변수는 Netflix 카탈로그 서비스에서 영화 타이틀의 메모리 내 캐시를 나타내도록 oData 프로토콜을 사용하도록 초기화 된 DataSource입니다.   바인딩 된 모든 위젯에 대한 읽기 전용 데이터 소스로만 작동하도록 구성되어 있습니다.

로컬 데이터 용 데이터 소스를 만드는 경우와 마찬가지로 .read () 메서드가 호출 될 때까지 Netflix 카탈로그 서비스에서 제공하는 데이터가로드되지 않습니다.

```
remoteDataSource.read();
```

데이터 소스가 Kendo UI 위젯 또는 차트에 바인드 될 때 명시 적 호출이 필요하지 않을 수 있습니다. 위젯의 기본 설정은 관련된 DataSource로 자동적으로 설정됩니다.

다음 예제는 또 다른 원격 엔드포인트에서 데이터를 위한 DataSource가 생성되는 방법을 보여줍니다.

```
    var remoteDataSource = new kendo.data.DataSource({
        transport: {
            read: {
                url: "http://search.twitter.com/search.json",
                dataType: "jsonp",
                data: {
                    q: function() {
                        return $("#searchFor").val();
                    }
                }
            }
        }
    });
```

이 예제에서 DataSource는 트위터 찾기 서비스로부터 트위트의 내장 메모리 캐시를 나타내기위해 초기화되어집니다.  이 엔드 포인트는 입력 매개 변수 q가 검색 서비스의 쿼리 문자열을 표시 할 수 있도록하는 JSON 기반 엔드 포인트 컨택을 사용합니다.  여기에서 해당 값은 페이지의 입력 요소에 의해 제공됩니다.

이 원격 엔드 포인트에 대해 DataSource가 수행하는 작업은 jQuery.ajax ()를 통해 수행되므로 사용자 에이전트가 적용한 것과 동일한 보안 제한 조건이 적용됩니다. 이 보안 제한 조건은 또한 다른 도메인에서 만들어진 XHR (XMLHttpRequests) 도 적용합니다.   위의 예에서 이런 경우이므로 `dataType` 구성 특성은 JSONP를 사용하도록 설정됩니다.

## 로컬 필터링
  
로컬 데이터 필터링은 DataSource를 사용하는 간단한 작업입니다. 그 컴포넌트는 하나 또는 더 많은 필터 표현식리스트를 허용합니다.  `and` 또는 `or` 로컬 오퍼레이터를 사용함으로서 합쳐질 수 있습니다. 필터 표현식 구조에 대해 더많은 정보를 원하면 필터 설정 옵션 문서를 참고하세요. 로컬 필터링은 작은 데이터셋에 편리합니다.성능 이슈가 생기기 때문에  큰 데이터셋을 사용하려면 피해야합니다.

```

        var words = [
            { 'w': 'kendo', 'length': 4 },
            { 'w': 'done', 'length': 4 },
            { 'w': 'keno', 'length': 4 },
            { 'w': 'node', 'length': 5 }
        ];
```


## 서버 필터링

서버 필터링은 대규모 데이터 세트에 편리합니다. 필요에 따라 스키마 및 필터 속성을 설정했는지 확인하세요.
다음 예제는 로컬 데이터의 특징이지만 `transport`에 의해 반환되어진 데이터는 같은 방법으로 수행될 것입니다. 
```
        //the JSON result from "{remote service}"
        {
            result: [
                { 'w': 'done', 'length': 4 },
                { 'w': 'node', 'length': 5 }
            ]
        }
```
