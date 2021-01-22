[TOC]

# 1007_ 관통프로젝트 DB

건들지 않은 파일들

앱 > apps.py / tests.py

프로젝트 > asgi.py / wsgi.py

=> 여기서 tests.py 를 오늘 추가할 것 !



## Test

django test 검색해서 MDN문서 참고하기~

```markdown
자동화된 테스트는 당신의 코드의 첫번째 실전 고객으로 역할을 수행하여, 당신의 웹사이트가 어떻게 동작해야하는지 엄격하게 정의하고 문서화하도록 압력을 준다. 종종 이 내용이 당신이 작성하게될 코드 예제나 관련문서의 기초 자료가 된다. 이러한 이유 때문에, 어떤 소프트웨어 개발 프로세스는 테스트 정의와 구현으로 시작되어, 테스트가 요구하는 동작을 충족하도록 코드가 작성되기도 한다.( 예를 들면, test-driven 과 behaviour-driven 개발론).
```

- `TTD(Test-Driven Development : 테스트 주도 개발)`

- `BDD(Behaviour-Driven Development : 행위 주도 개발)`

- 등등 (Driven Development)



테스트 무조건 써야하는 건 아님~ 하지만 단단한 프로젝트를 만들 수 있음!

- Unit tests (유닛 테스트)

독립적인 콤포넌트의 (성능이 아닌) 기능적인 동작을 검증한다. 흔히 class나 function 레벨로 수행한다.

- Regression tests ( 버그수정 확인 테스트 )

기존에 보고된 버그들이 재발하는지 테스트한다. 각 테스트는, 먼저 이전에 발생했던 버그가 수정되었는지 체크한 이후에, 버그 수정으로 인해 새롭게 발생되는 버그가 없는지 확인차 재수행하게 된다.

- Integration tests ( 통합 테스트 )

유닛 테스트를 완료한 각각의 독립적인 콤포넌트들이 함께 결합되어 수행하는 동작을 검증한다. 통합 테스트는 콤포넌트간에 요구되는 상호작용을 검사하며, 각 콤포넌트의 내부적인 동작까지 검증할 필요는 없다. 이 테스트는 단지 전체 웹사이트에 걸쳐 각 콤포넌트가 결합하여 수행하는 동작을 대상으로 한다.



=> 오늘은 유닛테스트를 중심으로 만들 것



### article create

- 서버를 킨다
- /articles/create/
- 데이터를 입력한다
  - 올바른 데이터
  - 올바르지 않은 데이터

- 저장을 누르고
- DB 새로운 article이 저장되었는지 확인



### 기본 클라스  django.test.TestCase

```python
class YourTestClass(TestCase):
    # 테스트를 하기전에 미리 만들어놔야 할 것
    def setUp(self):
        # Setup run before every test method.
        pass

    # 오늘은 사용안함
    def tearDown(self):
        # Clean up run after every test method.
        pass

    # test_라고 시작하는 것은 규칙~~ 그리고 최대한 길고 상세하게 쓰는 것을 지향
    def test_something_that_will_pass(self):
        self.assertFalse(False)

    def test_something_that_will_fail(self):
        self.assertTrue(False)
```



### 테스트 구조 개요

```python
catalog/
  /tests/
    __init__.py
    test_models.py
    test_forms.py
    test_views.py
```



크게 모델하고 뷰 할 것..