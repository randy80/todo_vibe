# Todo List Monorepo

Vue.js 3 프론트엔드와 Spring Boot 백엔드를 사용한 Todo 리스트 애플리케이션입니다.

## 프로젝트 구조

```
todo-monorepo/
├── frontend/           # Vue.js 3 애플리케이션
├── backend/            # Spring Boot 애플리케이션  
├── shared/             # 공통 타입 정의 및 유틸리티
├── docs/               # 프로젝트 문서
├── scripts/            # 빌드/배포 스크립트
└── docker/             # Docker 설정
```

## 기술 스택

### 프론트엔드
- Vue.js 3 (Composition API)
- TypeScript
- Vite
- Vue Router 4
- Pinia (상태관리)
- Vuetify 3 (UI 라이브러리)
- Axios (HTTP 클라이언트)

### 백엔드  
- Spring Boot 3.x
- Java 17+
- Spring Security + JWT
- Spring Data JPA
- PostgreSQL
- Maven

## 개발 환경 설정

### 필수 요구사항
- Node.js 18+
- Java 17+
- PostgreSQL 14+
- Maven 3.6+

### 설치 및 실행

1. 저장소 클론
```bash
git clone <repository-url>
cd todo-monorepo
```

2. 환경변수 설정
```bash
cp .env.example .env
# .env 파일을 편집하여 환경변수 설정
```

3. 의존성 설치
```bash
npm run install:all
```

4. 개발 서버 실행
```bash
npm run dev
```

### 개별 실행
```bash
# 프론트엔드만 실행
npm run dev:frontend

# 백엔드만 실행  
npm run dev:backend
```

## 빌드 및 테스트

```bash
# 전체 빌드
npm run build

# 전체 테스트
npm run test
```

## 문서

- [설계 문서](PROJECT_DESIGN.md)
- [할일 목록](TODO.md)
- [Claude 가이드](CLAUDE.md)

## 개발 가이드

개발 시작 전 TODO.md 파일을 참고하여 단계별로 진행하세요.