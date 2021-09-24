# TIL_Django3

## Django Form

- Form은 Django 프로젝트의 주요 유효성 검사 도구들 중 하나이며, 공격 및 우연한 데이터 손상에 대한 중요한 방어수단
- 단순화하고 자동화 할 수 있음, 안전하게 수행가능



###  Form 선언하기

```python
# articles/forms.py
from django import forms

class ArticeForm(forms.Form):
    title = forms.CharField(max_lenth=10)
    content = forms.Charfield()
```

- Model을 선언하는 것과 유사, 필드 타입 用
- forms 라이브러리에서 파생된 Form 클래스를 상속받음



### Form 사용하기

```python
# articles/views.py
from .forms import ArticleForm

def new(request):
    form = ArticleForm()
    context = {
        'form': form,
    }
    return render(request, 'articles/new.html', context)
```



### Form rendering options

- <label> 과 <input> 쌍에 대한 3가지 옵션

1. as_p()

   - 각 필드가 단락(<p>태그)으로 감싸져서 렌더링 됨

2. as_ul()

   - 각 필드가 목록 항목(<li>태그)으로 감싸져서 렌더링 됨

   - <ul> 태그는 직접 작성해야 함

     </ul>

3. as_table()

   - 각 필드가 테이블(<tr>태그) 행으로 감싸져서 렌더링 됨

   - <table> 태그는 직접 작성해야 함

### Django의 HTML input 요소 표현

- Form fields

  - input에 대한 유효성 검사 로직을 처리, 템플릿에서 직접 사용

- Widgets

  - 웹 페이지의 HTML input 요소 렌더링
  - GET/POST 딕셔너리에서 데이터 추출
  - 하지만 widgets은 반드시 form fields에 할당
  - 웹페이지에서 input element의 단순 raw한 렌더링 처리

  ``` python
  from django import forms
  
  class ArticleForm(forms.Form):
      title = forms.CharField(max_lengh=10)
      content = forms.CharField(widget=forms.Textarea)
  ```

  

  ```python
  # articles/forms.py
  from django import forms
  
  class ArticleForm(forms.Form):
      REGION_A = 'sl'
      REGION_B = 'dj'
      REGION_C = 'gm'
      REGION_D = 'gj'
      REGION_E = 'bs'
      REGIONS_CHOICES = [
          (REGION_A, '서울')
          (REGION_B, '대전')
          (REGION_C, '구미')
          (REGION_D, '광주')
          (REGION_E, '부산')
      ]
      title = forms.Charfield(max_length=10)
      content = forms.Charfield(widget=forms.Textarea)
      region = forms.Charfield(choice=REGIONS_CHOICES, widget=forms.Select())
      
  ```

  

## Model Form

```python
# articles/forms.py
from django import forms
from .models import Article

class ArticleForm(forms.ModelForm):
    
    class Meta:
        model = Article
        fields '__all__'
   
    
```



### Meta class

- Model의 정보를 작성하는 곳
- ModelForm을 사용할 경우 사용할 모델이 있어야 하는데, Meta class가 이를 구성함

- Inner Class
  - 클래스 내에 선언된 다른 클래스
  - 관련 클래스를 함께 그룹화 하여 가독성 및 프로그램 유지 관리를 지원
  - 외부에서 내부 클래스에 접근할 수 없으므로 코드의 복잡성을 줄일 수 있음
- Meta 데이터
  - "데이터에 대한 데이터"
  - ex) 사진촬영 - 사진 데이터 - 사진의 메타 데이터 = 촬영시각, 렌즈,  조리개 값



### create view 수정

```python
# article/views.py

def create(request):
    form = ArticleForm(request.POST)
    if form.is_valid():
        article = form.save()
        return redirect('articles:detail', article.pk)
    return redirect('articles:new')

# is valid()
- 유효성 검사 실행, boolean으로 반환

# save()
- form에 바인딩 된 데이터에서 데이터 베이스 객체를 만들고 저장
- ModelForm의 하위(sub) 클래스는 기존 모델 인스턴스를 키워드 인자 isntance로 받아 들일 수 있음
- 이것이 제공되면 해당 인스턴스를 업데이트
- 제공되지 않으면 지정된 모델의 새 인스턴스를 만듦

```



