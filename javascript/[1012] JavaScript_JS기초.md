[TOC]

# 1012_JavaScript_JS기초

## 1. History of JavaScript & Browser

### why JavaScript?

- 브라우저 화면을 동적으로 만들기 위해서!

- 자바스크립트 -> 브라우저조작을 하기 위한 것!



### JavaScript

- 팀 버너스리(www, http, uri 등의 창시자) / 브랜던 아이크(Javascript 설계자)

- 역사

  - 1994년 네스케이프사의 Netscape Navigatoe(NN) 브라우저가 표준
  - 정적인 HTML을 동적으로 표현하기 위한 언어 도입을 결정
  - 1995년 브랜던 아이크 주도로 개발된 'Mocha'를자체 브라우저에 도입
  - 이후 LiveScript라는 이름을 거쳐 지금의 JavaScript로 변경
  - MS(마이크로소프트)의 폭발적 성장, IE3에서 자체적인 JScript를 지원, 호환성 문제로 크로스 브라우징 등의 이슈 발생
  - 이후 Netscape 후계자들은 모질라 재단 기반의 Firefox를 개발
  - 계속되는 파편화를 방지하고 모든 브라우저에서 동일하게 동작하기 위한 표준의 필요성 제기
  - Netscape는 **ECMA** 인터네셔널에 기술 규격을 제출한 이후 표준 제정에 대한 논의 지속
  - 2008년 Google Chrome 등장 (표준을 잘 지킨다)
  - 자바스크립트 문제가 아니라 엔진이 문제!
  - JS의 태생적 한계
  - Node JS(2009) Runtime환경 등장 - Server Side가 가능해짐
  - Chrome 등장 이후 여러 과정을 거쳐 자바스크립트의 고질적 문제를 많이 해결한 ES2015(ES6) 등장
  - ECMAScript(ES6)는 기존 코드를 간결하게 작성할 수 있는 새로운 문법들이 추가되면서 더욱 발전할 수 있는 발판을 만듦
    - Arrow function
    - const, let
    - Promise
    - Object 축약문법

  - Cross Browsing Issue
    - jQuery

  - Vanilla JavaScript
    - 크로스 브라우징, 간편한 활동 등을 위해 많은 라이브러리 등장(대표적 jQuery)
    - 최근 표준화된 브라우저, ES6 이후의 다양한 도구의 등장으로 순수 자바스크립트 활용의 증대
    - 브라우저에 내장되어 있기 때문에 따로 설치할 필요없음

- **결론**

  - **History of JavaScript & Browser**
    - **브라우저 전쟁**
    - **파편화 & 표준화의 투쟁**

  - **브라우저 전쟁의 여파**
    - **Cross Browsing Issue**
    - **표준화(통합)을 위한 노력 (ex. jQuery)**
    - **Vanilla JavaScript**



## 2. DOM(Document Object Model)

- 브라우저에서 할 수 있는 일

  - DOM 조작
    - 문서(HTML) 조작

  - ~~BOM 조작~~ 지금안할것
    - navigator, screen, location, frames, history, XHR

  - JavaScript Core(SCMAScript)
    - Data Structure(Object, Array), Conditional Expression, Iteration



### DOM의 개념

- Document Object Model (문서 객체 모델) : 웹 페이지 문서 구조를 표현함으로써 스크립트 및 프로그래밍 언어와 페이지를 연결. DOM은 문서를 논리 트리로 표현. 각 노드는 객체를 갖고, DOM 메서드를 사용하면 프로그래밍적으로 트리에 접근할 수 있음



### DOM

- HTML, XML 등과 같은 문서를 다루기 위한 언어 독립적인 문서 모델 인터페이스
- 문서 구조, 스타일, 내용 등을 변경할 수 있도록 도우며, 구조화된 노드와 오브젝트로 문서를 표현
- 주요 객체
  - **Window: DOM을 표현하는 창. 가장 최상위 객체**
  - document: 페이지 콘텐츠의 Entry Point역할을 하며, <body>등과 같은 수많은 다른 요소들을 포함
  - navigator, location, history, screen

