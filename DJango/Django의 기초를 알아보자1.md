# DJango의 기초를 알아보자

- `$ python -m django --version` : Django가 설치되어있고, 어떤 버전인지 알 수 있습니다.

## 프로젝트 만들기
- 커맨드라인에서 cd명령으로 코드를 저장할 디렉토리로 이동 한 후, 다음의 명령을 수행합니다 `$ django-admin startproject mysite`
- 위의 명령은 현재 디렉토리에서 <b>mysite</b>라는 디렉토리를 생성할 것입니다. 
- 그러면 아래와 같은 것들이 생성됩니다.
```
mysite/
  manage.py
  mysite/
    _init_.py
    settings.py
    urls.py
    asgi.py
    wsgi.py
```

- manage.py : Django 프로젝트와 다양한 방법으로 상호작용하는 커맨드라인의 유틸리티.
- mysite/ : 디렉토리 내부. 프로젝트를 위한 python 패키지들이 저장됩니다.
- mysite/ \_\_init__.py : 이 디렉토리를 패키지처럼 다루라고 알려주는 용도의 파일
- mysite/urls.py : URL선언을 저장합니다.
- mysite/wsgi.py : 현재 프로젝트를 서비스하기 위한 WSGI 호환 웹 서버의 진입점입니다.

## 개발서버
`$ python manage.py runserver` 를 하면 
```
Performing system checks...

System check identified no issues (0 silenced).

You have unapplied migrations; your app may not work properly until they are applied.
Run 'python manage.py migrate' to apply them.

12월 07, 2021 - 15:50:53
Django version 3.2, using settings 'mysite.settings'
Starting development server at http://127.0.0.1:8000/
Quit the server with CONTROL-C.
```
이러한 출력을 볼 수 있습니다.

- 개발 서버 = 순수 python 으로 작성된 경량 웹서버. Django에 포함되어있어 아무 설정 없이 개발에 사용 가능합니다. 
- 앱을 생성하기 위해선 `manage.py`가 존재하는 디렉토리에서 다음의 명령을 입력해봅시다.
- `$ python manage.py startapp polls`
```
polls/
    __init__.py
    admin.py
    apps.py
    migrations/
        __init__.py
    models.py
    tests.py
    views.py
```
- 이런식으로 디렉토리가 생기고, 이 구조는 어플리케이션의 집이 되어줄 것입니다.

## 첫 번째 뷰 작성하기
- polls/views.py
```.py
from django.http import HttpResponse

def index(request):
    return HttpResponse("Hello, world. You're at the polls index.")
```
- 가장 간단한 형태의 뷰. 이와 연결된 URL이 있어야하는데 이를 위해 URLconf가 사용됩니다.
- polls 디렉토리에서 `urls.py` 를 생성해줍니다.
- polls/urls.py
```.py
from django.urls import path

from . import views

urlpatterns = [
    path('', views.index, name = 'index'),
]
```
- 최상위 URLconf 에서 polls.urls 모듈을 바라보게 설정. mysite/urls.py 파일을 열고, django.urls.include 를 import 하고, urlpatterns 리스트에 include() 함수를 다음과 같이 추가
- mysite/urls.py
```.py
from django.contrib import admin
from django.urls import include,path

urlpatterns = [
    path('polls/', include('polls.urls')),
    path('admin/', admin.site.urls),
]
```
- include() : 다른 URLconf들을 참조할 수 있도록 도와줌. Django가 함수 include() 를 만나게 되면, URL의 그 시점까지 일치하는 부분을 잘라내고, 남은 문자열 부분을 후속 처리를 위해 include 된 URLconf로 전달한다.
- 언제 include() 를 사용해야하는가? : 다른 URL 패턴을 포함할 때 마다 항상. (admin.site.urls 가 유일한 예외)
- path() : 함수에는 2개의 필수 인수인 route 와 view, 2개의 선택 가능한 인수로 kwargs와 name 까지 모두 4개의 인수가 전달 되었습니다.

## path()인수:route
- route 는 url 패턴을 가진 문자열. 요청이 처리될 때 , django는 urlpatterns의 첫번째 패턴부터 시작하여 일치하는 패턴을 찾을 떄 까지 요청된 URL을 각 패ㅌㄴ과 리스트의 순서대로 비교
- 패턴들은 GET이나 POST 의 매개 변수들 , 혹은 도메인 이름을 검색하지 않습니다.
- ex) https://www.example.com/myapp/ 이 요청된 경우 = URLconf는 오직 myapp/ 부분만봄
- ex) https://www.example.com/myapp/?page=3, 같은 요청에도, URLconf는 역시 myapp/ 부분만 신경씀
## path()인수 : view
- 일치하는 패턴을 찾으면, HttpRequest 객체를 첫번째 인수로 하고, 경로로부터 캡처된 값을 키워드 인수로 하여 특정한 view 함수를 호출합니다.
## path()인수: name
- URL에 이름을 지으면, 템프릿을 포함한 Django 어디에서나 명확하게 참조할 수 있습니다. 이 강력한 기능을 이용하여, 단 하나의 파일만 수정해도 project 내의 모든 URL 패턴을 바꿀 수 있도록 도와줌.

## 참고 사이트
- <a href = "https://docs.djangoproject.com/ko/3.2/intro/tutorial01/">Django 튜토리얼</a>
- 위의 사이트를 따라가며 Django를 익혔음. 이 글은 그저 다시 재정리? 타이핑? 하면서 머리에 박아넣기 위한 글임.
