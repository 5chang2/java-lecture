### 🏛️ DDL (Data Definition Language)

DDL은 데이터베이스의 구조를 정의하는, 마치 건물의 **설계도**를 그리는 것과 같은 역할을 합니다. 🏗️ DDL을 통해 우리는 데이터를 담을 공간(Database)을 만들고, 그 안에 체계적으로 데이터를 정리할 표(Table)의 구조를 설계하고, 필요에 따라 리모델링하거나 철거할 수 있습니다.

---

###  🗂️ 데이터 타입 (Data Types)
> 공식문서 https://dev.mysql.com/doc/refman/8.4/en/data-types.html

**데이터 타입**은 테이블의 각 열(Column)에 저장될 데이터의 종류를 미리 지정하는 규칙입니다. 올바른 데이터 타입을 선택하는 것은 **저장 공간을 효율적으로 사용**하고, **데이터의 정확성을 보장**하며, **검색 속도를 향상**시키는 데 매우 중요합니다.

---

####  **1. 숫자 타입 (Numeric Types)** 🔢

정수나 소수처럼 숫자 형태의 데이터를 저장할 때 사용합니다.

| 데이터 타입              | 설명 및 용도                                                                            | 예시                                   |
| ------------------- | ---------------------------------------------------------------------------------- | ------------------------------------ |
| **`INT`**           | 가장 일반적으로 사용되는 **정수**입니다. (약 -21억 ~ 21억)                                            | `user_id`, `post_id`, `나이`, `재고 수량`  |
| **`BIGINT`**        | `INT`보다 훨씬 큰 범위의 정수를 저장합니다. (약 -900경 ~ 900경)                                       | `은행 계좌 번호`, `매우 큰 시스템의 고유 ID`        |
| **`TINYINT`**       | 매우 작은 범위의 정수를 저장합니다. (-128 ~ 127)                                                  | `상태 코드 (0, 1, 2)`, `성별 (0: 남, 1: 여)` |
| **`DECIMAL(p, s)`** | **고정 소수점** 숫자로, 금융 정보처럼 절대적인 정확도가 필요할 때 사용합니다. `p`는 총 자릿수, `s`는 소수점 이하 자릿수를 의미합니다. | `상품 가격 (DECIMAL(10, 2))`, `계좌 잔액`    |
| **`DOUBLE`**        | **부동 소수점** 숫자로, 매우 큰 소수나 과학적 계산에 사용됩니다. 약간의 오차가 발생할 수 있습니다.                        | `GPS 좌표`, `과학 계산 결과`                 |

```sql
CREATE TABLE products (
    product_id   INT,
    price        DECIMAL(10, 2), -- 총 10자리 중 소수점 아래 2자리 (예: 12345678.99)
    stock        INT
);
```


#### **2. 문자열 타입 (String Types)** 📝

글자, 문장 등 텍스트 형태의 데이터를 저장할 때 사용합니다.

| 데이터 타입           | 설명 및 용도                                                                             | 예시                                        |
| ---------------- | ----------------------------------------------------------------------------------- | ----------------------------------------- |
| **`VARCHAR(n)`** | **가변 길이 문자열**로, `n`에 지정된 최대 길이까지 저장합니다. 가장 흔하게 사용되며, 실제 저장된 글자 수만큼만 공간을 차지해 효율적입니다. | `이메일 (VARCHAR(100))`, `닉네임 (VARCHAR(50))` |
| **`CHAR(n)`**    | **고정 길이 문자열**로, 항상 `n`만큼의 공간을 차지합니다. 실제 저장된 글자 수가 `n`보다 작아도 남는 공간은 공백으로 채워집니다.      | `성별 코드 ('M', 'F')`, `국가 코드 ('KR', 'US')`  |
| **`TEXT`**       | **매우 긴 텍스트**를 저장할 때 사용합니다. 최대 길이를 미리 지정할 필요가 없습니다.                                  | `게시글 본문`, `상품 상세 설명`, `긴 댓글`              |




