# Spring Boot 웹 개발 강의 교안

## 📖 강의 소개

이 강의는 **Java 기초를 마친 학생**을 대상으로 Spring Boot를 활용한 웹 애플리케이션 개발을 가르치기 위해 만들어진 교안입니다.

Instagram 클론코딩 프로젝트를 중심으로 실무에서 필요한 백엔드 개발 역량을 체계적으로 학습하며, 서버 사이드 렌더링(풀스택)과 REST API 서버 개발을 모두 경험합니다.

## 🎯 학습 목표

이 강의를 마치면 학습자는 다음을 할 수 있게 됩니다:

- Spring Boot 프레임워크의 핵심 개념과 동작 원리를 이해합니다
- MVC 패턴을 이해하고 웹 애플리케이션을 설계할 수 있습니다
- Thymeleaf를 사용하여 서버 사이드 렌더링 웹 애플리케이션을 개발할 수 있습니다
- RESTful API를 설계하고 구현할 수 있습니다
- Spring Data JPA와 MyBatis를 활용하여 데이터베이스를 연동할 수 있습니다
- Spring Security로 인증/인가를 구현할 수 있습니다
- 파일 업로드, 이미지 처리 등 실무 기능을 구현할 수 있습니다
- Instagram 수준의 소셜 미디어 플랫폼을 직접 개발할 수 있습니다

## 👥 대상 독자

### 선수 지식
- Java 기본 문법 및 객체 지향 프로그래밍 (본 저장소의 Java 강의 선수 학습 권장)
- 데이터베이스 기초 지식 (SQL 기본 문법)
- HTML/CSS 기초 (간단한 웹 페이지 구조 이해)
- HTTP 프로토콜 기본 개념

### 적합한 학습자
- Java를 배운 후 백엔드 개발을 시작하고 싶은 학생
- Spring Boot를 체계적으로 학습하고 싶은 학생
- 실무 수준의 프로젝트 경험을 쌓고 싶은 학생
- 풀스택 개발과 API 서버 개발을 모두 경험하고 싶은 학생

## 📚 커리큘럼

전체 강의는 13개 챕터로 구성되어 있으며, 기초부터 실전 프로젝트까지 단계적으로 학습합니다.

### Part 1: Spring Boot 기초 (챕터 1-3)
1. **Spring Boot 소개 및 환경 설정**
2. **Spring MVC 기초** (풀스택 - Thymeleaf)
3. **RESTful API 개발** (API 서버)

### Part 2: 데이터베이스 연동 (챕터 4-5)
4. **데이터베이스 연동 Part 1 - Spring Data JPA**
5. **데이터베이스 연동 Part 2 - MyBatis**

### Part 3: Instagram 클론코딩 프로젝트 (챕터 6-8)
6. **Instagram Part 1: 사용자 관리**
   - 회원가입/로그인 (풀스택 + API)
   - 프로필 관리
7. **Instagram Part 2: 게시물 관리**
   - 이미지 업로드
   - 게시물 CRUD
   - 피드 조회
8. **Instagram Part 3: 소셜 기능**
   - 좋아요/언라이크
   - 댓글 작성/삭제
   - 팔로우/언팔로우

### Part 4: 핵심 기능 (챕터 9-11)
9. **Spring Security** (인증/인가/JWT)
10. **예외 처리 및 유효성 검증**
11. **API 문서화** (Swagger/OpenAPI)

### Part 5: 테스트 및 배포 (챕터 12-13)
12. **테스트 기초** (Unit & Integration)
13. **배포 및 운영** (빌드/프로파일/로깅)

**상세 목차**: [목차.md](./목차.md)를 참고하세요.

## 💡 교육 방법론

### Plain Java vs Spring Boot 비교

Spring Boot가 어떤 문제를 해결하는지 이해하기 위해, 순수 Java로 웹 서버를 만들 때의 번거로움을 먼저 보여주고 Spring Boot의 장점을 비교합니다.

