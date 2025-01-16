## 프로젝트 구조 및 기술 스택

### 백엔드 (Python / FastAPI)
- 언어/프레임워크: Python 3.12, FastAPI v0.110.0  
- 데이터베이스: PostgreSQL 17 + asyncpg, ORM: SQLAlchemy v2
- 캐싱: Redis + fastapi-cache2  
- 마이그레이션: Alembic  
- 로깅: loguru  
- 주요 라이브러리: pydantic v2, pydantic-settings, aiohttp, uvicorn  
- 개발 도구: pytest, pytest-asyncio, black(line-length=88), isort, mypy  


## 백엔드 코드 스타일 및 구조

1. 코멘트 및 문서화:  
   모든 주석과 문서는 한국어로 작성하며, 로직의 의도와 사용 방법을 명확히 합니다.

2. 객체 지향 프로그래밍 지향:  
   가능하면 객체 지향 스타일로 작성합니다. 클래스 사용은 최대화하고, 클래스 메서드는 최대한 추상화하여 사용합니다. 

3. 변수 및 함수명:  
   `is_active`, `has_permission` 같은 보조동사를 활용하여 역할이 명확한 이름을 사용합니다.

4. 폴더 및 파일명:  
   소문자와 밑줄을 사용하고(예: `routers/user_routes.py`), 기능별로 명확히 구조화합니다.

5. RORO (Receive Object, Return Object) 패턴:  
   함수 입력은 객체로 받고, 출력도 객체로 반환하여 명확하고 예측 가능한 인터페이스를 만듭니다.

6. 타입 힌트와 검증:  
   모든 함수 시그니처에 Python 타입 힌트를 적용하고, Pydantic 모델을 통해 입력/출력 데이터 검증을 수행합니다.

7. 조건문 및 에러 처리:  
   불필요한 중첩을 피하고, 초기 조건 검증(guard clauses)을 통해 코드를 단순화합니다. 예상되는 에러는 `HTTPException`을 활용하고, 예외적인 상황은 미들웨어에서 처리합니다.

8. 비동기 처리:  
   `AsyncSession` 등 비동기 DB 연동을 활용하고, I/O 차단을 최소화합니다.

9. 캐싱 및 최적화:  
   Redis, fastapi-cache2 등을 사용해 빈번한 요청을 캐싱하고, 대용량 데이터셋은 지연 로딩으로 성능을 개선합니다.


### 백엔드
1. RESTful API 원칙 준수  
2. FastAPI 의존성 주입 활용  
3. API 키 기반 인증(X-API-Key) 필수  
4. 비동기 DB 연산 필수  
5. 구조화된 에러 처리 및 로깅  
6. 환경 변수 기반 설정 관리  
7. 헬스체크 엔드포인트 제공  
8. Alembic으로 DB 마이그레이션 관리 (마이그레이션은 동기적으로 실행)
9. CORS 설정으로 로컬 개발 지원  
10. 특정 도메인 처리 최적화
11. pydantic v2 사용 

## 중요
- 동일안 문제가 반복 되면 codebase를 이용해서 관련 코드를 다시 분석하고 문제를 해결하자.
- 모든 함수는 문서화 필수
- 모든 함수는 타입 힌트 필수
- 모든 함수는 테스트 코드 필수
- 모든 함수는 주석 필수
- 모든 함수는 예외 처리 필수