- 브라우저마다 각자의 방법으로 DOM을 구현
- 모든 문서의 노드들은 'DOM Tree' 라고 불리는 트리 구조의 모습을 나타낸다
- 브라우저 사이에 DOM 구현이 호환되지 않음에 따라, W3C에서 DOM표준 규격을 작성
- DOM은 문서의 기반이 되는 데이터 구조에 제한을 두지 않지만, 잘 구조화된 문서는 DOM을 사용해 트리 구조를 얻어낼 수 있다 (마크업의 중요성)
- 스크립트를 작성할 때 문서 조작을 위해 document 혹은 window객체를 사용할 수있다
  - **window 객체는 생략 가능**



### DOM 조작

#### 1. Selection (선택한다)

- 단일 Node
  - document.getElemantById(id)
  - document.querySelector(selector)
- HTMLCollection(live)
  - document.getElemantByTagName(tagName)
  - document.getElemantByClassName(class)
- NodeList(non-live)
  - document.querySelectorAll(selector)

=> **우리는 `querySelector()` 와 `querySelectorAll()` 많이 사용할 것**



#### 2. Manipulation (변경한다)

1) 속성

- innerText
  - 텍스트

- innerHTML
  - XSS 공격에 취약점이 있으므로 사용시 주의

-  Node attribute
  - element.style.backgroundColor
  - setAttribute(attributeName, value)
  - getAttribute(attributeName)

2) 새로운 요소를 만들어 붙이는 방법

- Document.createElement(tagName)
  - 특정 태그를 생성

- ParentNode.appendChild(Node)
  - 마지막 자식 요소로 추가

- ParentNode.removeChild(child Node)
  - 해당요소를 제거



**html 파일 브라우저로 열때 Alt+B**



- F12 or 검사
  - `window`
  - `document`
  - `console.log('')` - 프린트역할

- 자바스크립트 주석은 `//` 과 `/* */`
- 자바스크립트에서는 `-`하이픈 쓸일 없음 전부 카멜케이스로 작성됨 소문자로 시작 다음단어는 대문자로 시작 ex)`marginTop`



