[TOC]

Django에서 views.py를 구성하는 두가지 방법

- FBV (function based view)
- CBV (class based view)

# CBV

- "함수 단위가 아닌 클래스 단위"

## CBV 알아보기

> https://docs.djangoproject.com/ko/3.2/topics/class-based-views/intro/#

```bash
django-admin startproject cbv.
python -m venv venv
source venv/Scripts/activate
pip install django
python manage.py startapp articles
```

- settings.py 등록
- urls.py `path('articles/', include('articles.urls')),` 추가
- articles/urls.py

```python
from django.urls import path
from django.views.generic import TemplateView

urlpatterns = [
    path('about/', TemplateView.as_view(template_name="article/about.html")), # 방법 1
]
```

​	as_view라는 함수가 클래스에 있는 속성들을 가져와서 화면을 구성할 수 있도록 하는 메서드

​	실제로는 TemplateView를 그대로 실행하지 않고 이를 상속받아서 View를 만듬

- articles/templates/articles/about.html

```html
<h1>about</h1>
```

- TemplateView 상속받기

```python
# views.py

from django.shortcuts import render
from django.views.generic import TemplateView

def AboutView(TemplateView):
    template_name = 'articles/about.html'
```

​	TemplateView의 기능: Template파일을 render

​	ListView: 여러개의 데이터를 보여주는 뷰

```python
# urls.py
from .views import AboutView
urlpatterns = [
    path('about', AboutView.as_view()) # 방법 2. 가장 많이 구현하는 방식
]
```

- models.py

```python
from django.db import models

class Article(models.Model):
    title = models.CharField(max_length=50)
```

```bash
$ python manage.py makemigrations
$ python manage.py migrate
$ pip install django-seed # app 등록
$ python manage.py seed articles --number=10
```

### 이미 했던 방식 (FBV)

```python
# views.py

from django.shortcuts import render
from django.views.generic import TemplateView
from .models import Article

#
#
def index(request):
    if request.method == 'GET':
        articles = Article.objects.all()
        context = {
            'articles': articles
        }
        return render(request, 'articles/index.html', context)
```

```html
<h1>index</h1>
{{ articles }}
```

```python
# urls.py
path('index/', views.index)
```

### 새로운 방식 CBV

```python
# views.py
from django.views import View

class IndexView(View):
    def get(self, request): # GET방식, 아래는 똑같음
        articles = Article.objects.all()
        context = {
            'articles': articles
        }
        return render(request, 'articles/index.html', context)
        
```

```python
# urls.py
from .views import AboutView, IndexView # 추가

urlpatterns = [
    path('index2/', IndexView.as_view())
]
```

<br>

## 실제로 사용하기

> https://docs.djangoproject.com/ko/3.2/topics/class-based-views/generic-display/

- 쉬운 방법 : 제네릭 뷰 사용하기

새로운 방식에서 데이터를 보내는 방법

```python
# views.py
from django.views.generic import ListView # 추가

class ArticleListView(ListView): # 모델이름+상속받을뷰 # 추가
    model = Article
```

​	serializer와 유사

```python
# urls.py
from .views import AboutView, IndexView, ArticleListView # 추가

app_name = 'articles'

urlpatterns = [
    path('', ArticleListView.as_view(), name='index') # 추가
]

```

-  `앱이름/모델이름_view종류.html`을 찾으려 함
  - `article/article_list.html`
  - 이것이 우리가 template을 만들때 앱이름폴더를 한번 더 생성했던 이유!

- templates/article/article_list.html

```html
<h1>article index</h1>
{{ object_list }}

{ % for object in obejct_list % }
	<p>{{ object. title }}</p>
{ % endfor %}
```

​	{{ object_list }}: FBV의 {{ articles }}와 같음

​	articles는 article변수를 사용했는데 object라는 이름이 불편할 수 있음.

#### object 이름 바꾸기

```python
# views.py
class ArticleListView(ListView): # 모델이름+상속받을뷰 # 추가
    model = Article
    contzxt_object_name = 'articles' # 추가
```

- templates/article/article_list.html

```python
<h1>article index</h1>
{{ articles }}

{ % for article in articles % }
	<p>{{ article.title }}</p>
{ % endfor %}
```

#### model에 추가적인 데이터를 넣어 보여주고 싶을 때

```python
# views.py
class ArticleListView(ListView):
    model = Article
    context_object_name = 'articles'
    
    def get_context_data(self, **kwargs): # 이미 ListView에 있는 함수를 overide
        context = super().get_context_data(**kwargs)
        # super() 이미 있는건 그대로 실행을 해달라
        # context라는 데이터를 반환해줌
        context['name'] = 'Helia'
        return context
```

- templates/article/article_list.html

```python
<h1>article index</h1>
<!-- 추가 -->
<p>{{ name }}</p>
{{ articles }}

{ % for article in articles % }
	<p>{{ article.title }}</p>
{ % endfor %}
```

- 기존 CRUD와 login을 만드는 건 편하지만 커스터마이징을 해야할 때는 override가 귀찮음

#### 요소 정렬하기

