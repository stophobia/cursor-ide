# 🖱️ 모두의커서
![예시 이미지](assets/images/moduai_logo.png)
## 프로젝트 소개
**모두의커서**는 Cursor IDE 관련 정보를 공유하기 위한 GitHub 페이지입니다.  
본 저장소는 Cursor 설정, 사용법, 관련 개발 지시사항(예: FastAPI 개발 표준, PRD 문서 작성 지시사항) 및 코딩 규칙을 포함합니다.

## 주요 다룰 주제
- Cursor IDE 사용 가이드 및 팁 공유
- 개발 환경 설정 문서
- PRD(Product Requirement Document) 관리
- 코딩 규칙 및 스타일 가이드 제공

---

## Cursor 기본 정보 안내

### 1. Cursor Rules for AI 및 컨텍스트 창 정보

#### Cursor Rules for AI
Cursor의 AI 동작 커스터마이징에 관한 자세한 내용은 [Cursor 공식 문서](https://docs.cursor.com/context/rules-for-ai)를 참고하세요.

- **Global Rules**:  
  - Cursor Settings > General > Rules for AI에서 전역 설정으로 등록할 수 있습니다.
- **Project Rules (권장)**:  
  - 프로젝트별 설정은 `.cursor/rules` 폴더 내에 위치하며, glob 패턴을 활용해 파일/폴더별 규칙 적용이 가능합니다.
- **.cursorrules 파일**:  
  - 기존 방식으로 루트 폴더에 `.cursorrules` 파일을 사용할 수 있으나, 향후 지원 중단 예정이므로 Project Rules 방식을 권장합니다.


#### 커서 컨텍스트 (토큰) 창 정보
Cursor에서는 상황에 따라 다른 컨텍스트 창 토큰 제한을 사용합니다.

- **Chat과 Composer**: 기본적으로 약 40,000개의 토큰을 지원합니다. (대략, 영어 단어 기준 약 20,000 단어, 책 약 80페이지 분량)
- **Cmd-K**: TTFT와 품질의 균형을 맞추기 위해 약 10,000개의 토큰으로 제한됩니다. (대략, 영어 단어 기준 약 5,000 단어, 책 약 20페이지 분량)
- **Agent**: 60,000개의 토큰에서 시작하여 최대 120,000개의 토큰까지 지원합니다. (대략, 영어 단어 기준 약 60,000 단어, 책 약 240페이지 분량)
- 긴 대화의 경우, 토큰 공간을 보존하기 위해 컨텍스트를 자동으로 요약합니다.

이러한 임계값은 사용자 경험을 최적화하기 위해 수시로 변경될 수 있으므로, 최신 정보는 공식 문서를 참고하시기 바랍니다.

자세한 사용법은 [Cursor 사용법](https://docs.cursor.com/)도 확인하시기 바랍니다.



### 2. Cursor Rules & 개발 지시사항 설정
Cursor 내의 개발 환경은 여러 커스텀 rules 문서를 통해 관리됩니다.  
아래와 같이 각 지시사항 문서를 참조하여 개발 가이드라인을 숙지하시기 바랍니다.

- **FastAPI 개발 지시사항 (한글)**  
  - 문서 위치: `.cursor/rules/MOAI_FastAPI_kr.mdc`  
  - 주요 내용:  
    - 클래스 기반 프로그래밍, RORO 패턴 사용  
    - 비동기 작업 시 `async def` 사용 및 에러 처리(guard clause, try/except 사용)  
    - 명확한 변수명 및 함수명을 사용
    - 환경 변수, 캐싱, 로깅, DB 연결 등 인프라 관련 설정 관리

- **FastAPI 개발 지시사항 (영어)**  
  - 문서 위치: `.cursor/rules/MOAI_FastAPI_en.mdc`  
  - 핵심 가이드라인은 위의 한글 버전과 동일하며, 글로벌 개발팀과의 협업을 위해 제공됨

- **PRD 문서 작성 지시사항**  
  - 문서 위치: `.cursor/rules/MOAI_PRD.mdc`  
  - 주요 내용:  
    - 프로젝트 전체 개요, 아키텍처, 데이터 모델, API 엔드포인트, 변경 이력 등 문서화  
    - 각 도메인 별 PRD 파일(@PRD_project.md, @PRD_saju.md 등) 관리  
    - Git 브랜치 전략 및 커밋 메시지 작성 규칙 포함

> 참고: 각 개발 지시사항 문서에 '@PRD_project.md, @PRD_saju.md' 형태로 심볼릭 링크가 가능하며, 이를 통해 프로젝트 별 PRD 문서를 참조할 수 있습니다.

## FastAPI 및 PRD 관련 개발 지시사항

### FastAPI 개발 가이드
- **함수 및 비동기 작업**  
  모든 함수는 타입 힌트와 Pydantic v2 모델을 이용해 입력 검증 및 응답 스키마를 구성하며, `async def`를 이용해 비동기 처리를 수행합니다.
- **에러 핸들링**  
  Guard Clause 및 try/except 구조를 활용하여 사용자 친화적인 에러 메시지를 전달하고, HTTPException으로 예외를 처리합니다.
- **코드 구조**  
  - 라우터, 유틸리티, 모델, 의존성 주입 등의 구조로 파일을 분리합니다.  
  - 서비스 레이어, 레포지토리 패턴 등의 클래스 기반 디자인을 선호합니다.

### PRD(Product Requirement Document) 작성 가이드
- **문서 분리**  
  프로젝트 PRD는 @PRD_project.md, 디렉토리 구조는 @PRD_project_folder.md, Git 브랜치 전략은 @PRD_git_branch.md 등 각 역할에 맞게 문서를 분리 관리합니다.
- **상세 설명**  
  - 프로젝트 개요, 아키텍처, 데이터 모델, API 스펙, 에러 처리, 로깅 등의 요소를 상세히 기술합니다.
  - 코드 변경 시 관련 PRD 문서, Alembic 마이그레이션 스크립트 및 도메인 문서 간 동기화를 반드시 진행합니다.
- **협업과 업데이트**  
  문서 업데이트 및 변경 이력 관리를 통해 변경 사항을 추적하며, 팀원 간의 문서 리뷰를 정기적으로 진행합니다.

## 기타 참고 사항
- **CI/CD 파이프라인**:  
  정적 분석 도구(black, isort, mypy, ruff, flake8, bandit 등)를 통합하여 코드 리뷰 및 품질 관리를 수행합니다.
- **환경 변수 관리**:  
  pydantic-settings를 활용한 환경 변수 및 설정 파일 관리 전략이 마련되어 있으며, 로컬, 스테이징, 프로덕션 별로 설정을 분리합니다.
- **비동기 및 캐싱 전략**:  
  Redis 및 fastapi-cache2를 통한 캐싱, asyncpg/SQLAlchemy 2를 통한 비동기 DB 연결, 미들웨어를 활용한 에러 모니터링 및 성능 최적화를 적용합니다.

---

현재 정식 버전이 아니므로 개선해야 할 부분이 많습니다만 차차 개선해 나가도록 하겠습니다.
