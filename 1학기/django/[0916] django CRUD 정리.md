## 1. 가상환경 생성

- 가상환경 생성과 활성화

  ```bash
  $ python -m venv <가상환경이름(venv)>
  
  밑에처럼 선택해주면 밑에 액티브 필요옶음
  $ source venv/Scripts/activate
  ```

- 가상환경 생성된 폴더가 있는 곳에서 VS code 키고 

  ctrl+shift+P > Python: Select Interpreter > Python 3.7.7 64-bit('venv':venv) 선택

  > 좌측하단에 가상환경인지 확인!

- .gitignore 파일 최상단에 생성!

  gitignore.io 사이트에서 <Windows, macOS, VisualStudio Code, Python, Django, venv> 생성해서 파일에 전체 복사 후 저장!



## 2. 기본설정

python -m venv venv 가상환경만들고 ctrl+shipt+P해서 선택
**pip install -r requirements.txt** 이걸로 남한테 받은거에서 모든거 다운
python manage.py makemigrations 모델바꾸면 이거랑 밑에꺼는 필수
python manage.py migrate



- 생성 전 , 가상환경 이므로 장고 설치해주기

  ```$ pip install django```

  중간중간 계속해서 리스트 확인 ```$ pip list```

- Project, App 생성
  - 생성하는 폴더 안에 git bash창 열고 ```$ django-admin startproject <project name> ``` 
  - 그 폴더로 들어가서 manage.py 와 같은 위치에서 APP생성 ```$ python manage.py startapp <app name(복수형!)>```
  - settings.py 에서 INSTALLED_APPS에 ```'<app name>',```추가 
  - settings.py 에서 ```LANGUAGE_CODE = 'ko=kr'```로 한국어 설정 및 ```TIME_ZONE = 'Asia/Seoul'```로 한국시간 설정
  - ```$ python manage.py runserver```로 확인하기

- templates 생성

  - 전체 프로젝트에 적용되는 템플릿을 최상위 폴더에  templates를 생성하여 저장

  - 개별 app들에 적용되는 템플릿은 해당 app폴더에 templates 생성하여 저장 (templates/articles/다른 html)

  - 템플릿 상속

    - templates 폴더 안에 base.html 생성! 상속주는 기본구조 (bootstrap포함)
- settings.py에 경로 수정! ```'DIRS': [BASE_DIR / 'templates'], ``` 



일단 이 초기 설정부터 헷갈렸습니다..

## 3. templates > base.html

```html
# nav-bar를 bootstrap에서 가져오기 위해 링크 복사 후 붙여넣기
# 기본 block 설정!

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css" integrity="sha384-JcKb8q3iqJ61gNV9KGb8thSsNjpSL0n8PARn9HuZOnIxN0hoP+VmmDGMN5t9UJ0Z" crossorigin="anonymous">
  <title>CRUD</title>
</head>
<body>
  <nav class="navbar navbar-expand-lg navbar-light bg-light">
    <a class="navbar-brand" href="#">Review</a>
    <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarNav">
      <ul class="navbar-nav">
        <li class="nav-item">
          <a class="nav-link" href="{% url 'community:review_list' %}">list</a>
        </li>
        <li class="nav-item">
          <a class="nav-link" href="{% url 'community:new_review' %}">new</a>
        </li>
      </ul>
    </div>
  </nav>
  <div class="container">
    {% block content %}
    {% endblock %}
  </div>

  <script src="https://code.jquery.com/jquery-3.5.1.slim.min.js" integrity="sha384-DfXdz2htPH0lsSSs5nCTpuj/zy4C+OGpamoFVy38MVBnE+IbbVYUew+OrCXaRkfj" crossorigin="anonymous"></script>
  <script src="https://cdn.jsdelivr.net/npm/popper.js@1.16.1/dist/umd/popper.min.js" integrity="sha384-9/reFTGAW83EW2RDu2S0VKaIzap3H66lZH81PoYlFhbGU+6BZp6G7niu735Sk7lN" crossorigin="anonymous"></script>
  <script src="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/js/bootstrap.min.js" integrity="sha384-B4gt1jrGC7Jh4AgTPSdUtOBvfO8shuf57BaghqFfPlYxofvL8/KUEfYiJOMMV+rV" crossorigin="anonymous"></script>
</body>
</html>
```