```python
# views.py
class ArticleListView(ListView):
    model = Article
    context_object_name = 'articles'
    queryset = Article.objects.order_by('-id') # 추가
    template_name = 'articles/index.html' # template 이름도 바꿀 수 있음
    
    def get_context_data(self, **kwargs):
        context = super().get_context_data(**kwargs)
        context['name'] = 'Helia'
        return context
```

#### DetailView 사용하기

```python
# views.py
from django.views.generic import ListView, DetailView # 추가

class ArticleDetailView(DetailView):
    model = Article # 이것만 있어도 동작함
    # context_object_name = 'article' # 요소 이름 바꾸고 싶다면
    # template_name = 'articles/detail.html' # template 이름 바꾸고 싶다면
```

```python
# urls.py
from .views import AboutView, IndexView, ArticleDetailView # 추가
#
#
path('<int:pk>', ArticleDetailView.as_view(), name='detail'), # 추가
```

​	`articles/article_detail.html`파일을 자동으로 찾음

```html
<h1>detail</h1>
{{ object }}
{{ object.title }}
```

**조금 더 심화 : 동적 필터링, 추가 작업 수행**

- https://docs.djangoproject.com/ko/3.2/topics/class-based-views/generic-display/

#### 클래스 기반 뷰를 사용한 폼처리

> https://docs.djangoproject.com/ko/3.2/topics/class-based-views/generic-editing/

- 일반적으로 3개자 경로가 있음
  - GET - 폼 양식 제공
  - 유효하지 않은 POST - 폼 다시 표시
  - 유효한 POST - 데이터 처리하고 리디렉션
- FBV에서는 if문 분기처리, CBV에서는 FormView사용
  - ModelForm도 만들 필요가 없다고!

```python
# models.py

from django.db import models
from django.urls import reverse # 추가

class Article(models.Model):
    title = models.CharField(max_length=50)
    
    def get_absoulute.url(self):
        return reverse("articles:detail", kwargs={"pk": self.pk})
    # update를 할때 redirect위치를 만들어줌. pk값을 가져와서 그 detail로 이동
```

**CBV의 CRUD**

- ListView (R-N)
- DetailView (R-1)
- CreateView
- UpdateView
- DeleteView

**CREATE**

```python
# views.py
from django.views.generic import ListView, DetailView, CreateView # 추가

# 모델폼을 만들어주고 context로 html로 넘겨주며, 작성도 해주고 detail로 이동도 해줌
class ArticleCreateView(CreateView):
    model = Article
    fields = '__all__' # 모델폼과 같은 구조
    # 이 코드를 이용해서 모델폼을 만들고 그 폼을 이용해서 화면을 보여주도록 구성이 되어있음
```

```python
# urls.py
from .views import (AboutView, 
                    IndexView, 
                    ArticleListView,
                    ArticleDetailView,
                    ArticleCreateView, # 추가
) # 길어져서 구조 바꿈
#
#
path('create/', ArticleCreateView.as_view(), name='create')
```

- `articles/article_form.html`을 찾으려 함

```html
<h1>form</h1>

<form action="" method="POST">
    {% csrf_token %}
    {{ form }}
    <input type ="submit">
</form>
```

​	form이 생성됨. 제출하면 생성해주고 detail로 이동

​	어차피 자기자신 구조로 다시 보내면 처리해주기때문에 action이 비어있음

**UPDATE**

```python
# views.py
from django.views.generic import {ListView,
                                  DetailView,
                                  CreateView,
                                  UpdateView, # 추가
}

#
#

class ArticleUpdateView(UpdateView):
    model = Article
    fields = '__all__'
```

- urls.py
  - ArticleUpdateView 추가
  - `path('<int:pk>/update', ArticleUpdateView.as_view(), name='update'`

**DELETE**

```python
# views.py
from django.urls import reverse_lazy # 추가
from django.views.generic import {ListView,
                                  DetailView,
                                  CreateView,
                                  UpdateView, 
                                  DeleteView,# 추가
}

#
#

class ArticleDeleteView(DeleteView):
    model = Article
    success_url = reverse_lazy('articles:index') # app:urlname을 넣으면 그 url로 이동
```

urls.py

- ArticleDeleteView 추가
- `path('<int:pk>/delete', ArticleDeleteView.as_view(), name='delete'`

- `articles/article_confirm_delete.html`을 만들어짐
  - 삭제하시겠습니까?(Are you sure?) 전용 페이지를 띄워서 삭제하는 구조
    - Form으로 만들어져있음

articles/templates/articles/article_confirm_delete.html

```html
<h1>delete</h1>

<p>정말 삭제하시겠습니까?</p>
<form action="" method="POST">
    { % csrf_token %}
    <input type="submit">
</form>
```

- 삭제 버튼을 누르면 이 confirm페이지로 GET방식으로 이동하고, 이 안에서 POST 방식으로 삭제됨

#### 사용자 저장

```python
# models.py

from django.db import models
from django.urls import reverse 
from django.conf import settings # 추가

class Article(models.Model):
    title = models.CharField(max_length=50)
    user = models.ForeignKey(settings.AUTH_USER_MODEL, on_delete=models.CASCADE) # 추가, 유저 기록
    
    def get_absoulute.url(self):
        return reverse("articles:detail", kwargs={"pk": self.pk})
```

