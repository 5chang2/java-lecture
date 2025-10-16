### 🔗 JOIN: 흩어진 데이터 연결하기

**JOIN**은 관계형 데이터베이스의 '꽃'이라고 불리는 가장 강력하고 중요한 기능 중 하나입니다. 🧩 데이터를 정규화(Normalization)하는 과정에서 여러 테이블로 나누어 저장하는데, `JOIN`은 이렇게 흩어져 있는 데이터 조각들을 **외래 키(Foreign Key)**를 기준으로 다시 합쳐서 하나의 완성된 정보로 만들어줍니다.

예를 들어, `posts` 테이블에는 '누가' 글을 썼는지 `user_id`만 저장되어 있고, 실제 사용자의 닉네임은 `users` 테이블에 저장되어 있습니다. `JOIN`을 사용하면 이 두 테이블을 연결하여 "어떤 닉네임의 사용자가 어떤 글을 썼는지" 한 번에 알아낼 수 있습니다.

---

#### **실습 데이터 준비**

`JOIN`을 연습하기 위해 이전에 만들었던 `board_db`에 간단한 데이터를 넣고 시작하겠습니다.

```sql
-- 1. board_db 데이터베이스 선택
USE board_db;

-- 2. 간단한 users, posts 테이블 생성 (이미 있다면 생략)
CREATE TABLE users (
  user_id INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
  nickname VARCHAR(50) NOT NULL
);

CREATE TABLE posts (
  post_id INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
  title VARCHAR(100) NOT NULL,
  user_id INT
);

-- 3. 샘플 데이터 추가
-- users 테이블 데이터
INSERT INTO users (nickname) VALUES ('개발자김'), ('디자이너박'), ('기획자이');

-- posts 테이블 데이터
INSERT INTO posts (title, user_id) VALUES ('SQL 기초', 1), ('데이터베이스란?', 1), ('UI/UX 디자인', 2);
```

---

### **1. INNER JOIN (내부 조인)**

`INNER JOIN`은 가장 기본적이고 널리 사용되는 조인입니다. 두 테이블에서 **조인 조건이 일치하는 행만**을 결과로 가져옵니다. 즉, 양쪽 테이블에 모두 데이터가 존재하는 '교집합' 부분만 보여줍니다.

* **기본 문법**
  ```sql
  SELECT
    -- 조회할 컬럼 목록
  FROM
    테이블1
  INNER JOIN
    테이블2 ON 테이블1.연결컬럼 = 테이블2.연결컬럼;
  ```

* **실습 예제**: 각 게시글(`posts`)을 작성한 사용자(`users`)의 닉네임을 함께 조회해 봅시다.
  ```sql
  SELECT
    p.title,
    u.nickname
  FROM
    posts p
  INNER JOIN
    users u ON p.user_id = u.user_id;
  ```
  > **💡 결과**: '기획자이'는 작성한 글이 없으므로 `INNER JOIN` 결과에는 나타나지 않습니다.

  > **💡 테이블 별칭(Alias) 사용하기**
  >
  > `posts p`, `users u`처럼 테이블 이름 뒤에 별칭을 붙이면, 쿼리가 길어질 때 훨씬 간결하고 가독성 좋게 작성할 수 있습니다.

---

### **2. LEFT JOIN (외부 조인)**

`LEFT JOIN`은 **왼쪽 테이블(FROM 절에 먼저 오는 테이블)의 모든 데이터**를 우선적으로 보여주고, 그 다음 오른쪽 테이블에서 조인 조건에 맞는 데이터를 연결합니다. 만약 오른쪽 테이블에 일치하는 데이터가 없으면 해당 컬럼은 **`NULL`**로 표시됩니다.

* **기본 문법**
  ```sql
  SELECT
    -- 조회할 컬럼 목록
  FROM
    테이블1 -- 왼쪽 테이블
  LEFT JOIN
    테이블2 ON 테이블1.연결컬럼 = 테이블2.연결컬럼;
  ```

* **실습 예제**: 모든 사용자(`users`)의 목록과, 각 사용자가 작성한 게시글(`posts`)의 제목을 함께 조회해 봅시다.
  ```sql
  SELECT
    u.nickname,
    p.title
  FROM
    users u
  LEFT JOIN
    posts p ON u.user_id = p.user_id;
  ```
  > **💡 결과**: '기획자이'는 작성한 글이 없지만 `users` 테이블에 존재하므로 결과에 포함되며, `title` 컬럼은 `NULL`로 표시됩니다.

---

### **3. RIGHT JOIN (외부 조인)**

`RIGHT JOIN`은 `LEFT JOIN`과 반대로 동작합니다. **오른쪽 테이블(JOIN 절에 오는 테이블)의 모든 데이터**를 우선적으로 보여주고, 왼쪽 테이블에서 조건에 맞는 데이터를 연결합니다. 일치하는 데이터가 없으면 왼쪽 테이블의 컬럼은 **`NULL`**로 표시됩니다.

* **실습 예제**: 모든 게시글(`posts`)과 그 글을 작성한 사용자(`users`)의 닉네임을 조회합니다. (이 경우 `INNER JOIN`과 결과가 동일합니다.)
  ```sql
  SELECT
    u.nickname,
    p.title
  FROM
    users u
  RIGHT JOIN
    posts p ON u.user_id = p.user_id;
  ```
  > **💡 언제 사용할까?**
  >
  > `RIGHT JOIN`은 `LEFT JOIN`으로 바꿔 쓸 수 있는 경우가 많아 상대적으로 사용 빈도가 낮지만, 쿼리 구조상 오른쪽 테이블을 기준으로 데이터를 봐야 할 때 유용합니다.

---

### **4. SELF JOIN (셀프 조인)**

`SELF JOIN`은 특별한 문법이 있는 것이 아니라, **하나의 테이블을 자기 자신과 조인**하는 기법을 의미합니다. 같은 테이블 내에서 행과 행 사이의 관계를 찾아야 할 때 사용합니다. 이때 반드시 **테이블 별칭(Alias)**을 사용하여 두 테이블을 구분해야 합니다.

* **실습 예제**: `sakila` 데이터베이스의 `film` 테이블을 사용하여, 상영 시간(`length`)이 동일한 다른 영화들의 목록을 찾아봅시다.
  ```sql
  USE sakila;

  SELECT
    f1.title AS '영화1',
    f2.title AS '영화2',
    f1.length
  FROM
    film f1
  INNER JOIN
    film f2 ON f1.length = f2.length AND f1.film_id != f2.film_id
  LIMIT 10; -- 결과가 너무 많으므로 10개만 확인
  ```
  > **💡 `f1.film_id != f2.film_id`**
  >
  > 이 조건이 없으면 모든 영화가 자기 자신과 조인되므로, 자기 자신을 제외하기 위해 추가하는 중요한 조건입니다.