**예시**:
| Plain Java (Servlet) | Spring Boot |
|----------------------|-------------|
| 복잡한 설정 파일 (web.xml) | 자동 설정 |
| 수동 의존성 관리 | Spring Boot Starter |
| 서버 설치 및 배포 복잡 | 내장 서버 (Tomcat) |
| 반복적인 보일러플레이트 | Convention over Configuration |

### 풀스택 + API 서버 병행 학습

**두 가지 개발 방식을 모두 학습합니다:**

#### 1. 풀스택 개발 (Server-Side Rendering)
- **기술**: Spring MVC + Thymeleaf
- **용도**: 전통적인 웹 애플리케이션
- **장점**: SEO, 빠른 초기 로딩
- **예제**: 로그인 페이지, 프로필 페이지

#### 2. API 서버 개발 (REST API)
- **기술**: @RestController + JSON
- **용도**: 프론트엔드 프레임워크와 분리 (React/Vue)
- **장점**: 확장성, 모바일 앱 대응
- **예제**: `/api/users`, `/api/posts`

#### 학습 흐름
```
1. 기본 개념 (풀스택 방식으로 학습)
   └─> Thymeleaf로 화면 만들기

2. 같은 기능을 API 서버로 구현
   └─> JSON 응답으로 변경

3. 프로젝트에 두 방식 모두 적용
```

### Instagram 클론코딩 프로젝트

실무 수준의 소셜 미디어 플랫폼을 단계적으로 구축합니다.

**주요 기능**:
- 사용자 관리 (회원가입, 로그인, 프로필)
- 게시물 관리 (이미지 업로드, CRUD, 피드)
- 소셜 기능 (좋아요, 댓글, 팔로우)

**프로젝트 구조**:
```
student/
├── starter/          # 실습 시작 코드 (뼈대만 제공)
├── solution/         # 완성 코드 (참고용)
└── templates/        # 프로젝트 템플릿
```

### JPA vs MyBatis 비교

두 가지 ORM 도구를 모두 다루며, 각각의 장단점을 이해합니다.

**비교**:
| 특징 | Spring Data JPA | MyBatis |
|------|----------------|---------|
| 접근 방식 | 객체 중심 | SQL 중심 |
| 학습 곡선 | 높음 | 낮음 |
| 생산성 | 높음 (CRUD 자동 생성) | 중간 |
| 복잡한 쿼리 | JPQL/QueryDSL 필요 | SQL 직접 작성 용이 |
| 사용 케이스 | CRUD 중심 애플리케이션 | 복잡한 쿼리가 많은 경우 |

### 실습 중심 학습

각 섹션마다 실습 문제를 제공하여 즉시 적용할 수 있도록 합니다.
- 이론 설명 → 예제 코드 시연 → 실습 문제 → 답안 설명

## 📋 강의 진행 가이드

### 권장 진행 시간
- **전체 과정**: 약 50-60시간
- **챕터당**: 3-5시간
- **Instagram 프로젝트**: 15-20시간 (챕터 6-8)
- **실습 시간**: 각 챕터당 1-2시간 별도

### 진행 순서
1. 개념 설명 (Plain Java와 비교 포함)
2. Spring Boot 코드 예제 시연
3. 실습 문제 제시
4. 학습자 실습 및 질의응답
5. 답안 설명 및 피드백

### 준비물
- JDK 21 설치
- IntelliJ IDEA (Community/Ultimate)
- MySQL 8.0+
- Postman 또는 Insomnia (API 테스트용)
- Git

### 실습 환경 구성

