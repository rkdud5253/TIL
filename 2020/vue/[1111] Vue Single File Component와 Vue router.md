[TOC]

# 1111_Vue : Single File Component 와 Vue router

## 핵심요약

### Vue Intro

- Why Vue.js?
  - 사용자 경험(UX)
  - DOM Reactive

- Core Concepts of Vue.js
  - CSR(Client Side Rendering)
  - SPA(Single Page Application)
  - MVVM(Model / View / ViewModel)

### Vue Directive

- Vue Instance & data binding
- v-if, v-else, v-else-if
- **v-on(@)** 💡
- **v-bind(:)** 💡
- v-model
- method, computed, watch, v-text & v-html, v-show





## 1. Single File Component (SFC)

### Component

- 컴포넌트는 다시 사용할 수 있는 범용성을 위해 개발된 소프트웨어 구성 요소를 일컫는다

- 컴포넌트는 기본 HTML 엘리먼트를 확장하여 **재사용 가능한 코드**를 캡슐화하는데 도움이 됨
- **Vue컴포넌트는 Vue인스턴스이기도 함** 💥

- **유지, 보수 그리고 재사용성** 💥

- .vue

**=> 화면의 특정 영역에 대한 HTML, CSS, JavaScript 코드를 <u>하나의 파일 (.vue)</u>에서 관리**

=> Vue 컴포넌트 === Vue 인스턴스 === .vue File





## 2. Vue CLI

### Component Development

- 어떻게 컴포넌트 기반으로 개발을 할까?



- JS의 태생적 한계

- Over the Browser - Node.js



### npm (Node Package Manager)

- 자바스크립트 프로그래밍 언어를 위한 패키지 관리자
- 자바스크립트 런타임 환경 Node.js의 기본 패키지 관리자



### Vue CLI

- Command line interface for rapid Vue.js development





## 3. Babel & Webpack

### Babel? Webpack?

- History of JavaScript? **파편화 & 표준화**
- 어떤 문제를 해결하기 위해 존재하는 도구인가?



### Babel - compile(r)

- complie - 특정 프로그래밍 언어로 쓰여있는 문서를 다른 프로그래밍 언어도 옮기는 프로그램 => **번역기!**

=> **파편화된 (크로스 브라우징 이슈) JavaScript 문법을 변환**하기 위해 존재하는 도구



### Webpack - Bundle(r)

- bundler - 묶음

- 자바스크립트는 모듈이라는 개념이 없음

=> 모듈 간의 **의존성** 문제를 해결하기 위해 존재하는 도구



### Babel & Webpack

- Webpack을 사용해 구축
- Plugin을 통해 기능 확장 가능
- 빌드 도구 (Webpack)의 세팅에 시간을 쓸 필요없이 앱으로 서비스를 개발하는 것에만 집중할 수 있게 해준다



### 정리

- Node.js
  - JavaScript Runtime Environment
  - JavaScript를 브라우저 밖에서 실행 할 수 있는 새로운 환경

- Babel
  - Complier
  - 신버전의 JavaScript 코드를 구버전의 JavaScript로 바꿔주는 도구

- Webpack
  - Bundler
  - 모듈간의 의존성 문제를 해결하기 위한 도구



---

Node.js 설치하고

vscode에서 터미널열어서

`$ node -v` => v14.15.0

`$ npm -v` => 6.14.8

버전 나오면 정상

---

```bash
npm install -g @vue/cli
```

```bash
vue create my-first-vue-cli-project
```

-> 세가지 옵션이 뜰 것

첫번째꺼 설치할것 vue2

성공했으면

```bash
cd my-first-vue-cli-project
```

```bash
npm run serve
```

-> 주소뜨는거 클릭하기!



### App.vue

컴포넌트 쓰기 위해서는

1. 불러온다
2. 등록한다
3. 보여준다



```bash
npm install
```

```bash
vue add router
```

-> y

-> y



다시 npm run serve



lunch-lotto ~~ > src > views 에서 파일하나 만들기

" TheLunch.vue "

v치고 엔터!



영상보기,..

템플릿 안에는 1개의 엘리먼트만 들어가야한다!!!💥

```vue
<script>
exprot default {
name: 'TheLunch'
}
</script>
```

index.js가서

8~12번째 복사

,,, 영상보기



```bash
npm install lodash
```

스크립트 안에

import _ from 'lodash'





----------

## 4. 프로젝트 Pass Props & Emit Events

### Pass Props & Emit Events

Parent --------> Pass Props ---------> Child

​            <-------- Emit Events <--------



- 단방향 데이터! 부모에서 자식으로 흐른다
- 모든 prop들은 부모와 자식 사이에 단방향으로 내려가는 바인딩 형태를 취한다 

- 부모의 속성이 변경되면 자식 속성에게 전달되지만, 반대 방향으로 는 전달되지 않는다
- 앱의 데이터 흐름을 이해하기 어렵게 만드는 일을 막기 위해서이다



### Youtube Project

=> npm install 이 명령어는 내가 직접 프로젝트를 생성한게 아닌 -> git pull 혹은 clone을 받은경우 친다!

node_modules가 존재하지 않을 때, 해당 프로젝트에서 의존하고 있는 패키지들을 설치하기 위해 진행하는 것!

플젝을 직접 생성 한 경우, node_modules 폴더가 존재한다

```bash
$ npm install
```

```vue
// SearchBar.vue
<template>
  <div>
    <input @keypress.enter="onInputKeyword" type="text">
  </div>
</template>

<script>
export default {
  name: 'SearchBar',
  methods: {
    onInputKeyword: function (event) {
      // console.log(event.target.value)
      this.$emit('input-change', event.target.value)
      // 자식이 올려줌 1) 이벤트, 2) 넘길 데이터
    }
  }
}
</script>
```

```vue
<template>
  <div class="container">
    <h1>My First Youtube Project</h1>
    <!-- 3.보여준다. -->
    <SearchBar @input-change="onInputChange" />
  </div>
</template>

<script>
// import axios from 'axios'

//1. 불러온다.
import SearchBar from '@/components/SearchBar'

// 전체폴더에서 파일만들기 .env.local
// 거기서 밑에 코드 넣기
// VUE_APP_YOUTUBE_API_KEY=내API키
// 대문자필수! VUE_APP은 반드시 존재해야함! 공백없음!


const API_KEY = process.env.VUE_APP_YOUTUBE_API_KEY
const API_URL = 'https://www.googleapis.com/youtube/v3/search'


export default {
  name: 'App',
  components: {
    // ES6 Object 축약 문법
    // SearchBar: SearchBar, 
    //2. 등록한다.
    SearchBar,
  },
  data: function () {
    return {
      inputValue: '',
      videos: [],
    }
  },
  methods: {
    onInputChange: function (inputText) {
      console.log('데이터가 SearchBar로부터 올라왔다!!!!')
      console.log(inputText)

      //1. 자식 컴포넌트(SearchBar.vue)로부터 올라온 데이터 inputValue라는 App.vue 컴포넌트 데이터에 넣는다.
      this.inputValue = inputText

      //2. Youtube API로 요청을 위한 준비를 한다.
      const params = {
        key: API_KEY,
        part: 'snippet',
        type: 'video',
        q: this.inputValue,
      }

      //3. Youtube로 axios를 활용해 요청을 보낸다.
      axios.get(API_URL, {
        params,
        // params: params,
      })
      .then((res) => {
        console.log(res)
        console.log(res.data.items)
      
      //4. Youtube로부터 응답 받은 영상 목록(배열)을 배열에 넣는다.
      // this.videos = res.data.items
      })
      .catch((err) => {
        console.log(err)
      })
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

```

