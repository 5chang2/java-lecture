### ## 🌏 world 데이터베이스 SQL 연습 문제
> **💡 실습 준비**
>
> 모든 문제를 시작하기 전, `world` 데이터베이스를 사용하겠다고 MySQL에 알려주세요.
>
```sql
USE world;
```

---

### ### **Level 1: 기본 조회 및 필터링**

1.  `city` 테이블에서 `CountryCode`가 'KOR'인 도시들을 인구수(Population)가 많은 순서대로 정렬하여 조회하세요.
```sql
SELECT Name, Population FROM city WHERE CountryCode = 'KOR' ORDER BY Population DESC;
```

2.  `country` 테이블에서 독립 연도(IndepYear)가 없는(NULL) 국가들의 이름과 정부 형태(GovernmentForm)를 조회하세요.
```sql
SELECT Name, GovernmentForm FROM country WHERE IndepYear IS NULL;
```

3.  `countrylanguage` table에서 'Spanish' 언어를 사용하는 국가들의 국가 코드(CountryCode)를 조회하세요.
```sql
SELECT CountryCode FROM countrylanguage WHERE Language = 'Spanish';
```

4.  `country` 테이블에서 평균 수명(LifeExpectancy)이 80세 이상인 국가들의 이름과 평균 수명을 조회하고, 평균 수명이 높은 순서대로 정렬하세요.
```sql
SELECT Name, LifeExpectancy FROM country WHERE LifeExpectancy >= 80 ORDER BY LifeExpectancy DESC;
```

5.  `country` 테이블에서 이름이 'United'로 시작하는 모든 국가의 이름(Name)과 대륙(Continent)을 조회하세요.
```sql
SELECT Name, Continent FROM country WHERE Name LIKE 'United%';
```

---

### ### **Level 2: 다양한 조건 필터링 및 그룹화**

1.  `country` 테이블에서 아시아(Asia) 또는 유럽(Europe) 대륙에 속한 국가들의 이름, 대륙, 인구를 조회하세요.
```sql
SELECT Name, Continent, Population FROM country WHERE Continent IN ('Asia', 'Europe');
```

2.  `country` 테이블에서 인구가 1억명 이상이면서 정부 형태(GovernmentForm)가 'Republic'인 국가들의 이름과 인구를 조회하세요.
```sql
SELECT Name, Population FROM country WHERE Population >= 100000000 AND GovernmentForm = 'Republic';
```

3.  `city` 테이블에서 인구가 500만에서 700만 사이인 도시들의 이름과 인구수, 국가 코드를 조회하세요.
```sql
SELECT Name, Population, CountryCode FROM city WHERE Population BETWEEN 5000000 AND 7000000;
```

4.  `countrylanguage` 테이블에서 각 국가 코드(CountryCode)별로 몇 개의 언어가 사용되는지 계산하여, 국가 코드와 언어의 수를 '언어_수' 라는 별칭으로 조회하세요.
```sql
SELECT CountryCode, COUNT(*) AS '언어_수' FROM countrylanguage GROUP BY CountryCode;
```

5.  `country` 테이블에 존재하는 모든 정부 형태(GovernmentForm)를 중복 없이 조회하세요.
```sql
SELECT DISTINCT GovernmentForm FROM country;
```

---

### ### **Level 3: 고급 집계 및 결과 필터링**

1.  `country` 테이블에서 각 대륙(Continent)의 평균 수명(LifeExpectancy)을 계산하고, 그 평균 수명이 75세 이상인 대륙만 조회하세요.
```sql
SELECT Continent, AVG(LifeExpectancy) AS avg_life_expectancy
FROM country
GROUP BY Continent
HAVING avg_life_expectancy >= 75;
```

2.  `city` 테이블에서 국가 코드('KOR', 'CHN', 'JPN')에 해당하는 도시들 중, 각 국가별로 도시의 총 인구수를 계산하여 조회하세요.
```sql
SELECT CountryCode, SUM(Population) AS total_population
FROM city
WHERE CountryCode IN ('KOR', 'CHN', 'JPN')
GROUP BY CountryCode;
```

3.  `countrylanguage` 테이블에서 공식 언어(IsOfficial = 'T')가 2개 이상인 국가들의 국가 코드와 공식 언어의 수를 조회하세요.
```sql
SELECT CountryCode, COUNT(*) AS official_language_count
FROM countrylanguage
WHERE IsOfficial = 'T'
GROUP BY CountryCode
HAVING official_language_count >= 2;
```

4.  `country` 테이블에서 대륙별로 국가의 수, 총 인구, 평균 GNP를 계산하고, 국가 수가 10개 이상인 대륙만 필터링하여 총 인구가 많은 순서로 정렬하세요.
```sql
SELECT Continent, COUNT(*) AS country_count, SUM(Population) AS total_population, AVG(GNP) AS avg_gnp
FROM country
GROUP BY Continent
HAVING country_count >= 10
ORDER BY total_population DESC;
```

