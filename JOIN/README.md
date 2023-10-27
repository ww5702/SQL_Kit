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
