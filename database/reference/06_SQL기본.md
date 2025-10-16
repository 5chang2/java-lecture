
## 💬 SQL (Structured Query Language) 이란?

**SQL**은 데이터베이스에 저장된 데이터를 관리하고 처리하기 위해 사용하는 **표준 프로그래밍 언어**입니다. 👨‍💻 데이터베이스에게 데이터를 **삽입(INSERT)**, **조회(SELECT)**, **수정(UPDATE)**, **삭제(DELETE)** 해달라고 요청하는 '대화 수단'이라고 생각할 수 있습니다.

---

###  📜 SQL 기본 규칙

SQL을 작성할 때는 몇 가지 기본적인 규칙과 약속이 있습니다.

1. **세미콜론(;)으로 마무리**: 모든 SQL 문장의 끝은 세미콜론(;)으로 맺어야 합니다. 이는 명령어의 끝을 명확히 구분해주는 역할을 합니다.
    
2. **대소문자 구분**:
    
    - **SQL 키워드**: `SELECT`, `FROM`, `WHERE`와 같은 명령어는 대소문자를 구분하지 않습니다. (`SELECT`와 `select`는 동일). 하지만 **가독성을 위해 키워드는 대문자**로 작성하는 것이 일반적인 관례입니다.
        
    - **테이블/컬럼명**: 테이블과 컬럼 이름의 대소문자 구분 여부는 사용하는 **데이터베이스 종류에 따라 다릅니다.**
        
        - **MySQL**: 기본적으로 구분하지 않음
            
        - **Oracle, PostgreSQL**: 기본적으로 구분함
            
3. **주석(Comments) 작성**:
    
    - `--`: 한 줄 주석을 작성할 때 사용합니다.
        
    - `/* */`: 여러 줄에 걸쳐 주석을 작성할 때 사용합니다.
        
    
    ```SQL
    -- 이것은 한 줄 주석입니다.
    SELECT 
        employee_id, -- 직원의 ID
        first_name
    FROM employees;
    
    /*
      이것은 여러 줄 주석입니다.
      여러 줄에 걸쳐 코드에 대한 설명을 추가할 수 있습니다.
    */
    ```
    
4. **공백과 들여쓰기**:
    
    - SQL은 여러 개의 공백을 하나의 공백으로 취급합니다.
        
    - 명령문을 여러 줄에 걸쳐 작성할 수 있으며, 가독성을 높이기 위해 적절한 **들여쓰기와 줄 바꿈**을 사용하는 것이 좋습니다. 아래 세 쿼리는 모두 동일하게 동작합니다.
        
    ```SQL
    -- 가독성이 낮은 예
    SELECT * FROM employees WHERE salary > 50000;
    
    -- 가독성이 좋은 예 (추천)
    SELECT 
        * FROM 
        employees 
    WHERE 
        salary > 50000;
    ```
    

---

###  🗂️ SQL 명령어 분류

SQL 명령어는 그 기능에 따라 크게 4가지로 나눌 수 있습니다.

- **DDL (Data Definition Language, 데이터 정의어)** 데이터베이스의 구조, 즉 테이블이나 인덱스 같은 '데이터를 담는 틀'을 **정의하고 변경, 삭제**하는 명령어입니다.
    
    - `CREATE`, `ALTER`, `DROP`
        
- **DML (Data Manipulation Language, 데이터 조작어)** 데이터베이스에 저장된 실제 데이터를 **조작(입력, 수정, 삭제, 조회)**하는 명령어입니다. 가장 자주 사용됩니다.
    
    - `INSERT`, `UPDATE`, `DELETE`, `SELECT`
        
- **DCL (Data Control Language, 데이터 제어어)** 데이터베이스에 대한 **접근 권한을 제어**하고 보안을 설정하는 명령어입니다.
    
    - `GRANT`, `REVOKE`
        
- **TCL (Transaction Control Language, 트랜잭션 제어어)** 논리적인 작업 단위인 **트랜잭션(Transaction)**을 제어하는 명령어입니다.
    
    - `COMMIT`, `ROLLBACK`
        

