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
