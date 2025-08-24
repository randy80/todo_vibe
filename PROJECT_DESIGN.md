# Todo 리스트 모노리포 프로젝트 설계 문서

## 프로젝트 개요
- **목적**: 사용자가 할 일을 관리할 수 있는 웹 애플리케이션
- **아키텍처**: 모노리포 구조로 프론트엔드와 백엔드를 함께 관리
- **기술 스택**: Vue.js 3 (프론트엔드) + Spring Boot (백엔드)

## 모노리포 구조
```
todo-monorepo/
├── frontend/           # Vue.js 3 애플리케이션
│   ├── src/
│   ├── public/
│   ├── package.json
│   └── vite.config.js
├── backend/            # Spring Boot 애플리케이션
│   ├── src/main/java/
│   ├── src/main/resources/
│   ├── pom.xml
│   └── application.yml
├── shared/             # 공통 타입 정의 및 유틸리티
│   └── types/
├── docs/               # 프로젝트 문서
├── docker/             # Docker 설정
├── scripts/            # 빌드/배포 스크립트
├── package.json        # 루트 패키지 (workspaces)
└── README.md
```

## 프론트엔드 아키텍처 (Vue.js 3)

### 기술 스택
- **프레임워크**: Vue.js 3 with Composition API
- **빌드 도구**: Vite
- **상태관리**: Pinia
- **라우팅**: Vue Router 4
- **UI 라이브러리**: Vuetify 3 또는 Element Plus
- **HTTP 클라이언트**: Axios
- **타입스크립트**: TypeScript 지원

### 컴포넌트 구조
```
frontend/src/
├── components/
│   ├── common/         # 공통 컴포넌트
│   │   ├── Header.vue
│   │   ├── Footer.vue
│   │   └── Loading.vue
│   └── todo/           # Todo 관련 컴포넌트
│       ├── TodoList.vue
│       ├── TodoItem.vue
│       ├── TodoForm.vue
│       └── TodoFilter.vue
├── views/              # 페이지 컴포넌트
│   ├── Home.vue
│   ├── Login.vue
│   └── Dashboard.vue
├── stores/             # Pinia 스토어
│   ├── auth.js
│   └── todo.js
├── services/           # API 서비스
│   ├── api.js
│   ├── auth.service.js
│   └── todo.service.js
├── utils/              # 유틸리티 함수
├── types/              # TypeScript 타입 정의
└── router/             # 라우터 설정
```

### 주요 기능
- 사용자 인증 (로그인/회원가입)
- Todo 항목 CRUD (생성, 조회, 수정, 삭제)
- Todo 상태 관리 (완료/미완료)
- Todo 필터링 및 검색
- 반응형 디자인

## 백엔드 아키텍처 (Spring Boot)

### 기술 스택
- **프레임워크**: Spring Boot 3.x
- **보안**: Spring Security + JWT
- **데이터베이스**: PostgreSQL
- **ORM**: Spring Data JPA
- **API 문서**: OpenAPI 3 (Swagger)
- **테스팅**: JUnit 5, TestContainers

### 패키지 구조
```
backend/src/main/java/com/todo/
├── TodoApplication.java
├── config/             # 설정 클래스
│   ├── SecurityConfig.java
│   ├── JwtConfig.java
│   └── DatabaseConfig.java
├── controller/         # REST 컨트롤러
│   ├── AuthController.java
│   └── TodoController.java
├── service/            # 비즈니스 로직
│   ├── AuthService.java
│   └── TodoService.java
├── repository/         # 데이터 접근 계층
│   ├── UserRepository.java
│   └── TodoRepository.java
├── entity/             # JPA 엔티티
│   ├── User.java
│   └── Todo.java
├── dto/                # 데이터 전송 객체
│   ├── request/
│   └── response/
├── security/           # 보안 관련
│   ├── JwtTokenProvider.java
│   └── UserDetailsServiceImpl.java
└── exception/          # 예외 처리
    ├── GlobalExceptionHandler.java
    └── CustomExceptions.java
```

### 주요 기능
- JWT 기반 인증/인가
- RESTful API 제공
- 사용자 관리
- Todo CRUD API
- 입력 검증 및 예외 처리

## 데이터베이스 설계

### User 테이블
```sql
CREATE TABLE users (
    id BIGSERIAL PRIMARY KEY,
    username VARCHAR(50) UNIQUE NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    password VARCHAR(255) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### Todo 테이블
```sql
CREATE TABLE todos (
    id BIGSERIAL PRIMARY KEY,
    title VARCHAR(255) NOT NULL,
    description TEXT,
    completed BOOLEAN DEFAULT FALSE,
    priority VARCHAR(20) DEFAULT 'MEDIUM',
    due_date DATE,
    user_id BIGINT REFERENCES users(id) ON DELETE CASCADE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

## API 설계

### 인증 API
- `POST /api/auth/register` - 회원가입
- `POST /api/auth/login` - 로그인
- `POST /api/auth/logout` - 로그아웃
- `POST /api/auth/refresh` - 토큰 갱신

### Todo API
- `GET /api/todos` - Todo 목록 조회 (페이징, 필터링)
- `POST /api/todos` - Todo 생성
- `GET /api/todos/{id}` - 특정 Todo 조회
- `PUT /api/todos/{id}` - Todo 수정
- `DELETE /api/todos/{id}` - Todo 삭제
- `PATCH /api/todos/{id}/complete` - Todo 완료 상태 변경

### 응답 형식
```json
{
  "success": true,
  "data": {},
  "message": "Success",
  "timestamp": "2024-08-24T17:10:00Z"
}
```

## 개발 환경 설정

### 필수 도구
- Node.js 18+ (프론트엔드)
- Java 17+ (백엔드)
- PostgreSQL 14+
- Docker & Docker Compose

### 빌드 및 실행 명령어
```bash
# 전체 프로젝트 설치
npm install

# 프론트엔드 개발 서버
npm run dev:frontend

# 백엔드 개발 서버
npm run dev:backend

# 전체 빌드
npm run build

# Docker로 실행
docker-compose up -d
```

## 배포 전략

### 개발 환경
- Docker Compose를 사용한 로컬 개발 환경
- 핫 리로드 지원

### 프로덕션 환경
- 프론트엔드: Nginx 정적 호스팅
- 백엔드: Spring Boot JAR
- 데이터베이스: PostgreSQL
- 리버스 프록시: Nginx

## 보안 고려사항

1. **인증**: JWT 토큰 기반 인증
2. **CORS**: 프론트엔드 도메인만 허용
3. **입력 검증**: 모든 사용자 입력 검증
4. **SQL 인젝션 방지**: JPA Parameter Binding 사용
5. **비밀번호**: BCrypt 해싱
6. **HTTPS**: 프로덕션 환경에서 강제

## 테스트 전략

### 프론트엔드
- Unit Tests: Vitest
- Component Tests: Vue Test Utils
- E2E Tests: Cypress

### 백엔드
- Unit Tests: JUnit 5
- Integration Tests: TestContainers
- API Tests: MockMvc

## 모니터링 및 로깅

- **로깅**: Logback (백엔드), Console (프론트엔드)
- **메트릭**: Spring Boot Actuator
- **헬스체크**: `/actuator/health`