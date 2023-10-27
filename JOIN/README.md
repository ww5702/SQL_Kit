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