## 4. App > models.py

```python
from django.db import models

# Create your models here.
class Review(models.Model):
    title = models.CharField(max_length=100)
    content = models.TextField()
    rank = models.IntegerField()
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)
    
    def __str__(self):
        return f'{ self.title }'
```

```bash
# 수정할 때마다 해줘야 함
$ python manage.py makemigrations
$ python manage.py migrate
```

잘못 작성해도 폴더삭제는 금물!

## 5. Project > admin.py

```python
from django.contrib import admin
from .models import Review

# Register your models here.
admin.site.register(Review)
```

```bash
$ python manage.py createsuperuser
```

- 아이디, 이메일(엔터쳐서 넘어감), 비밀번호 설정하기!

## 6. Project > urls.py

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('community/', include('community.urls')),
]
```

## 7. APP > 새로운 파일 생성 > urls.py

```python
from django.urls import path
from . import views

app_name = 'community'
urlpatterns = [
    path('', views.review_list, name='review_list'),
    path('new_review/', views.new_review, name='new_review'),
    path('create_review/', views.create_review, name='create_review'),
]

```

- 여기서 path 경로를 하나하나 설정해주기 (url, view, html반복!)



## 8. APP > view.py

```python
from django.shortcuts import render, redirect
from .models import Review

# Create your views here.

def review_list(request):
    reviews = Review.objects.all()
    context = {
        'reviews': reviews
    }
    return render(request, 'community/review_list.html', context)


def new_review(request):
    return render(request, 'community/new_review.html')


def create_review(request):
    title = request.POST.get('title')
    content = request.POST.get('content')
    rank = request.POST.get('rank')

    review = Review.objects.create(title=title, content=content, rank=rank)
    return redirect('community:review_list')
```

## 9. APP > templates > community(APP) > review_list.html

```python
{% extends 'base.html' %}
{% block content %}
  <h1>Review List</h1>
  <a href="{% url 'community:new_review' %}">NEW</a>
  {% for review in reviews %}
    <h3>제목: {{ review.title }}</h3>
    <p>내용: {{ review.content }}</p>
    <p>평점: {{ review.rank }}</p>
    <p>{{ review.created_at }}</p>
    <hr>
  {% endfor %}
{% endblock %}
```

- 상속받아서 웹에서 보여주고 싶은 내용 작성

## 10. APP > templates > community(APP) > new_review.html

```python
{% extends 'base.html' %}
{% block content %}
  <h1>NEW</h1>
  <form action="{% url 'community:create_review' %}" method="POST">
    {% csrf_token %}
    <label for="title">TITLE: </label>
    <input type="text" id="title" name="title">
    <br>
    <label for="content">CONTENT: </label>
    <textarea name="content" id="content" cols="30" rows="10"></textarea>
    <br>
    <label for="rank">RANK: </label>
    <input type="number" id="rank" name="rank">
    <br>
    <input type="submit" value="제출">
  </form>
{% endblock %}
```

- 상속받아서 new페이지 작성하는 부분

- 여기서 오류 조심 !!! ```{% csrf_token %}```  작성 안해서 오류남!!!

  POST 쓰면 주의해서 꼭 써주기!!!! 



> 9,10 번에서  경로 설정해주는게 굉장히 헷갈렸습니다.!!! 그래도 오늘 연습으로 조금은 알아가는 것 같아서 좋았습니다. 연습을 많이해야겠다고 느꼈습니다..



# 결과!!

# ![리스트](README.assets/리스트.JPG)![뉴](README.assets/뉴.JPG)