<!-- 목차 -->
---
- [장고 개요](#장고-개요)
- [주요 프레임워크 컴포넌트](#주요-프레임워크-컴포넌트)
<!-- -->

---
---

# 장고 개요
> 장고는 컴포넌트로 구성된 프레임워크이다
> - 장고 컴포넌트는 느슨하게 결합되어 있어 독립적으로 관리할 수 있으며, 여러 계층의 책임을 분리하는데 이점이 있다
> - 코드 재사용성을 최대로 제공한다
> - introspection과 같은 python의 동적 기능을 활용해 코드의 양을 줄여준다

---
## 주요 프레임워크 컴포넌트
### __MTV(Model-Template-View) 패턴을 따른다__
> - __모델__\
논리적 데이터 구조를 정의하는 데이터베이스와 뷰 사이의 데이터 핸들러이다
> - __템플릿__\
프레젠테이션 계층으로 장고는 브라우저가 렌더링하는 모든 것을 가진 일반 텍스트 템플릿 시스템을 사용한다
> - __뷰__\
모델을 통해 데이터베이스와 통신하고 뷰를 위해 데이터를 템플릿으로 전송한다

프레임워크 자체가 컨트롤러의 역할을 한다\
개발 시 항상 모델, 뷰, 템플릿 및 URL로 작업한다

---
## 장고가 HTTP 요청을 처리하고 응답을 생성하는 방법
> 1. 웹 브라우저가 URL로 페이지를 요청하고 웹 서버가 HTTP 요청을 장고에 전달한다
> 2. 장고는 설정된 URL 패턴을 살펴보고 처음으로 일치하는 URL 패턴을 발견한다
> 3. 장고는 일치하는 URL 패턴에 해당하는 뷰를 실행한다
> 4. 뷰는 가능한 데이터 모델을 사용해 데이터베이스로부터 정보를 검색한다
> 5. 데이터 모델은 데이터 정의 및 동작을 제공하며 데이터베이스에 질의하는 데 사용된다
> 6. 뷰는 템플릿(일반적으로 HTML)을 렌더링하여 데이터를 표시하고 HTTP 응답과 함께 반환한다
+ 추가로 장고는 요청/응답 프로세스에 미들웨어라고 하는 후크를 포함하고 있다

---
## 프로젝트 생성
__초기 프로젝트 파일 구조 생성__ \
`django-admin startproject mysite`
> - __manage.py__ \
프로젝트와 상호작용할 때 사용하는 커맨드라인 도구
> - __mysite/__init__.py__ \
mysite 디렉터리를 python 모듈로 취급하도록 python에 지시하는 빈 파일
> - __mysite/asgi.py__ \
ASGI 호환 웹서버와 함께 ASGI(Asynchronous Server Gateway Interface) 애플리케이션으로 프로젝트를 실행하기 위한 구성
>   - ASGI는 비동기 웹 서버 및 애플리케이션을 위한 python 표준
> - __settings.py__ \
프로젝트 설정 및 구성하며 초기 기본 설정을 포함
> - __urls.py__ \
URL 패턴이 정의되며 이곳에 정의된 각 URL은 뷰에 매핑됨
> - __wsgi.py__ \
WSGI 호환 웹 서버와 함께 WSGI(Web Server Gateway Interface) 애플리케이션으로 프로젝트를 실행하기 위한 구성

---
## 초기 데이터베이스 마이그레이션 적용
- 기본 구성은 SQLite3으로 설정되어있다
- 프로젝트 폴더로 이동해 `python manage.py migrate` 명령어로 `INSTALLED_APPS` 설정에 열거된 애플리케이션을 위한 테이블들이 데이터베이스에 생성된다

## 개발 서버 실행
- 프로덕션 서버를 구성하기 위한 시간을 소비하지 않고 빠르게 코드를 실행할 수 있는 경량 웹서버가 포함되어있다
- 코드의 변경 사항을 지속적으로 확인해 반영해준다
`python manage.py runserver`
> - 다만 이 서버는 개발 전용으로 프로덕션 용도로 적합하지 않다

---

## 프로젝트 설정
### settings.py 파일
> - __DEBUG__ \
프로젝트의 디버그 모드를 설정하는 옵션이다 \
True일 경우 애플리케이션에서 처리하지 않은 예외가 발생할 때 자세한 오류 페이지를 표시한다 \
민감한 데이터가 노출될 수 있으므로 프로덕션 환경에서는 반드시 False로 설정해야한다

> - __ALLOWED_HOSTS__ \
장고 사이트를 제공할 수 있도록 이 설정에 도메인/호스트를 추가해야한다
DEBUG가 True이거나 테스트가 동작 중일 때는 적용되지 않는다

> - __INSTALLED_APPS__ \
장고에게 이 사이트에서 어떤 애플리케이션들을 활성화할지 알려주는 설정으로 모든 프로젝트에서 편집해야한다 \
기본적으로 장고에 포함되어있는 애플리케이션은 다음과 같다 \
    django.contrib.admin: 관리 사이트 \
    django.contrib.auth: 인증 프레임워크 \
    django.contrib.contenttypes: 콘텐츠 유형 처리를 위한 프레임워크 \
    django.contrib.sessions: 세션 프레임워크 \
    django.contrib.messages: 메시징 프레임워크 \
    django.contrib.staticfiles: 정적 파일 관리 프레임워크 \

> - __MIDDLEWARE__ \
실행할 미들웨어가 포함되어있는 목록

> - __ROOT_URLCONF__ \
애플리케이션의 루트 URL 패턴이 정의된 파이썬 모듈

> - __DATABASES__ \
프로젝트에서 사용할 모든 데이터베이스 설정을 포함하는 딕셔너리
항상 기본 데이터베이스가 있어야한다
기본 구성은 SQLite3이다

> - __LANGUAGE_CODE__ \
장고 사이트의 기본 언어 코드 설정

> - __USE_TZ__ \
장고에 시간대 지원 여부를 설정하는 옵션이다 \
장고는 시간대를 인식하는 datetime을 지원한다 \
이 설정은 startproject 관리 명령으로 새 프로젝트를 생성 시 True로 설정된다

---

## 프로젝트와 애플리케이션
> - __프로젝트__ \
몇 가지 설정이 있는 장고의 설치 \
다른 장고 프로젝트에서도 사용할 수 있는 블로그, 위키 또는 포럼 같은 여러 애플리케이션을 포함하는 웹사이트로 설명할 수 있다

> - __애플리케이션__ \
모델, 뷰, 템플릿 및 URL의 그룹 \
애플리케이션은 프레임워크와 상호작용을 통해 특정 기능을 제공하고 다양한 프로젝트에서 재사용할 수 있다

---

## 애플리케이션 생성하기
#### 블로그 애플리케이션
> - **\_\_init\_\_.py** \
블로그 디렉터리를 파이썬 모듈로 취급하도록 지시하는 빈 파일

> - __admin.py__ \
장고 관리 사이트에 포함할 모델을 등록하는 곳 \
선택 사항이다

> - __apps.py__ \
blog 애플리케이션의 주요 구성이 포함되는 곳

> - __migrations__ \
애플리케이션의 데이터베이스 마이그레이션이 포함되는 곳 \
마이그레이션으로 장고는 모델 변경 사항을 추적하고 데이터베이스를 동기화할 수 있다

> - __models.py__ \
애플리케이션의 데이터 모델이 포함되는 곳 \
장고 애플리케이션에 필수적이지만 비워 둘 수 있다

> - __test.py__ \
애플리케이션을 위한 테스트를 추가하는 곳

> - __views.py__ \
애플리케이션의 로직이 위치하는 곳
각 뷰는 HTTP 요청을 수신해서 처리하고 응답을 반환한다

---

## 블로그 데이터 모델 만들기
- 장고 모델은 데이터의 정보와 동작의 근원이다
- django.db.models.Model의 하위 클래스인 파이썬 클래스로 구성된다
- 각 모델은 데이터베이스 필드가 클래스의 각 속성을 표현하는 단일 데이터베이스 테이블에 매핑된다
- 모델을 만들 때 장고는 데이터베이스의 객체를 쉽게 쿼리할 수 있는 API를 제공한다

## 게시물 모델 만들기
이전에 생성한 blog의 models.py 파일을 수정해
블로그 게시물(Post)을 데이터베이스에 저장할 수 있는 Post 모델을 정의한다

``` python
from django.db import models

class Post(models.Model):
    title = models.CharField(max_length=250)
    slug = models.SlugField(max_length=250)
    body = models.TextField()

    def __str__(self):
        return self.title
```
제목(title), 짧은 레이블(slug), 본문(body)로 데이터 모델을 생성하는 코드

> - __title__ \
게시물의 제목 필드 \
SQL 데이터베이스의 VARCHAR로 변환되는 CharField 필드이다

> - __slug__ \
SQL 데이터베이스에서 VARCHAR로 변환되는 SlugField 필드이다 \
slug는 문자, 숫자, 밑줄, 하이픈만 포함하는 짧은 레이블이다 \

> - __body__ \
게시물의 본문을 저장하는 필드이다 \
SQL 데이터베이스의 TEXT 칼럼으로 변환되는 TextField 필드이다

+ 모델 클래스의 \_\_str\_\_() 매서드는 객체를 표현하는 문자열을 반환하는 파이썬의 기본 메서드이다 \
장고는 이 메서드를 사용해 장고 관리 사이트와 같은 여러 위치에서 객체의 이름으로 표시한다

장고는 모델 필드에 맞는 데이터베이스 칼럼을 생성한다 \
장고는 기본적으로 각 모델에 자동으로 증가하는 기본(primary) 키 필드를 추가한다 \
+ 기본 키 필드의 유형은 각 애플리케이션 구성 혹은 DEFAULT_AUTO_FIELD 설정을 통해 전역적으로 지정된다
+ startapp 명령어로 애플리케이션을 생성할 때 DEFAULT_AUTO_FIELD의 기본 값은 BigAutoField이다 (64비트 정수 ID)
+ 모델 기본 키를 지정하지 않으면 장고가 이 필드를 자동으로 추가한다

모델 필드에 primary_key=True를 설정해 모델 필드 중 하나를 기본 키로 정의할 수 있다


## datetime 필드 추가하기
게시물의 게시 날짜와 시간을 저장할 필드를 생성한다 \
Post 객체가 생성되고 마지막으로 수정된 날짜와 시간을 저장한다
``` python
from django.db import models
from django.utils import timezone

class Post(models.Model):
    title = models.CharField(max_length=250)
    slug = models.SlugField(max_length=250)
    body = models.TextField()
    publish = models.DateTimeField(default=timezone.now)
    created = models.DateTimeField(auto_now_add=True)
    updated = models.DateTimeField(auto_now=True)

    def __str__(self):
        return self.title
```
> - __publish__ \
SQL 데이터베이스의 DATETIME 칼럼으로 변환되는 DateTimeField 필드이다 \
게시물이 게시된 날짜와 시간을 저장하는데 사용한다 \
__timezone.now__는 시간대를 인식하여 알맞은 형식으로 datetime을 반환한다

> - __created__ \
DateTimeField 필드이다 \
게시물이 생성된 날짜와 시간을 저장하는데 사용한다 \
__auto_now_add__ 를 사용해 객체를 생성할 때 날짜를 자동으로 저장한다

> - __updated__ \
DateTimeField 필드이다 \
게시물이 갱신된 마지막 날짜와 시간을 저장하는데 사용한다 \
__auto_now__ 를 사용해 객체가 저장될 때 날짜를 자동으로 갱신한다

## 기본 정렬 순서 정의하기
