장고에서 프로젝트를 시작할 때 `django-admin startproject mysite` 명령어를 사용해서 프로젝트를 시작하곤 한다. 하지만 책에 따르면 이 명령어에 의해 만들어지는 디폴트 레이아웃은 비효율적이다.

### startproject 명령어로 생성된 레이아웃

---

: myproject 라는 프로젝트를 생성하고, myapp1, myapp2라는 앱을 생성했는데, 같은 위치에 있기 때문에 둘의 관계가 명확하지 않다. 이름을 분명하게 짓지않으면 헷갈릴 가능성이 높다. 또한 [settings.py](http://settings.py) 파일도 프로젝트 폴더  한 단계 아래에 위치하기 때문에 프로젝트 전체에 영향을 주는 설정이 아니라 마치 저 디렉토리의 setting에만 관여할 것 같은 느낌을 준다. 부가적으로 .gitignore나 [README.md](http://readme.md) 처럼 매 프로젝트 필수적으로 사용하는 파일들을 생성해주지 않기 때문에 매번 직접만들어야하는 불편함이있다.

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c219a3b0-ac89-4adb-a929-5d19b456e9cd/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c219a3b0-ac89-4adb-a929-5d19b456e9cd/Untitled.png)



### 우리가 원하는 모습의 레이아웃

---

- 위에서 언급한 불편함을 없애기 위해 구성된 프로젝트 레이아웃은 다음과 같다.

```python
<repository_root>/              (1)              
	- <configuration_root>/       (2)
	- <django_project_root>/      (3)          
```

(1)   absolute root directory of the project, configuration_root와 django_project_root 이외에도, `manage.py`,  `README.md`, `.gitignore`, `requirements.txt` 파일 등이 포함된다.

(2)  장고 프로젝트의 실제 root directory,

(3) settings module & base URLConf([urls.py](http://urls.py)) ,  `__init__.py` 를 포함해야 한다. (이닛파일이 없으면 파이썬 패키지로 인식되지 않는다)

이와 같은 레이아웃을 간편하게 생성하기 위해서 `Cookiecutter`라는 파이썬 패키지를 사용할 것이다.



### Cookiecutter 로 프로젝트 생성하기

---

쿠키커터 깃헙 : https://github.com/pydanny/cookiecutter-django

```python
$ pip install "cookiecutter>=1.7.0"

/// 위 명령어로 쿠키커터 패키지를 설치한다.

$ cookiecutter <https://github.com/pydanny/cookiecutter-django>

/// 위 명령어로 쿠키커터를 실행한다.
```

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/824649a5-d046-487b-ad11-e584f9c47e6f/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/824649a5-d046-487b-ad11-e584f9c47e6f/Untitled.png)

실행시 다음과 같이 여러가지 질문들이 나오며, 스킵하려면 그냥 엔터를 치면 되고 입력하려면 입력하면 된다. 예를 들어 timezone 에서 Asia/Seoul 을 미리 적으면 [settings.py](http://settings.py) 을 알아서 변경해주어서 편리하다. 쿠키커터를 사용하여 만든 프로젝트 레이아웃은 다음과 같다.

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/54fdbd29-1413-4201-8218-f8a8648ff41c/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/54fdbd29-1413-4201-8218-f8a8648ff41c/Untitled.png)

한 눈에 보기에도 매우 다른 레이아웃이다. cookiecutter가 자동으로 생성해준 파일들이 많고,  requirements.txt .gitignore 등, config 파일이 접근하기 쉽게 루트디렉토리 바로 아래에 위치한다는 것이다. 파일 갯수가 많이 늘어서 복잡해보이지만 이중 필요한 파일만 남겨두고 삭제해서 사용하면 기존의 프로젝트 레이아웃보다 편리하고 확장성이 있다.

이 상태로 [manage.py](http://manage.py) 를 하면 에러가 생긴다. requirements.txt 에서 local.txt 파일을  install 하자.

(venv 사용을 잊지말자)

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6d618a9d-9550-48e2-8ad4-52fc3f50557c/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6d618a9d-9550-48e2-8ad4-52fc3f50557c/Untitled.png)

```python
$ pip install -r requirements/local.txt
```

requirements.txt 를 모두 설치하고 나서도 장고 서버를 실행하려고 하면 에러가 뜰 것이다. django-admin startproject 를 사용해서 프로젝트를 시작할때는 장고에서 기본으로 제공하는 sqlite3  데이터베이스를 이용하지만, 쿠키커터는 사용할 디비를 직접 설정해주어야하기 때문이다. MySQL같은 디비를 이 곳에 설정해주면된다. 이번에는 편의상 sqlite3를 사용하도록 설정할 것이다.

```python
myproject > config > settings 

BASE_DIR = Path(__file__).resolve().parent.parent

# DATABASES
# ------------------------------------------------------------------------------
# <https://docs.djangoproject.com/en/dev/ref/settings/#databases>

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': BASE_DIR / 'db.sqlite3',
    }
}
```

여기까지 기본 설정을 마치면 서버를 실행할 수 있다. 그러면 기존의 로켓페이지가 아닌 아래와 같은 창이 뜰 것이다.

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/fc7e0d91-8f94-43de-88bd-03de4b724dd2/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/fc7e0d91-8f94-43de-88bd-03de4b724dd2/Untitled.png)