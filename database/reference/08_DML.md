### 🖋️ DML (Data Manipulation Language): 데이터 조작하고 생명 불어넣기

DDL로 데이터의 뼈대를 만들었다면, **DML**은 그 안에 **내용을 채우고, 읽고, 수정하고, 삭제하는** 역할을 합니다. ✍️ 즉, 실제 데이터를 직접 다루는 가장 빈번하게 사용되는 명령어입니다.

---

#### 1. `INSERT`: 새로운 데이터 추가하기

`INSERT` 명령어는 테이블에 새로운 행(row)을 추가하여 데이터를 저장합니다.

* **기본 문법**
    ```sql
    INSERT INTO 테이블명 (컬럼1, 컬럼2, ...) VALUES (값1, 값2, ...);
    ```

* **실습 예제**: 위에서 만든 `users`와 `posts` 테이블에 데이터를 추가해 봅시다.

    ```sql
    -- DML 작업을 위해 데이터베이스를 선택합니다.
    USE board_db;

    -- [예제 1] users 테이블에 새로운 회원 2명 추가
    INSERT INTO users (email, nickname) 
    VALUES ('kim@example.com', '개발자김씨');

    INSERT INTO users (email, nickname) 
    VALUES ('park@example.com', '디자이너박');

    -- [예제 2] posts 테이블에 새로운 게시글 추가
    -- '개발자김씨'(user_id=1)가 작성한 글을 추가합니다.
    INSERT INTO posts (title, content, user_id) 
    VALUES ('SQL이란 무엇인가?', 'SQL은 데이터베이스를 다루는 언어입니다.', 1);

    -- '디자이너박'(user_id=2)이 작성한 글을 추가합니다.
    INSERT INTO posts (title, content, user_id) 
    VALUES ('좋은 UI/UX 디자인', '사용자 경험이 중요합니다.', 2);
    ```

> **💡 중요!**: `posts` 테이블에 데이터를 추가할 때, `user_id`에는 반드시 `users` 테이블에 **실제로 존재하는 `user_id`**를 넣어야 합니다. `FOREIGN KEY` 제약조건 덕분에 존재하지 않는 ID를 넣으려고 하면 오류가 발생하여 데이터의 신뢰성을 지켜줍니다.

---

#### 2. `SELECT`: 데이터 조회하기

`SELECT`는 테이블에서 원하는 데이터를 꺼내오는, 가장 중요하고 많이 사용되는 명령어입니다.

* **`*` (Asterisk): 모든 컬럼 조회**
    ```sql
    -- users 테이블의 모든 데이터를 조회합니다.
    SELECT * FROM users;
    ```

* **특정 컬럼만 지정하여 조회**
    ```sql
    -- posts 테이블에서 제목(title)과 내용(content)만 조회합니다.
    SELECT title, content FROM posts;
    ```

* **`WHERE`: 조건에 맞는 데이터만 필터링**
    `WHERE` 절을 사용하면 원하는 조건에 맞는 데이터만 골라서 볼 수 있습니다.
    ```sql
    -- user_id가 1인 사용자의 정보만 조회합니다.
    SELECT * FROM users WHERE user_id = 1;

    -- '개발자김씨'가 작성한 모든 게시글을 조회합니다.
    SELECT * FROM posts WHERE user_id = 1;
    ```

* **`ORDER BY`: 결과 정렬하기**
    조회된 결과를 특정 컬럼 기준으로 정렬합니다. `DESC`는 내림차순, `ASC`는 오름차순(기본값)입니다.
    ```sql
    -- 모든 회원을 닉네임(nickname) 가나다순으로 정렬하여 조회합니다.
    SELECT * FROM users ORDER BY nickname ASC;

    -- 모든 게시글을 최신순(post_id가 큰 순서)으로 정렬하여 조회합니다.
    SELECT * FROM posts ORDER BY post_id DESC;
    ```

---

#### 3. `UPDATE`: 기존 데이터 수정하기

`UPDATE` 명령어는 이미 저장된 데이터의 내용을 변경합니다.

* **기본 문법**
    ```sql
    UPDATE 테이블명 SET 변경할컬럼 = 새로운값 WHERE 조건;
    ```

> **⚠️ 경고**: `UPDATE` 문에서 **`WHERE` 절을 생략하면 테이블의 모든 데이터가 변경**되는 대참사가 발생할 수 있습니다. 수정을 원하는 데이터를 정확히 지정하는 습관이 매우 중요합니다.

* **실습 예제**
    ```sql
    -- '개발자김씨'(user_id=1)의 닉네임을 '숙련된개발자김씨'로 변경합니다.
    UPDATE users
    SET nickname = '숙련된개발자김씨'
    WHERE user_id = 1;

    -- (확인) 변경이 잘 되었는지 확인합니다.
    SELECT * FROM users WHERE user_id = 1;
    ```

---

#### 4. `DELETE`: 데이터 삭제하기

`DELETE` 명령어는 테이블에서 특정 행을 삭제합니다.

* **기본 문법**
    ```sql
    DELETE FROM 테이블명 WHERE 조건;
    ```

> **⚠️ 경고**: `DELETE` 역시 **`WHERE` 절을 생략하면 테이블의 모든 데이터가 삭제**됩니다. `UPDATE`와 마찬가지로 삭제할 데이터를 명확히 지정해야 합니다.

* **실습 예제**
    ```sql
    -- '디자이너박'(user_id=2)이 작성한 게시글(post_id=2)을 삭제합니다.
    DELETE FROM posts WHERE post_id = 2;

    -- (확인) 전체 게시글을 조회하여 데이터가 삭제되었는지 확인합니다.
    SELECT * FROM posts;
    ```