- makemigrations, migrate, 기존 data의 default user1이 작성한것으로 설정
  - create form에서 user란이 생김

```python
# views.py

from django.contrib.auth.mixins import LoginRequiredMixin

class ArticleCreateView(LoginRequiredMixin, CreateView): # 인자로 추가
    model = Article
    # fields = '__all__'
    fields = ('title',) # user말고 title만 보여줄 수 있도록 저장
```

- user 입력 후 저장 처리가 필요 -> LoginRequiredMixin 상속
   - login_required 데코레이터 동작과 같은 역할도 함
     	- 생성했을 때 로그인 안되어있으면 로그인 페이지로 리다이렉트, 넥스트도 있어서 로그인한뒤 어디로 갈지도 기록함

**로그인 기능 가져오기**

```bash
$ python manage.py startapp accounts # 등록
```

- app이 아닌 main!! urls.py

```python
# urls.py

path('accunts/', include('django.contrib.auth.urls')) # 원래는 'accounts.urls'를 넣었었음
```

- login, logout, password change, password reset 등을 구현해줌
- `registration/login.html`을 찾음
- accounts/templates/registration/login.html

```html
<h1>login</h1>
<form action="" method="POST">
    {% csrf_token %}
    {{ form }}
    <input type="submit">
</form>
```

- 로그인한 뒤 이동되는 곳은 settings에서 설정 가능

```python
# settings.py
# 최하단
LOGIN_REDIRECT_URL = 'articles:index'
# default는 /accounts/profile/
```

**게시물 생성 시 사용자 저장** (1:N)

```python
# views.py

class ArticleCreateView(LoginRequiredMixin, CreateView):
    model = Article
    fields = ('title',)
    
    def form_valid(self, form): # override
        form.instance.user = self.request.user # 현재 로그인한 사람
        return super().form_valid(form) # 하던거 계속해~
```

<br>

---

<br>

# test.py

- 사람이 하던 test를 코드로 작성

- setup()
  - 하나의 함수를 하나의 테스트 단위로 사용

```python
# test.py

from django.test import TestCase

# Create your tests here.
class ArticleTest(TestCase):
    def setUp(self):
        User = get_user_model()
        user = User.objects.create_user(username='test', password='123') # 회원가입
        Article.objects.create(title='hello', user=user) # 게시물
   	
    # 타이틀이 잘 저장되는지 확인하기 위한 테스트
    def test_article_title(self):
        article = Article.objects.get(pk=1)
        self.assertEqual(article.title, 'hello')
    
    # aritcle이 잘 생성되는지 확인하기 위한 테스트
    def test_article_create(self):
        c = Client()
        # 0. 로그인 확인 # 로그인을 안했을때 안들어가지는지(잘 막았는지) 검증
        res = c.get('/articles/create/')
        self.assertEqual(res.status_code, 302) 
        
        # 1. /articles/create/ 로 GET 요청 
        c. login(username='test', password='123')
        res = c.get('/articles/create/') # status 200 출력
        self.assertTemplateUsed(res, 'articles/article_form.html') # res가 가는곳에 이 문서가 있니
        self.assertContains(res, '<h1>form</h1>')
        
        # 2. /articles/create/ 로 POST 요청(invalid)
        res = c.post('/articles/create/')
        self.assertContains(res, 'This field is required')
        self.assertEqual(res.status_code, 200)
        
        # 3. /artices/create/ 로 POST 요청(valid)
        before = Article.objects.last()
        res = c.post('/articles/create/', {'title':'hi'})
        after = Article.objects.last()
        self.assertEqual(res.status_code, 302)
        self.assertEqual(res.url, '/article/2/')
        self.assertNotEqual(before, after) # 저장 전과 후의 마지막 게시물이 다른지 확인
        
    # article 리스트가 잘 출력되는지 확인하기 위한 테스트
   	def test_article_list(self):
        c = Client()
        res = c.get('/articles/')
        context_articles = res.context.get('articles')
        queryset_articles = Article.objects.all()
        queryset_articles = Article.objects.all()
        
        self.assertEqual(list(context_articles), list(queryset_articles))
        self.assertTemplateUsed(res, 'articles/article_list.html')
        
```

- 시작은 `test_`이어야 함

```bash
$ python manage.py test
```

- setup()은 공통적으로 매 함수마다 공통적으로 먼저 실행되는 것.
- c = Client()
  - 브라우저를 하나 띄우는 느낌. 요청을 보내고 확인해줌.
- res = 요청에 대한 응답 객체를 가져와 저장
- self.assertEqual(res.status_code, 302)
  - a와 b가 같은지 비교해줌
  - 같다면 통과, 다르다면 에러를 발생시킴 (AssertionError)
-  self.assertTemplateUsed(res, 'articles/article_form.html')
  - a가 가는 url에 문서 b가 있는지 알려줌

- self.assertContains(res, '<h1>form</h1>')
  - a가 간 문서에 b라는 내용이 있는지 알려줌
- 