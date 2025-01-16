# 프로젝트 PRD(Product Requirement Document)

## 1. 프로젝트 개요

### 1.1 목적
- FastAPI 기반의 현대적이고 확장 가능한 백엔드 서비스 제공
- 체계적이고 유지보수가 용이한 코드베이스 구축

### 1.2 기술 스택
- **언어**: Python 3.12
- **프레임워크**: FastAPI v0.110.0
- **데이터베이스**: PostgreSQL 17 + asyncpg
- **ORM**: SQLAlchemy v2
- **캐싱**: Redis + fastapi-cache2
- **마이그레이션**: Alembic
- **로깅**: loguru
- **개발 도구**: 
  - 코드 품질: black, isort, mypy, ruff
  - API 문서: Swagger/OpenAPI

## 2. 프로젝트 구조

```
ModuAI-Blog/                # 프로젝트 루트
├── .devcontainer/            # 개발 컨테이너 설정
├── .env.dev                  # 개발 환경 변수
├── .env.example              # 환경 변수 예시
├── .env.prod                 # 프로덕션 환경 변수
├── .env.staging              # 스테이징 환경 변수
├── .github/                  # GitHub 설정
│   └── workflows/            # CI/CD 워크플로우
├── .gitignore                # Git 제외 파일
├── .vscode/                  # VS Code 설정
├── alembic.ini               # Alembic 설정
├── config/                   # 설정 파일
├── dataset/                  # 데이터셋
├── docker/                   # 도커 설정
├── docs/                     # 문서
│   └── PRD/                  # PRD 문서
├── logs/                     # 로그 파일
├── migrations/               # Alembic 마이그레이션
├── poetry.lock               # 의존성 잠금 파일
├── pyproject.toml            # 프로젝트 설정
├── scripts/                  # 유틸리티 스크립트
└── src/                      # 소스 코드
    ├── __init__.py           # 패키지 초기화
    ├── api/                  # API 정의
    │   └── v1/              # API 버전 1
    ├── apps/                 # 도메인별 앱
    │   ├── blog/            # 블로그 관리
    │   └── users/           # 사용자 관리
    ├── common/               # 공통 유틸리티
    │   ├── exceptions/      # 예외 처리
    │   └── utils/           # 유틸리티
    ├── core/                 # 핵심 기능
    │   ├── config/          # 설정
    │   ├── database/        # DB 연결
    │   └── security/        # 보안
    └── main.py              # 애플리케이션 진입점
```

## 3. 주요 디렉토리 설명

