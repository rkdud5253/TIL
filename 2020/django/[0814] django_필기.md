# django

> dynamic web, web application program

- 동적 웹페이지 : 사용자의 요청에 따라 다른 데이터를 응답해주는 것 👉 `static web` : 정적 웹페이지, 이미 정해진 데이터만을 보여주는 것

### What?

- 장고란: Python Opensource Web Framework
  - `파이썬`으로 작성된
  - `오픈소스` 웹 어플리케이션 프레임워크로,
  - `웹 페이지를 개발`하는 과정에서 겪는 어려움을 줄이는 목적으로 만들어진
  - `라이브러리`의 모임
- 웹 프레임 워크란:
  - 웹 구현에 필요한 기본적인 구조, 필요한 코드들을 갖춘 라이브러리
  - 통상적으로 데이터베이스 연동, 템플릿 형태의 표준, 세션 관리, 코드 재사용 등의 기능을 포함한다. 그 외 URL Parsing, DB setting, Object Relation Mapping, Security, Content Management, Temlpate, Caching, Web Server Setting...

### Why?

- 우리의 주력 언어인 파이썬을 이용할 수 있는 프레임워크

- 검증된 프레임워크: Spotify, Instagram, Dropbox, Delivery Hero 등

- 풀스택 프레임워크

  💡 `플래스크` : 마이크로프레임워크로 조금 더 작은 스케일의 프로젝트에 많이 사용됨.

- 널리 사용되는 프레임워크: 꾸준히 업데이트가 이루어지고, 개발자 커뮤니티가 활발함

### How?

- `모델 - 뷰 - 컨트롤러 모델(MVC)` : 통상 소프트웨어 공학에서 사용되는 소프트웨어 디자인 패턴으로, 사용자 인터페이스로부터 비즈니스 로직을 분리하여 서로 영향 없이 쉽게 고칠 수 있다.

  - 모델 : 애플리케이션의 정보(데이터)
  - 뷰 : 텍스트, 체크박스 항목 등과 같은 사용자 인터페이스 요소
  - 컨트롤러 : 데이터와 비즈니스 로직 사이의 상호 동작

- django는MVC가 아닌 `MTV` 모델을 따른다

  - Model - Template - View
  - `Model` : 데이터 관리
  - `Template` : 인터페이스(화면) / MVC의 View에 해당
  - `View` : 중간 관리(상호동작) / MVC의 Controller에 해당

- 동작 순서:

  1. 사용자로부터 HTTP 요청(request)이 발생하면

  2. `URLS(urls.py)`에서 해당 요청을 받아 확인한 뒤

  3. `View(views.py)`에서 작성된 함수의 로직을 통해

  4. 해당 요청에 대응되는

     ```
     Template(<filename>.html)
     ```

     을 불러온 뒤

     - 필요한 경우 `Model(models.py)`과 결합하여 템플릿을 출력하기도 한다

  5. 사용자에게 HTTP 응답(response)으로 출력해준다! (HTML)

### django 실습하기

- 파이썬 버전 확인하기 - 3.7.7

  💡 `python -V` : git bash에서 파이썬 버전을 확인하는 명령어 (대문자V!!!!!!)

- `pip install django`

  - 특정 버전을 설치할 때는 `pip install django==2.1.15` 등으로 설치!
  - `pip list` 를 통해 내 pip 목록과 버전을 확인할 수 있다

- VS code 익스텐션 설치하기 : `Django` by Baptiste Darthenay

  - 컨+슆+P로 open settings (json)열고

    ```json
    //django
    "files.associations": {
        "**/*.html": "html",
        "**/templates/**/*.html": "django-html",
        "**/templates/**/*": "django-txt",
        "**/requirements{/**,*}.{txt,in}": "pip-requirements"
    },
    ```

  - html 자동완성 설정도 추가해준다!

    ```json
    "emmet.includeLanguages": {"django-html": "html"}
    ```

- 장고 프로젝트 시작하기 : `django-admin startproject <project_name>`

  - 프로젝트 이름에는
    - `-` 사용할 수 없음
    - 숫자로 시작할 수 없음 (끝날 수는 있음)
    - 파이썬, 장고의 기본 함수 및 모듈 이름 생성할 수 없음

- 장고 프로젝트의 서버 생성하기 : `python [manage.py](<http://manage.py>) runserver`

  - 서버 끌 때는 `ctrl + c`

  - http://127.0.0.1:8000/

    ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/116de22b-2b16-4ed9-8955-86f862ef1fdc/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/116de22b-2b16-4ed9-8955-86f862ef1fdc/Untitled.png)

    내 첫번째 장고 프로젝트 서버야!

  - 서버 생성시 만들어지는 기본 파일들:

    - `__init__.py` : 프로젝트 파일을 하나의 python package로 기능할 수 있게 모듈화시키는 파일
    - `[asgi.py](<http://asgi.py>)` : Asynchronous Server Gateway Interface, 비동기 웹서버에 배포할 때 사용하는 파일. 장고3에서 추가됨
    - `[wsgi.py](<http://wsgi.py>)` : asgi와 동일한 역할을 하되, 일반적인 웹서버에 배포하는 파일
    - `[settings.py](<http://settings.py>)` : 장고 프로젝트의 모든 세팅을 주관하는 파일
    - `[urls.py](<http://urls.py>)` : http 요청이 왔을 때 가장 처음 받아주는 파일

