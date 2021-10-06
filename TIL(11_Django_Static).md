# TIL_Django_Static

## Static fiels

- 정적 파일
- 응답할 때 별도의 처리 없이 파일 내용을 그대로 보여주면 되는 파일

## STATIC_ROOT

- collectstatic이 배포를 위해 정적 파일을 수집하는 디렉토리의 절대 경로
- django 프로젝트에서 사용하는 모든 정적 파일을 한 곳에 모아 넣은 경로
- 개발 과정에서 setting.py의 DEBUG 값이 True로 설정되어 있으면 해당 값은 작용되지 않음
- 실 서비스 환경에서 django의 모든 정적 파일을 다른 웹 서버가 직접 제공

```python
# settings.py
STATIC_ROOT = BASE_DIR / 'staticfiles'

$ python manage.py collectstatic
```



### STATIC_URL

- STATIC_ROOT에 있는 정적 파일을 참조할 때 사용할 url
- 실제 파일이나 디렉토리가 아니며, url로만 존재
- 비어있지 않은 값으로 설정한다면 반드시 / 로 끝나야함

```python
# settings.py

STATIC_URL = '/static/'
```



### STATIC_DIRS

- app/static/ 디렉토리 경로를 사용하는 것 외에 추갖거인 정적 파일 경로를 정의

```python
STATICFILES_DIRS = [
    BASE_DIR / 'static',
]
```



### 정적파일 사용하기

```django
# articles/detail.html

(% extends %)
{% load static %} --- # load 필수!!

~~~~~~~
	<img src="{% static 'articles/sample-img-1.png' %}" alt="sample-img">

```



## Media file

- 사용자가 웹에서 업로드하는 정적 파일
- 유저가 업로드 한 모든 정적 파일



### ImageField

- 이미지 업로드에 사용되는 모델 필드
- FileField를 상속받는 서브 클래스이기 때문에 FileField의 모든 속성 및 메서드를 사용 가능, 사용자에 의해 업로드 된 객체가 유요한 이미지인지 검사
- 최대 길이 100자인 문자열로 DB에 생성, max_length로 변경 가능
- Pillow 라이브러리 설치 필요
- $ pip install Pillow



### FileField

- 파일 업로드에 사용되는 모델 필드

- 2개의 선택인자 가지고 있음

  - storage

  - upload_to
    - 문자열 값이나 경로 지정
    - 함수 호출
    - instance / filename을 인자로 사용함(必)

```python
# Model.py
class MyModel(models.Model):
    # MEIDA_ROOT/uploads/ 경로로 파일 업로드
    upload = models.FileField(upload_to='uploads/')
```

```python
#models.py

def articles_image_path(instance, filename):
    return f'user_{instance.user.pk}/{filename}'

class Article(models.Model):
    image = models.ImageField(upload_to=articles_image_path)
```



### MEDIA_ROOT

- 사용자가 업로드 한 파일들을 보관할 디렉토리의 절대 경로
- 성능을 위해 데이터베이스에 저장 X
- STATIC_ROOT와 반드시 다른 경로로 지정

```python
# setting.py
MEDIA_ROOT = BASE_DIR / 'media'
```

### MEDIA_URL

- MEDIA_ROOT 에서 제공되는  미디어를 처리하는  URL
- 업로드된 파일의 주소를 만들어 줌
- 비어있지 않은 값이면 /로 끝나야함 必
- STATIC)_URL과 다른 경로로 지정!

```python
MEDIA_URL = '/media/'
```



```python
# crud/urls.py

from django.contrib import admin
from django.urls import path, include
from django.conf import settings
from django.conf.urls.static import static

urlpatterns = [
    path(~~~~~~),
    path(~~~~)
] + static(settings.MEIDA_URL, decument_root=settings.MEDIA_ROOT)
```



## 이미지 업로드

### ImageField

- upload_to='images/'
  - 실제 이미지가 저장되는 경로
- blank=True
  - 이미지 필드에 빈 값 허용

```html
<!-- articles/create.html -->  
									# 인코딩 속성 
<form action="{% ~~}" method="POST" enctype="multipart/form-data">
                                    
    <input ~~~~ accept="image/*"> --> 업로드시 이미지파일만 보이게 설정
</form>
```

```python
# view.py
def create(request):
    ~~~~~~
    ~~~~
    form = ArticleForm(request.POST, request.FILES) --> 순서 중요
    # Data, File 순이기 때문에 위치인자로만 생성
```



## 이미지 Resizing

- 실제 원본 이미지를 서버에 그대로 업로드 하는 것은 서버의 부담이 큰 작업
- 업로드 될 때 이미지 자체를 resizing 하는 것
- django-imagekit 설치
- INSTALLED_APPS에 추가

```python
$ pip install django-imagekit

INSTALLED_APP = [
    '''
    'imagekit',
    '''
]
```