5.  `country` 테이블에서 인구가 10번째로 많은 국가부터 15번째로 많은 국가까지의 이름과 인구를 조회하세요.
```sql
SELECT Name, Population FROM country ORDER BY Population DESC LIMIT 6 OFFSET 9;
```


---

### ## 🎬 Sakila `film` 테이블 SQL 연습 문제

> **💡 실습 준비**
>
> 모든 문제를 시작하기 전, `sakila` 데이터베이스를 사용하겠다고 MySQL에 알려주세요.
>
> ```sql
> USE sakila;
> ```

---

### ### **Level 1: 기본 조회, 필터링, 정렬**

1.  등급(`rating`)이 'R'인 모든 영화의 제목(`title`)과 상영 시간(`length`)을 조회하세요.
```sql
SELECT title, length FROM film WHERE rating = 'R';
```

2.  상영 시간(`length`)이 3시간(180분) 이상인 영화의 제목과 상영 시간을, 상영 시간이 긴 순서대로 정렬하여 조회하세요.
```sql
SELECT title, length FROM film WHERE length >= 180 ORDER BY length DESC;
```

3.  대여료(`rental_rate`)가 가장 비싼 상위 10개의 영화 제목과 대여료를 조회하세요.
```sql
SELECT title, rental_rate FROM film ORDER BY rental_rate DESC LIMIT 10;
```

4.  영화 제목(`title`)이 'C'로 시작하는 모든 영화의 제목과 등급(`rating`)을 조회하세요.
```sql
SELECT title, rating FROM film WHERE title LIKE 'C%';
```

5.  모든 영화를 등급(`rating`) 순으로 먼저 정렬하고, 같은 등급 내에서는 제목(`title`)의 알파벳 순으로 정렬하여 조회하세요.
```sql
SELECT title, rating FROM film ORDER BY rating ASC, title ASC;
```

---

### ### **Level 2: 다양한 조건 필터링 및 기본 그룹화**

1.  등급(`rating`)이 'PG'이거나 'G'인 모든 영화의 제목과 등급을 조회하세요.
```sql
SELECT title, rating FROM film WHERE rating IN ('PG', 'G');
    ```

2.  대여 기간(`rental_duration`)은 3일인데, 교체 비용(`replacement_cost`)은 20달러 미만인 영화의 제목, 대여 기간, 교체 비용을 조회하세요.
```sql
SELECT title, rental_duration, replacement_cost FROM film WHERE rental_duration = 3 AND replacement_cost < 20;
```

3.  교체 비용(`replacement_cost`)이 10달러에서 12달러 사이인 영화의 제목과 교체 비용을 조회하세요.
```sql
SELECT title, replacement_cost FROM film WHERE replacement_cost BETWEEN 10 AND 12;
```

4.  `film` 테이블에 존재하는 모든 영화의 등급(`rating`) 종류를 중복 없이 조회하세요.
```sql
SELECT DISTINCT rating FROM film;
```

5.  각 등급(`rating`)별로 총 몇 개의 영화가 있는지 계산하여, 등급과 영화의 수를 '영화_수'라는 별칭으로 조회하세요.
```sql
SELECT rating, COUNT(*) AS '영화_수' FROM film GROUP BY rating;
```

---

### ### **Level 3: 고급 집계 및 결과 필터링**

1.  각 등급(`rating`)별 영화의 평균 상영 시간(`length`)을 계산하고, 평균 상영 시간이 120분 이상인 등급만 조회하세요.
```sql
SELECT rating, AVG(length) AS avg_length
FROM film
GROUP BY rating
HAVING avg_length >= 120;
```

2.  각 등급(`rating`)별로 영화의 최소, 최대, 평균 대여료(`rental_rate`)를 계산하여 조회하세요.
```sql
SELECT
	rating,
	MIN(rental_rate) AS min_rate,
	MAX(rental_rate) AS max_rate,
	AVG(rental_rate) AS avg_rate
FROM film
GROUP BY rating;
```

3.  특별 영상(`special_features`)에 'Trailers'가 포함된 영화들 중, 각 등급(`rating`)별로 영화가 몇 개씩 있는지 계산하세요.
```sql
SELECT rating, COUNT(*) AS count_with_trailers
FROM film
WHERE special_features LIKE '%Trailers%'
GROUP BY rating;
```

4.  대여 기간(`rental_duration`)별로 영화들의 평균 교체 비용(`replacement_cost`)을 계산하되, 평균 교체 비용이 20달러 이상인 그룹만 필터링하여 조회하세요.
```sql
SELECT rental_duration, AVG(replacement_cost) AS avg_cost
FROM film
GROUP BY rental_duration
HAVING avg_cost >= 20;
```

5.  상영 시간(`length`)을 기준으로 21번째로 긴 영화부터 30번째로 긴 영화까지 10개의 영화 제목과 상영 시간을 조회하세요.
```sql
SELECT title, length FROM film ORDER BY length DESC LIMIT 10 OFFSET 20;
```