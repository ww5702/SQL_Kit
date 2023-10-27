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
