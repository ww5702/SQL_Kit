```
select MAX MIN SUM (aaaa)
을 통해서 테이블의 max min sum값을 구할 수 있다.
```
FOOD_PRODUCT 테이블에서 가격이 제일 비싼 식품의   
식품 ID, 식품 이름, 식품 코드, 식품분류, 식품 가격을 조회하는 SQL문을 작성해주세요.   
```
SELECT PRODUCT_ID, PRODUCT_NAME, PRODUCT_CD, CATEGORY, PRICE
from FOOD_PRODUCT
where PRICE = (SELECT MAX(PRICE) as PRICE FROM FOOD_PRODUCT)

where 절에서 다시 select를 이용해 해당 max(PIRCE)값만 추출해준다.
```
가장 최근에 들어온 동물을 구하자
```
SELECT MAX(DATETIME) AS 시간
from ANIMAL_INS

max값을 한다면 가장 최근에 들어온 동물을 반환할 수 있다.
min값을 이용한다면 가장 먼저 들어온 동물의 시간을 반환할 수 있다.
```
