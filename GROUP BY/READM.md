USED_GOODS_BOARD와 USED_GOODS_USER 테이블에서   
완료된 중고 거래의 총금액이 70만 원 이상인 사람의   
회원 ID, 닉네임, 총거래금액을 조회하는 SQL문을 작성해주세요.   
결과는 총거래금액을 기준으로 오름차순 정렬해주세요.
```
SELECT B.USER_ID, B.NICKNAME, SUM(PRICE) AS TOTAL_SALES
from USED_GOODS_BOARD as A 
JOIN USED_GOODS_USER AS B ON A.WRITER_ID = B.USER_ID
WHERE STATUS = 'DONE'
GROUP BY A.WRITER_ID
HAVING TOTAL_SALES >= 700000
order by TOTAL_SALES
```
REST_INFO 테이블에서 음식종류별로 즐겨찾기수가   
가장 많은 식당의 음식 종류, ID, 식당 이름, 즐겨찾기수를   
조회하는 SQL문을 작성해주세요.   
이때 결과는 음식 종류를 기준으로 내림차순 정렬해주세요.   
```
SELECT FOOD_TYPE, REST_ID, REST_NAME, FAVORITES
from REST_INFO
where (FOOD_TYPE, FAVORITES)
IN (SELECT FOOD_TYPE, MAX(FAVORITES) FROM REST_INFO GROUP BY FOOD_TYPE)
order by FOOD_TYPE DESC

먼저 where 안에 각각의 음식 종류와 즐겨찾기가 가장 많은 음식점을 골라준다
그리고 그 데이터와 일치하는 식당만 추려서 조회한다.
```
2022년 1월의 도서 판매 데이터를 기준으로 저자 별,   
카테고리 별 매출액 (TOTAL_SALES = 판매량 * 판매가) 을 구하여,   
저자 ID, 저자명, 카테고리, 매출액 리스트를 출력하는 SQL문을 작성해주세요.   
결과는 저자 ID를 오름차순으로, 저자 ID가 같다면 카테고리를 내림차순 정렬해주세요.   
```
SELECT A.AUTHOR_ID, AUTHOR_NAME, CATEGORY, SUM((SALES * PRICE)) AS TOTAL_SALES
FROM BOOK_SALES as s
JOIN BOOK B on S.BOOK_ID = B.BOOK_ID
JOIN AUTHOR A ON B.AUTHOR_ID = A.AUTHOR_ID
where YEAR(S.SALES_DATE) = 2022 AND MONTH(S.SALES_DATE) = 01
group by CATEGORY, AUTHOR_ID
order by AUTHOR_ID, CATEGORY DESC

BOOK_SALES에 BOOK, AUTHOR 테이블을 통합시켜주고
SALES_DATE의 값을 선별해준다.

```
CAR_RENTAL_COMPANY_CAR 테이블에서 '통풍시트','열선시트','가죽시트'   
중 하나 이상의 옵션이 포함된 자동차가 자동차 종류 별로 몇 대인지   
출력하는 SQL문을 작성해주세요.   
이때 자동차 수에 대한 컬럼명은 CARS로 지정하고,   
결과는 자동차 종류를 기준으로 오름차순 정렬해주세요.   
```
SELECT CAR_TYPE, COUNT(CAR_TYPE) AS CARS
from CAR_RENTAL_COMPANY_CAR
where OPTIONS LIKE '%통풍시트%' OR 
OPTIONS LIKE '%열선시트%' OR 
OPTIONS LIKE '%가죽시트%'
group by CAR_TYPE
order by CAR_TYPE

```

