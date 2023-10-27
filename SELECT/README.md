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