```SQL
CREATE TABLE members (
    email      VARCHAR(100),
    gender     CHAR(1), -- 'M' 또는 'F' 만 저장
    profile    TEXT
);
```

---

#### ### **3. 날짜와 시간 타입 (Date and Time Types)** ⏰

날짜나 시간 정보를 저장할 때 사용합니다.

|데이터 타입|설명 및 용도|예시 (저장 형태)|
|---|---|---|
|**`DATE`**|**날짜** 정보만 저장합니다.|`'2025-10-13'`|
|**`DATETIME`**|**날짜와 시간** 정보를 저장합니다. 가장 일반적으로 사용됩니다.|`'2025-10-13 17:25:00'`|
|**`TIMESTAMP`**|**날짜와 시간**을 저장하며, 데이터가 생성되거나 수정될 때의 시각을 자동으로 기록하는 기능이 있습니다. `수정일` 컬럼에 유용합니다.|`'2025-10-13 17:25:00'`|


```SQL
CREATE TABLE articles (
    title         VARCHAR(255),
    created_at    DATETIME DEFAULT NOW(),
    updated_at    TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);
```

---

#### 1. `CREATE`: 새로운 객체 만들기

`CREATE` 명령어는 데이터베이스, 테이블 등 새로운 구조를 생성하는 가장 기본적인 명령어입니다.

- **`CREATE DATABASE`**: 모든 테이블을 담을 가장 큰 저장 공간인 데이터베이스를 생성합니다.
    
    ```SQL
    -- board_db 라는 이름의 데이터베이스 생성 (한글 깨짐 방지 설정 포함)
    CREATE DATABASE board_db CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci;
    ```
    
- **`CREATE TABLE`**: 실제 데이터가 행과 열의 형태로 저장될 테이블을 생성합니다. 테이블을 만들 땐, 테이블 간의 관계를 정의하는 것이 매우 중요합니다.
    
    
    
```SQL
-- CREATE TABLE을 사용하기 전, 어떤 데이터베이스에서 작업할지 선택해야 합니다.
USE board_db;

-- [예제 1] 회원 정보를 담을 users 테이블 생성
CREATE TABLE users (
	user_id      INT             NOT NULL AUTO_INCREMENT,
	email        VARCHAR(100)    NOT NULL UNIQUE,
	nickname     VARCHAR(50)     NOT NULL,
	created_at   DATETIME        DEFAULT NOW(),
	PRIMARY KEY (user_id)
);

-- [예제 2] 게시글 정보를 담을 posts 테이블 생성 (users 테이블과 관계 설정)
CREATE TABLE posts (
	post_id      INT             NOT NULL AUTO_INCREMENT,
	title        VARCHAR(100)    NOT NULL,
	content      TEXT,
	created_at   DATETIME        DEFAULT NOW(),
	user_id      INT             NOT NULL, -- 작성자 ID (users 테이블의 user_id를 참조)
	PRIMARY KEY (post_id),
	FOREIGN KEY (user_id) REFERENCES users(user_id)
);
```
    
    > **💡 제약조건(Constraints)이란?**
    
    > 테이블에 데이터가 저장될 때 특정 규칙을 강제하여 데이터의 무결성을 지키는 중요한 요소입니다.
    
    > - `NOT NULL`: 이 열은 비어 있을 수 없습니다. (필수 값)
    >     
    > - `AUTO_INCREMENT`: 새로운 데이터가 추가될 때마다 숫자를 1씩 자동으로 증가시킵니다.
    >     
    > - `PRIMARY KEY`: 테이블의 각 행을 고유하게 식별하는 **대표 키**입니다. `NOT NULL`과 `UNIQUE` 속성을 모두 가집니다.
    >     
    > - `UNIQUE`: 이 열의 모든 값은 서로 중복될 수 없습니다. (예: 이메일, 아이디)
    >     
    > - `DEFAULT`: 값을 지정하지 않았을 때 자동으로 입력될 기본값을 설정합니다. (예: `DEFAULT NOW()`)
    >     
    > - `FOREIGN KEY`: 다른 테이블의 `PRIMARY KEY`를 참조하여 테이블 간의 **관계**를 맺어줍니다. 존재하지 않는 사용자가 글을 쓰는 것을 막아주는 등 데이터의 신뢰도를 보장합니다.
    >     
    

