# Cyptocurrency app

https://www.youtube.com/watch?v=9DDX3US3kss&t=2536s
https://velog.io/@jungsangu/RTK-Query-%EC%8B%9C%EC%9E%91%ED%95%98%EA%B8%B0

## 디렉토리 구조 및 import

```jsx
- components/index.js
export { default as Navbar } from './Navbar';

- App.js
import { Navbar, Footer, ..... } from './components';

- jsx, js 확장자명 구분하는 것 추천
jsx : 컴포넌트 의미
js : 로직, 함수 등등 의미
```

## 레이아웃 구조

```jsx
<HEADER />

<LAYOUT>
    <SWITCH>
        <ROUTE exact path="/모시기"/>
        <ROUTE exact path="/모시기"/>
        <ROUTE exact path="/모시기"/>
        <ROUTE exact path="/모시기"/>
    </SWITCH>
</LAYOUT>

<FOOTER />
```

<br />
<br />

# <em>데이터 통신 액션 분리 - @reduxjs/toolkit</em> (RTK)

1.  configureStore

    ````js
    // 기존 store를 생성하던 과정
    import { createStore } from 'redux';
    import rootReducer from './module/rootReducer';

        const devTools = window.__REDUX_DEVTOOLS_EXTENSION__ && window.__REDUX_DEVTOOLS_EXTENSION__();
        const store = createStore(rootReducer, devTools);
        ```
        ==> toolkit 버전
        ```js
        import { configureStore } from '@reduxjs/toolkit';

        const store = configureStore({ reducer: rootReducer });
        ```

    <br />

    ````

2.  RTK Query

    리덕스 툴킷의 data fetching, caching 기능

        ```js
        import { createApi, fetchBaseQuery } from '@reduxjs/toolkit/query/react';

        // request Header
        const cryptoApiHeaders = {
            'x-rapidapi-host': 'coinranking1.p.rapidapi.com',
            'x-rapidapi-key': '모시기모시기모시기모시기'
        };

        // request 기본 서버 주소
        const baseUrl = 'https://coinranking1.p.rapidapi.com';

        const createRequest = (url) => ({ url, headers: cryptoApiHeaders });

        export const cryptoApi = createApi({
            // 리듀서의 이름을 정하고
            reducerPath: 'cryptoApi',
            // 기본 주소 정하고
            baseQuery: fetchBaseQuery({ baseUrl }),
            // 이제 각 endpoint마다 나눠서 훅을 생성한다.
            endpoints: (builder) => ({
                getCryptos: builder.query({
                    query: () => createRequest('/coins')
                })
            })
        })

        ==>
        export const {
            useGetCryptosQuery
            // ?? 이게 어디서나왔나 싶지만 저기 endpoints에서 각 메소드 이름마다 맞춰서 훅을생성한다
        } = cryptoApi;
        ```
        이렇게 생성된 리듀서를 STORE에 넣어준다

        ```js
        import { cryptoApi } from '../services/cryptoApi';

        export default configureStore({
            reducer: {
                [cryptoApi.reducerPath]: cryptoApi.reducer
            },
        });
        ```
