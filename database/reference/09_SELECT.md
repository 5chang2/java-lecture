

> **💡 실습 준비**
>
> 실습을 시작하기 전, `world` 데이터베이스를 사용하겠다고 MySQL에 알려주세요.


```sql
USE world;
 ```

---

### ### 1. `WHERE`: 조건에 맞는 데이터만 골라내기

`WHERE` 절은 `SELECT` 문에서 가장 기본적이면서도 강력한 필터링 도구입니다. 테이블의 전체 데이터 중 특정 조건을 만족하는 행(row)만 선택하여 가져옵니다.

* **비교 연산자**: `=` (같다), `!=` 또는 `<>` (다르다), `>` (크다), `<` (작다), `>=` (크거나 같다), `<=` (작거나 같다)
    ```sql
    -- 대한민국(South Korea)의 정보를 조회
    SELECT * FROM country WHERE Name = 'South Korea';

    -- 인구가 1억명 이상인 국가들을 조회
    SELECT Name, Population FROM country WHERE Population >= 100000000;
    ```

* **논리 연산자**: `AND`, `OR`, `NOT`
    여러 조건을 조합하여 더 상세한 필터링이 가능합니다.
    ```sql
    -- 아시아(Asia) 대륙에 속하면서, 인구가 5천만명 이상인 국가를 조회
    SELECT Name, Continent, Population FROM country WHERE Continent = 'Asia' AND Population >= 50000000;
    ```

* **기타 유용한 연산자**:
    * **`LIKE`**: 문자열의 일부가 일치하는 데이터를 찾습니다. (`%`는 여러 글자, `_`는 한 글자를 의미)
    * **`IN (...)`**: 괄호 안의 목록에 포함된 값과 일치하는 데이터를 찾습니다.
    * **`BETWEEN a AND b`**: a와 b 사이의 범위에 있는 데이터를 찾습니다. (a, b 포함)

    ```sql
    -- 이름이 'Ko'로 시작하는 국가를 조회
    SELECT Name FROM country WHERE Name LIKE 'Ko%';

    -- 대한민국, 일본, 중국의 정보를 조회
    SELECT * FROM country WHERE Name IN ('South Korea', 'Japan', 'China');

    -- 평균 수명(LifeExpectancy)이 80세에서 82세 사이인 국가를 조회
    SELECT Name, LifeExpectancy FROM country WHERE LifeExpectancy BETWEEN 80 AND 82;
    ```

---

### ### 2. `DISTINCT`와 `AS`: 결과 가공하기

* **`DISTINCT`**: 조회 결과에서 **중복된 행을 제거**하고 고유한 값만 보여줍니다.
    ```sql
    -- world 데이터베이스에 있는 대륙(Continent)의 종류를 중복 없이 조회
    SELECT DISTINCT Continent FROM country;
    ```

* **`AS` (Alias)**: 컬럼이나 테이블의 이름을 **별칭**으로 바꿔서 보여줍니다. 결과 화면을 더 명확하게 만들거나, 복잡한 쿼리에서 테이블 이름을 간소화할 때 사용합니다.
    ```sql
    -- country 테이블의 Name을 '국가명', Population을 '인구'라는 별칭으로 조회
    SELECT Name AS '국가명', Population AS '인구' FROM country;
    ```

---

### ### 3. `ORDER BY`: 결과 정렬하기

`ORDER BY` 절은 조회된 결과를 특정 컬럼의 값을 기준으로 정렬합니다.

* **`ASC` (Ascending)**: 오름차순 (기본값, 생략 가능)
* **`DESC` (Descending)**: 내림차순

```sql
-- 국가 면적(SurfaceArea)이 넓은 순서대로 정렬하여 조회
SELECT Name, SurfaceArea FROM country ORDER BY SurfaceArea DESC;

-- 대륙(Continent) 순으로 먼저 정렬하고, 같은 대륙 내에서는 인구 순으로 정렬
SELECT Name, Continent, Population FROM country ORDER BY Continent ASC, Population DESC;
````

---

### ### 4. `GROUP BY`와 집계 함수: 그룹별로 통계내기 📊

`GROUP BY` 절은 특정 컬럼의 값이 같은 행들을 하나의 그룹으로 묶어주는 역할을 합니다. 주로 **집계 함수**와 함께 사용되어 그룹별 통계를 낼 때 강력한 힘을 발휘합니다.

- **주요 집계 함수(Aggregate Functions)**:
    
    - `COUNT()`: 그룹의 행 개수
        
    - `SUM()`: 그룹의 합계
        
    - `AVG()`: 그룹의 평균
        
    - `MAX()` / `MIN()`: 그룹의 최댓값 / 최솟값
        



```SQL
-- 각 대륙별로 몇 개의 나라가 있는지 조회
SELECT Continent, COUNT(*) AS '국가_수'
FROM country
GROUP BY Continent;

-- 각 대륙의 총 인구수(SUM)와 평균 인구수(AVG)를 조회
SELECT Continent, SUM(Population) AS '대륙별_총인구', AVG(Population) AS '대륙별_평균인구'
FROM country
GROUP BY Continent;
```

---

### ### 5. `HAVING`: 그룹에 대한 조건 설정하기

`HAVING` 절은 `GROUP BY`로 만들어진 그룹에 대한 조건을 설정하는 필터입니다.

> **💡 `WHERE` vs `HAVING`**
> 
> - **`WHERE`**: 그룹화하기 **전**의 원본 데이터에 대한 필터링
>     
> - **`HAVING`**: 그룹화한 **후**의 결과 데이터(주로 집계 함수 결과)에 대한 필터링
>     



```SQL
-- 대륙에 속한 국가가 10개 이상인 대륙만 조회
SELECT Continent, COUNT(*) AS number_of_countries
FROM country
GROUP BY Continent
HAVING number_of_countries >= 10;
```

---

### ### 6. `LIMIT`와 `OFFSET`: 페이지네이션 구현하기 📖

`LIMIT`와 `OFFSET`은 대량의 데이터를 나눠서 보여주는, 즉 **페이지네이션**을 구현할 때 필수적인 기능입니다.

- **`LIMIT`**: 조회할 결과의 **최대 개수**를 제한합니다.
    
- **`OFFSET`**: 몇 번째 행부터 결과를 가져올지 **시작점**을 지정합니다. (0부터 시작)
    



```SQL
-- 인구가 가장 많은 상위 5개 국가를 조회 (1페이지)
SELECT Name, Population FROM country ORDER BY Population DESC LIMIT 5;

-- 인구가 6번째부터 10번째로 많은 5개 국가를 조회 (2페이지)
SELECT Name, Population FROM country ORDER BY Population DESC LIMIT 5 OFFSET 5;
```

> **쿼리 실행 순서 요약**
> 
> SQL은 우리가 작성한 순서가 아닌, 정해진 내부 규칙에 따라 실행됩니다.
> 
> FROM → WHERE → GROUP BY → HAVING → SELECT → ORDER BY → LIMIT