# SPA vs MPA
- SPA(Single Page Application)는 한 개(Single)의 Page로 구성된 Application이다.  
MPA(Multiple Page Application)는 여러 개(Multiple)의 Page로 구성된 Application이다.
- SPA는 웹 애플리케이션에 필요한 모든 정적 리소스를 최초에 한번 다운로드하고, 이후 새로운 페이지 요청 시 페이지 갱신에 필요한 데이터만을 전달받아 페이지를 갱신하게 된다.  
반면 MPA는 새로운 페이지를 요청할 때마다 정적 리소스를 다운로드한다. 매번 전체 페이지가 다시 렌더링 된다.
## SPA
- SPA는 CSR(Client Side Rendering)방식으로 렌더링한다.
- 단 한번만 리소스(HTML, CSS, JavaScript)를 로딩한다.  
그 이후에는 데이터를 받아올 때만 서버와 통신한다.
- 최초 페이지를 로딩한 시점부터는 페이지 리로딩 없이 필요한 부분만 서버로부터 받아서 화면을 갱신하는 것이다.  
이를 통해 네이티브 앱에 가까운 자연스러운 페이지 이동과 UX를 제공할 수 있다.
- Angular, React, Vue 등 프론트엔드 기술들이 나오면서 유행하고 있다.
- SPA 방식이 모두 CSR인 것은 아니다.
<center>

![image](https://user-images.githubusercontent.com/59672592/173553491-c8f6a391-90f1-4788-a829-c19da19462c6.png)  
(출처 : https://www.excellentwebworld.com/what-is-a-single-page-application/)

</center>

### SPA 장점
- 사용자 친화적 (UX)
    - 전체 페이지를 업데이트 할 필요가 없기 때문에 빠르고 ‘깜빡’ 거림이 없다.
- 필요한 리소스만 부분적으로 로딩 (성능)
    - SPA의 Application은 서버에게 정적리소스를 한 번만 요청한다.그리고 받은 데이터는 전부 저장해놓는다. (캐시=Cache)
- 서버의 템플릿 연산을 클라이언트로 분산 (성능)
- 컴포넌트별 개발 용이 (생산성)
- 프론트 엔드와 백엔드 분리로 개발업무 분업화 및 협업이 용이
### SPA 단점
- 초기 구동 속도
    - SPA는 최초 접속 시 사이트 구성과 관련된 모든 리소스를 한 번에 받아오기 때문에 초기 구동 속도가 상대적으로 느리다.
- 화면 변하는 모습
    - 데이터를 별도로 요청하고 받아와서 화면을 구성하므로 설계에 따라서 화면이 변하는 모습이 사용자에게 노출될 수 있다.
- SEO(Search Engine Optimization) 문제
    - 네이버, 구글에 검색했을 때 우리 웹사이트가 잘 나오게 하는 것을 검색엔진 최적화라고 말한다.
    - 웹페이지가 각각 100개씩 있는 페이지는 검색 봇이 페이지를 읽을 수 있다.  
    하지만, 페이지는 1개이고 필요한 부분만 JavaScript로 바꿔준다면?  
    검색봇이 페이지를 읽을 수 없게 된다.
    - 이를 해결하기 위해 SSR with Hydration 기법이 나왔는데, 대표적으로 React 진영의 Next.js와 Vue 진영의 Nuxt.js가 위 기법을 구현한 프레임 워크다.  
    즉, 처음엔 서버사이드 렌더링을 하고, 그 후 다른 페이지들에선 클라이언트 사이드 렌더링을 이용하는 방식이다.
## MPA
- MPA는 SSR(Server Side Application) 방식으로 렌더링한다.  
새로운 페이지를 요청할 때마다 서버에서 렌더링된 정적 리소스(HTML, CSS, JavaScript)가 다운로드된다.  
페이지 이동하거나 새로고침하면 전체 페이지를 다시 렌더링한다.
### MPA 장점
- SEO 관점에서 유리하다.
    - MPA는 완성된 형태의 HTML 파일을 서버로부터 전달받는다.  
    따라서 검색엔진이 페이지를 크롤링하기에 적합하다.
- 첫 로딩 매우 짧다.
    - 서버에서 이미 렌더링해 가져오기 때문이다.
<center>

![image](https://user-images.githubusercontent.com/59672592/173568931-9aea3e62-67de-4a55-9f8c-573fcffc4845.png)  
(출처 : https://www.excellentwebworld.com/what-is-a-single-page-application/)

</center>

# SSR vs CSR
## SSR
웹의 초기부터 SPA에 대한 구현체들이 나오기 전까지는 전통적인 웹사이트들은 모두 MPA 형태로 서비스해 왔다.  
MPA는 페이지를 이동할 때마다 새로운 페이지를 요청한다. 모든 템플릿은 서버 연산을 통해서 렌더링하고 완성된 페이지 형태로 응답한다. 이 과정을 서버 사이드 렌더링(SSR)이라고 부른다.
<center>

![image](https://user-images.githubusercontent.com/59672592/173574722-0c35acd9-a43f-4298-9ccb-e33c5078ad94.png)
(출처: [The Benefits of Server Side Rendering Over Client Side Rendering](https://medium.com/walmartglobaltech/the-benefits-of-server-side-rendering-over-client-side-rendering-5d07ff2cefe8))

</center>

- SSR을 사용하면 모든 데이터가 매핑된 서비스 페이지를 클라이언트(브라우저)에게 바로 보여줄 수 있다.
- 버를 이용해서 페이지를 구성하기 때문에 클라이언트에서 구성하는 CSR(client-side rendering)보다 페이지를 구성하는 속도는 늦어지지만 전체적으로 사용자에게 보여주는 콘텐츠 구성이 완료되는 시점은 빨라진다.
- SEO(search engine optimization) 또한 쉽게 구성할 수 있다.

## CSR
최초에 한번 서버에서 전체 페이지를 로딩하여 보여주고 이후에는 사용자의 요청이 올 때마다, 리소스를 서버에서 제공한 후 클라이언트가 해석하고 렌더링하는 방식이다. SEO가 어렵다는 큰 단점이 있다.  

<center>

![image](https://user-images.githubusercontent.com/59672592/173574681-06a464e6-0a2e-4727-a164-24891d5e5c19.png)  
(출처: [The Benefits of Server Side Rendering Over Client Side Rendering](https://medium.com/walmartglobaltech/the-benefits-of-server-side-rendering-over-client-side-rendering-5d07ff2cefe8))

</center>


## 참고
- [hanamon.kr](https://hanamon.kr/spa-mpa-ssr-csr-%EC%9E%A5%EB%8B%A8%EC%A0%90-%EB%9C%BB%EC%A0%95%EB%A6%AC/)
- [Neul_bo.log](https://velog.io/@ken1204/SPA%EC%97%90-%EB%8C%80%ED%95%98%EC%97%AC)
- [NAVER D2](https://d2.naver.com/helloworld/7804182)