[TOC]

# 1014_JavaScript_JS심화

목차

- ECMAScript

- Coding Style Guide

- AJAX

- Callback Function

- Promise



## 1. ECMAScript

### ECMAScript 요약

- 변수 (let, const, var(안씀)) + hoisting
- 타입과 연산자 (null, undefind)
- 조건 & 반복 (for, forof forin, while, switch...)
- 함수 (선언/표현)
- 자료구조
  - Array (Array Helper Method - forEach, map, reduce, every, find, filter...)
  - Object (JSON, key와value)



### ASI (Automatic Semicolon Insertion)(;)

- 내부적으로 문장이 끝나는 지점에 마침표를 찍어준다

- 아직도 논쟁중 - 찍느냐 vs 안찍느냐
- 우리는 안찍을 것





## 2. Coding Style Guide

### JavaScript Style Guide

- Airbnb
- Google
- JavaScript Standard Style (standardjs)
  - https://standardjs.com/rules-kokr.html



### why?

- 왜 지켜야하는가?
  - 맞춤법을 지키는 것이라 생각하자~!





## 3. AJAX 💡

- AJAX (에이젝스)

### AJAX - 기존

- client ----->(request)----->Server
- client <-----(response)<------Server
- 문서 전체가 바뀜

### AJAX - 새로운방식

- client ----->(request)----->Server
- client <-----(response)<------Server
- 문서의 일부만 바뀜



### AJAX (Asynchronous JavaScript And XML)

- 서버와 통신하기위해 XMLHttpRequest 객체를 사용하는것
- JSON, XML, HTML 그리고 일반 텍스트 형식을 포함한 다양한 포맷을 주고 받을 수 있음
- 페이지 전체를 리프레쉬하지 않고서도 수행되는 "비동기성"
- Event가 있으면 전체페이지가 아닌 일부분을 업데이트 할 수 있음

<주요 특징>

=> **페이지 새로고침 없이 서버에 요청**

=> **서버로부터 데이터를 받고 작업을 수행**



- A New Approach 새로운 접근! 
- Gmail, Google Maps, Google...



### XHR (XMLHttpRequest)

- XHR 객체는 서버와 상호작용하기 위해 사용됨
- 전체 페이지의 새로고침 없이 URL로부터 데이터를 받아올 수 있음
- 웹페이지가 사용하고 있는 것을 방해하지 않으면서 페이지의 일부를 업데이트할 수 있도록 해줌
- XMLHttpRequest는 AJAX프로그래밍에 주로 사용됨





Async & Sync

### How JavaScript works

- Asynchronous
- Single Thread
- Event Loop



영상다시보기 설명 듣기~~ (강의참고)

#### 1) Asynchronous(비동기)

- <u>**기다려주지않음**</u>

print(todo) / console.log(todo)

JSON형태로 보여줌 / 빈문자열 (기다려주지않음!!!) 



#### 2) Single Thread

왜 기다려주지 않을까?

- 한번에 하나의 일만 **혼자** 할 수 있다

동기 - 순서대로 하다가 하나가 늦어지면 기다림 뒤에꺼는 그게 해결돼야 할 수 있음

비동기 - 요청을 보내고 다른일 할 수 있음, 기다리지 않는다 -> 혼자 일해서!



#### 3) Event Loop:star:

- **어떻게일을하나? 이벤트루프에 기반한 메커니즘**

- **Call Stack**
  - 요청이 들어올 때마다 해당 요청을 순차적으로 처리하는 Stack(LIFO) 형태의 자료 구조
  - 함수 호출 기록

- **Web API (Browser API)**
  - JavaScript 엔진이 아닌 브라우저 영역에서 제공하는 API
  - (XHR도 브라우저 영역에서 제공하는 API)

- **Task Queue**
  - 콜백 함수가 대기하는 Queue(FIFO) 형태의 자료 구조

- **Event Loop**
  - call Stack에 현재 실행 중인 Task가 없는지 확인하고 Task Queue에 Task가 있는지 확인

(강의 설명 참고!!)

-> 순서이해하기!!!! Queue는 Stack이 비어야지 들어간다?

-> 0초로 설정해도 Queue에 들어갔다오기때문에.. 다름?



