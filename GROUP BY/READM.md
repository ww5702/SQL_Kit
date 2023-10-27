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
