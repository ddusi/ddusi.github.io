2020-02-10-django url include multiple



## 3.django urls include를 여러개 써서 효율적인 관리

### django url include multiple





​	django를 쓸 때, 프로젝트의 url을 include를 써서 고정적인 url을 쉽게 관리하거나, 앱별로 url을 관리 할 수 있는 강력한 기능이 있다.  하지만 나는 사용하면서 하나의 app에 하나의 urls.py파일로 손쉽게 관리할 수 없을까 하는 마음에 검색해보게 되었다.



- project/ urls.py

```python
from django.contrib import admin
from django.urls import path,include
from mainapp import views
from mainapp.main import views as main_views

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('mainapp.urls')),# 추가 부분
]
```



include기능으로 일단 mainapp.urls 를 불러온다. 

그리고 나서 mainapp의 urls파일을 만든다.



- mainapp/ urls.py

```python
from django.urls import path, include
from . import views
from mainapp.main import views as main_views
from mainapp.video import views as video_views

# /main 으로 시작하는 하위 url 설정
main_patterns = [
    path('',main_views.main),
    path('signup/', main_views.signup, name='signup'),
    path('signin/', main_views.signin, name='signin'),
]

# /video 으로 시작하는 하위 url 설정
video_patterns = [
    path('', video_views.swipe),
    path('show/', video_views.show, name='show'),
    path('detail/<int:id>', video_views.detail, name='detail'),
    path('like/', video_views.like, name='like'),
]

# 변수로 설정한 값을 include함.
urlpatterns = [
    path('main/', include(main_patterns)),
    path('video/', include(video_patterns)),
]
```



mainapp의 urls파일이 핵심이다. 여기에서 각각의 url들을 inport할때 각각 변수를 선언하여 include를 한다.  이 때, 알아보기 쉽게 짜는게 중요! 



이렇게 코드를 짠다면 이제 app 하나에 여러개의 url에 include를 사용할 수 있다. 

그리고나서 app 하위폴더로 각각의 폴더를 만들어 view.py를 만든다. 



- mainapp/main/view.py

```python
from django.shortcuts import render, redirect
from django.http import HttpResponse


def main(request): #메인 화면
    return render(
    request, 
    'mainapp/index.html', 
    {})
```



- mainapp/video/view.py

```python
from django.shortcuts import render, redirect
from django.core import serializers
from django.http import HttpResponse, JsonResponse
from mainapp.models import *
from scipy.spatial import distance
from django.utils import timezone


def video(request): #video 페이지
    return render(request, 'mainapp/video.html', {})

def show(request): #show 페이지
    return render(request, 'mainapp/show.html', {})

def like(request): #like 페이지
    return render(request, 'mainapp/like.html', {})

def mypage(request): #mypage 페이지
    return render(request,
    'mainapp/mypage.html',
    {})
```



불편함이라면 각각의 하위폴더별로 view를 관리해야한다는 점이 있지만, url들을 한눈에 쉽게 관리 할 수 있다.







참고: https://www.webforefront.com/django/consolidatedjangourls.html