#### 1. Spring Boot 프로젝트 생성
- [Spring Initializr](https://start.spring.io/) 활용
- Gradle 프로젝트
- Java 21
- 필요한 의존성 선택

#### 2. 데이터베이스 설정
```properties
# application.properties
spring.datasource.url=jdbc:mysql://localhost:3306/instagram
spring.datasource.username=root
spring.datasource.password=password
spring.jpa.hibernate.ddl-auto=update
```

## 🔗 관련 자료

- **목차**: [목차.md](./목차.md) - 전체 강의 목차 및 섹션 링크
- **참고 자료**: `reference/` 폴더 - Spring Boot 가이드, 예제 코드
- **학생용 자료**: `student/` 폴더 - 프로젝트 템플릿, 실습 자료
  - `student/starter/`: 실습 시작 코드
  - `student/solution/`: 완성 코드 (참고용)
  - `student/templates/`: 프로젝트 템플릿

## 📌 주의사항

- 이 교안은 **강사용**입니다. 학생들에게는 `student/` 폴더의 자료를 배포하세요.
- Java 기초가 부족한 학생은 본 저장소의 Java 강의를 먼저 학습하도록 안내하세요.
- Instagram 프로젝트는 단계별로 진행하며, 각 단계를 완료한 후 다음 단계로 넘어가세요.
- **풀스택과 API 서버를 혼동하지 않도록** 각 방식의 차이를 명확히 설명하세요.
- **JPA와 MyBatis의 사용 목적이 다름**을 강조하고, 상황에 맞게 선택하는 법을 가르치세요.
- 실습 시 학습자들이 직접 코드를 작성하도록 유도하세요 (복사-붙여넣기 지양).
- 에러가 발생했을 때 로그를 읽고 디버깅하는 방법을 가르쳐주세요.
- Spring Boot 버전에 따라 API가 변경될 수 있으니 최신 공식 문서를 참고하세요.

---

## 🤖 AI 작업 가이드 (Claude Code)

이 섹션은 Claude Code나 다른 AI 도구로 이 강의 교안을 작성하거나 수정할 때 참고하는 가이드입니다.

### 대상 독자

**Java 기초를 마친 학생**을 대상으로 합니다.
- Java 기본 문법 및 OOP 이해
- 데이터베이스 기초 지식 (SQL)
- 웹 개발 경험은 없거나 적음
- Spring Boot는 처음 배움

### 교육 접근법

**실무 중심의 프로젝트 기반 학습 + Plain Java와의 비교**가 핵심입니다.

모든 주요 개념을 설명할 때:
1. 왜 Spring Boot가 필요한지 (Plain Java의 문제점)
2. Spring Boot가 어떻게 문제를 해결하는지
3. 실제 프로젝트에 어떻게 적용하는지

### 주요 교육 패턴

#### 1. Plain Java vs Spring Boot 비교

**항상 비교를 통해 Spring Boot의 가치를 설명합니다:**

```markdown
**Plain Java (Servlet)**:
\`\`\`java
// web.xml 설정 필요
// 서블릿 등록, 매핑 등 복잡한 설정
@WebServlet("/hello")
public class HelloServlet extends HttpServlet {
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) {
        // 복잡한 보일러플레이트
    }
}
\`\`\`

**Spring Boot**:
\`\`\`java
@RestController
public class HelloController {
    @GetMapping("/hello")
    public String hello() {
        return "Hello, World!";
    }
}
\`\`\`
```

#### 2. 풀스택 + API 서버 병행 학습

**두 가지 방식을 모두 제시합니다:**

```markdown
### 방식 1: 풀스택 (Thymeleaf)
\`\`\`java
@Controller
public class UserController {
    @GetMapping("/users")
    public String getUsers(Model model) {
        model.addAttribute("users", userService.findAll());
        return "users";  // users.html 렌더링
    }
}
\`\`\`

### 방식 2: API 서버 (REST)
\`\`\`java
@RestController
@RequestMapping("/api")
public class UserApiController {
    @GetMapping("/users")
    public List<User> getUsers() {
        return userService.findAll();  // JSON 응답
    }
}
\`\`\`
```

#### 3. Instagram 프로젝트 중심 학습

**모든 개념을 Instagram 프로젝트에 적용합니다:**

- 회원가입 → Spring Security
- 게시물 업로드 → 파일 처리
- 좋아요 → 관계 매핑
- 피드 → 복잡한 쿼리

각 챕터에서 배운 내용을 즉시 프로젝트에 적용하여 실무 감각을 키웁니다.

#### 4. JPA vs MyBatis 비교

**두 도구의 차이를 명확히 설명합니다:**

```markdown
### JPA 방식
\`\`\`java
@Repository
public interface UserRepository extends JpaRepository<User, Long> {
    List<User> findByUsername(String username);
}
\`\`\`

### MyBatis 방식
\`\`\`java
@Mapper
public interface UserMapper {
    @Select("SELECT * FROM users WHERE username = #{username}")
    List<User> findByUsername(String username);
}
\`\`\`

**언제 JPA를 사용할까?**
- CRUD 중심 애플리케이션
- 객체 지향적 접근 선호

**언제 MyBatis를 사용할까?**
- 복잡한 SQL 쿼리가 많은 경우
- 기존 SQL을 재사용해야 하는 경우
```

#### 5. 계층 구조 강조

**항상 3-tier 아키텍처를 유지합니다:**

```
Controller (요청 처리)
    ↓
Service (비즈니스 로직)
    ↓
Repository (데이터 액세스)
```

### 콘텐츠 작성 규칙

1. **언어**: 모든 내용은 한국어로 작성
2. **비교 학습**: Plain Java와 Spring Boot를 항상 비교
3. **실습 중심**: 각 섹션마다 Instagram 프로젝트 관련 실습 포함
4. **두 방식 제시**: 풀스택 + API 서버 방식 모두 설명
5. **JPA + MyBatis**: 두 도구를 모두 다루되, 차이점 명확히 구분
6. **테스트 비중**: 기본적인 테스트만 포함 (깊이 있게 다루지 않음)
7. **버전**: Spring Boot 3.2+, Java 21 기준

### 파일 구조 규칙

- **챕터 디렉토리**: `NN_주제_이름` (예: `06_Instagram_프로젝트_Part1_사용자_관리`)
- **섹션 파일**: `N.N_소주제_이름.md` (예: `6.1_회원가입_구현.md`)
- **목차 업데이트**: 새 섹션 추가 시 `목차.md` 즉시 업데이트

### Instagram 프로젝트 구조

**student 폴더 구조**:
```
student/
├── starter/          # 실습 시작 코드 (뼈대만)
├── solution/         # 완성 코드 (참고용)
└── templates/        # 프로젝트 템플릿
```

**프로젝트 진행 방식**:
- 챕터 6-8에서 Instagram 프로젝트를 단계적으로 구축
- 각 챕터마다 starter 코드 제공 (이전 챕터 완성 코드 기반)
- 학생이 직접 구현 후 solution 코드와 비교

### reference 폴더 활용

- reference 폴더의 파일은 **참고 자료**일 뿐
- 내용을 그대로 복사하지 말고, Java 기초 학습자 관점에서 재구성
- Instagram 프로젝트에 맞게 예제를 커스터마이징

### 실습 문제 작성 가이드

**각 실습 문제는 다음 형식을 따릅니다:**

```markdown
## 실습 문제

### 문제 1: 사용자 회원가입 API 구현

**요구사항**:
- POST `/api/users/signup` 엔드포인트 구현
- 요청 본문: username, email, password
- 비밀번호는 BCrypt로 암호화
- 중복 사용자명 체크

**힌트**:
- @PostMapping 사용
- UserService에 비즈니스 로직 작성
- @Valid로 유효성 검증

**답안**:
(상세한 답안 코드 제공)
```

---

## 💬 피드백

강의 중 발견된 오류나 개선 사항은 저장소에 이슈로 남겨주세요.
