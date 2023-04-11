# 인스타그램 클론코딩

### 230412

- 게시글 생성 CREATE

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




