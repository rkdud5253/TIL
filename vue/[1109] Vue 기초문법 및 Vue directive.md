[TOC]

# 1109_Vue 기초 문법 및 Vue directive

## 1. Hello Vue.js

### Vue.js

- 프론트엔드 개발은 HTML, CSS, 그리고 JavaScript를 활용해서 데이터를 볼 수 있게 만들어 준다. 이 작업을 통해 사용자는 데이터를 눈으로 볼 수 있고 데이터와 상호작용 할 수 있다.

- Server -> HTML(비어있는) -> (**T(Browser)** -> HTML)



### CSR(Client Side Rendering)

- 예를들어, 재료를 다 준뒤에 직접 만들라고 주는 것..?

- SSR(Server side Rendering) - 예를 들어, 다 완성된 제품을 주는 것?



### SPA(Single Page Application)

- 받은 단일 페이지 안에서 해결하는 것



### Why?

- **사용자 경험(UX) 향상** - 새로고침 안해도됨



### Why Vue.js?

- LIKE with Vanilla JavaScript
- Reactive - 페이스북(무수히 많은 Data)

- Reactive - Vanilla JavaScript

- Reactive - Vue.js => 위의 코드보다 더 간단하게 만들 수 있다!





## 2. Concepts of Vue.js

### MVVM (Model / View / ViewModel)

- Vue에서 Model은 JacaScript **Object**이다
- Vue에서 View는 **DOM(HTML)**이다
- Vue에서 ViewModel은 **모든 Vue Instance**이다

- HTML => DOM과 Data의 중개자 => {key:value}



### Django & Vue.js

| Django      | Vue.js  |
| ----------- | ------- |
| 1. url      | 1. data |
| 2. view     | 2. DOM  |
| 3. template |         |



- 구글 vue dev tools 설치, vs code에서 Vetur 설치



------------------------------------

## webex

- <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>

공식문서에서 가져온 CDN을 body 위에 넣어줌

-------------------



- 자료 올려주신거 vscode로 잘보기~😁💡



## 3. 정리

- 왜 Vue.js를 쓰나?
  - 데이터에 반응한다 (Reactive.. data..) -> 데이터가 바뀌면 데이터가지는 DOM을 바꿀 수 있음

- Vue Instance 만들고 조작
- `v-for` : 반복할때 사용
- `v-if / v-else-if / v-else` : 조건
- `v-bind` : 표준속성에 연결할때 /  클래스 바인딩할때 씀 => `:`
- `v-on` : 이벤트리스너 이벤트가 발생하면 하는일 , 이벤트에 대한 내용을 이어서 갈 수 있음 => `@__`

- `v-model` :  속성과 양방향 바인딩을 해줌  (input, textarea, select에서 사용가능)

- `v-text` : {{}}
- `v-html` : data안에 넣어줘야하니까 위험함

- `v-show` :  렌더링 자주 바뀌는 과정에서 유리함
- `v-if `:  렌더링 자체를 하지않기 때문에 한번만 렌더링할때는 좋지만 자주하면 위에꺼쓰기
- `lodash` : 프로그래밍적 로밍 하기 힘들때 파이썬에서 사용하는 것처럼 쓰는 라이브러리? CDN가져와서 쓰기