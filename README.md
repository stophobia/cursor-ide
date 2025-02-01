# 🖱️ 모두의커서
![예시 이미지](assets/images/moduai_logo.png)
## 프로젝트 소개
**모두의커서**는 Cursor IDE 관련 정보를 공유하기 위한 GitHub 페이지입니다.  
본 저장소는 Cursor 설정, 사용법, 관련 개발 지시사항(예: FastAPI 개발 표준, PRD 문서 작성 지시사항) 및 코딩 규칙을 포함합니다.

## 주요 다룰 주제
- Cursor IDE 사용 가이드 및 팁 공유
- 개발 환경 설정 문서
- PRD(Product Requirements Document) 관리
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
  - 문서 위치: [.cursor/rules/MOAI_FastAPI_kr.mdc](.cursor/rules/MOAI_FastAPI_kr.mdc)
  - 주요 내용:  
    - 클래스 기반 프로그래밍, RORO 패턴 사용  
    - 비동기 작업 시 `async def` 사용 및 에러 처리(guard clause, try/except 사용)  
    - 명확한 변수명 및 함수명을 사용
    - 환경 변수, 캐싱, 로깅, DB 연결 등 인프라 관련 설정 관리
    - 프로젝트 별 PRD 문서 참조 가능
    - 자신의 프로젝트에 맞게 추가/수정 사용 권장

- **FastAPI 개발 지시사항 (영어)**  
  - 문서 위치: [.cursor/rules/MOAI_FastAPI_en.mdc](.cursor/rules/MOAI_FastAPI_en.mdc)  
  - 핵심 가이드라인은 위의 한글 버전과 동일하며, Context Token 절약을 위한 영어 버전 추가 제공

- **PRD 문서 작성 지시사항**  
  - 문서 위치: [.cursor/rules/MOAI_PRD.mdc](.cursor/rules/MOAI_PRD.mdc)  
  - 주요 내용:  
    - 프로젝트 전체 개요, 아키텍처, 데이터 모델, API 엔드포인트, 변경 이력 등 문서화  
    - 각 도메인 별 PRD 파일(@PRD_project.md, @PRD_saju.md 등) 관리  
    - Git 브랜치 전략 및 커밋 메시지 작성 규칙 포함

> 참고: 각 개발 지시사항 문서에 '@PRD_project.md, @PRD_saju.md' 형태로 심볼릭 링크가 가능하며, 이를 통해 프로젝트 별 PRD 문서를 참조할 수 있습니다.


### 3. 제품 요구사항 문서 (PRD) 소개

본 프로젝트는 제품 요구사항 문서(PRD)를 통해 프로젝트의 핵심 비즈니스 로직, 기능 요구사항, 데이터 모델, API 설계, 보안 및 테스트 전략 등을 명확히 정의하고 있습니다. 

각 PRD 문서는 다음과 같이 구성되어 있습니다.

- **전체 프로젝트 요구사항**  
  - [PRD_project.md](PRD/PRD_project.md)  
    프로젝트의 개요, 주요 기능, 기술 스택 및 아키텍처 개요가 포함되어 있으며, 전반적인 제품 요구사항을 상세하게 설명합니다.

- **프로젝트 전체 폴더 구조 및 역할**  
  - [PRD_project_folders.md](PRD/PRD_project_folders.md)  
    도메인 중심의 폴더 구조, API 라우팅, 비즈니스 로직 및 공통 기능 모듈의 역할과 위치를 명확히 하여, 유지보수성과 확장성을 높이는 설계를 제안합니다.

- **Git 브랜치 및 커밋 메시지 전략**  
  - [PRD_git_branch.md](PRD/PRD_git_branch.md)  
    Git 브랜치 전략과 커밋 메시지 작성 규칙을 정의하여, 안정적이고 일관된 형상 관리를 지원합니다.

- **도메인별 제품 요구사항 문서**  
  - [PRD_order.md](PRD/domain/PRD_order.md)  
    주문(Order) 도메인의 요구사항과 비즈니스 로직, API 엔드포인트 등을 상세하게 기술합니다.
  - [PRD_product.md](PRD/domain/PRD_product.md)  
    상품(Product) 도메인에 대한 등록, 조회, 수정, 삭제 및 관련 비즈니스 로직이 포함됩니다.
  - [PRD_user.md](PRD/domain/PRD_user.md)  
    사용자(User) 도메인의 회원가입, 로그인, 프로필 관리 등의 기능과 보안 요구사항을 다룹니다.

> 모든 팀원은 최신 PRD 문서를 참고하여, 코드 변경 시 해당 문서와 동기화를 진행함으로써 일관된 개발 기준과 형상 관리를 유지해야 합니다.

---

아직 개선해야 할 부분이 많습니다만 시간이 허락이 되는데로 계속해서 업데이트 하도록 하겠습니다. 
