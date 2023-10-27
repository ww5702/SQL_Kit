7월 아이스크림 총 주문량과 상반기의 아이스크림 총 주문량을 더한 값이 큰 순서대로   
상위 3개의 맛을 조회하는 SQL 문을 작성해주세요.   
```
SELECT F.FLAVOR
from FIRST_HALF as F
join JULY as J on F.FLAVOR = J.FLAVOR
GROUP BY F.FLAVOR
order by (SUM(F.TOTAL_ORDER) + SUM(J.TOTAL_ORDER)) DESC
LIMIT 3;

join을 해주고
3개만 출력해줘야 하기에 limit 3을 건다   
```
자동차 종류가 '세단' 또는 'SUV' 인 자동차 중   
2022년 11월 1일부터 2022년 11월 30일까지 대여 가능하고   
30일간의 대여 금액이 50만원 이상 200만원 미만인 자동차에 대해서   
자동차 ID, 자동차 종류, 대여 금액(컬럼명: FEE) 리스트를 출력하는   
SQL문을 작성해주세요.   
결과는 대여 금액을 기준으로 내림차순 정렬하고,   
대여 금액이 같은 경우 자동차 종류를 기준으로 오름차순 정렬,   
자동차 종류까지 같은 경우 자동차 ID를 기준으로 내림차순 정렬해주세요.   
```
SELECT A.CAR_ID, A.CAR_TYPE, ROUND(A.DAILY_FEE*30*(100-D.DISCOUNT_RATE)/100) AS FEE
from CAR_RENTAL_COMPANY_CAR as A
join CAR_RENTAL_COMPANY_RENTAL_HISTORY as H
on H.CAR_ID = A.CAR_ID
join CAR_RENTAL_COMPANY_DISCOUNT_PLAN as D
on D.CAR_TYPE = A.CAR_TYPE
where A.CAR_ID NOT IN (
    SELECT CAR_ID
    FROM CAR_RENTAL_COMPANY_RENTAL_HISTORY
    WHERE END_DATE > '2022-11-01' AND START_DATE < '2022-12-01') AND D.DURATION_TYPE = '30일 이상'
group by A.CAR_ID
having A.CAR_TYPE IN ('세단', 'SUV') AND (FEE >= 500000 AND FEE < 2000000)
order by FEE DESC, CAR_TYPE, CAR_ID DESC

조건들을 하나씩 하나씩 비교하면서 정렬하면 된다
```
'경제' 카테고리에 속하는 도서들의 도서 ID(BOOK_ID), 저자명(AUTHOR_NAME), 출판일(PUBLISHED_DATE)   
리스트를 출력하는 SQL문을 작성해주세요.   
결과는 출판일을 기준으로 오름차순 정렬해주세요.   
```
SELECT B.BOOK_ID, A.AUTHOR_NAME, DATE_FORMAT(B.PUBLISHED_DATE, '%Y-%m-%d') AS PUBLISHED_DATE
FROM BOOK B
JOIN AUTHOR A ON B.AUTHOR_ID = A.AUTHOR_ID
WHERE CATEGORY = '경제'
ORDER BY PUBLISHED_DATE

원하는 날짜 format을 지정해줄 수도 있다.   
```
FOOD_PRODUCT와 FOOD_ORDER 테이블에서 생산일자가   
2022년 5월인 식품들의 식품 ID, 식품 이름, 총매출을 조회하는 SQL문을 작성해주세요.   
이때 결과는 총매출을 기준으로 내림차순 정렬해주시고 총매출이 같다면 식품 ID를 기준으로 오름차순 정렬해주세요.   
```
SELECT O.PRODUCT_ID, P.PRODUCT_NAME, SUM(PRICE * AMOUNT) AS TOTAL_SALES
from FOOD_PRODUCT AS P
join FOOD_ORDER AS O on P.PRODUCT_ID = O.PRODUCT_ID
where O.PRODUCE_DATE like '2022-05%'
group by P.PRODUCT_ID
order by TOTAL_SALES DESC, P.PRODUCT_ID
```
MEMBER_PROFILE와 REST_REVIEW 테이블에서 리뷰를 가장 많이 작성한   
회원의 리뷰들을 조회하는 SQL문을 작성해주세요.   
회원 이름, 리뷰 텍스트, 리뷰 작성일이 출력되도록 작성해주시고,   
결과는 리뷰 작성일을 기준으로 오름차순,   
리뷰 작성일이 같다면 리뷰 텍스트를 기준으로 오름차순 정렬해주세요.   
```
SELECT P.MEMBER_NAME, R.REVIEW_TEXT, DATE_FORMAT(R.REVIEW_DATE, '%Y-%m-%d') AS REVIEW_DATE
from MEMBER_PROFILE AS P
join REST_REVIEW AS R on P.MEMBER_ID = R.MEMBER_ID
where P.MEMBER_ID = (SELECT MEMBER_ID
                    FROM REST_REVIEW
                    GROUP BY MEMBER_ID
                    ORDER BY COUNT(MEMBER_ID) DESC 
                    LIMIT 1)
order by R.REVIEW_DATE, R.REVIEW_TEXT

똑같지만 where MEMBERID가 제일 많은 ID를 골라야 하니 해당 부분만
따로 SELECT를 이용해 count를 사용하여 하나의 아이디를 반환해준다,
```
천재지변으로 인해 일부 데이터가 유실되었습니다.   
입양을 간 기록은 있는데, 보호소에 들어온 기록이 없는   
동물의 ID와 이름을 ID 순으로 조회하는 SQL문을 작성해주세요.   
```
SELECT O.ANIMAL_ID, O.NAME
from ANIMAL_OUTS as O
left join ANIMAL_INS as I on I.ANIMAL_ID = O.ANIMAL_ID 
where I.ANIMAL_ID is NULL
order by O.ANIMAL_ID

한쪽에는 없는 기록을 찾는거라 left join을 사용하였다.
```

```
where I.DATETIME > O.DATETIME
같은 형식의 날짜라면 이렇게 비교도 가능
```