> #### **💡 트랜잭션(Transaction)이란?**
> 
> 데이터베이스의 상태를 변화시키는 **하나의 논리적인 작업 단위**를 의미합니다. 관련된 작업들이 **'전부 성공'**하거나 **'전부 실패'**하는 것을 보장하여 데이터의 일관성을 유지합니다.
> 
> - **예시 (계좌 이체)**: A가 B에게 5만원을 송금할 때,
>     
>     1. A 계좌에서 5만원 출금 (UPDATE)
>         
>     2. B 계좌에 5만원 입금 (UPDATE)
>         
>     
>     이 두 작업은 하나의 트랜잭션으로 묶여야 합니다. 만약 1번 작업만 성공하고 시스템이 멈추면 큰 문제가 발생하기 때문입니다. 트랜잭션은 이 두 작업이 **모두 성공해야만 최종 저장(COMMIT)**하고, 하나라도 실패하면 **모두 없던 일로 되돌립니다(ROLLBACK).**


---


### DDL

#### **1단계: 데이터베이스 생성 및 선택**

게시글 데이터를 담을 `board_db`라는 데이터베이스를 생성하고, 이 공간에서 작업을 시작하겠다고 MySQL에 알려줍니다.


```sql
-- 1. board_db 데이터베이스 생성
CREATE DATABASE board_db CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci;

-- 2. 앞으로 board_db에서 모든 작업을 수행하겠다고 선언
USE board_db;
```

#### **2단계: 테이블 생성 (`CREATE TABLE`)**

게시글 정보를 담을 `post` 테이블 하나만 간단하게 만들어 보겠습니다.


```sql
-- 3. 게시글 정보를 담을 post 테이블 생성
CREATE TABLE post (
    post_id     INT             NOT NULL AUTO_INCREMENT,
    title       VARCHAR(100)    NOT NULL,
    content     TEXT,
    PRIMARY KEY (post_id)
);
```


---

### DML

#### **3단계: 데이터 추가 (`INSERT INTO`)**

`post` 테이블에 두 개의 샘플 게시글을 추가해 보겠습니다.

```sql
-- 4. post 테이블에 데이터 2건 추가
INSERT INTO post (title, content) VALUES ('첫 번째 글입니다', '안녕하세요. SQL 실습입니다.');
INSERT INTO post (title, content) VALUES ('두 번째 글', 'DDL과 DML을 배우고 있습니다.');
```

#### **4단계: 데이터 조회 (`SELECT`)**

이제 우리가 넣은 데이터를 조회하는 연습을 합니다.

```sql
-- 5. 모든 게시글의 전체 내용 조회하기
SELECT * FROM post;

-- 6. 게시글의 제목만 조회하기
SELECT title FROM post;
```

#### **5단계: 데이터 수정 (`UPDATE`)**

첫 번째 게시글의 내용을 수정해 봅시다. `WHERE` 절로 어떤 데이터를 수정할지 명확히 지정하는 것이 매우 중요합니다.

```sql
-- 7. 첫 번째 글(post_id = 1)의 내용을 수정
UPDATE post
SET content = '내용을 성공적으로 수정했습니다.'
WHERE post_id = 1;

-- (확인) 수정이 잘 되었는지 첫 번째 글만 다시 조회해 보세요.
SELECT * FROM post WHERE post_id = 1;
```

#### **6단계: 데이터 삭제 (`DELETE`)**

두 번째 게시글을 삭제해 봅시다. `DELETE` 역시 `WHERE` 절이 없으면 모든 데이터가 삭제되니 항상 주의해야 합니다.

```sql
-- 8. 두 번째 글(post_id = 2) 데이터를 삭제
DELETE FROM post WHERE post_id = 2;

-- (확인) 전체 게시글을 다시 조회해서 데이터가 삭제되었는지 확인해보세요.
SELECT * FROM post;
```