# Todo 리스트 모노리포 프로젝트 개발 할일 목록

## AI 협업 가이드
이 파일은 Claude Code와 같은 AI 도구와의 협업을 위해 최적화되었습니다.

### 사용 방법
1. **작업 요청**: "TODO.md의 Phase 1-1번을 구현해줘"
2. **진행 상황 업데이트**: 완료된 항목은 `- [x]`로 표시
3. **이슈 추가**: 문제 발생 시 `❌ [문제 설명]` 형태로 기록
4. **의존성 확인**: `🔗 의존성` 섹션을 참고하여 순서대로 진행

## 진행 상태
- 🔄 진행 중
- ✅ 완료  
- ⏸️ 대기 중
- ❌ 차단됨

---

## Phase 1: 프로젝트 초기 설정

### ✅ 1. 모노리포 구조 및 루트 설정
**🔗 의존성**: 없음 (시작점)  
**📁 생성할 파일**: `package.json`, `.gitignore`, `.env.example`, `README.md`

**세부 작업**:
- [x] 루트 `package.json` 생성 (workspaces 설정)
  ```bash
  npm init -y
  # workspaces: ["frontend", "backend"]
  ```
- [x] 디렉토리 구조 생성
  ```bash
  mkdir -p frontend backend shared docs scripts docker
  ```
- [x] 루트 레벨 설정 파일들 생성
  - [x] `.gitignore` (Node.js, Java, IDE 설정)
  - [x] `.env.example` (환경변수 템플릿)
  - [x] `README.md` (프로젝트 개요)
- [x] 개발 스크립트 설정 (`package.json`의 scripts 섹션)
- [x] concurrently 의존성 설치

**✅ 완료 조건**: 디렉토리 구조 생성 완료 및 루트 package.json에서 `npm run dev` 명령어 동작

### ✅ 2. Vue.js 3 프론트엔드 프로젝트 초기화
**🔗 의존성**: 1번 완료 후  
**📁 생성할 파일**: `frontend/package.json`, `frontend/vite.config.ts`, `frontend/tsconfig.json`

**세부 작업**:
- [x] Vite + Vue 3 + TypeScript 프로젝트 생성
  ```bash
  cd frontend
  npm create vue@latest . --typescript --router --pinia
  ```
- [x] 추가 의존성 설치
  ```bash
  npm install axios @types/axios
  npm install vuetify@next @mdi/js
  ```
- [x] 폴더 구조 생성
  ```bash
  mkdir -p src/{components/common,components/todo,views,stores,services,types,utils}
  ```
- [x] Vite 설정 파일 구성 (프록시 설정, 환경 변수)

**✅ 완료 조건**: `npm run dev` 실행 시 Vue 앱이 localhost:5173에서 정상 동작

### ✅ 3. Spring Boot 백엔드 프로젝트 초기화
- [x] Spring Boot 3.x 프로젝트 생성
- [x] 필수 의존성 추가 (Spring Web, JPA, Security, PostgreSQL)
- [x] 기본 패키지 구조 생성
- [x] `application.yml` 기본 설정

### ⏸️ 4. PostgreSQL 데이터베이스 및 스키마 설정
- [ ] Docker Compose로 PostgreSQL 컨테이너 설정
- [ ] 데이터베이스 및 테이블 스키마 생성 스크립트
- [ ] 초기 데이터 시드 스크립트 작성
- [ ] 백엔드와 데이터베이스 연결 테스트

---

## Phase 2: 백엔드 개발

### ⏸️ 5. JWT 기반 사용자 인증 구현
- [ ] User 엔티티 및 Repository 생성
- [ ] JWT 토큰 제공자 구현
- [ ] Spring Security 설정
- [ ] 인증 관련 컨트롤러 구현
  - [ ] 회원가입 API
  - [ ] 로그인 API
  - [ ] 토큰 갱신 API
- [ ] 비밀번호 암호화 설정

### ⏸️ 6. Todo CRUD API 구현
- [ ] Todo 엔티티 및 Repository 생성
- [ ] Todo 서비스 레이어 구현
- [ ] Todo 컨트롤러 구현
  - [ ] Todo 목록 조회 (페이징, 필터링)
  - [ ] Todo 생성
  - [ ] Todo 수정
  - [ ] Todo 삭제
  - [ ] Todo 완료 상태 변경
- [ ] DTO 클래스 생성
- [ ] 입력 검증 및 예외 처리

---

## Phase 3: 프론트엔드 개발

### ⏸️ 7. 프론트엔드 프로젝트 구조 및 의존성 설정
- [ ] 컴포넌트 폴더 구조 설정
- [ ] TypeScript 타입 정의 파일 생성
- [ ] 라우터 설정 (`vue-router`)
- [ ] UI 라이브러리 설정 및 테마 구성
- [ ] 전역 스타일 설정

### ⏸️ 8. 인증 관련 컴포넌트 구현
- [ ] 로그인 페이지 구현
- [ ] 회원가입 페이지 구현
- [ ] 인증 가드 (Route Guard) 설정
- [ ] 인증 상태 관리
- [ ] 토큰 자동 갱신 로직

