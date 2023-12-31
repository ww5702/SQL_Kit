PATIENT 테이블에서 12세 이하인 여자 환자의 이름, 번호, 성별, 나이, 전화번호를 조회   
이때 전화번호가 없는 경우, 'NONE'으로 출력시켜주고,   
나이를 기준으로 내림차순, 같다면 이름을 기준으로 정렬   
```
SELECT 이름, 번호, 성별, 나이, ifnull(전화번호, 'NONE') as 전화번호
from PATINET
where (나이 <= 12) and (성별 = 'W')
order by 나이 DESC, 이름

ifnull을 통해 'NONE'을 사용할 수 있고
as를 통해 테이블의 이름을 정해줄 수 있다.
```
CAR 테이블에서 자동차 종류가 'SUV'인 자동차들의   
평균 일일 대여 요금을 출력하는 SQL문을 작성해주세요.   
이때 평균 일일 대여 요금은 소수 첫 번째 자리에서 반올림하고,   
컬럼명은 AVERAGE_FEE 로 지정해주세요.   
```
SELECT ROUND(AVG(평균일일대여요금) AS AVERAGE_FEE
from CAR
where CAR_TYPE = 'SUV'

AVG를 통해 평균값을 구해줄 수 있고
ROUND를 통해 소수 첫번째 자리에서 반올림할 수 있다.
```
BOOK 테이블에서 2021년에 출판된 '인문' 카테고리에 속하는   
도서 리스트를 찾아서 도서 ID(BOOK_ID),   
출판일 (PUBLISHED_DATE)을 출력하는 SQL문을 작성해주세요.   
결과는 출판일을 기준으로 오름차순 정렬해주세요.   
```
SELECT BOOK_ID, DATE_FORMAT(PUBLISHED_DATE, '%Y-%m-%d') AS PUBLISHED_DATE
from BOOK
where CATEGORY = '인문' AND YEAR(PUBLISHED_DATE) = '2021'
order by PUBLISHED_DATE ASC

DATE_FORMAT을 이용해 %Y-%m-%d을 사용해 년 월 일을 나눌수 있다.
YEAR, MONTH, DAY로 불러올수있다.   
```
전화번호가 NULL인 경우에는 출력대상에서 제외시켜달라
```
where TLNO is NOT NULL
```
상반기 아이스크림 총주문량이 3,000보다 높으면서   
아이스크림의 주 성분이 과일인 아이스크림의 맛을 총주문량이   
큰 순서대로 조회하는 SQL 문을 작성해주세요.   
```
SELECT a.FLAVOR
from FIRST_HALF AS a
LEFT JOIN ICECREAM_INFO AS b
ON a.FLAVOR = b.FLAVOR
where a.TOTAL_ORDER > 3000 and b.INGREDIENT_TYPE = 'fruit_based'
order by a.TOTAL_ORDER DESC

두개의 테이블이 나오게 됨으로 테이블을 합쳐줘야 하기에
left join   on 을 이용해 합쳐준다.

```
USED_GOODS_BOARD와 USED_GOODS_REPLY 테이블에서   
2022년 10월에 작성된 게시글 제목, 게시글 ID, 댓글 ID,   
댓글 작성자 ID, 댓글 내용, 댓글 작성일을 조회하는 SQL문을 작성해주세요.   
결과는 댓글 작성일을 기준으로 오름차순 정렬해주시고,   
댓글 작성일이 같다면 게시글 제목을 기준으로 오름차순 정렬해주세요.
```
SELECT B.TITLE, B.BOARD_ID, R.REPLY_ID, R.WRITER_ID, R.CONTENTS, 
DATE_FORMAT(R.CREATED_DATE,"%Y-%m-%d") AS CREATED_DATE
FROM USED_GOODS_BOARD AS B  
INNER JOIN USED_GOODS_REPLY AS R 
ON B.BOARD_ID = R.BOARD_ID
WHERE DATE_FORMAT(B.CREATED_DATE, '%Y-%m') = '2022-10'
ORDER BY R.CREATED_DATE ASC,  B.TITLE ASC;

INNERJOIN을 이용해 완전한 교집합을 구한다
R.CREATED_DATE를 포맷시켜 오름차순으로 정렬할 수 있도록 한다

```
REST_INFO와 REST_REVIEW 테이블에서 서울에 위치한 식당들의   
식당 ID, 식당 이름, 음식 종류, 즐겨찾기수, 주소, 리뷰 평균 점수를 조회하는   
SQL문을 작성해주세요.   
이때 리뷰 평균점수는 소수점 세 번째 자리에서 반올림 해주시고   
결과는 평균점수를 기준으로 내림차순 정렬해주시고,   
평균점수가 같다면 즐겨찾기수를 기준으로 내림차순 정렬해주세요.
```
SELECT R.REST_ID, I.REST_NAME, I.FOOD_TYPE, I.FAVORITES, I.ADDRESS, ROUND(AVG(R.REVIEW_SCORE),2) AS SCORE
from REST_REVIEW as R
INNER JOIN REST_INFO AS I ON R.REST_ID = I.REST_ID
GROUP BY R.REST_ID
HAVING I.ADDRESS LIKE '서울%'
order by SCORE DESC, I.FAVORITES DESC


```
