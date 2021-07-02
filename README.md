# Database
**MARIADB로 진행**
## JOIN이란
> 관계형 DB에선 중복 데이터를 피하기 위해 데이터의 속성을 분류해 여러 테이블로 나누어 놓는 '정규화' 작업을 한다. 이렇게 정규화된 데이터에서 원하는 결과를 도출하기 위해 여러 테이블을 조합할 필요성이 생기는데 이런경우 사용하는 명령어가 컬럼을 기준으로 행을 합쳐 가상의 테이블 처럼 만들어 결과를 보여주는 연산인 **JOIN** 이다.  
**조인의 대표적 종류**
 1) INNER JOIN
 2) OUTER JOIN
 3) SELF JOIN
 4) CROSS JOIN
 <img src = "https://t1.daumcdn.net/cfile/tistory/99473C435C0D1ECD07"/>
 
 ### 1. INNER JOIN(내부 조인)
 > INNER JOIN은 키 값이 있는 두 테이블의 컬럼 값을 비교한후 조건에 맞는 값만을 가져오고 나머지는 버린다. 간단하게 말해 조건에 맞는 값들만 검색하는 조인 방식이다.
 <img src="https://t1.daumcdn.net/cfile/tistory/251A374456EB994D13"/>
 
 * SQL은 명시적 조인표현과 암시적 조인 표현으로 구분을 지정한다.
   1) 명시적 조인 표현
   > 테이블에 조인하라는 것을 지정하기 위해 'JOIN' 명령을 사용하고 ON의 키워드를 사용해 조인에 대한 조건을 걸어준다.
   ```
   select * from people as p inner join people_filmo as pf on p.peopleCd = pf.peopleCd
   // people은 영화 관련 인물들 테이블, people_filmo는 인물들과 관련되 영화에 대한 테이블(=movie와 people의 N:M관계에서 나온 테이블)
   ```
   2) 암시적 조인 표현
   > select구문의 from절에서 , 를 사용하여 단순히 조인을 위한 여러 테이블을 나열하면된다. 
   ```
   select * from people as p, people_filmo as pf where p.peopleCd = pf.peopleCd
   ```
  ### 2. CROSS JOIN(교차 조인)
  > CROSS JOIN은 카디션 곱 이라고도 하며 조인되는 두 테이블에서 곱집합을 반환한다... 즉 m열을 가진 테이블과 n열을 가진 테이블이 교차조인되면 m * n개의 열이 생성된다.
  => people 테이블에 '이병헌','황정민' 이있고 movie 테이블에 '국제시장','남산의 부장들' 이있다. 이병헌은 남산, 황정민은 국제시장만 연관되어있다. 이상황에서 교차 조인시 이병헌 | 국제시장,  이병헌 | 남산의 부장들 , 황정민 | 국제시장, 황정민 | 남산의 부장들  이렇게 조인이 된다 
  
  ### 3. OUTER JOIN(외부 조인)
  > Outer join 은 조인하는 여러 테이블에서 한쪽에는 데이터가 있고 한쪽에는 데이터가 없는 경우 데이터가 있는쪽 테이블의 내용을 전부 출력하는 방식이다. 즉 조인 조건에 만족하지않아도 해당 행을 출력하고 싶은 경우 사용할수 있다.
  * outer join에는 left,right,full outer join이 있다.
   #### 3-1 LEFT OUTER JOIN
   > LEFT OUTER JOIN은 조인문의 왼쪽에 있는 테이블의 모든 결과를 가져온후 오른쪽 테이블의 데이터를 매칭하고, 매칭되는 데이터가 없는 경우 NULL을 표기해준다.
   <img src="https://t1.daumcdn.net/cfile/tistory/224EFA4656EF49B309"/>
   ```
   select * from people as p left (outer 생략가능) join people_filmo as pf on p.peopleCd = pf.peopleCd;
   //people 테이블에서 활동내역이 없으면 filmo테이블에 없지만 left join시 활동내역없는 people데이터도 출력되며 filmo와 관련된 컬럼에는 null로 출력되게 된다.
   ```
   #### 3-2 RIGHT OUTER JOIN
   > RIGHT OUTER JOIN은 조인문의 오른쪽에 있는 테이블의 모든 결과를 가져온후 왼쪽 테이블의 데이터를 매칭하고, 매칭되는 데이터가 없는 경우 NULL을 표기해준다.
   <img src="https://t1.daumcdn.net/cfile/tistory/2418A25056EF4BA912"/>
   ```
   select * from people as p right (outer 생략가능) join people_filmo as pf on p.peopleCd = pf.peopleCd;
   //people 테이블에서 활동내역이 없으면 filmo테이블에 없지만 right join시 people이 없는 people_filmo데이터도 출력되며 people와 관련된 컬럼에는 null로 출력되게 된다.(이건 테이블 구조상 예시가 조금 이상하긴 하지만 이해를 위한 예제이기에 감안했다.)
   ```
   #### 3-3 FULL OUTER JOIN
   > FULL OUTER JOIN은 LEFT OUTER JOIN과 RIGHT OUTER JOIN을 합친 것이다. mysql의 경우 Full outer join을 지원하지 않아 다른 방식으로 구현한다.(대표적 UNION 함수)
   <img src="https://t1.daumcdn.net/cfile/tistory/232EF54356EF4DA123"/>
   ```
   select * from people as p right (outer 생략가능) join people_filmo as pf on p.peopleCd = pf.peopleCd union select * from people as p left join people_filmo as pf on p.peopleCd = pf.peopleCd ;
   //연관없는 양쪽 테이블의 데이터들도 모두 가져온다.
   ```
 ### 4. SELF JOIN 
 > self join은 테이블에서 자기자신을 조인시키는 것이다.
 ```
 select * from people as p join people as sp on p.peopleCd = sp.peopleCd
 ```
