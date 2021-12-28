# DJango의 기초를 알아보자 2
## DJango 관리자
### 관리자 소개
- 개발자들이 회원들을 관리하는거라면 상관이 없지만 서비스를 이용할 사장님 같은 비전공자들을 위한 클릭만으로 관리가 가능한 관리자 페이지가 필요하겠죠?
### 관리자 생성
- 그러기 위해선 우선 관리 사이트에 로그인할 수 있는 사용자를 생성해야합니다. `$ python manage.py createsuperuser` 이후 절차를 따라갑니다.
- 이제 `/admin` 을 입력해주면 어드민 창이 뜰겁니다.
- 앞서 생성한 Superuser 게정으로 로그인하면 Django의 관리 인덱스 페이지가 보입니다.
### 관리 사이트에서 poll app 을 변경가능하도록 만들기
- 그런데 만들면 poll app 이 관리 인덱스 페이지에 보이지 않을겁니다. 이땐 아래의 코드를 `polls/admin.py` 에 입력해줍시다.
```.py
from django.contrib import admin
from .models import Question

admin.site.register(Question)
```

### 자유로운 관리 기능
- Question 을 클릭하면 질문들을 위한 Change list 로 이동합니다. 이 페이지는 DB에 저장된 모든 질문들을 보여줍니다. (이전에 등록했던 What's up? 이라는 질문이 있을거에요.)
#### 여기서 알아둘 것들:
- 이 서식은 Question 모델에서 자동으로 생성되었습니다
- 모델의 각 필드 유형들은 (DateTimeField, CharField) 적절한 HTML 입력 위젯으로 표현됩니다. 필드의 각 유형들은 Django 관리 사이트에서 어떻게 표현해되어야 할지 알고 있습니다.
- 각각의 DateTimeField 는 JavaScript 로 작성된 단축 기능과 연결됩니다. 날짜는 《오늘》(《Today》) 버튼과 달력 팝업에서 입력할 수 있으며, 시간은 《지금》(《Now》) 버튼과 일반적으로 입력하는 시간들을 제공하는 편리한 팝업을 통해서도 입력할 수 있습니다.

#### 페이지의 아래 부분에서 다음과 같은 몇가지 옵션을 제공합니다. (페이지에서 긁어옴)
- 저장(Save) – 이 유형의 객체에 대한 변경사항을 저장하고, 변경된 목록 페이지를 보여줍니다
- 저장 및 편집 계속(Save and continue editing) – 이 객체에 대한 변경사항을 저장하고, 현재 편집창을 갱신합니다
- 저장 및 다른 이름으로 추가(Save and add another) – 변경사항을 저장하고, 이 유형의 객체에 대한 비어있는 새로운 입력창을 불러옵니다
- 삭제(Delete) – 삭제를 확인하는 페이지를 띄웁니다.
- 만약 《Date published》 의 값이 Tutorial 1 에서 질문을 생성했을때의 시간과 일치하지 않는다면, TIME_ZONE (시간대) 설정을 깜빡 하신것일지도 모릅니다. 이 설정을 바꾸시고 다시 페이지를 불러오시면 올바른 값이 표현됩니다.
-《Date published》 의 값을 《오늘》(《Today》) 과 《지금》(《Now》) 단축버튼을 눌러 바꾸십시요. 그런 후, 《저장 및 편집 계속》(《Save and continue editing》) 을 누르십시요. 그런 후, 우측 상단의 《히스토리》(《History》) 버튼을 누르십시요. Django 관리사이트를 통해 누가(username) 언제(timestamp) 무엇을 바꾸었는지 목록을 확인할 수 있습니다.
 
## DJango 뷰
### 뷰 추가하기
- `polls/views.py` 에 뷰를 추가해봅시다. 
```.py
def detail(request, question_id):
    return HttpResponse("You're looking at question %s." % question_id)

def results(request, question_id):
    response = "You're looking at the results of question %s."
    return HttpResponse(response % question_id)

def vote(request, question_id):
    return HttpResponse("You're voting on question %s." % question_id)
```
- 다음의 path() 호출을 추가하여 이러한 새로운 뷰를 polls.urls 모듈로 연결해주세요.
```.py
from django.urls import path
from . import views

urlpatterns = [
    path('', views.index, name='index'),
    path('<int:question_id>/', views.detail, name='detail'), 
    path('<int:question_id>/results/', views.results, name='results'),
    path('<int:question_id>/vote/', views.vote, name='vote'),
]
```
- 이제 브라우저에 polls/34/ 입력하면 detail() 함수를 호출해 url에 입력한 id 를 호출해요. 다른 것도 같은 방식이에요.

### 뷰가 실제로 뭔가를 하도록 만들기
- 각 뷰는 두 가지중 하나는 하게되어있는데 요청된 페이지의 내용이 담긴 HttpResponse 객체를 반환하던가, 혹은 Http404 같은 예외를 발생하게 해줘요.
- 뷰는 DB레코드도 읽을 수 있고 서드 파티로 제공되는 템플릿 시스템도 사용 가능해요. PDF생성하거나 XML을 출력하거나 실시간 zip 파일도 만들 수 있어요. python의 어떤 라이브러리라도 사용 가능!
- 아래의 코드는 새로운 index() 뷰 하나를 호출했을 때, 시스템에 저장된 최소한 5 개의 투표 질문이 콤마로 분리되어, 발행일에 따라 출력됩니다.
```.py
from django.http import HttpResponse

from .models import Question


def index(request):
    latest_question_list = Question.objects.order_by('-pub_date')[:5]
    output = ', '.join([q.question_text for q in latest_question_list])
    return HttpResponse(output)
```
- 근데 저희는 페이지를 보여줄때 글자만 보여주진 않잖아요? HTML 형식으로 보여주기 때문에 `Templates` 라는 디렉토리를 만들어 템플릿들을 넣어봅시다.
- 템플릿에는 다음과 같은 코드를 입력합니다. (경로 : polls/templates/polls/index.html)
```.html
{% if latest_question_list %}
    <ul>
    {% for question in latest_question_list %}
        <li><a href="/polls/{{ question.id }}/">{{ question.question_text }}</a></li>
    {% endfor %}
    </ul>
{% else %}
    <p>No polls are available.</p>
{% endif %}
```
- 이제 템플릿을 이용하여 index 뷰를 업데이트 해볼게요
```.py

### from django.http import HttpResponse
### from django.template import loader

### from .models import Question


### def index(request):
    ### latest_question_list = Question.objects.order_by('-pub_date')[:5]
    ### template = loader.get_template('polls/index.html')
    ### context = {
        ### 'latest_question_list': latest_question_list,
    ### }
    ### return HttpResponse(template.render(context, request))


from django.shortcuts import render

from .models import Question


def index(request):
    latest_question_list = Question.objects.order_by('-pub_date')[:5]
    context = {'latest_question_list': latest_question_list}
    return render(request, 'polls/index.html', context)
```
- 이때 Django가 제공하는 단축 기능을 (shortcuts) 를 사용한다면 더 쉽게 작성 가능합니다. (주석 처리된게 render() 을 쓰기전 , 주석 처리가 되지 않은게  render() 을 쓴 후 입니다.)
- 모든 뷰에 적용한다면 loader 와 HttpResponse를 임포트하지 않아도됩니다. (
- render() 함수는 request 객체를 첫번째 인수로 받고, 템플릿 이름을 두번째 인수로 받으며. context 사전형 객체를 세번째 선택적 인수로 받습니다.
- 인수로 지정된 context로 표현된 템플릿의 HttpResponse 객체가 반환됩니다.
  
### 404에러 일으키기
- 4번 질문이 없는데 /4 라고 주소창에 치면 오류가 나야겠죠? 뷰의 코드를 조금 만져봅시다
```.py
from django.http import Http404
from django.shortcuts import render

from .models import Question
# ...
def detail(request, question_id):
    try:
        question = Question.objects.get(pk=question_id)
    except Question.DoesNotExist:
        raise Http404("Question does not exist")
    return render(request, 'polls/detail.html', {'question': question})
```
- 이제 뷰는 요청된 질문의 ID가 없을 경우 http404 예외를 발생시킵니다. 위의 예제를 동작시키기 위해 아래의 내용이 들어있는 파일도 작성해줍니다.
```.html
<!--polls/templates/polls/detail.html-->

{{ question }}
```
- 그러면 이제 존재하지 않은? 질문의 ID를 주소창에 입력하면 404 창이 뜨게됩니다.

### 지름길 : get_object_or_404()
- 객체가 존재하지 않을때 get() 을 사용해 Http404 예외를 발생시키는것은 자주 쓰이는 용법인데 Django에서는 이 기능에 대한 단축기능을 제공합니다.
```.py
### polls/views.py
from django.shortcuts import get_object_or_404, render

from .models import Question
# ...
def detail(request, question_id):
    question = get_object_or_404(Question, pk=question_id)
    return render(request, 'polls/detail.html', {'question': question})
```
- get_object_or_404() 함수는 Django 모델을 첫번째 인자로 받고, 몇개의 키워드 인수를 모델 관리자의 get() 함수에 넘깁니다. 만약 객체가 존재하지 않으면 404 예외가 발생합니다.

### 템플릿 시스템 사용하기
- detail() 뷰로 돌아가봅시다. context 변수 question 이 주어졌을때, polls/detail.html 이라는 템플릿이 어떻게 보이는지 봐봅시다.
```.html
<!-- polls/templates/polls/detail.html>
<h1>{{ question.question_text }}</h1>
<ul>
{% for choice in question.choice_set.all %}
    <li>{{ choice.choice_text }}</li>
{% endfor %}
</ul>

```
- 변수의 속성에 접근하기 위해 점-탐색 문법을 사용합니다. {{ question.question_text }} 구문을 보면 먼저 question 객체에 대해 사전형으로 탐색하고 탐색이 실패하면 속성값을 탐색. 만약 속성 탐색에서도 실패한다면 리스트의 인덱스 탐색을 시도하게됩니다.
- {% for %} 반복 구문에서 메소드 호출이 일어납니다. 