##### setTimeout()

setTimeout()은 코드를 바로 실행하지 않고 지정한 시간만큼 기다렸다가 로직을 실행하는 Web API의 한 종류이다.

```null
// #1
console.log('Hello');
// #2
setTimeout(function () {
	console.log('Bye');
}, 3000);
// #3
console.log('Hello Again');

>>>
Hello
Hello Again

Bye
```



## 4. Callback Function 💡

- 함수가 인자로 넘어감

  1) return -> 함수

  2) 변수에 담기 -> 함수

  3) 인자로 넘길 수 있다 -> 함수

- Python(map), JavaScript(map), Django(urls.py), addEventListener

- 모든 비동기 + ~할때  =>  call back
- 직접적으로() 호출하지않고 어느 시점에 알아서 시행!





## 5. Promise

### 1. sync (동기)

- 기다린다. 무한대기



### 2. async (비동기)

- 기다릴때 + 다른일을 한다
  - 답이 도착하면 문제해결
    - 문제해결되면 알려주기



### 3. Callback Function

- Callback Function으로 해결할 수 있다



### 4. Callback Hell

- 기다릴때 + 다른일을 한다
  - 답이 도착하면 문제해결
    - 문제해결되면 알려주기
      - 알려주면 ~하기
        - ~하면 ~하기
          - ...

- 코드 복잡함.. 콜백지옥! -> 디버깅 힘들고, 본인 코드 못읽을 확률 높아짐



### 5. Promise 💡

- 그래서 등장한 Promise! 직관적으로 보일 수 있게!
- **Promise 객체는 비동기 작업이 맞이할 <u>미래의 완료 또는 실패</u>와 그 결과 값을 나타낸다.**
- **Promise는 비동기 작업의 최종 완료 또는 실패를 나타내는 객체이다.**



#### .then / .catch

- `resolve(성공)`, `reject(실패)`

- `.then(doSomething(callback function))` - 성공했을 때 할 일

- `.catch(doSomething(callback function))` - 실패했을 때 할 일



- return 이 그냥 Promise!
- `return new Promise function ~`
- 그래서 이렇게

```javascript
// 참고
getArticle('https://jsonplaceholder.typicode.com/todos/1')
	.then(function (res) {
    	const article = JSON.parse(res)
        return article.title
	})
	.then(function (res) {
    	console.log(res)
	})
	.catch(function (error) {
    	console.log(error)
	})
```

=> 얘도 결국 .then반복 되면서 약간 직관적이지 못하게 됨 chaining?



그래서!

#### async & await (ES8+)

- 최근에 사용되고 있음

##### Syntactic Sugar

- promise-based지만,

- 문법을 사용하기 쉽게
- 반드시 비동기 로직이 포함되어 있어야 함
- => 내부는 비동기적으로 동작하지만 동기적으로 코드를 짤 수 있다

```javascript
// 참고
async function getTitleInArticle (url) {
    const res = await getArticle(url)
    const title = JSON.parse(res).title
    console.log(title)
}
```

```javascript
//3. async & await
//3-1. 기본 axios 요청
function getTodo () {
    console.log('1')
    axios.get('https://jsonplaceholder.typicode.com/todos/1')
        .then(function (res) {
        console.log(res.data.title)
    })
    console.log('2')
}
getTodo()

>>>
1
2
delectus aut autem
XHR finished loading: GET "https://jsonplaceholder.typicode.com/todos/1".
    

//3-2. async & await
async function getTodo2 () {
    console.log('1')
    await axios.get('https://jsonplaceholder.typicode.com/todos/1')
        .then(function (res) {
        console.log(res)
    })
    // const response =  await axios.get('https://jsonplaceholder.typicode.com/todos/1')
    // console.log(response)
    console.log('2')
}
getTodo2()

>>>
1
{data: {…}, status: 200, statusText: "", headers: {…}, config: {…}, …}
2
XHR finished loading: GET "https://jsonplaceholder.typicode.com/todos/1".
```



#### Axios :star::star::star:

=> Promise기반으로 요청을 날려주는 Axios 라이브러리를 통해 처리할 것!

