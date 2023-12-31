## 목차

1. [간단한 코드 설명](#1-간단한-코드-설명)
2. [코드 전문](#2-코드-전문)
3. [message를 표시하고 싶을 경우](#3-message를-표시하고-싶은-경우)
4. [로그인을 했을 경우에만 편집, 삭제를 하고싶은 경우](#4-로그인을-했을-경우에만-편집-삭제를-하고싶은-경우)
---

참고 : [Working with forms | Django documentation | Django (djangoproject.com)](https://docs.djangoproject.com/en/4.2/topics/forms/)

 
## 1. 간단한 코드 설명

### 1. forms.py

-   forms.py에서는 `from django import forms` 안의 Form 클래스를 사용한다. 이 Form instance는 is\_valid() 메소드를 가지고 있는데, 얘들은 Form의 모든 field들이 유효한지를 검사한다. 그리고 이 메소드가 불러지고 Form의 필드들이 모두 유효한 데이터를 가지고 있다면
    1.  True를 리턴
    2.  form의 데이터들은 `cleaned_data`에 위치시킨다. 따라서 아래와 views.py안에 아래와 같이 코드를 작성한 것.

```
  if form.is_valid():
            username = form.cleaned_data['username']    # form안의 cleaned_data['username']을 username이라는 변수에 대입
            password = form.cleaned_data['username']
```
<br>

### 2. login.html

-   다음과 같이 작성할 수 있다.
-   `{% for field in form %} <div class="fieldWrapper"> {{ field.errors }} {{ field.label_tag }} {{ field }} {% if field.help_text %} <p class="help"> {{ field.help_text|safe }} </p> {% endif %} </div> {% endfor %}`
-   {{ field }} 가 가진 유용한 attribute들이 있다
    1.  `{{ field.errors }}` : `<ul class="errorlist">` 가 가진 모든 유효한 에러들의 결과값들이다.`{% for error in field.error %}`로 커스터마이징 가능하다. 이것을 이용해서 각 에러에 맞는 에러메시지 작성가능하다.
    2.  `{{ field.field }}` : form 클래스에서의 Field(속성값들?)에 관한 것이다. 따라서 Field attribute에 접근 가능. `{{ char_field.field.max_length}}`
    3.  `{{ field.help\_text }}` : field의 help text와 관련되어있다.
    4.  `{{ field.html\_name }}`
    5.  `{{ field.id\_for\_label }}` : 해당 field를 위해서 ID가 사용될 수 있다.
    6.  `{{ field.is\_hidden }}` : form field가 hidden filed거나 False 일 때 이 값이 True가ㅣ 된다.
    7.  `{{ field.label }}` : field의 라벨이다. 예를 들면 Email address 같은 것.
    8.  `{{ field.label\_tag}}` : field의 label들은 HTML의 `<laber> 태그`안에 감싸져 있다. 이것을 의미
    9.  `{{ field.value }}` : filed의 value. 예를 들면, [gildong@example.com](mailto:gildong@example.com)

<br>

---
<br>

## 2. 코드 전문

### 1. views.py

```python
from django.shortcuts import render, redirect
from .forms import LoginForm, RegisterForm
from django.contrib import messages
from django.contrib.auth import authenticate, login, logout
# Create your views here.

# =========================== login / logout ===========================
def sign_in(request):
    if request.method=='GET':
        form = LoginForm()
        return render(request, 'users/login.html', {'form' : form})

    elif request.method=='POST':
        form = LoginForm(request.POST)

        if form.is_valid():
            username = form.cleaned_data['username']
            password = form.cleaned_data['password']
            user=authenticate(request, username=username, password=password)
            if user is not None:
                login(request, user)
                messages.success(request,f'Hi {username.title()}, welcome back!')
                return redirect('posts')
            else:
                messages.error(request,"Invalid username or password")
                return render(request, 'users/login.html',{'form' : form})

def sign_out(request):
    logout(request)
    messages.success(request, f"You've been logged out")     
    return redirect('login')       


# =========================== 회원등록 ===========================
def sign_up(request,false=None):
    if request.method == 'GET':
        form = RegisterForm()
        return render(request,'users/register.html',{'form':form})
    elif request.method == 'POST' :
        form = RegisterForm(request.POST)
        if form.is_valid():
            user = form.save(commit=false)
            user.username = user.username.lower()
            user.save()
            messages.success(request,"You've signed up successfully")
            login(request,user) #signup에 성공하면 그것을 이용해서 바로 로그인
            return redirect('posts')
        else : 
            return render(request,'users/register.html',{'form':form})
```
<br>

### 2. urls.py

```python
from django.urls import path
from . import views

urlpatterns = [
    path('login/',views.sign_in,name="login"),
    path('logout/',views.sign_out, name='logout'),
    path('register/',views.sign_up, name="register")
]
```
<br>

### 3. form.py

```python
from django import forms
from django.contrib.auth.models import User
from django.contrib.auth.forms import UserCreationForm

class LoginForm(forms.Form):
    username = forms.CharField(max_length=65)
    password = forms.CharField(max_length=65, widget=forms.PasswordInput)

class RegisterForm(UserCreationForm):
    class Meta:
        model = User
        fields = ['username', 'email', 'password1','password2']  #model이 사용하는 모든 field
```
<br>

### 4. login.html

```html
{% extends 'base.html' %}

{% block content %}
<form method='POST' novalidate>
    {% csrf_token %}
    <h2>Login</h2>

    {% for field in form %}
    <p>
        {%if field.errors %}
        <ul class="errorlist">
            {% for error in field.errors%}
            <li> {{error}} </li>
            {% endfor %}
        </ul>
        {% endif %}
        {{ field.label_tag }} {{ field }}
    </p>
    {% endfor %}
    <input type="submit" value="Login" />
</form>
{% endblock content%}
```
<br>

### 5. register.html

```html
<!-- field가 가진 attribute 이용 -->
{% extends 'base.html' %}

{% block content %}
<form method="POST" novalidate>
    {% csrf_token %}
    <h2> Sign up </h2>
    {% for field in form %}
    <p>
        {% if field.errors %}
            {{field.errors}}
        {% endif %}
        {{field.label_tag}} {{field}}
    </p>
    {% endfor %}
    <input type = "submit" value = "Register" />
    <p> Already has an account? <a href = "{%url 'login'%}"> Login </a></p>
</form>
{% endblock content %}
```

<br>

---
<br>

### 6. 결과

1. login 화면
![login](login.PNG)

<br>

2. logout
127.0.0.1:8000/logout을 하면 바로 login 페이지로 redirect

<br>

3. register
![register](register.PNG)

<br>

---

<br>

## 3. message를 표시하고 싶은 경우
- base.html
```python
{%load static %}
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <link rel="stylesheet" href="https://www.w3schools.com/w3css/4/w3.css">
    <link rel="stylesheet" href="https://fonts.googleapis.com/css?family=Raleway">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css">
    <style>
    body,h1,h2,h3,h4,h5,h6 {font-family: "Raleway", sans-serif}
    </style>
    <script src="{% static 'js/app.js' %}" defer></script>
    <title>My Site</title>
</head>
<body>
    <header>
        {% if request.user.is_authenticated %}
            <a href="{%url 'posts' %}"> My Posts </a>
            <a href="{%url 'post-create' %}"> New Posts </a>
            <span> Hi {{ request.user.username | title }} </span>
            <a href="{%url 'logout' %}"> Logout </a>
        {% else %}
            <a href="{%url 'login' %}"> Login </a>
            <a href="{%url 'register' %}"> Register </a>
        {% endif %}
    </header>
<main>
    {% if messages %}
        <div class = "messages">
            {% for message in messages %}
                <div class="alert {% if message.tags %} alert-{{message.tags}}"{% endif %}>
                    {{ message }}
                </div>
            {% endfor %}
        </div>
    {% endif %}
    {% block content %}
    {% endblock content %}
</main>
</body>
</html>
```

<br>


### 1. 결과
![msg](msg.PNG)

<br>

---

<br>

## 4. 로그인을 했을 경우에만 편집, 삭제를 하고싶은 경우
- blog/views.py

```python
from django.shortcuts import render, redirect, get_object_or_404
from django.http import HttpResponse
from django.contrib import messages
from .models import Post
from .forms import PostForm

from django.contrib.auth.decorators import login_required

# Create your views here.

def home(request):
    posts=Post.objects.all()
    context = {'posts' : posts}
    return render(request, 'blog/home.html', context)

def about(request):
    return render(request, 'blog/about.html')

def web01(request):
    return HttpResponse('<h1> Web01 page </h1>')

def web02(request):
    return HttpResponse('<h1> Web02 page </h1>')

#====================================

@login_required
def create_post(request):
    if request.method=='GET':
        context={'form':PostForm()}
        return render(request, 'blog/post_form.html', context)
    elif request.method == 'POST':
        form = PostForm(request.POST)
        if form.is_valid():
            form.save()
            return redirect('posts')    #path('', views.home, name="posts"),
        else:
            return redirect(request,'blog/post_form.html', {'form':form})
        
#====================================

@login_required
def edit_post(request,id):
    queryset = Post.objects.filter(author=request.user)
    post = get_object_or_404(queryset,id=id)
    
    # post=get_object_or_404(Post, id=id) #원본 : URL 패턴과 일치하지 않으면 404로 리턴
    if request.method=='GET':   # get : http://127.0.0.1:8000/post/edit/1
        context={'form': PostForm(instance=post),'id':id}
        return render(request,'blog/post_form.html',context)
    elif request.method == 'POST':
        form = PostForm(request.POST, instance=post)
        if form.is_valid():
            form.save()
            messages.success(request,'The post has been updated successfully.')
            return redirect('posts')
        else:
            messages.error(request,'Please correct the following errors:')
            return render(request,'blog/post_form.html',{'form':form})
            
            
@login_required    
def delete_post(request,id):
    queryset = Post.objects.filter(author=request.user)
    post=get_object_or_404(queryset,id=id)
    # post=get_object_or_404(Post,id=id)
    context={'post':post}
    if request.method == 'GET': # get : http://127.0.0.1:8000/post/delete/1
        return render(request,'blog/post_confirm_delete.html',context)
    elif request.method == 'POST':
        post.delete()
        messages.success(request,'The post has been deleted successfully.')
        return redirect('posts')
```

- blog/home.html

```html
{% extends 'base.html' %}
{% block content %}
<h1>My Posts</h1>
{% for post in posts%}
<h2>{{ post.title }}</h2>
<small>Published on {{ post.published_at }} by {{ post.author}}</small>
<p>{{ post.content }}</p>

{% if request.user.is_authenticated and reques.user == post.author %}
<p>
    <a href="{% url 'post-edit' post.id %}"> Edit</a>
    <a href="{% url 'post-delete' post.id %}"> Delete </a>
</p>
{% endif %}

{% endfor%}
{% endblock %}
```

### 결과

- 로그인 했을 때
![login](login.isvalid.PNG)

- 로그아웃 했을 때
![logout](whenloggedout.PNG)