- 장고 프로젝트 앱 만들기 : `python [manage.py](<http://manage.py>) startapp <app_name>`

  - 장고는 하나의 프로젝트 안에 여러 개의 app들이 모여 있으며, 각 앱들이 웹페이지 내에서의 한 파트들을 담당하는 방식으로 동작한다.
  - app의 이름은 복수형으로 만들어주는 것을 권장!
  - 앱 생성시 만들어지는 기본 파일들:
    - `migrations` : (모델과 관련됨) (다음주에)
    - `__ init __ .py` :
    - `[admin.py](<http://admin.py>)` : 관리자들이 사용하는 관리 전용 파일
    - `[apps.py](<http://apps.py>)` : 앱에 관한 기본 정보가 담겨 있는 파일
    - `[models.py](<http://models.py>)` : (다음주에)
    - `[tests.py](<http://tests.py>)` : 배포 전 테스트코드를 작성하는 파일
    - `[views.py](<http://views.py>)` : MTV의 V, 디자인 패턴을 담당함

- 앱을 프로젝트에 등록하기 :

  - 생성된 앱 폴더는 장고 프로젝트 서버 폴더에 들어가 있지 않음. 따라서 해당 디렉토리 내의 세팅을 변경하여 프로젝트에 앱을 연결해주는 절차가 필요함

  - 단, 앱을 먼저 만들고 등록해야 함. 등록을 먼저 하면 생성이 되지 않음!

  - ```
    [settings.py](<http://settings.py>)
    ```

     \> 

    ```
    INSTALLED APPS
    ```

    - 앱 목록 작성 권장 순서 :
      1. local apps
         - 로컬에서 생성한 앱을 리스트의 맨 위에 올리는 것이 장고의 권장사항 (로딩 순서에 차이가 있음)
      2. 3rd party apps
      3. django default apps

- 장고 프로젝트 현지화 설정

  - ```
    [settings.py](<http://settings.py>)
    ```

     \> 

    ```
    #Internationalization
    ```

    - `LANGUAGE_CODE` > `ko-kr`
    - `TIME_ZONE`

- 장고 프로젝트의 URL 설정하기:

  1. 사용할 app의 `[views.py](<http://views.py>)` 에서 url 주소 설정

     ```python
     def index(request):
     		pass
     ```

     - views 파일의 모든 함수는 첫 번째 인자로 request를 가진다!
     - 아직 templates를 생성하지 않았으므로 우선은 pass 입력 (템플릿 생성 후 확인)

  2. 프로젝트의 `[urls.py](<http://urls.py>)` 에서 해당 app 내의 view 함수 import

     ```python
     from articles import views
     ```

  3. 프로젝트의 `url.py`에서 path 함수를 사용하여 해당 app의 view로 연결하는 설정 생성

     ```python
     urlpatterns = [
         path('index/', views.index),
     ]
     ```

     - `index/` 라는 url을 통해 요청이 들어오면 path 함수가 실행되며,
     - 이 path 함수는  articles 앱 디렉토리의 (모듈화된) view 파일에서 index라는 함수를 불러와 실행한다!

- 장고 프로젝트의 template 생성하기:

  1. 원하는 app의 폴더 내에 `templates` 라는 폴더를 생성!

  2. 사용할 app의 `[views.py](<http://views.py>)` 에서 url 주소와 템플릿 연결

     ```python
     def index(request):
     		return render(request, 'index.html')
     ```

     - 장고의 모든 템플릿은 반드시 [templates] 라는 이름의 폴더에 생성해야 한다! 그래야 render 할 때 따로 주소값을 설정하지 않아도 바로 해당 디렉토리의 html들을 불러올 수 있다!
     - 장고 프로젝트의 settings를 보면 APP_DIRS = True 인 것 때문에

- variable routing: url 명을 변수화하기

  ```json
  path('hello/<str:name>/', views.hello)
  ```

# ⚠️ 코드 작성 순서: 데이터의 흐름과 동일

1. [urls.py](http://urls.py)
2. [view.py](http://view.py)
3. templates

# ⚠️ django conventions:

- ```
  trailing comma
  ```

   :

  - 목록을 작성할 때 맨 마지막 요소의 뒤에도 쉼표를 붙여, 다음 번에 요소를 추가하기 쉽도록 하는 컨벤션이 있다!

- app 목록 작성 

  ```
  [settings.py](<http://settings.py>)
  ```

   \> 

  ```
  INSTALLED APPS
  ```

  1. local apps
  2. 3rd party apps
  3. django default apps

- view 목록 작성 

  ```
  [views.py](<http://views.py>)
  ```

  - 각 view 간에는 두 줄 띄어쓰기

- django imports style guide

  1. standart library
  2. 3rd party library
  3. django core : 장고 내장 모듈
  4. local django : 직접 생성, 혹은 다른 뷰에서 가져오는 모듈

# Django Template Language(DTL)

- django template system에서 사용하는 built-in template system이다.
- 조건, 반복, 치환, 필터, 변수 등의 기능을 제공한다.
- 프로그래밍적 로직이 아니라 프리젠테이션을 표현하기 위한 것! 템플릿의 역할을 넘어설 수 없다.
- 파이썬처럼 if, for문을 사용할 수 있지만 이것은 비슷한 구조를 가진 것일 뿐, 자체적인 문법 구조이지 파이썬 코드가 실행되는 것은 아닙니다.

### Syntax(문법)

- variable: `{{ }}` https://docs.djangoproject.com/en/3.1/ref/templates/language/#variables
- filter:  `{{ variable | filter }}` https://docs.djangoproject.com/en/3.1/ref/templates/language/#filters
- tags: `{% tag %}` https://docs.djangoproject.com/en/3.1/ref/templates/language/#tags

# 템플릿 시스템 설계

- 장고는 템플릿 시스템이 **표현(프리젠테이션)**을 제어하는 도구이자, 표현에 관련된 로직일 뿐이라고 생각한다.
- 따라서, 템플릿 시스템에서는 이러한 기본 목표를 넘어서는 기능을 지원해서는 안 된다.