### 3.1 소스 코드 (src/)
- **api/**: API 엔드포인트 정의
- **apps/**: 도메인별 애플리케이션 모듈
- **core/**: 핵심 기능 및 설정
- **common/**: 공통 유틸리티 및 예외 처리

### 3.2 설정 파일
- **.env.{환경}**: 환경별 설정 파일
- **alembic.ini**: 데이터베이스 마이그레이션 설정
- **pyproject.toml**: 프로젝트 메타데이터 및 의존성

### 3.3 개발 도구
- **.devcontainer/**: 개발 환경 컨테이너 설정
- **.vscode/**: VS Code 설정
- **docker/**: 도커 관련 설정

### 3.4 데이터 및 리소스
- **dataset/**: 데이터셋 파일
- **data/**: 데이터 파일
- **logs/**: 로그 파일
- **migrations/**: DB 마이그레이션 파일

## 4. 환경 설정

### 4.1 개발 환경 (.env.dev)
```
# 데이터베이스 설정
DATABASE_URL=postgresql+asyncpg://user:password@localhost:5432/db_name

# Redis 설정
REDIS_URL=redis://localhost:6379

# JWT 설정
SECRET_KEY=your-secret-key
ALGORITHM=HS256
ACCESS_TOKEN_EXPIRE_MINUTES=30

# 로깅 설정
LOG_LEVEL=DEBUG
```

### 4.2 스테이징 환경 (.env.staging)
```
# 데이터베이스 설정
DATABASE_URL=postgresql+asyncpg://user:password@staging-db:5432/db_name

# Redis 설정
REDIS_URL=redis://staging-redis:6379

# JWT 설정
SECRET_KEY=staging-secret-key
ALGORITHM=HS256
ACCESS_TOKEN_EXPIRE_MINUTES=30

# 로깅 설정
LOG_LEVEL=INFO
```

### 4.5 프로덕션 환경 (.env.prod)
```
# 데이터베이스 설정
DATABASE_URL=postgresql+asyncpg://user:password@prod-db:5432/db_name

# Redis 설정
REDIS_URL=redis://prod-redis:6379
```

## 5. 개발 도구 설정

### 5.1 Poetry 설정 (pyproject.toml)
```toml
[tool.poetry]
name = "ModuAI-Blog"
version = "0.1.0"
description = "cursor ide 정보 공유 페이지"
authors = ["모두의AI"]

[tool.poetry.dependencies]
python = "^3.12"
fastapi = "^0.110.0"
sqlalchemy = "^2.0.0"
alembic = "^1.13.0"
pydantic = "^2.0.0"
pydantic-settings = "^2.1.0"
redis = "^5.0.1"
fastapi-cache2 = "^0.2.1"
python-jose = {extras = ["cryptography"], version = "^3.3.0"}
passlib = {extras = ["bcrypt"], version = "^1.7.4"}
python-multipart = "^0.0.9"
uvicorn = "^0.27.0"
loguru = "^0.7.2"
asyncpg = "^0.30.0"
uuid7 = "^0.1.0"
psycopg2-binary = "^2.9.10"

[tool.poetry.group.dev.dependencies]
black = "^24.1.0"
isort = "^5.13.0"
mypy = "^1.8.0"
ruff = "^0.2.0"
```

### 5.2 코드 스타일 설정
```toml
[tool.black]
line-length = 88
target-version = ["py312"]

[tool.isort]
profile = "black"
multi_line_output = 3

[tool.mypy]
python_version = "3.12"
strict = true
plugins = ["pydantic.mypy"]

[tool.ruff]
line-length = 88
target-version = "py312"
``` 

## 6. 코드 스타일 가이드

### 6.1 Python 코딩 스타일
- Black 포맷터 설정 (line-length=88)
- isort를 사용한 import 정렬
- Ruff를 통한 린팅
- mypy를 통한 타입 체크

### 6.2 문서화 규칙
- 모든 함수/클래스는 한글 문서화
- 모든 코드는 타입 힌트 필수
- 복잡한 로직은 인라인 주석 추가

### 6.3 메시지 처리 규칙
- 모든 API 응답 메시지는 상수로 관리
- 각 앱의 `constants/messages.py`에 정의
- 메시지 상수는 다음과 같이 구분:
  ```python
  # 성공 메시지
  SUCCESS_MESSAGES = {
      "CREATE": "리소스가 성공적으로 생성되었습니다.",
      "UPDATE": "리소스가 성공적으로 수정되었습니다.",
      "DELETE": "리소스가 성공적으로 삭제되었습니다.",
  }

  # 에러 메시지
  ERROR_MESSAGES = {
      "NOT_FOUND": "리소스를 찾을 수 없습니다.",
      "INVALID_INPUT": "유효하지 않은 입력값입니다.",
      "CREATE_ERROR": "리소스 생성 중 오류가 발생했습니다.",
      "UPDATE_ERROR": "리소스 수정 중 오류가 발생했습니다.",
      "DELETE_ERROR": "리소스 삭제 중 오류가 발생했습니다.",
  }
  ```

### 6.4 API 응답 형식

#### 기본 응답 형식
- 성공 응답:
  - 생성/수정: `{"message": "성공 메시지", "data": {...}}`
  - 삭제: `{"message": "성공 메시지"}`
  - 조회: `{"data": {...}}` 또는 `{"data": [...]}`

- 에러 응답:
  - 클라이언트 에러: `{"detail": "에러 메시지"}`
  - 유효성 검사 에러: `{"detail": [{"type": "error_type", "loc": [...], "msg": "에러 메시지", "input": ...}]}`

#### 주요 HTTP 상태 코드
- 200 OK: 성공 (조회/수정/삭제)
- 201 Created: 새로운 리소스 생성
- 400 Bad Request: 잘못된 요청
- 401 Unauthorized: 인증 필요
- 403 Forbidden: 권한 없음
- 404 Not Found: 리소스를 찾을 수 없음
- 409 Conflict: 리소스 충돌
- 422 Unprocessable Entity: 유효하지 않은 입력값
- 500 Internal Server Error: 서버 오류

## 7. 개발 프로세스

### 7.1 브랜치 전략
```markdown
- main: 프로덕션 브랜치
- develop: 개발 브랜치
- feature/*: 기능 개발
- bugfix/*: 버그 수정
- release/*: 릴리즈 준비
```

### 7.2 커밋 메시지 규칙
```markdown
feat: 새로운 기능 추가
fix: 버그 수정
docs: 문서 수정
style: 코드 포맷팅
refactor: 코드 리팩토링
chore: 빌드 업무 수정
```

### 7.3 코드 리뷰 프로세스
```markdown
1. PR 생성 전 체크리스트
   - 코드 스타일 가이드 준수
   - 문서화 완료

2. 리뷰어 체크리스트
   - 비즈니스 로직 검증
   - 코드 품질 검토
```

## 8. 앱별 PRD 문서

### 8.1 앱 문서 구조
각 앱의 PRD 문서는 다음과 같은 구조를 따릅니다:
1. 개요: 앱의 목적과 주요 기능
2. 폴더 구조: 앱의 파일 구조와 역할
3. 모델 정의: 데이터베이스 모델 스키마
4. 스키마 정의: API 요청/응답 스키마
5. 상수 정의: 검증 상수와 메시지
6. 서비스 로직: 비즈니스 로직 설명
7. API 엔드포인트: API 명세
8. API 응답 예시: 상세 응답 형식
9. 의존성: 필요한 패키지와 환경 변수

### 8.2 앱별 문서 목록

#### 8.2.1 계정 관리 
- 사용자 인증과 계정 관리를 담당하는 핵심 모듈
- 주요 기능:
  - 계정 생성/수정/삭제
  - 이메일 인증
  - 로그인/로그아웃
  - 토큰 기반 인증


#### 8.2.2 블로그 관리 
- 블로그 게시글 관리를 담당하는 모듈
- 주요 기능:
  - 게시글 생성/수정/삭제
  - 게시글 조회
  - 게시글 검색
  - 게시글 페이지네이션
    
### 8.3 문서 관리 지침
1. 모든 앱 문서는 `docs/PRD` 디렉토리에 위치
2. 파일명은 앱 이름을 소문자로 하고 `.md` 확장자 사용
3. 문서 변경 시 관련된 다른 문서도 함께 검토
4. 코드 변경 시 문서도 함께 변경