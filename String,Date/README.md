USED_GOODS_BOARD 테이블에서 2022년 10월 5일에 등록된   
중고거래 게시물의 게시글 ID, 작성자 ID, 게시글 제목, 가격, 거래상태를   
조회하는 SQL문을 작성해주세요.   
거래상태가 SALE 이면 판매중, RESERVED이면 예약중,  
DONE이면 거래완료 분류하여 출력해주시고,   
결과는 게시글 ID를 기준으로 내림차순 정렬해주세요.   
```
SELECT BOARD_ID, WRITER_ID, TITLE, PRICE, CASE
WHEN STATUS = 'SALE' THEN '판매중'
WHEN STATUS = 'RESERVED' THEN '예약중'
WHEN STATUS = 'DONE' THEN '거래완료'
END AS STATUS
from USED_GOODS_BOARD
where CREATED_DATE LIKE '2022-10-05'
order by BOARD_ID DESC

when a = '22' then 'aa' 와같이 if문 사용가능
end 를 무조건 붙여야한다.
```
CAR_RENTAL_COMPANY_RENTAL_HISTORY 테이블에서   
대여 시작일이 2022년 9월에 속하는 대여 기록에 대해서   
대여 기간이 30일 이상이면 '장기 대여' 그렇지 않으면 '단기 대여' 로   
표시하는 컬럼(컬럼명: RENT_TYPE)을 추가하여   
대여기록을 출력하는 SQL문을 작성해주세요.   
결과는 대여 기록 ID를 기준으로 내림차순 정렬해주세요.

```
SELECT HISTORY_ID,CAR_ID,DATE_FORMAT(START_DATE,'%Y-%m-%d'),DATE_FORMAT(END_DATE,'%Y-%m-%d'), CASE
WHEN DATEDIFF(END_DATE,START_DATE) < 29 then '단기 대여'
ELSE '장기 대여'
END AS RENT_TYPE
from CAR_RENTAL_COMPANY_RENTAL_HISTORY
where START_DATE LIKE '2022-09%'
order by HISTORY_ID DESC

DATEDFFF(a,b)를 통해서 비교할 수 있다.
```
