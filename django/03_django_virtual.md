[TOC]



# 가상환경

## Virtual Environment

- 파이썬 인터프리터, 라이브러리 및 스크립트가 "시스템 파이썬"(즉, 운영 체제 일부로 설치되어있는 것)에 설치된 모든 라이브러리와 격리 되어있는 파이썬 환경
- 각 가상 환경은 고유한 파이썬 환경을 가지며 독립적으로 설치된 패키지 집합을 가짐
- 대표적인 가상 환경 지원 시스템
  - venv, virtualenv, conda, pyenv(Mac)
  - python 3.3 부터 venv가 기본 모듈로 사용
- 하나의 독립적인 프로젝트 구성, 라이브러리(버전) 관리, 협업을 위해 사용
- https://docs.python.org/ko/3/tutorial/venv.html

<br>

**프로젝트 시작 전 3단계**

1. `venv` **(new)**
2. `.gitignore`
3. `README.md`

<br>

**가상환경 구성**

- 생성

  ```bash
  $ python -m venv venv
  ```

  - `-m 모듈 인자` : 오른쪽에 나올 모듈을 인자와 함께 실행시켜줘
  - 가상화 하는 폴더의 이름을 venv로 해줘

- 활성화

  ```bash
  $ source venv/Scripts/activate
  ```

  ```
  (venv)
  ```

  - 경로의 파일을 실행시킨다.

- 비활성화

  ```bash
  $ deactivate
  ```

- 확인

  ```bash
  $ pip list
  ```

  ```bash
  Package    Version
  ---------- -------
  pip        20.1.1
  setuptools 47.1.0
  (venv) 
  ```

- 삭제
  
  - 비활성화 후 venv 폴더 삭제
- README.md
  
  - 파이썬 버전 명시

<br>

- 장고 설치 `pip install django`

<br>

**가상환경 라이브러리 기록 및 설치**

- `requirements.txt` 생성

  - 프로젝트를 구동하기 위한 필수 라이브러리를 기록

  1. 최상위 폴더 내에 requirements.txt 생성(건너뛰기 가능 - 자동 생성)

  2. 라이브러리 파일을 txt파일에 기록

     ```bash
     $ pip freeze > requirements.txt
     ```

     - `pip freeze` 라이브러리 파일을 그대로 보여준다

       ```bash
       $ pip freeze
       ```

       ```bash
       asgiref==3.3.1
       Django==3.1.7
       pytz==2021.1
       sqlparse==0.4.1
       (venv) 
       ```

- `requirements.txt` 기반 설치

  ```bash
  $ pip install -r requirements.txt
  ```

<br>

---

<br>

## **Fixture**

> django가 데이터베이스로 가져오는 방법을 알고 있는 데이터 모음
>
> json, YAML 등
>
> https://docs.djangoproject.com/ko/3.1/howto/initial-data/

### `Dump data`

>  `dump` : 그 상태를 그대로 저장하는 것. 
>
> `덤프를 뜨다`
>
> https://docs.djangoproject.com/en/3.1/ref/django-admin/#dumpdata

- `venv`와 `db.sqlite`를 git으로 관리하지 않기 때문에 `Fixture`로 `Dump data`를 공유
- db를 git으로 관리하지 않는 이유 : 각자 데이터 생성 시 db충돌이 일어나기 때문 

<br>

**Fixture 생성 및 공유**

- Fixtures 폴더 생성

  - `app/fixtures/appname`
  - 기본적인 구조가 Templtes와 같음
    - Fixtures내에 App이름과 같은 폴더가 존재하는 구조

- `app/fixtures/appname` 폴더 안에 json파일 저장

- `Dump data` 생성

  ```bash
  $ python manage.py dumpdata movies.movie
  # python manage.py dumpdata [App이름][.Model이름(소문자로)]
  ```

  - Model 이름을 소문자로 적어야 하는 것에 주의

  - INDENT 옵션

    ```bash
    python manage.py --indent 4 dumpdata movies.movie
    ```

- `git push`공유

**Fixture 공유받기**

- `git pull` 내려받기

- makemigrations, migrate 점검

- `loaddata`

  ```bash
  $ python manage.py loaddata /movies.json
  ```

  - 표(db.sqlite)의 형식에 맞춰서 json파일의 데이터를 입력(직렬화)
  - json 파일에 pk가 명시되어 있다면 고정값으러 덮어씌워지고, 그렇지 않다면 추가된다.

- 확인

  ```bash
  $ python manage.py runserver
  ```

<br>

---

<br>

> ### 수정에 따른 반영

> #### 1. 선언된 구조에 기반한 구조 번역본 생성

- `models.py` -> `makemigrations`

- model에 수정이 일어나면 기존 json 파일의 구조도 수정하거나 추가된 구조에 대한 디폴트값을 설정해주어야 함 (번거로움)
- 초기에 모델링을 잘 해두는 것이 중요함.

<br>

> ####  2. 구조 번역본에 기반한 표 생성

- `migrations/0001.initial.py` -> `migrations`
- 새로운 migration 파일이 생겼거나 db.sqlite(표)가 지워진 경우 진행

<br>

> #### 3. Fixtures 내부의 json형식의 dump data 수정본을 반영

- `app/fixtures/appname`내의  `movies.jason` 
  -> `$ python manage.py loaddata movies/movies.json`

<br>

---

<br>

> 알아두기

**충돌하는 과정**

- db.sqlite를 넘긴 뒤 각각 superuser을 생성
  - 아이디 ,비번을 같게 생성하더라도 생성된 시간과 환경에 따라서 저장되는 로직이 달라서 다른 데이터가 생성됨.
  - 각자 코드 수정 후 git push를 했을 때 충돌 알림이 뜨지만 db.sqlite는 충돌을 보기도어렵고 수정할수도 없음
  - 고로 json파일로 데이터를 주고받는 것이 적합.



















