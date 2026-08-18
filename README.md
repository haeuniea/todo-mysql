# Todo MySQL API

Spring Boot와 Spring Data JPA를 활용하여 구현한 MySQL 기반 Todo REST API 프로젝트입니다.

기존 인메모리 기반 Todo API를 확장하여 MySQL에 데이터를 영속적으로 저장하고,
Entity와 DTO를 분리하여 CRUD 기능을 구현했습니다.

## 개발 환경

- Java 21
- Spring Boot 4.1.0
- Gradle
- Spring Web MVC
- Spring Data JPA
- MySQL 8.0
- Docker
- Lombok
- Springdoc OpenAPI (Swagger)
- JUnit 5
- Mockito
- Testcontainers

## 프로젝트 구조

```text
com.asdf.todo
├── config
│   └── ApiDocumentationConfig
├── controller
│   └── TodoController
├── dto
│   ├── TodoRequestDto
│   └── TodoResponseDto
├── entity
│   └── Todo
├── repository
│   └── TodoRepository
├── service
│   └── TodoService
├── util
│   └── EntityDtoMapper
└── TodoApplication
```

### 계층 구조

```text
REST Client
     ↓
Controller
     ↓
Service
     ↓
Repository
     ↓
JPA / Hibernate
     ↓
MySQL
```

## 주요 기능

| HTTP Method | Endpoint | 기능 |
|---|---|---|
| GET | `/api/todos/v2` | 전체 Todo 조회 |
| GET | `/api/todos/v2/{id}` | 특정 Todo 조회 |
| POST | `/api/todos/v2` | Todo 생성 |
| PUT | `/api/todos/v2/{id}` | Todo 수정 |
| DELETE | `/api/todos/v2/{id}` | Todo 삭제 |

## 데이터 저장 방식

Spring Data JPA를 이용하여 Todo 데이터를 MySQL에 저장합니다.

기존 인메모리 방식의 `Map` 대신 `JpaRepository`를 사용하며,
요청과 응답에는 `TodoRequestDto`, `TodoResponseDto`를 사용합니다.

## 실행 방법

### 1. MySQL 실행

Docker를 이용하여 MySQL 컨테이너를 실행합니다.

```bash
docker start mysql-todo
```

> 최초 실행 시에는 프로젝트에서 사용하는 MySQL 컨테이너를 먼저 생성해야 합니다.  
> mysql-todo용 Docker MySQL은 호스트의 `3307` 포트를 사용합니다.

### 2. 프로젝트 빌드

WSL2 터미널에서 프로젝트 디렉토리로 이동하여 빌드합니다.

```bash
cd ~/eog-springboot4/todo-mysql
gradle build
```

### 3. 애플리케이션 실행

```bash
gradle bootRun
```

### 4. Swagger UI 접속

애플리케이션 실행 후 브라우저에서 Swagger UI에 접속하여 API를 확인하고 테스트할 수 있습니다.

```text
http://localhost:8080/swagger-ui/index.html
```


## 테스트

```bash
./gradlew test
```

- `TodoControllerTests`: MockMvc와 Mockito를 이용한 Controller 테스트
- `TodoServiceTests`: Testcontainers MySQL을 이용한 Service 및 JPA 테스트

## 학습 내용

- Spring Data JPA와 `JpaRepository`
- JPA Entity와 MySQL 테이블 매핑
- Entity와 DTO 분리
- DTO ↔ Entity 변환
- `@Transactional`을 이용한 트랜잭션 처리
- Docker를 이용한 MySQL 실행
- Testcontainers를 이용한 테스트

## 참고

이 프로젝트는 『스프링 부트 개발자 온보딩 가이드』의 예제를 참고하여 학습 목적으로 구현했습니다.

기존 `todo-in-memory` 프로젝트를 MySQL 기반으로 확장했으며,
현재 학습 환경에 맞게 Spring Boot 3에서 Spring Boot 4.1.0으로 변경하여 진행했습니다.