# Git 브랜치 및 커밋 메시지 전략

이 문서는 Git 브랜치 전략과 커밋 메시지 작성 규칙에 대한 표준을 정의하여, 프로젝트에서 안정적이고 일관된 형상 관리를 수행하기 위한 가이드라인을 제공합니다.

---

## 1. 브랜치 유형 및 역할

### 1.1 main 브랜치
- **목적**: 프로덕션 환경에 배포 가능한 안정적인 코드를 유지합니다.
- **특징**: 직접 커밋하지 않으며, 항상 배포 전 최종 테스트를 거친 코드만 포함합니다.

### 1.2 develop 브랜치
- **목적**: 모든 신규 기능 및 버그 수정이 통합되는 개발 브랜치입니다.
- **특징**: 기능 브랜치, 버그 수정 브랜치 등에서 작업 완료된 코드가 병합됩니다.

### 1.3 feature 브랜치 (`feature/<기능명-영어>`)
- **목적**: 개별 기능 개발을 위한 브랜치입니다.
- **활용 절차**:
  1. `develop` 브랜치에서 분기합니다.
     ```bash
     git checkout develop
     git pull origin develop
     git checkout -b feature/<기능명-영어>
     ```
  2. 기능 개발 후 `develop` 브랜치에 병합합니다.
     ```bash
     git checkout develop
     git merge feature/<기능명-영어>
     git push origin develop
     ```

### 1.4 bugfix 브랜치 (`bugfix/<버그-설명-영어>`)
- **목적**: 코드의 버그를 수정하기 위한 브랜치입니다.
- **활용 절차**:
  1. `develop` 브랜치에서 분기합니다.
     ```bash
     git checkout develop
     git pull origin develop
     git checkout -b bugfix/<버그-설명-영어>
     ```
  2. 버그 수정 후 `develop` 브랜치로 병합합니다.
     ```bash
     git checkout develop
     git merge bugfix/<버그-설명-영어>
     git push origin develop
     ```

### 1.5 release 브랜치 (`release/<버전번호>`)
- **목적**: 배포 전 최종 테스트 및 버그 수정을 위한 브랜치입니다.
- **활용 절차**:
  1. `develop` 브랜치에서 분기합니다.
     ```bash
     git checkout develop
     git pull origin develop
     git checkout -b release/<버전번호>
     ```
  2. 릴리즈 준비 후 `main`에 병합하고 태그를 추가합니다.
     ```bash
     git checkout main
     git merge release/<버전번호>
     git tag -a v<버전번호> -m "Release version <버전번호>"
     git push origin main --tags
     ```
  3. 병합된 변경 사항을 다시 `develop` 브랜치에 반영합니다.
     ```bash
     git checkout develop
     git merge release/<버전번호>
     git push origin develop
     ```

### 1.6 hotfix 브랜치 (`hotfix/<버그-설명-영어>`)
- **목적**: 프로덕션 환경에서 긴급 버그 수정을 위한 브랜치입니다.
- **활용 절차**:
  1. `main` 브랜치에서 분기합니다.
     ```bash
     git checkout main
     git pull origin main
     git checkout -b hotfix/<버그-설명-영어>
     ```
  2. 긴급 수정 후 `main`에 병합하고 태그를 추가합니다.
     ```bash
     git checkout main
     git merge hotfix/<버그-설명-영어>
     git tag -a v<버전번호> -m "Hotfix version <버전번호>"
     git push origin main --tags
     ```
  3. 수정 사항을 `develop` 브랜치에 병합합니다.
     ```bash
     git checkout develop
     git merge hotfix/<버그-설명-영어>
     git push origin develop
     ```

---

## 2. 커밋 메시지 작성 규칙

효과적인 형상 관리를 위해 다음과 같은 커밋 메시지 작성 규칙을 준수합니다.

### 2.1 커밋 메시지 형식
- **형식**: `<type>: <subject>`
  - **type**: `main`, `develop`, `feature`, `bugfix`, `release`, `hotfix`
  - **subject**: 50자 이내의 간결한 설명 (현재 시제, 영문)
  
- **본문**: 변경의 이유(Why)와 변경된 내용을(What) 중심으로 한국어로 작성합니다.
  
- **푸터**: 관련 이슈 번호나 추가 정보(APex 예시: `#123`)를 포함합니다.

### 2.2 추천 커밋 동사
- Add, Remove, Fix, Update, Implement, Refactor 등, 의미에 부합하는 동사를 사용합니다.

---

## 3. 브랜치 네이밍 규칙 요약

- **feature 브랜치**: `feature/<기능명-영어>`
- **bugfix 브랜치**: `bugfix/<버그-설명-영어>`
- **release 브랜치**: `release/<버전번호>`
- **hotfix 브랜치**: `hotfix/<버그-설명-영어>`

---

## 4. 협업 및 문서 업데이트

- 모든 팀원은 본 문서를 참고하여 브랜치 전략 및 커밋 메시지 규칙을 준수해야 합니다.
- 코드 변경이나 새로운 기능 추가 시, 관련 PRD 문서 및 다른 개발 문서와 동기화하여 일관성을 유지합니다.
- 정기적으로 문서를 리뷰하고 필요에 따라 업데이트합니다.

---

본 가이드라인은 프로젝트의 형상 관리와 일관된 협업을 위해 반드시 준수되어야 합니다.