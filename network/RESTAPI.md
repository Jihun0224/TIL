# REST란?

<center>

![image](https://user-images.githubusercontent.com/59672592/174579322-db15a102-714c-4f37-84da-88714fb39941.png)

</center>

- "Representational State Transfer"
- 자원을 이름으로 구분하여 해당 자원의 상태를 주고 받는 모든 것
- 기본적으로 웹의 기존 기술과 HTTP 프로토콜을 그대로 활용하기 때문에 웹의 장점을 최대한 활용할 수 있는 아키텍처 스타일

> 즉, HTTP(Uniform Resource Idintifier)를 통해 자원을 명시하고
HTTP Method(POST, GET, PUT, DELETE)를 통해 해당 자원에 대한 CURD Operation을 적용하는 것을 의미한다.
<center>

![image](https://user-images.githubusercontent.com/59672592/174581277-310f9cd1-1dac-4e81-982e-7a9f5fa47c26.png)

</center>

```
CRUD Operation

Create : 생성(POST)
Read : 조회(GET)
Update : 수정(PUT)
Delete : 삭제(DELETE)
HEAD: header 정보 조회(HEAD)
```

## REST 특징 

- Server-Client(서버-클라이언트 구조)
    - 자원이 있는 쪽이 Server, 자원을 요청하는 쪽이 Client가 된다
- Stateless(무상태)
    - HTTP 프로토콜은 Stateless Protocol리므로 REST 역시 무상태성을 갖는다.
    - Client의 context를 Server에 저장하지 않는다.
        - 즉, 세션과 쿠키와 같은 context 정보를 신경쓰지 않아도 되므로 구현이 단순해진다.
    - Server는 각각의 요청을 완전히 별개의 것으로 인식하고 처리한다.
        - 각 API서버는 Client의 요청만을 단순 처리한다.
- Cacheable(캐시 처리 가능)
    - 웹 표준 HTTP 프로토콜을 그대로 사용하므로 웹에서 사용하는 기존의 인프라를 그대로 활용할 수 있다.
    - 즉, HTTP가 가진 가장 강력한 특징 중 하나인 캐싱 기능을 적용할 수 있다.
    - 대량의 요청을 효율적으로 처리하기 위해 캐시가 요구된다.
    - 캐시 사용을 통해 응답시간이 빨라지고 REST Server 트랜잭션이 발생하지 않기 때문에 전체 응답시간, 성능, 서버의 자원 이용률을 향상시킬 수 있다.
- Layered System(계층화)
    - Client는 REST API Server만 호출한다.
    - REST Server는 다중 계층으로 구성될 수 있다.
        - API Server는 순수 비즈니스 로직을 수행하고 그 앞에 보안, 로드밸런싱, 암호화, 사용자 인증 등을 추가하여 구조상의 유연성을 줄 수 있다.
    - Proxy, 게이트웨이 같은 네트워크 기반의 중간 매체를 사용할 수 있다.
- Code-On-Demand(optional)
    - Server로부터 스크립트를 받아서 Client에서 실행한다.
    - 반드시 충족할 필요는 없다.
- Uniform Interface(인터페이스 일관성)
    - URI로 지정한 Resource에 대한 조작을 통일되고 한정적인 인터페이스로 수행한다.
    - HTTP 표준 프로토콜에 따르는 모든 플랫폼에서 사용이 가능하다.
        - 특정 언어나 기술에 종속되지 않는다.

## REST 구성요소
1. 자원(Resource):URI
    - 모든 자원에 고유한 ID가 존재하고, 이 자원은 Server에 존재한다.
    - 자원을 구별하는 ID는 '/groups/:gourp_id'와 같은 HTTP URI다
    - Client는 URI를 이용해서 자원을 지정하고 해당 자원의 상태에 대한 조작을 Server에 요청한다.
2. 행위(Verb): HTTP Method
    - HTTP 프로토콜의 Method를 사용한다.
    - HTTP 프로토콜은 GET, POST, PUT, DELETE와 같은 메서드를 제공한다.
3. 표현(Representation of Resource)
    - Client가 자원의 상태에 대한 조작을 요청하면 Server는 이어 적절한 응답을 보낸다.
    - REST에서 하나의 자원을 JSON, XML, TEXT, RSS 등 여러 형태의 Representation으로 나타내어 질 수 있다.
    - JSON 혹은 XML를 통해 데이터를 주고 받는 것이 일반적이다.
## REST가 필요한 이유
- 애플리케이션 분리 및 통합
- 다양한 클라이언트의 등장
- 최근의 서버 프로그램은 다양한 브라우저와 안드로이드폰, 아이폰과 같은 모바일 디바이스에서도 통신할 수 있어야 한다.
- 이러한 멀티 플랫폼에 대한 지원을 위해 서비스 자원에 대한 아키텍처를 세우고 이용하는 방법을 모색한 결과, REST에 관심을 가지게 되었다.


## REST의 장점
- HTTP 프로토콜의 인프라 사용, 별도의 인프라를 구축할 필요가 없다.
- 모든 플랫폼에서 사용이 가능하다.
- Hypermedia API의 기본을 충실히 지키면서 범용성을 보장한다.
- REST API 메시지가 의도하는 바를 명확하게 나타내므로 의도하는 바를 쉽게 파악할 수 있다.
- 여러가지 서비스 디자인에서 생길 수 있는 문제를 최소화한다.
- 서버와 클라이언트의 역할을 명확하게 분리한다.

## REST의 단점
- 표준이 존재하지 않으므로, 프로젝트별로 정의가 필요하다.
- 사용할 수 있는 메서드가 4가지로 제한된다.
- 구형 브라우저가 아직 제대로 지원해주지 못하는 부분이 존재한다.

# REST API
<center>

![image](https://user-images.githubusercontent.com/59672592/174579545-52e7b23e-7075-4216-9940-9e961f67fd65.png)

</center>

## API(Application Programming Interface)
데이터와 기능의 집합을 제공하여 컴퓨터 프로그램간 상호작용을 촉진하며, 서로 정보를 교환가능 하도록 하는 것
## REST API
- REST 기반으로 서비스 API를 구현한 것
- 최근 Open API(누구나 사용할 수 있도록 공개된 API: 구글 맵, 공공 데이터 등), 마이크로 서비스(하나의 큰 애플리케이션을 여러 개의 작은 애플리케이션으로 쪼개어 변경과 조합이 가능하도록 만든 아키텍처) 등을 제공하는 업체 대부분은 REST API를 제공한다.

## REST API 특징
- 사내 시스템들도 REST 기반으로 시스템을 분산해 확장성과 재사용성을 높여 유지보수 및 운용을 편리하게 할 수 있다.
- REST는 HTTP표준을 기반으로 구현하므로, HTTP를 지원하는 프로그램언어로 클라이언,서버를 구현할 수 있다.
- REST API를 제작하면 델파이 클라이언트 뿐 아니라, 자바,C#,웹 등을 이용해 클라이언트를 제작할 수 있다.

## REST API 설계 규칙
REST API 설계 예시
1. URI는 동사보다는 명사를, 대문자보다는 소문자를 사용하여야 한다.
```
Bad Example resource/Running
Good Example  resource/run
```

2. 마지막에 슬래시 (/)를 포함하지 않는다.
```
Bad Example resource/test/  
Good Example  resource/test
 ```

3. 언더바 대신 하이폰을 사용한다.
```
Bad Example resource/test_blog
Good Example  resource/test-blog
 ```

4. 파일확장자는 URI에 포함하지 않는다.
```
Bad Example resource/photo.jpg  
Good Example  resource/photo  
```
5. 행위를 포함하지 않는다.
```
Bad Example resource/delete-post/1  
Good Example  resource/post/1  
```

## 응답상태코드
```
1xx : 전송 프로토콜 수준의 정보 교환
2xx : 클라어인트 요청이 성공적으로 수행됨
3xx : 클라이언트는 요청을 완료하기 위해 추가적인 행동을 취해야 함
4xx : 클라이언트의 잘못된 요청
5xx : 서버쪽 오류로 인한 상태코드
```

# RESTful
- RESTful은 일반적으로 REST라는 아키텍처를 구현하는 웹 서비스를 나타내기 위해 사용되는 용어이다.
    - ‘REST API’를 제공하는 웹 서비스를 ‘RESTful’하다고 할 수 있다.
- RESTful은 REST를 REST답게 쓰기 위한 방법으로, 누군가가 공식적으로 발표한 것이 아니다.
    - 즉, REST 원리를 따르는 시스템은 RESTful이란 용어로 지칭된다.
---

# References
- https://gmlwjd9405.github.io/2018/09/21/rest-and-restful.html
- https://gocoder.tistory.com/2462