- **Promise** based HTTP client for the **browser and node.js**
  - 편하게 (직관적으로) 요청을 보내자!
  - Primise 베이스로 요청을 보내는 것! (.then(성공)과 .catch(실패))

- python의 request와 비슷



=> 라이브러리니까 설치해야함. 그런데 install, import 하지않고 CDN쓸 것 / 바디안에 script위에 붙이기!

https://github.com/axios/axios

```javascript
<script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
```

=> axios가 리턴하는 대상은 Promise (console확인)

그리고 .then, .catch로 꺼내오기 callback함수씀

```javascript
// 참고
axios.get('https://jsonplaceholder.typicode.com/todos/1')
	.then(function (res) {
    	console.log(res.data.title)
	})
	.catch(function (error) {
    	console.log(error)
	})
```

- .catch가 없으면 `Uncaught Error` 오류





## 실습

기존코드 + AJAX , Axios...

새로고침하지않고 좋아요 기능 할 수 있게!

하트 + 몇명이 좋아합니다 기능 바꾸기

개발자도구 확인

```html
# articles > templates > articles > index.html
# 오른쪽 하단 django HTML을 그냥 HTML로 바꾸면 JavaScript 자동완성 가능

{% extends 'base.html' %}

{% block content %}
  <h1 class="text-center">Articles</h1>
  <a href="{% url 'articles:create' %}">NEW</a>
  <hr>
  {% for article in articles %}
    <p><b>작성자 : <a href="{% url 'accounts:profile' article.user.username %}">{{ article.user }}</a></b></p>
    <p>글 번호: {{ article.pk }}</p>
    <p>글 제목: {{ article.title }}</p>
    <p>글 내용: {{ article.content }}</p>
    <form class="d-inline like-form" data-article-id="{{ article.pk }}">
      {% csrf_token %}
      {% if user in article.like_users.all %}
        <button class="btn btn-link">
          <i id="like-{{ article.pk }}" class="fas fa-heart fa-lg" style="color:crimson;"></i>
        </button>
      {% else %}
        <button class="btn btn-link">
          <i id="like-{{ article.pk }}" class="fas fa-heart fa-lg" style="color:black;"></i>
        </button>
      {% endif %}
    </form>
    <p>
      <span id="like-count-{{ article.pk }}">
        {{ article.like_users.all|length }} 명이 이 글을 좋아합니다.<br>
      </span>
    </p>
    <a href="{% url 'articles:detail' article.pk %}">[detail]</a>
    <hr>
  {% endfor %}
  <script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
  <script>
    const forms = document.querySelectorAll('.like-form')
    

    forms.forEach(function (form) {
      form.addEventListener('submit', function (event) {
        event.preventDefault()
        // console.log(event)
        const articleId = event.target.dataset.articleId
        const csrftoken = document.querySelector('[name=csrfmiddlewaretoken]').value
        
        axios.post(`http://127.0.0.1:8000/articles/${articleId}/like/`, {}, {
          headers: {
            'X-CSRFToken': csrftoken
            }}
        )
        .then(function (res) {
          // console.log(res)
          const count = res.data.count
          const liked = res.data.liked
          // console.log(count, liked)

          const likeIconColor = document.querySelector(`#like-${articleId}`)
          // console.log(likeIconColor)
          const likeCount = document.querySelector(`#like-count-${articleId}`)
          // console.log(likeCount)

          likeCount.innerText = `${count} 명이 이 글을 좋아합니다`

          if (liked) {
            likeIconColor.style.color = 'crimson'
          } else {
            likeIconColor.style.color = 'black'
          }

        })
      })
    })
  </script>
{% endblock %}
```

```python
# articles > views.py

from django.http import JsonResponse

@require_POST
def like(request, article_pk):
    if request.user.is_authenticated:
        article = get_object_or_404(Article, pk=article_pk)
        user = request.user

        if article.like_users.filter(pk=user.pk).exists():
        # if user in article.like_users.all():
            article.like_users.remove(user)
            liked = False
        else:
            article.like_users.add(user)
            liked = True

        like_status = {
            'liked': liked,
            'count': article.like_users.count(),
        }
        return JsonResponse(like_status)
        # return redirect('articles:index')
    return redirect('accounts:login')
```

