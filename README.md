# Cyptocurrency app

https://www.youtube.com/watch?v=9DDX3US3kss&t=2536s

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