### ⏸️ 9. Todo 관련 컴포넌트 및 뷰 구현
- [ ] Todo 목록 컴포넌트 (`TodoList.vue`)
- [ ] Todo 아이템 컴포넌트 (`TodoItem.vue`)
- [ ] Todo 생성/수정 폼 (`TodoForm.vue`)
- [ ] Todo 필터 컴포넌트 (`TodoFilter.vue`)
- [ ] 대시보드 페이지 구현
- [ ] 반응형 디자인 적용

### ⏸️ 10. API 통합 설정
- [ ] Axios 인스턴스 설정
- [ ] API 서비스 파일 생성
  - [ ] 인증 API 서비스
  - [ ] Todo API 서비스
- [ ] HTTP 인터셉터 설정 (토큰 자동 첨부, 에러 처리)
- [ ] API 에러 핸들링

### ⏸️ 11. Pinia를 사용한 상태 관리 구현
- [ ] 인증 스토어 (`auth.js`) 구현
- [ ] Todo 스토어 (`todo.js`) 구현
- [ ] 전역 상태와 컴포넌트 연결
- [ ] 상태 지속성 설정 (localStorage)

---

## Phase 4: 통합 및 개발 환경

### ⏸️ 12. 개발용 Docker 설정
- [ ] 프론트엔드 Dockerfile 작성
- [ ] 백엔드 Dockerfile 작성
- [ ] Docker Compose 개발 환경 구성
- [ ] 핫 리로드 설정
- [ ] 환경 변수 설정

### ⏸️ 13. 보안 설정 및 CORS 구성
- [ ] CORS 설정 (백엔드)
- [ ] CSP (Content Security Policy) 설정
- [ ] 환경별 보안 설정
- [ ] HTTPS 설정 (프로덕션)

---

## Phase 5: 테스트

### ⏸️ 14. 백엔드 단위 테스트 작성
- [ ] 서비스 레이어 테스트
- [ ] 컨트롤러 테스트 (MockMvc)
- [ ] Repository 테스트 (TestContainers)
- [ ] 통합 테스트
- [ ] 테스트 커버리지 설정

### ⏸️ 15. 프론트엔드 컴포넌트 테스트 작성
- [ ] 컴포넌트 단위 테스트 (Vue Test Utils)
- [ ] 스토어 테스트
- [ ] API 서비스 테스트
- [ ] E2E 테스트 (Cypress) 설정

---

## Phase 6: 빌드 및 배포

### ⏸️ 16. 빌드 스크립트 및 CI/CD 파이프라인 설정
- [ ] 프론트엔드 빌드 스크립트
- [ ] 백엔드 빌드 스크립트 (Maven/Gradle)
- [ ] 통합 빌드 스크립트
- [ ] GitHub Actions 또는 GitLab CI 설정
- [ ] 자동 테스트 실행

### ⏸️ 17. 모니터링 및 로깅 설정
- [ ] 백엔드 로깅 설정 (Logback)
- [ ] Spring Boot Actuator 설정
- [ ] 프론트엔드 에러 로깅
- [ ] 헬스체크 엔드포인트

### ⏸️ 18. 배포 문서 작성
- [ ] 로컬 개발 환경 설정 가이드
- [ ] 프로덕션 배포 가이드
- [ ] API 문서 (OpenAPI/Swagger)
- [ ] 사용자 가이드
- [ ] CLAUDE.md 업데이트

---

## 추가 개선 사항 (Optional)

### ⏸️ 성능 최적화
- [ ] 프론트엔드 코드 스플리팅
- [ ] 이미지 최적화
- [ ] 백엔드 캐싱 구현 (Redis)
- [ ] 데이터베이스 인덱스 최적화

### ⏸️ 기능 확장
- [ ] Todo 카테고리/태그 기능
- [ ] 파일 첨부 기능
- [ ] 알림 기능
- [ ] 다크 모드 지원
- [ ] 다국어 지원 (i18n)

### ⏸️ 보안 강화
- [ ] Rate Limiting
- [ ] API 버전 관리
- [ ] 감사 로그
- [ ] 데이터 백업 전략

---

## 진행 노트
- 각 단계별로 완료 후 체크박스에 ✅ 표시
- 문제가 발생한 경우 해당 항목에 이슈 링크나 설명 추가
- 새로운 요구사항이나 개선사항 발견 시 해당 섹션에 추가

## AI 협업 개선 사항
이 TODO.md 파일의 AI 협업 최적화가 적용된 부분:
- ✅ **구체적인 명령어**: 각 작업에 실행할 bash 명령어 제공
- ✅ **의존성 명시**: 작업 순서와 전제조건 표시
- ✅ **완료 조건**: 각 단계의 성공 기준 명확화
- ✅ **파일 경로**: 생성/수정할 파일 목록 제공
- ⚠️  **부분 적용**: Phase 1-1, 1-2번만 상세화 (예시용)

### 전체 파일 최적화 시 고려사항
1. **파일 크기**: 모든 작업을 상세화하면 매우 긴 파일이 됨
2. **유지보수**: 요구사항 변경 시 업데이트 복잡도 증가  
3. **가독성**: 너무 상세하면 개요 파악이 어려워짐

**권장 접근법**: 현재 진행 중인 Phase만 상세화하고 나머지는 요약 형태로 유지