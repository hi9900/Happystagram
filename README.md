# 인스타그램 클론코딩

### 230413

- 이미지 파일 추가 및 조회 기능 구현

  - 이미지 업로드를 위한 전처리

    - 가상환경에 Pillow 라이브러리 설치 후 freeze

    - `settings.py` 설정 추가

      ```python
      MEDIA_ROOT = BASE_DIR / 'media'
      MEDIA_URL = '/media/'
      ```
    
    - `instapjt/urls.py`

      ```python
      urlpatterns = [...]
      + static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
      ```
  
  - `models.py` 이미지 파일 필드 추가 후 **마이그레이션**

  - `posts/views.py` create 함수에 request.FILES 추가

  - `posts/create.html` 이미지 파일을 입력받기 위해 form 태그 수정

    `<form enctype="multipart/form-data">`

  - `posts/posts.html` 메인화면에서 이미지를 출력 (이미지가 없을 시 출력하지 않음)

    처음에는 이미지가 없을 시 alt가 출력되는 것으로 생각 후 조회 for문 안에 img 태그 작성

    `<img src="{{ post.image.url }}" alt="">`

    모든 이미지가 출력되지 않아서 if 문으로 이미지가 존재할 시 출력되게 함 -> why?

    ```django
    {% if post.image %}
      <img src="{{ post.image.url }}" alt="">
    {% endif %}
    ```

### 230412

- 게시글 생성 CREATE 구현

  - `posts/urls.py` create 경로 추가

    - 엔드포인트 `create/`, 경로 이름 create

  - `posts/views.py` create 함수 생성

    - POST 요청, form 유효성 검사 통과 시 게시글 생성 후

    - 메인화면(posts:index) 이동

  - `posts/create.html` 생성

    - `base.html`을 상속받고, form 태그로 POST 요청을 전송

  - `base.html` 상단 네비바의 `NewPost`를 누르면 게시글 작성 화면(posts:create)로 이동

  - 게시글 조회 READ 구현: 메인화면에서 게시글 조회

    - `posts/views.py`: index 함수 수정
    
      - Post 모델 import

      - queryAPI를 사용해서 Post에 저장된 게시글의 정보를 context로 전달

    - `posts/post.html`: 게시글 조회 화면 담당

      - for 문을 통해 post 조회

    - `posts/index.html` post.html을 include 받아 게시글 조회

    > ### 게시글 조회 화면을 `index.html`에 작성하지 않는 이유?
    >
    > 코드의 재사용성을 위해
    >
    > 한 html 안에 많은 내용이 들어가면 가독성이 떨어지고, 똑같은 일을 계속해서 적어야 하므로 비효율적
    >
    > 때문에 자주 사용할 영역을 따로 만들어두어 include 받아오기
    >
    > +추가과제
    >
    > create, update, signup에 비슷한 생김새의 form 태그를 사용하는 데, 
    >
    > form 태그 안의 내용물을 구성하는 것은 view에서 넘겨준 정보이다.
    >
    > include를 사용하여 form을 구현한 html을 가져와서 쓰면 한 줄로 form 태그를 여러 곳에서 사용 가능하다.
    >
    > form.html을 include 해서 사용해 보기

  - 게시글 삭제 DELETE 구현

    - `posts/urls.py`에 게시글 삭제에 관한 경로 추가

      - 엔드포인트: `pk/delete/`, 경로 이름: delete

    - `posts/views.py`: delete 함수 생성

      - post 요청일 때, 요청된 pk의 게시글 삭제

      - 삭제 후 메인화면으로 이동

    - `posts/post.html`: form을 이용해 삭제 버튼 추가

### 230411

- instapjt 프로젝트 생성

- posts 앱 생성
  
  - `settings.py` 에서 앱 등록
  
  - 프로젝트의 `urls.py` 에 앱의 `urls.py` 등록
    
    - `include`를 사용하여 엔드포인트 `posts/` 로 지정

- 앱의 `urls.py` 설정
  
  - `app_name='posts'`

- `base.html`
  
  - 프로젝트 최상단에 `templates` 폴더 안 생성
  
  - Bootstrap, fontawesome의 CDN과 상단 네비게이션 바
  
  - `settings.py` 에서 `base.html`에 대한 경로 수정

- `index`: 메인 화면에 대한 경로 설정
  
  - `http://127.0.0.1:8000/posts/`

- `views.index` 메인화면에 대한 요청 처리 함수

- `templates/posts/index.html` 생성
  
  - `base.html` 을 상속

- `base.html` 상단 네비게이션 바의 Home을 누르면 메인화면으로 이동하는 경로 설정