```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Basic DOM Manipulation</title>
  <style>
    #king {
      color: red;
    }
  </style>
</head>
<body>
  <h1 id="header">DOM Manipulation</h1>
  <h2 id="langHeader">Programming Languages</h2>
  <ul>
    <li class="lang">Python</li>
    <li class="lang">Java</li>
    <li class="lang" id="specialLang">JavaScript</li>
  </ul>

  <h2 id="frameHeader">Frameworks</h2>
  <ul>
    <li class="framework" id="specialFrame">Django</li>
    <li class="framework">Spring</li>
    <li class="framework">Vue.js</li>
  </ul>

  <script>
    //1. Selection - querySelector / querySelectorAll
    //1-1. window & document
    // console.log(window)
    // console.log(document)
    // console.log(window.document)

    //1-2. querySelector
    const mainHeader = document.querySelector('h1')
    const langHeader = document.querySelector('#langHeader')
    const frameHeader = document.querySelector('#frameHeader')
    // console.log(mainHeader, langHeader, frameHeader)

    //1-3. querySelectorAll
    const langLi = document.querySelectorAll('.lang')
    const frameworkLi = document.querySelectorAll('.framework')
    // console.log(langLi, frameworkLi)

    //1-4. 여러 개의 요소 -> 첫 번째로 일치하는 요소
    const selectOne= document.querySelector('.lang')
    // console.log(selectOne)

    //1-5. 복합 선택자
    const selectDescendant = document.querySelector('body li')
    // const selectDescendant = document.querySelectorAll('body li')
    const selectChild = document.querySelector('body > li')
    // console.log(selectDescendant) 
    // console.log(selectChild) 

    //1-6. getElementById, getElementByClassName 
    const selectSepcialLang = document.getElementById('specialLang')
    const selectAllLangs = document.getElementsByClassName('framework')
    const selectAllLiTags = document.getElementsByTagName('li')
    // console.log(selectSepcialLang, selectAllLangs, selectAllLiTags)

    //2. Manipulation
    //2-1. Creation
    const browserHeader = document.createElement('h2')
    const ul = document.createElement('ul')
    const li1 = document.createElement('li')
    const li2 = document.createElement('li')
    const li3 = document.createElement('li')
    // console.log(browserHeader, li1, li2, li3) 

    //2-2. innerText & innerHTML / append & appendChild
    browserHeader.innerText = 'Browsers'
    li1.innerText = 'IE'
    li2.innerText = '<strong>FireFox</strong>'
    li3.innerHTML = '<strong>Chrome</strong>'
    // console.log(browserHeader, li1, li2, li3)

    //2-3. append DOM 
    const body = document.querySelector('body')
    body.appendChild(browserHeader)
    body.appendChild(ul)

    ul.append(li1, li2, li3) 
    // ul.appendChild(li1, li2, li3) 

    //2-4. Delete
    // removeChild
    // ul.removeChild(li1) 
    // ul.removeChild(li2)

    // remove
    // ul.remove()
    // body.remove()


    //2-5. Element Styling
    li1.style.cursor = 'pointer'
    li2.style.color = 'blue'
    li3.style.background = 'red'

    // setAttribute
    li3.setAttribute('id', 'king')

    // getAttribute
    const getAttr = li1.getAttribute('style')
    const getAttr2 = li3.getAttribute('style')
    console.log(getAttr)
    console.log(getAttr2)

  </script>
</body>
</html>
```



```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Basic JavaScript Core Things</title>
</head>
<body>
  <script>
    // Conditional Expression
    const myName = 'ssafy 4th'
    
    // === : 일치비교연산자(권장), == : 동등비교연산자(알아서 형변환하기때문에 권장x)
    if (myName === 'ssafy 4th') {
      console.log('ssafy 4th님 환영합니다.')
    } else if (myName === 'ssafy 3th') {
      console.log('ssafy 3th님 환영합니다.')
    } else {
      console.log('환영합니다.')
    }

    // Iteration 
    // + for ... in / for ... of
    for (let i = 0; i < 6; i++) {
      console.log(i)
    }

    // Function Declaration & Call
    //1. 함수 선언
    // 함수 선언식
    function add (num1, num2) {
      // console.log(num1 + num2)
      return num1 + num2
    }

    // 함수 표현식
    const sub = function (num1, num2) {
      // console.log(num1 - num2)
      return num1 - num2
    }

    // arrow function
    const multi = (num1, num2) => {
      return num1 * num2
    }

    //2. 함수 호출
    const result1 = add(2, 7)
    const result2 = sub(7, 2)
    const result3 = multi(7, 2)

    console.log(result1, result2, result3)
  </script>
</body>
</html>
```



## 3. Event(Listener)

- click, submit, keydown, mouseover,,,



### :star:addEventListener:star:

- ~~하면, ~~한다

- **특정 이벤트**가 발생하면, <u>할 일</u>을 등록하자 :star2:
- EventTarget.addEventListener(**type**, <u>listener</u>) :star2:
- ex) EventTarget(button)에서 어떠한 이벤트(click)가 발생하면, alert메세지를 보여준다. => `EventTarget.addEventListener('click' function() {})`



