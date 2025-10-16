# 3장 SQL 기초 - 샘플 데이터베이스 안내

이 장의 실습에서는 MySQL 공식 샘플 데이터베이스를 사용합니다.

---

## 사용하는 샘플 데이터베이스

### 1. world 데이터베이스

**설명**: 세계 각국의 정보를 담은 간단한 데이터베이스

**테이블 구조**:
- `city`: 도시 정보 (4,079개 행)
- `country`: 국가 정보 (239개 행)
- `countrylanguage`: 국가별 언어 정보 (984개 행)

**주요 컬럼**:
```sql
-- country 테이블
Code         -- 국가 코드 (PK)
Name         -- 국가명
Continent    -- 대륙
Region       -- 지역
Population   -- 인구
LifeExpectancy -- 평균 수명
GNP          -- 국민총생산

-- city 테이블
ID           -- 도시 ID (PK)
Name         -- 도시명
CountryCode  -- 국가 코드 (FK)
District     -- 지역
Population   -- 인구
```

**사용 섹션**: 3.1, 3.2, 3.3, 3.5

---

### 2. sakila 데이터베이스

**설명**: DVD 대여점 비즈니스 모델을 나타내는 복잡한 데이터베이스

**주요 테이블**:
- `film`: 영화 정보 (1,000개 행)
- `actor`: 배우 정보 (200개 행)
- `category`: 카테고리 정보 (16개 행)
- `customer`: 고객 정보 (599개 행)
- `rental`: 대여 기록 (16,044개 행)
- `payment`: 결제 기록 (16,049개 행)
- `inventory`: 재고 정보 (4,581개 행)

**주요 컬럼**:
```sql
-- film 테이블
film_id           -- 영화 ID (PK)
title             -- 영화 제목
description       -- 설명
release_year      -- 개봉 연도
rental_rate       -- 대여 가격
length            -- 상영 시간 (분)
rating            -- 등급 (G, PG, PG-13, R, NC-17)

-- rental 테이블
rental_id         -- 대여 ID (PK)
rental_date       -- 대여일
inventory_id      -- 재고 ID (FK)
customer_id       -- 고객 ID (FK)
return_date       -- 반납일
```

**사용 섹션**: 3.4, 3.5, 3.6

---

## 샘플 데이터베이스 설치 방법

### 방법 1: MySQL Workbench 사용 (권장)

1. MySQL Workbench 실행
2. 메뉴: `File` → `Run SQL Script`
3. 스크립트 파일 선택:
   - world: `world.sql`
   - sakila: `sakila-schema.sql` → `sakila-data.sql` 순서대로
4. 실행

### 방법 2: 명령줄 사용

```bash
# world 데이터베이스
mysql -u root -p < world.sql

# sakila 데이터베이스
mysql -u root -p < sakila-schema.sql
mysql -u root -p < sakila-data.sql
```

### 방법 3: MySQL 서버에 직접 다운로드

**world**:
```bash
# Linux/Mac
wget https://downloads.mysql.com/docs/world-db.tar.gz
tar -xzf world-db.tar.gz
mysql -u root -p < world-db/world.sql

# Windows
# 웹 브라우저로 다운로드 후 압축 해제하여 사용
```

**sakila**:
```bash
# Linux/Mac
wget https://downloads.mysql.com/docs/sakila-db.tar.gz
tar -xzf sakila-db.tar.gz
mysql -u root -p < sakila-db/sakila-schema.sql
mysql -u root -p < sakila-db/sakila-data.sql
```

---

## 설치 확인

### world 데이터베이스 확인

```sql
USE world;

-- 테이블 목록 확인
SHOW TABLES;

-- 데이터 확인
SELECT COUNT(*) FROM country;  -- 239개
SELECT COUNT(*) FROM city;     -- 4079개

-- 샘플 데이터
SELECT * FROM country LIMIT 5;
```

### sakila 데이터베이스 확인

```sql
USE sakila;

-- 테이블 목록 확인
SHOW TABLES;

-- 데이터 확인
SELECT COUNT(*) FROM film;     -- 1000개
SELECT COUNT(*) FROM actor;    -- 200개

-- 샘플 데이터
SELECT * FROM film LIMIT 5;
```

---

## 자주 사용하는 쿼리

### world 데이터베이스

```sql
-- 대한민국 정보
SELECT * FROM country WHERE Name = 'South Korea';

-- 인구 상위 10개 도시
SELECT Name, Population
FROM city
ORDER BY Population DESC
LIMIT 10;

-- 아시아 국가 수
SELECT COUNT(*)
FROM country
WHERE Continent = 'Asia';
```

### sakila 데이터베이스

```sql
-- 등급별 영화 수
SELECT rating, COUNT(*)
FROM film
GROUP BY rating;

-- 가장 비싼 대여 가격
SELECT title, rental_rate
FROM film
ORDER BY rental_rate DESC
LIMIT 10;

-- 2005년 5월 대여 건수
SELECT COUNT(*)
FROM rental
WHERE rental_date BETWEEN '2005-05-01' AND '2005-05-31';
```

---

## 각 섹션별 사용 DB

| 섹션 | 데이터베이스 | 설명 |
|------|--------------|------|
| 3.1 SELECT 기본 | world | 간단한 조회 연습 |
| 3.2 WHERE 절 | world | 조건 필터링 연습 |
| 3.3 정렬과 제한 | world | 정렬 및 페이지네이션 |
| 3.4 INSERT/UPDATE/DELETE | sakila | 데이터 조작 연습 |
| 3.5 기본 함수 | world, sakila | 집계 및 함수 연습 |
| 3.6 실습 프로젝트 | sakila | 종합 실습 |

---

## 참고 자료

- [MySQL Sample Databases 공식 문서](https://dev.mysql.com/doc/index-other.html)
- [world 데이터베이스 다운로드](https://downloads.mysql.com/docs/world-db.tar.gz)
- [sakila 데이터베이스 다운로드](https://downloads.mysql.com/docs/sakila-db.tar.gz)
- [sakila 데이터베이스 구조 설명](https://dev.mysql.com/doc/sakila/en/)

---

## 문제 해결

### 1. 샘플 데이터베이스가 없다고 나올 때

```sql
-- 현재 데이터베이스 목록 확인
SHOW DATABASES;

-- world나 sakila가 없으면 설치 필요
```

### 2. 한글이 깨질 때

```sql
-- 데이터베이스 문자셋 확인
SHOW VARIABLES LIKE 'character%';

-- UTF-8로 설정
SET NAMES utf8mb4;
```

### 3. 권한 오류가 날 때

```sql
-- 현재 사용자 권한 확인
SHOW GRANTS;

-- root 계정으로 실행하거나, 관리자에게 권한 요청
```

---

## 실습 준비 체크리스트

- [ ] MySQL 서버 설치 완료
- [ ] MySQL Workbench 또는 CLI 접속 가능
- [ ] world 데이터베이스 설치 완료
- [ ] sakila 데이터베이스 설치 완료
- [ ] 샘플 쿼리 실행하여 데이터 확인

준비가 완료되었으면 3.1부터 실습을 시작하세요!
