[TOC]

# 1113_Vue:Vuex

## Vuex

- 뷰엑스
- Vue.js 애플리케이션에 대한 **상태 관리 패턴 + 라이브러리**

- **중앙 집중식 저장소**



- Vue.js에서 부모-자식 컴포넌트 관계는 **props는 아래로, events는 위로**
- **부모는 props를 통해 자식에게 데이터를 전달하고, 자식은 events를 통해 부모에게 메시지를 보낸다**



### Vuex Core Concept

- 상태관리 패턴?
  - 상태는 앱을 작동하는 원본 소스
  - 뷰는 상태의 선언적 매핑
  - 액션은 뷰에서 사용자 입력에 대해 반응적으로 상태를 바꾸는 방법
  - 단방향 데이터 흐름 (Actions, Statem View) 무한반복



- 그러나 공통의 상태를 공유하는 여러 컴포넌트가 있는 경우 단순함이 빠르게 저하됨

  - 여러 뷰는 같은 상태에 의존

  - 서로 다른 뷰의 작업은 동일한 상태를 반영해야 할 수 있기 때문

  - 결과적으로 유지보수가 불가능한 코드로 빠르게 변경됨

  - 그래서 모든 컴폰트는 트리에 상관없이 상태에 엑세스하거나 동작을 트리거 할 수 있다 => Vuex

    

---

<중요 4가지!>💡

#### State / Getters / Mutations / Actions

- **State**
  - (중앙에서 관리하는) 모든 데이터 (==상태)
  - data

- **Getters**
  - 저장소의 상태를 기준으로 계산해야 하는 값
  - 실제 상태 (data)를 변경하지 않음
  - computed와 유사

- **Mutations**
  - state를 변경하는 로직
  - 동기적인 작업! (반드시 동기적인 작업으로 처리해줘야 함, 상태를 바꾸는 함수기 때문에)
  - 첫 번째 인자로 항상 state를 받고 commit(메서드)을 통해 호출함

- **Actions**
  - state를 직접 변경하지 않고 mutations에 정의된 메서드를 호출해서 변경
  - 데이터 fetch 및 처리 & 가공, 비동기 작업 (state변경하지않음)
  - 첫 번째 인자로 항상 context를 받고 dispatch로 actions의 메서드를 호출함

------------



- Vuex는 언제 사용해야 하나?

  - 공유된 상태 관리를 처리하는데 유용하지만, 개념에 대한 이해와 시작하는 비용도 함께 든다

  - 앱이 단순하다면 Vuex없이 괜찮을 것

  - 그러나 중대형 규모의 SPA를구축하는 경우 Vuex를 자연스럽게 선택할 수 있는 단계가 올 것! 필요할 때 쓰자

    



프로젝트 만들고, cd, serve 켜보기~

vue ui 로 프로젝트 확인해볼 수 있음

```bash
$ vue add vuex 
```



- 새로 고침해도 안없어지게!

`npm install vuex-persistedstate`

`import createPersistedState from "vuex-persistedstate"`

plugins: [

  createPersistedState(),

 ]





- 배포

`npm run build`

netlify 깃헙으로 로그인

sites 에서 dist폴더 넣고

주소이름도 바꾸기 가능!



수정사항 반영은 더 복잡. 다시보기로 보자..@