```python
form = ArticleForm(request.POST)

new_article = f.save()

article = Article.objects.get(pk=1)
form = ArticleForm(request.POST, instance=article)
form.save()
```



### create View 함수 구조 변경

```python
def create(request):
    if request.method == 'POST':
        form = ArticleForm(request.POST)
        if form.is_valid():
            article = form.save()
            return redirect('articles:detail', article.pk)
     else:
        form = ArticleForm()
     context = {
         'form': form,
     }
    return render(request, 'articles/create.html', context)
```



### Widgets 적용하기

```python
# 첫번째 방식
# articles/forms.py

class ArticleForm(forms.ModelForm):
    
    class Meta:
        model = Article
        fields = '__all__'
        widgets = {
            'title': forms.TextInput(attrs={
                'class': 'title',
                'placeholder': 'Enter the title',
                'maxlength': 10,
                }
             )
         }
```

```python
#두번째 방식(권장)
class ArticleForm(forms.ModelForm):
    title = forms.CharField(
    	label='제목',
    	widget=forms.TextInput(
        	attrs={
                'class': 'my-title',
                'placeholder': 'Enter the title',
            }
        ),
    )
    
    class Meta:
        model = Article
        fields = '__all__'
```



### DELETE

```python
# views.py

def delete(reqeust.pk):
    article = Article.objectsget(pk=pk)
    if request.method == 'POST':
        article.delete()
        return redirect('articles:index')
    return redirect('articles:detail', article.pk)
```



### UPDATE

```python
def update(request, pk):
    article = Article.ojbects.get(pk=pk)
    if request.method == 'POST':
        form = ArticleForm(request.POST, instance=article)
        if form.is_valid():
            form.save()
            return redirect('articles:detail', article.pk)
        
     else:
        form = ArticleForm(instance=article)
     context = {
         'form': form,
     }
    return render(request, 'articles/update.html', context)
```



### Form & ModelForm

- Form
  - 어떤 Model에 저장해야 하는지 알 수 없으므로 유효성 검사 이후 cleaned_data 딕셔너리를 생성
  - cleaned_data 딕셔너리에서 데이터를 가져온 후 .save() 호출
  - model에 연관되지 않는 데이터를 받을 때 사용
- ModelForm
  - django가 해당 model에서 양식에 필요한 대부분의 정보를 이미 정의
  - 어떤 레코드를 만드러야 할 지 알고 있으므로 바로 .save() 호출 가능





## Handling HTTP reqeusts



### Django shortcuts functions

- django.shortcuts 패키지는 개발에 도움 될 수 있는 여러 함수와 클래스 제공
- shortcuts functions 종류
  - render()
  - redirect()
  - get_object_or_404()
    - 모델 manager objects에서 get()을 호출하지만, 해당 객체가 없을 경우 DoesNotExist 예외 대신 Http 404를 띄움
    - get()메서드에 경우 조건에 맞는 데이터가 없을 경우 에러 발생
  - get_list_or_404()



### Django View decorators

- Django는 다양한 HTTP 기능을 지원하기 위해 뷰에 적용할 수 있는 여러 데코레이터를 제공

- Allowed HTTP methods
  - 요청 메서드에 따라 view 함수에 대한 엑세스 제한
  - 요청이 조건을 충족시키지 못하면 405 Method Not Allowed 리턴
  - require_http_methods(), require_POST(), require_safe()
- require_http_methods()
  - view 함수가 특정한 method 요청에 대해서만 허용
- require_POST()
  - view 함수가 POST method 요청만 승인하도록 하는 데코레이터

```python
@require_http_method(['GET', 'POST'])
def create(request):
    pass

@require_POST
def delete(request, pk):
    article = get_object_or_404(Article, pk=pk)
    article.delete()
    return redirect('articles:index')
```