---

#### 2. `ALTER`: 기존 테이블 구조 수정하기

`ALTER` 명령어는 이미 만들어진 테이블의 구조를 변경할 때 사용합니다. 마치 지어진 건물을 리모델링하는 것과 같습니다.

- **`ADD COLUMN`**: 새로운 열(Column)을 추가합니다.
    
```SQL
-- posts 테이블에 '조회수(view_count)' 열을 추가하고 기본값으로 0을 설정합니다.
ALTER TABLE posts ADD view_count INT DEFAULT 0;
```
    
- **`MODIFY COLUMN`**: 기존 열의 데이터 타입이나 제약조건을 수정합니다.
    
```SQL
-- posts 테이블의 title 열의 최대 길이를 200으로 변경합니다.
ALTER TABLE posts MODIFY title VARCHAR(200) NOT NULL;
```
    
- **`CHANGE COLUMN`**: 기존 열의 **이름과 정의를 한 번에** 수정합니다. (MySQL에서 유용)
    
```SQL
-- users 테이블의 nickname 열 이름을 user_nickname으로 바꾸고 타입을 VARCHAR(30)으로 변경합니다.
ALTER TABLE users CHANGE nickname user_nickname VARCHAR(30) NOT NULL;
```
    
- **`DROP COLUMN`**: 기존 열을 삭제합니다.
    
    ```SQL
    -- posts 테이블에서 '조회수(view_count)' 열을 삭제합니다.
    ALTER TABLE posts DROP COLUMN view_count;
    ```
    
- **`ADD CONSTRAINT`**: 제약조건을 추가합니다.
    ```SQL
    -- users 테이블의 user_nickname 열에 UNIQUE 제약조건을 추가합니다.
    ALTER TABLE users ADD CONSTRAINT unique_nickname UNIQUE (user_nickname);
    ```
    

---

#### 3. `TRUNCATE`: 테이블 데이터 초기화하기

`TRUNCATE`는 테이블의 구조는 그대로 남겨두고, **안의 모든 데이터만** 빠르게 삭제하는 명령어입니다. `DELETE`문으로 모든 데이터를 삭제하는 것보다 훨씬 빠르지만, 되돌릴 수 없으므로 주의해야 합니다.

```SQL
-- ⚠️ 경고: 이 명령어는 posts 테이블의 모든 데이터를 삭제하지만, 테이블 구조는 남겨둡니다.
TRUNCATE TABLE posts;
```

---

#### 4. `DROP`: 객체 완전히 삭제하기

`DROP` 명령어는 테이블이나 데이터베이스 같은 구조를 **완전히 삭제**합니다. 데이터까지 모두 사라지며 되돌릴 수 없으므로 매우 신중하게 사용해야 합니다.

- **`DROP TABLE`**: 테이블의 구조와 모든 데이터를 영구적으로 삭제합니다.
    
    ```SQL
    -- ⚠️ 경고: 이 명령어는 posts 테이블과 안의 모든 데이터를 영원히 삭제합니다!
    DROP TABLE posts;
    ```
    
- **`DROP DATABASE`**: 데이터베이스와 그 안에 포함된 모든 테이블을 영구적으로 삭제합니다.
    
    ```SQL
    -- ⚠️ 초강력 경고: 이 명령어는 board_db 전체를 영원히 삭제합니다!
    DROP DATABASE board_db;
    ```