```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Add Event Listener</title>
</head>
<body>
  <!-- 1. onclick -->
  <button onclick="alertMessage()">나를 눌러봐!</button>

  <!-- 2. addEventListener -->
  <button id="myButton">나를 눌러봐!!</button>
  <hr>

	<!-- 3. addEventListener2 -->
  <p id="myParagraph"></p>

  <form action="#">
    <label for="myTextInput">내용을 입력하세요.</label>
    <input id="myTextInput" type="text">
  </form>
  <hr>

  <!-- 4. addEventListener3 -->
  <h2>Change My Color</h2>
  <label for="changeColorInput">원하는 색상을 영어로 입력하세요.</label>
  <input id="changeColorInput"></input>
  <hr>

  <script>
    // 1. onclick
    const alertMessage = function() {
      alert('안녕하세요!')
    }

    // 2. addEventListener - click
    const myButton = document.querySelector('#myButton')
    
    myButton.addEventListener('click', alertMessage)

    // 3. addEventListener - keydown
    const myTextInput = document.querySelector('#myTextInput')

    myTextInput.addEventListener('keydown', function (event) {
      // console.log(event)
      // console.log(event.target.value)
      const myParagraph = document.querySelector('#myParagraph')
      myParagraph.innerText = event.target.value

    })

    // 4. addeventListener = keydown
    const changeColorInput = document.querySelector('#changeColorInput')

    changeColorInput.addEventListener('keydown', function () {
      const h2 = document.querySelector('h2')
      h2.style.color = event.target.value
    })
  </script>
</body>
</html>
```



```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>preventDefault</title>
	<style>
    body {
      height: 10000px;
    }
  </style>
</head>
<body>
  <!-- 1. checkbox -->
  <input type="checkbox" id="myCheckBox">
  <hr>

  <!-- 2. submit -->
  <form action="/articles/" id="myForm">
    <input type="text">
    <input type="submit">
  </form>
  <hr>

  <!-- 3. link -->
  <a href="https://google.com" target="_blank" id="myLink">GoToGoogle</a>
  <hr>

  <!-- 4. input -->
  <input type="text" id="myInput">
  
  <script>
    const form = document.querySelector('#myForm')

    form.addEventListener('submit', function (event) {
      console.log(event)
      console.log(event.cancelable)
      event.preventDefault()
    })
  </script>
</body>
</html>
```



```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>todo CRUD</title>
  <style>
    .done {
      text-decoration: line-through;
    }
  </style>
</head>
<body>
  <input type="text">
  <button>Todo!</button>
  <ul></ul>

  <script>
    const button = document.querySelector('button')
    const input = document.querySelector('input')
    
    // function (여기는 이벤트객체..)
    // function 이름을 만들어주었으니까 밑에서 그냥 이름써주면됨
    function addTodoUpdateDelete () {
      const content = input.value
      
      if (content) {
        const li = document.createElement('li')
        li.innerText = content
    
        const ul = document.querySelector('ul')
        ul.appendChild(li)
        // 입력값지워줌
        input.value = ''

        // li.style.textDecoration = 'line-through'
        li.addEventListener('click', function (event) {
          // if (event.target.classList.contains('done')) {
          //   event.target.classList.add('done')
          // } else {
          //   event.target.classList.remove('done')
          // }

          event.target.classList.toggle('done')
        })
        
        // li.remove()
        const deleteButton = document.createElement('button')

        deleteButton.innerText = 'X'
        deleteButton.style.marginLeft = '10px'

        li.appendChild(deleteButton)

        // Delete
        deleteButton.addEventListener('click', function () {
          li.remove()
        })

      } else {
        alert('빈값안됨')
      }
    }

    button.addEventListener('click', addTodoUpdateDelete)
    input.addEventListener('keydown', function (event) {
      // console.log(event)
      if (event.code === 'Enter') {
        addTodoUpdateDelete()
      }
    })
  </script>
</body>
</html>
```

-> 마지막꺼 한글은 뒷글자가 한번 더 나온다.. 뭘까?

keydown을 keypress로쓰고 keyup keydown을 예외처리? 그냥 찾아보기

-> 한글이.. 특수 ㅠㅠ