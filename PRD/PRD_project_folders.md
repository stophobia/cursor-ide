## 전체 개요
도메인 중심으로 각 영역을 모듈화(Domain-Driven 혹은 Layered Architecture)
API 라우팅, 비즈니스 로직, DB 모델 등을 폴더 관점에서 명확히 분리
FastAPI 라우터를 버전/도메인별로 구성해 가독성과 유지보수성을 향상
공통 기능(보안, 설정, 예외처리 등)은 core/나 common/ 같은 전역 폴더로 모아둠

## 디렉토리 구조

```bash
# 전체 개요

이 문서는 일반적인 프로젝트에서 적용할 폴더 구조 및 각 디렉토리의 역할을 기술합니다. 본 구조는 Domain-Driven Design 또는 Layered Architecture 원칙을 기반으로 하여, 각 영역을 모듈화하고 역할을 명확히 분리함으로써 유지보수성과 확장성을 극대화하는 것을 목표로 합니다.

---

## 디렉토리 구조

```bash
ModuAI/                        # 프로젝트 루트 디렉토리
├── .github/                       # GitHub Actions 및 CI/CD 설정 파일
│   └── workflows/                 # CI/CD 파이프라인 및 워크플로우 정의
│
├── .vscode/                       # VS Code 개발 환경 설정 파일
│   ├── extensions.json            # 확장 프로그램 설정
│   ├── launch.json                 # 디버깅 설정
│   ├── settings.json               # 설정 파일
│   └── tasks.json                  # 작업 설정
│
├── app/                           # FastAPI 애플리케이션 디렉토리
│   ├── main.py                    # FastAPI 실행 진입점
│   │
│   ├── apis/                      # API 라우팅 계층
│   │   └── v1/                    # API 버전 1
│   │       ├── auth.py            # 인증 및 권한 관련 엔드포인트
│   │       ├── items.py           # 아이템 관련 엔드포인트
│   │       └── users.py           # 사용자 관련 엔드포인트
│   │
│   ├── common/                    # 프로젝트 전반에서 사용되는 공통 기능
│   │   ├── constants.py           # 상수 정의
│   │   ├── enums.py               # 열거형 정의
│   │   ├── responses.py           # 표준 응답 형식 정의
│   │   ├── utils.py               # 공통 유틸리티 함수
│   │   └── validators.py          # 데이터 검증 로직
│   │
│   ├── core/                      # 핵심 기능 및 설정 모듈
│   │   ├── config.py              # 환경 변수 및 설정 관리 (pydantic-settings 활용)
│   │   ├── database.py            # 데이터베이스 연결 및 관리
│   │   ├── error_handler.py       # 전역 에러 처리
│   │   ├── exceptions.py          # 커스텀 예외 정의
│   │   ├── logger.py              # 로깅 설정
│   │   └── security.py            # 보안 관련 기능 (인증, 인가 등)
│   │
│   ├── dependencies/              # 의존성 주입 및 초기화 모듈
│   │   ├── db.py                  # 데이터베이스 세션 의존성
│   │   └── repositories.py        # 데이터 접근 및 리포지토리 로직
│   │
│   └── domains/                   # 도메인 별 비즈니스 로직
│       ├── orders/                # 주문 도메인
│       │   ├── models.py          # 주문 관련 데이터 모델
│       │   └── services.py        # 주문 처리 비즈니스 로직
│       ├── products/              # 상품 도메인
│       │   ├── models.py          # 상품 관련 데이터 모델
│       │   └── services.py        # 상품 관리 비즈니스 로직
│       └── users/                 # 사용자 도메인
│           ├── models.py          # 사용자 관련 데이터 모델
│           └── services.py        # 사용자 관리 비즈니스 로직
│
├── data/                          # 데이터 파일 및 SQL 스크립트
│   └── sql/                       # 데이터베이스 스크립트
│
├── docker/                        # 도커 설정 및 구성 파일
│   ├── dev/                       # 개발 환경 도커 파일
│   │   ├── Dockerfile             
│   │   └── docker-compose.yml     
│   └── prod/                      # 프로덕션 환경 도커 파일
│       ├── Dockerfile             
│       └── docker-compose.yml     
│
├── docs/                          # 프로젝트 관련 문서
│   ├── PRD/                       # 제품 요구사항 및 내부 지시사항 문서
│   │   ├── PRD_project.md         # 전체 프로젝트 개요 및 요구사항 문서
│   │   ├── PRD_git.md             # Git 브랜치 및 커밋 가이드라인 문서
│   │   └── PRD_project_folder.md  # (현재 문서) 프로젝트 폴더 구조 및 역할
│   └── api/                       # API 문서 및 스펙
│
├── logs/                          # 로그 파일 디렉토리
│   └── app.log                   # 애플리케이션 로그 파일
│
├── migrations/                    # Alembic을 이용한 DB 마이그레이션 스크립트
│   ├── env.py                     
│   └── versions/                  
│
├── scripts/                       # 유틸리티 스크립트 모음
│   ├── export-env.sh              # 환경 변수 스크립트
│   └── start-docker.sh            # 도커 실행 스크립트
│
├── tests/                         # 테스트 코드 디렉토리
│   ├── unit/                     # 단위 테스트
│   └── integration/              # 통합 테스트
│
├── .env.example                   # 환경 변수 예제 파일
├── alembic.ini                    # Alembic 설정 파일
├── docker-compose.yml             # 전체 도커 컴포즈 설정 파일
├── poetry.lock                    # Poetry 의존성 잠금 파일
├── pyproject.toml                 # 프로젝트 메타데이터 및 설정 파일
└── README.md                      # 프로젝트 설명 및 설치 가이드
```

## 핵심 포인트

1. **도메인 중심 구조**
   - `app/domains/` 아래에 각 도메인별 폴더 구성
   - 각 도메인은 models, services, repositories 등 완결된 구조
   - 도메인간 의존성 최소화

2. **계층화된 아키텍처**
   - API 라우팅 (`apis/`)
   - 비즈니스 로직 (`domains/`)
   - 데이터 접근 계층 (`repositories/`)
   - 공통 기능 (`core/`, `common/`)

3. **설정 및 환경 분리**
   - 개발/스테이징 환경 분리 (`docker/`)
   - 환경변수 기반 설정 (`.env`)
   - Docker 기반 일관된 환경

4. **문서화**
   - PRD 문서 (`docs/PRD/`)
   - API 문서 (`docs/api/`)
   - 마이그레이션 이력 (`migrations/`)

5. **데이터 관리**
   - SQL 스크립트 (`data/sql/`)
   - 사주/만세력 데이터셋 (`dataset/`)
   - 마이그레이션 기반 DB 스키마 관리

6. **개발 도구 통합**
   - VS Code 설정 (`.vscode/`)
   - GitHub Actions CI/CD
   - Docker 기반 개발/배포

7. **모니터링 및 로깅**
   - 구조화된 로깅 (`logs/`)
   - 에러 추적 및 모니터링

