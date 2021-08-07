# Database
**MARIADB로 진행**
## DATABASE란
> DATABASE는 어느 한 조직의 여러 응용시스템 들이 공용할 수 있도록 통합되고 저장된 운영 데이터의 집합을 말하며 자료의 집중화를 통해서 중복된 자료를 최소화 시켜 다양한 응용분야를 효과적으로 컴퓨터에서 지원할 수 있도록 체계적으로 구성되 자료의 집합이다.
## DATABASE의 특성
 1) 실시간 접근성 : 수시적이고 비정형적인 질의에 대하여 실시간 처리로 응답할 수 있다.
 2) 지속적 변화 : 새로운데이터의 삽입, 삭제, 갱신을 통해 현재의 정확한 자료를 유지하면서 변화한다.
 3) 동시 공용 : 다수의 사용자가 동시에 원하는 데이터베이스에 접근하여 이용할 수 있다.
 4) 내용에 의한 참조 : 데이터 참조는 데이터베이스에 저장된 레코드들의 위치나 주소에 의해서가 아니라 사용자가 요구하는 데이터의 내용 즉 값에따라 참조된다.
## 데이터 '무결성'과 '일관성'
* 무결성 : 무결성은 정밀성,정확성과 일맥상통하다. DB에 저장된 데이터값과 그것이 표현하는 현실 세계의 실제값이 일치하는 정확성을 의미한다. 
ex ) 

| 전화번호 1 | 전화번호2 | 전화번호3 |
|---|:---:|---| 
| 010-1111-1111 | 010-1111-1111 | 010-1111-1111 |

전화번호1,2,3 이렇게 똑같은 번호가 저장되어있고 같은 사람이 사용하는 번호이다. 그런데 기존에 사용하던 번호를 바꾸게 되어 전화번호도 010-2222-2222로 변경했다

| 전화번호 1 | 전화번호2 | 전화번호3 |
|---|:---:|---| 
| 010-2222-2222 | 010-2222-2222 | 010-1111-1111 |

전화번호1,2는 바뀌었는데 3은 그대로이다 이상태를 **'일관성 이 깨졌다'** 라고 이야기 한다. 데이터가 일치되어야 하는데 불일치가 된것이고 전체적으로 확정해서 보게되면 무결성이 깨진것이다.
**데이터 베이스의 가장 큰 목표는 '데이터 무결성'을 높이는 것** 이다
 ### 데이터 정합성과 무결성
 * 데이터 정합성
  > 어떤 데이터들의 값이 서로 일치하는 상황.
  * **정합성은 데이터가 서로 모순이 없이 일관되게 일치** 해야 한다는 의미이다. 외래키 제약조건이라고도 한다
 * 데이터 무결성
  > 데이터가 현실과 정확하게 일치하는지 보는 것이다.
  > 참조 무결성은 외래키의 개념과 관련된다. 참조 무결성 규칙은 모든 외래키 값은 두가지 상태 가운데 하나에만 속함을 규정한다. 일반적 상태는 외래키 값이 데이터베이스의 특정 테이블의 기본 키 값을 참조하는 것이다. 이는 비즈니스 규칙에따라 달라질수 있으며 외래키값은 빈값을 허용한다.
 ## 키(key) = 식별자(identifier)
 > 튜플을 유일하게 식별할 수 있는 속성 집합을 그 릴레이션의 키라고 하며 튜플을 검색하거나 정렬할떄 튜플들을 서로 구분할 수 있는 기준이 되는 속성을 말한다.
  ### 키의 특성
  > 키의 특성을 **유일성과 최소성** 2가지가 있는데 유일성은 하나의 키 값으로 하나의 튜플만을 유일하게 식별할 수 있는것이고 최소성은 키를 구성하는 속성 하나만 제외시켜도 유일성이 꺠지도록 꼭 필요한 최소의 속성이 구성되는것을 말한다.
  ### 키의 종류
   1) 슈퍼키 
    > 슈퍼키는 튜플을 유일하게 구분하기 위하여 한개 이상의 속성들의 집합으로 이루어진 키를 말하고 유일성은 만족시키지만 최소성은 만족시키지 못한다
   
   | 학번 | 성명 | 주민번호 | 학과 |
   |---|---|---|---|
   | 100 | 백번이 | 100100-1001001 | 전자 |
   | 200 | 이백번이 | 200200-2002002 | 컴퓨터 |
   | 300 | 삼백번이 | 300300-3003003 | 경영 |
   
   위의 학생 테이블에서 유일하게 식별할 수 있는 컬럼은 학번과 주민번호이다. 성명,학과는 중복값있을수 있기에 유일성 만족x. => 학번과 주민번호가 슈퍼키이다. 그리고 유일성만 만족시키면 되기 때문에 {학번,주민번호}, {학번,성명}(물론 다른것들 추가되도 상관 x) 이렇게 두개의 속성으로 묶어도 슈퍼키라고 할수 있다. 근데 굳이 학번하나로 충분히 구분해 낼수 있는데 다른값이 들어갈 필요성은 크게 없고 최소성또한 만족시키지 못한다.
 * 정리하자면 슈퍼키는 유일하게 식볋 낼수 있는 속성이 있다면 그 속성들은 모두 슈퍼키가 될수 있다. '학번'만 가지고 유일하게 식별 할 수 있다고 한다면 학번 이라는 속성은 최소성과 유일성 모두 만족이 된다. 근데 {학번,성명} 이렇게 2개의 속성을 넣어버리면 학번 하나만 가지고도 식별할 수 있는데 굳이 성명이라는 속성이 더 있기에 최소성은 만족을 못하는 것이다.
  2) 후보키
   > 후보키는 유일하게 구분할 수 있는 최소 슈퍼키를 의미하며 슈퍼키와는 다르게 후보키는 최소성과 유일성 모두 만족한다. 하나의 테이블에 속하는 모든 튜플들은 중복된 값을 가질수 없으므로 모든 테이블은 반드시 하나 이의 후보키를 갖는다.
   
   | 학번 | 성명 | 주민번호 | 학과 |
   |---|---|---|---|
   | 100 | 백번이 | 100100-1001001 | 전자 |
   | 200 | 이백번이 | 200200-2002002 | 컴퓨터 |
   | 300 | 삼백번이 | 300300-3003003 | 경영 |
   
   위 학생테이블에서 유일학 ㅔ식별할 수있는 속성은 학번과 주민번호이므로 후보키는 학번과 주민번호이다. {학번,주민번호} 이렇게 2개의 속성으로 묶고 보면 누가 어떤 학과인지 파악할수 있고 이오같이 2개 이상의 속성으로 키를 구성한것을 '복합키'라고 한다(물론 주민번호를 pk로 사용하면 안된다.)
   
  3) 기본키 (Primary key) PK , 주식별자, 주키
  > 기본키는 유일하게 식별해 낼 수 있는 속성중 후보키가 되는것 중에서 선정된 키이다. 기본키는 무조건 존재 해야하며 중복값이나 널을 허용하지 않는다.
  
  | 학번 | 성명 | 주민번호 | 학과 |
   |---|---|---|---|
   | 100 | 백번이 | 100100-1001001 | 전자 |
   | 200 | 이백번이 | 200200-2002002 | 컴퓨터 |
   | 300 | 삼백번이 | 300300-3003003 | 경영 |
   
   위의 학생 테이블은 학번과 주민 번호가 슈퍼키와 후보키를 모두 만족하지만 주민번호는 애초에 변경 가능성 있는 속성이고 가능성이 희박하더라도 민감한 개인정보이기 때문에 pk로 사용하기 적절치 않다. 따라서 학번을 pk로 설정하는 것이 맞다.
  
   | 학번 | 과목코드 | 학점 | 학과 |
   |---|---|---|---|
   | 100 | A001 | A+ | 전자 |
   | 200 | A001 | B | 컴퓨터 |
   | 200 | B002 | B | 컴퓨터 |
   | 300 | B002 | C | 경영 |
   | 300 | C003 | A+ | 경영 | 
   
   위의 <수강> 테이블은 모든 항목이 서로 중복되기 때문에 2개의 속성을 후보키로 구성해서 사용해야한다.{학번, 과목코드} 이렇게 묶어서 사용하면 어떤학생이 어떤 과목에서 몇점을 받았는지 파악 가능하다.
   
  4) 대체키
  > 대체키는 하나의 테이블에 존재하는 후보키들 중에서 기본키를 제외한 나머지 후보키를 말한다. 즉 후보키 - 기본키 = 대체키 이렇게 되고 보조키 라고도 한다.
  5) 외래키
  > 외래키는 어떤 테이블의 pk값과 일치함을 요구하는 다른 테이블의 한 속성(컬럼)을 의미하고 **외래키를 포함하는 테이블이 참조하는 테이블이 되고 대응되는 기본키를 포함하는 테이블이 피참조 테이블이 된다** 또 RDBM에서 한 테이블의 외래키는 피참조 테이블의 기본키와 대응되어 테이블 간의 참조관계를 표현하는데 사용되는 중요한 속성이다.
## 무결성 제약조건
 * 무결성의 개념 : 무결성은 데이터베이스에 저장된 데이터 값과 그것이 표현하는 현실세계의 값이 일치하는 정확성을 의미한다
 * 무결성 제약 조건 이론 3가지
 > 무결성 제약조건은 크게 개체 무결성, 참조무결성, 도메인무결성 이렇게 3개가 있다
  1) 개체 무결성
  > 개체 무결성은 기본키와 관련된 제약조건으로 한 테이블의 기본키를 구성하는 어떠한 속성도 절대 널 값이나 중복값은 가질 수 없다는 제약 조건이다.
  
   | 학번 | 성명 | 주민번호 | 학과 |
   |---|---|---|---|
   | 100 | 백번이 | 100100-1001001 | 전자 |
   | 200 | 이백번이 | 200200-2002002 | 컴퓨터 |
   | 300 | 삼백번이 | 300300-3003003 | 경영 |
   |     | 사색번이 | 400400-4004004 | 디자인 |
   
   | 학번 | 성명 | 주민번호 | 학과 |
   |---|---|---|---|
   | 100 | 백번이 | 100100-1001001 | 전자 |
   | 200 | 이백번이 | 200200-2002002 | 컴퓨터 |
   | 300 | 삼백번이 | 300300-3003003 | 경영 |
   | 300 | 사색번이 | 400400-4004004 | 디자인 |
   
   **위의 테이블의 기본키(pk)인 학번 속성이 비어있거나 = null이거나, 학번이 중복되면 '개체무결성 원칙'에 위배 되었다고 하며 개체무결성 원칙을 지키기 위해선 NUll 대신 다른 튜플과 구별되는 값으로 적용해줘야 한다.**
   
   2) 도메인 무결성
   > 도메인무결성은 주어진 속성의 값이 그 속성이 정의된 도메인에 속한 값이어야 한다는 제약조건이다.
   
   | 학번 | 성명 | 학년 | 학과 |
   |---|---|---|---|
   | 100 | 백번이 | 1| 전자 |
   | 200 | 이백번이 | 2 | 컴퓨터 |
   | 300 | 삼백번이 | 3 | 경영 |
   | 300 | 사색번이 | 5 | 디자인 |
   
   위의 학생 테이블은 4년제 대학교라고 가정했을때 학년은 5학년이 되어선 안된다 도메인이 들어올수 있는 범위는 1~4까지의 범위여야 한다.(사실 도메인의 정의가 감이 안잡혔는데 실제의 어떤 값의 조건 정도로 파악하면 될듯하다 말로 설명하기 애매하게 감이 잡힘) 
   
   3) 참조 무결성
   > 참조무결성은 외래키와 관련된 제약조건으로 테이블1에 저장된 튜플이 테이블2에 있는 튜플을 참고하려면 참조되는 튜플이 반드시 테이블2에 존재해야 한다는 제약조건이다. 테이블은 참조할 수 없는 외래키 값을 가질수 없으며 외래키 값은 피참조 테이블의 기본값으로 존재해야 한다. 외래키의 속성들은 피참조 테이블의 기본키와 도메인이 동일해야하고 외래키의 속성 갯수와 피참조 테이블의 기본키 속성 갯수는 같아야 한다.

 ### 데이터베이스 무결성 제약조건 명령
  1) NOT NULL : age컬럼에 NOT NULL 제약조건을 걸어 놓으면 데이터 입력시 age 컬럼값에는 꼭 값을 입력해야한다. NULL이 되면 오류가 발생함
  2) UNIQUE : 해당 테이블에 있어서 존재하는 값이 유일해야 한다. age 컬럼에 UNIQUE 제약조건을 걸어 놓으면 데이터 입력시 age컬럼에 19가 입력되었다면 기존 튜플값에 19가 있으면 오류가 나고 없어서 입력된후에 19값은 더이상 해당 테이블에 입력될 수 없다.
  3) PRIMARY KEY : 하나의 테이블에 있는 데이터들을 식별하기 위한 기준이 되는 제약조건. 한개의 테이블에 한 컬럼만 생성가능하다. PK는 NOT NULL + UNIQUE의 속성을 가진다.
  4) FOREIGN KEY : 
  * **FOREIGN KEY의 무결성 유지를 위한 참조행동 **   
  
   > 데이터베이스 사용자가 SQL-DML을 통해 지정된 데이터를 관리하고자 할때 한 테이블의 튜플들이 아니라 보통 여러 테이블에서 튜플을 검색하여 조건에 맞게 조작을 한다. 이때 테이블간에는 유기적은 연결이 있어야 하는데 이는 테이블의 외래키가 다른 테이블의 기본키를 참조함으로써 이루어 진다.
 
   * create table 명령을 정의할때 외래키가 기본키를 참조하는 옵션을 주어 다양한 참조행동을 명시할 수 있다. 참조행동의 기본값은 NO ACTION이다.

   * **[ON DELETE {CASCADE | SET NULL | SET DEFAULT | NO ACTION | RESTRICT}]** : 참조되는 테이블의 데이터가 삭제시의 제약
   * **[ON UPDATE {CASCADE | SET NULL | SET DEFAULT | NO ACTION | RESTRICT}]** : 참조되는 테이블의 데이터가 변경시의 제약
   * NO ACTION : DB 엔진자체에서 에러가 나며 부모테이블의 행에대한 삭제 or 변경 동작이 롤백된다.
   * CASCADE : 부모테이블에서 해당 행이 업데이트 되거나 삭제될때 참조 테이블에서도 해당 행이 업데이터 또는 삭제된다.
   * SET NULL : 부모테이블에서 행을 삭제 or 수정한 경우 자식 테이블에서 해당 외래키를 구성하는 모든 값이 NULL로 설정된다. 다만 이경우 외래키의 속성이 NULL을 허용해야 하고 NOT NULL인경우 에러가 발생한다.
   * SET DEFAULT :  부모테이블에서 행을 삭제 or 수정한 경우 자식 테이블에서 해당 외래키를 구성하는 모든 값이 기본값(DEFAULT값)으로 설정된다. 이 제약 조건을 실행하려면 모든 외래키 열에 기본정의가 되어있어야하고 기본값이 명시되어있지 않은경우는 NULL이 기본값이나 외래키의 속성이 NOT NULL인경우 에러가 발생한다.
   * RESTRICT : 자식테이블에 데이터가 남아있는 경우 부모 테이블의 데이터는 수정 or 삭제를 할 수 없다.
  5) CHECK : 조건에 부합하는 데이터만 입력이 가능하도록 하는 제약조건이다. 조건에는 기본연산자나 비교연산자 IN,NOT IN 등등 사용이 가능하다.  

## SQL
> SQL은 IBM연구소에서 개발한 SEQUEL에서 연유한 것이고 관계대수와 관계해석을 기초로한 고급 데이터 언어이다.
 ### SQL의 종류
 <img src = "https://img1.daumcdn.net/thumb/R800x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F210F5B4A55D45A950D"/>
 
  #### DDL (데이터 정의어)
  > DDL은 DBMS에서 사용할 데이터베이스의 정의 및 변경을 위해서 사용하는 언어이며 외부스키마 명세를 정의하고 스키마에 사용되는 제약 조건 명세를 정의하고 DB의 논리적 데이터 구조와 물리적 데이터 구조 및 구조간의 사상을 정의한다. 그리고 DDL로 정의된 내용은 '메타데이터'가 되고 '시스템 카탈로그'에 저장되며 번역한 결과가 '데이터 사전'이라는 특별한 파일에 여러개의 테이블로서 저장되어 관리된다
   * 시스템 카탈로그 = 데이터 사전
   >  DB에 포함된 다양한 데이터객체(테이블,뷰,인덱스등)에대한 정보들을 유지,관리 하기 위한 시스템 DB이다. DB에 포함되는 모든 데이터 객체에 대한 정의나 명세에 관한 정보를 유지 관리하고, DBMS가 스스로 생성하고 유지되는 DB 내의 특별한 테이블 집합체이다. 데이터 사전이라고도 하며 시스템 카탈로그에 저장된 정보를 메타데이터 라고 한다. 
  * DDL의 명령어 종류엔 Create(정의), Alter(변경), Drop(삭제) 이렇게 3가지의 명령이 있다.
  1) Create : create는 스키마,도메인,뷰,테이블,인덱스 등을 '정의'하는 명령어 이다.
     + DB에서 도메인이란? -> 릴레이션에 포함된 각각의 속성들이 가질 수 있는 값들의 집합이라고 할 수 있다. 도메인이라는 개념이 필요한 이유는 릴레이션에 저장되는 데이터 값들이 본래 의도했던 값들만 저장되고 관리하기 위해서다.
   1) Domain 정의 : 기본적으로 테이블 생성시나 생성후 특정 컬럼에 제약조건을 거는 경우 도메인 정보를 통해 제약을 거는 경우가 많다. ex) alter table member add constraint valid_age check(age >= 20 and age < 40); -> 이경우 age컬럼 값을 20~39 제한하는 도메인내용이 있고 이를 위해 제한한다. 
   2) 테이블 정의
   > 도메인을 정의하는 명령문은 create table이다.
  
   ```
    CREATE TABLE `friends` (
  `friend_id` int(10) NOT NULL AUTO_INCREMENT,
  `name` varchar(100) NOT NULL,
  `age` int(10) NOT NULL,
  `region_id` int(10) DEFAULT NULL,
  PRIMARY KEY (`friend_id`),
  KEY `region_id` (`region_id`),
  CONSTRAINT `friends_ibfk_1` FOREIGN KEY (`region_id`) REFERENCES `region` (`region_id`),
  CONSTRAINT `valid_age` CHECK (`age` >= 20 and `age` < 40) );
  ```
 2) ALTER
 > ALTER는 테이블의 정의를 변경하는 명령어이다.
 * Alter table 테이블_이름 add 컬럼명 data_type [default '기본값'];
 * Alter table 테이블_이름 MODIFY 컬럼명 새data_type [default '기본값'];
 * Alter table 테이블_이름 CHANGE 컬럼명 새컬럼명 data_type [default '기본값'];
 * Alter table 테이블_이름 DROP 컬럼명; 
 3) DROP
 > DROP은 스키마,테이블,인덱스 등을 삭제하는 명령이다.
  #### DCL (데이터 제어어)
  > 다수의 사용자가 DB를 공용하고 정확성을 유지하기 위한 데이터 제어를 정의하고 기술하는 언어이며 데이터의 보안, 무결성, 회복과 밀접한 관련이 있다. 불법적 사용자로 부터 데이터 보호를 위한 보안을 명세하고 데이터 정확성을 위한 무결성을 명세한다. 또한 시스템 장애에 대비한 데이터 회복과 병행 수행 제어를 명시한다.(TCL은 조금 나중에 명시)
  * DCL 명령어의 종류 
   * 사용 권한을 부여하는 **GRANT** 명령
   * 사용 권한을 취소하는 **REVOKE** 명령
   * 정상적인 완료가 되었다는 신호를 보내주는 **COMMIT** 명령
   * 비정상적 종료를 알리는 **ROLLBACK** 명령 (COMMIT과 ROLLBACK은 TCL이라는 트랜잭션 명령어로 따로 분류된다.)
   1) GRANT : GRANT명령은 사용자에게 해당 객체에 대한 특정 사용권한을 부여할 때 사용하는 명령문이다. 
     * 권한 종류 : select, insert, update, delete
   2) REVOKE : 사용자에게 해당 객체에 대한 특정 사용권한을 취소할때 사용하는 명령문입니다. 
     * 권한 종류 : select, insert, update, delete
   #### DML (데이터 조작어)
   > DML은 사용자로 하여금 데이터를 처리 할 수 있게 하는 도구 역할을 해주는 언어이고 사용자와 DB간의 인터페이스를 제공한다. 데이터 조작어에는 질의어가 있으며 질의어는 터미널에서 주로 사용하는 비절차적 데이터 언어이다.
   * 종류
     * 튜플을 검색하는 **SELECT**
     * 튜플을 삽입하는 **INSERT**
     * 튜플을 변경하는 **UPDATE**
     * 튜플을 삭제하는 **DELETE**
    
   * 자세한건 이후에 함수들을 통해 다룰예정
   
  ### 최적화와 인덱스
   * 인덱스 : 대표적 예시는 책의 색인을 생각하면된다. 인덱스는 빠른 검색을 가능하게 해주고, 데이터가 정렬되어있다.
    * 기존에 employees 라는 30만건정도 있는 테이블에 'Tommaso'라는 이름을 가진 사원을 찾는경우 0.053초 정도 걸렸다. 별로 안걸린것 같지만 사실 느린편이고 데이터가 몇억건이 있다고 생각하면 속도는 현저히 줄어들 것이다.
    * 그렇다면 인덱스를 생성후 다시 검색하면 어떨까? 결과는 0.003초가 나왔다. 결국 인덱스는 검색을 빠르게 해준다는 큰 장점이 있다 (실행계획타입은 ref) 
    * alter table employees add key(=index) (first_name);  해당 명령어는 first_name에 대한 인덱스를 데이터베이스가 가지고 있어 first_name을 활용한 검색에 큰 도움을 주게된다.
   * 인덱스(키)의 종류
     * 인덱스의 종류와 만들기
      * alter table table_name add primary key ...
       * pk가 있는 테이블은 자동적으로 pk를 기준으로 솔팅되기 때문에 pk를 통한 검색은 인덱스를 찾지 않는다.
      * alter table table_name unique key_name...
       * 테이블에 한개밖에 없는 값을 나타내기에 하나의 내용을 찾기위해 검색시 유용하다.
      * alter table table_name add KEY key_name...
       * 일반적인 인덱스(키)가 key 이다.
      * alter table table_name add FULLTEXT key_name...
    * 일반적으로 다음의 경우에 인덱스를 만든다
     * Where 절에서 비교하는 '컬럼'
     * order by 로 정렬하는 컬럼
     * group by 로 그룹화 하는 컬럼
   
   * 다만 인덱스는 검색에서는 좋은 성능을 자랑하지만 추가,수정,삭제의 경우는 만들어진 인덱스에 끼워넣거나 변경하거나, 빼주는 과정을 거치기때문에 성능이 저하된다. 결국 꼭 필요한 컬럼에만 인덱스를 설정해야 한다.
   * 또한 인덱스 설정도 잘해줘야한다. 예를들어 first_name과 last_name둘을 하나의 인덱스로 잡아놓으면 first_name을 기준으로 정렬되어 검색하고 first_name이 같은 것중 last_name을 정렬하기 때문에 last_name만으로 검색시에는 인덱스를 사용하지 않게된다.

 ### 실행계획
 | type | 설명 | 
 |---|---|
 | const | pk나 uk를 사용해서 1건을 가져오는 쿼리 |
 | eq-ref | 조인에서 두번쨰 이후에 읽는 테이블의 프라이머리키로 조인 |
 | ref | 인덱스에 equal검색 |
 | fulltext | 전문검색 인덱스를 활용 |
 | range | 인덱스를 범위로 검색 | 
 | ALL | 테이블 full scan |
 
 * eq-ref : 일반적으로 조인은 where조건이 있는 쪽이 먼저 조인의 앞 테이블이 되는것이 일반적으로 빠르다. 먼저 조건에 대한 데이터를 찾아 놓고 조인하는 편이 빠르기 때문. explain 쿼리문 으로 쿼리 실행단계를 살펴보고 결정하는게 좋은 방법.
 * ref : 일반적 인덱스 적용시 실행계획.
 * range : 인덱스가 있는 컬럼을 where구문에 범위를 적용해 검색된 실행

 ### Like
  > 해당 people 테이블에 name에 인덱스가 있는 상황이다.
  ```
  CREATE TABLE `people` (
   `peopleCd` char(8) NOT NULL,
   `name` varchar(20) NOT NULL,
   `nameEn` varchar(100) NOT NULL,
   `repRole` varchar(20) NOT NULL,
   PRIMARY KEY (`peopleCd`),
   KEY `name_2` (`name`),
   FULLTEXT KEY `name` (`name`),
   FULLTEXT KEY `nameEn` (`nameEn`)
 ) ENGINE=InnoDB DEFAULT CHARSET=utf8 |
  ```
  * like 연산 뒤의 % 는 와일드카드라고 한다.
  * 이름이 '이병'으로 시작하는 사람 (good query) 
   * select peopleCd, name from people where name like '이병%'
    * 위처럼 like연산 뒤에 첫 글자가 있으므로 정렬되어있는 인덱스로 검색이 가능하다. '이병'으로 시작하는 처음부터 끝까지 찾는다는 명령. 실행계획을 봐도 '이병ㄱ'~'이병ㅎ'까지의 검색이기 때문에 range 타입으로 실행된다. 
   * select peopleCd, name from people where name like '%병헌' (bad query)
   * select peopleCd, name from people where name like '%병%' (bad query)
    * 와일드카드가 검색어 앞에온경우에는 강력한 검색을(넓은 범위의 검색을) 할수 있지만 인덱스를 타고 검색을 할수 없기 때문에 속도가 느리다.
  => Like 연산은 왠만하면 % 지양해야 한다. 데이터가 많으면 많을수록 속도가 느려진다..
   
 ### Full-Text Search (전체문서 검색)
 > CREATE TABLE `movie` (
  `movieCd` char(8) NOT NULL,
  `title` varchar(100) NOT NULL,
  `titleEn` varchar(100) NOT NULL,
  `productYear` char(4) NOT NULL,
  `openDate` date NOT NULL,
  `nation` varchar(20) NOT NULL,
  `genre` varchar(20) NOT NULL,
  PRIMARY KEY (`movieCd`),
  KEY `nation` (`nation`),
  FULLTEXT KEY `title` (`title`),
  FULLTEXT KEY `titleEn` (`titleEn`));
  
 > Full-Text Search는 인덱스를 통해 단어별로 쪼개서 검색이 가능하게 하는 검색기능이다. 만약 '로마의 휴일' 이라는 단어중 '휴일' 검색을 통해 찾을땐 Like는 " like '%휴일' " 이렇게 검색하기 때문에 인덱스를 타지 못해 속도가 느리다.  
 * fulltext 생성 : alter table table_name add fulltext key_name (target_column);
 * fulltext 삭제 : alter table table_name drop key_name ; 
 * '로마의 휴일'이라는 제목의 영화를 검색시
  * select * from movie where match(title) against('로마') : '로마' 라는 단어가 들어간 영화를 찾는다.match(탐색할 컬럼명), against(탐색할 단어)의 문법이다. 근데 '로마의 휴일'은 목록에 없다. 즉 title 컬럼내에 '로마'라는 단어자체를 검색해서 찾는 것이기 때문에 ' '로마의' 휴일' 은 검색되지 않는다.
  * 다만 match내의 컬럼명은 fulltext 인덱스가 적용되어있어야한다.   
  * select * from movie where match(title) against('로마*' in boolean mode): fulltext에서도 ' * ' 를 사용해 와일드카드를 사용할 수 있고 boolean모드에서 사용가능하기 때문에 in boolean mode라는 것을 명시해서 함께 사용해줘야 한다. 이렇게 되면 '로마의 휴일'을 찾을수 있고 '열정의 람바다'라는 것도 ('열정*' in boolean mode) 이러한 방식으로 찾을 수 있다.
  * 또한 boolean mode에선 강력한 검색도 사용할 수 있는데 단어 앞에 +를 붙히면 필수검색 단어라는 명시를 해줄수 있다.
  ```
  select * from movie where match(title) against('+열정* +냉정*' in boolean mode) 은 열정과 냉정이라는 단어가 들어간 단어를 모두 찾아준다 ex => '냉정과 열정사이'  
  select * from movie where match(title) against('+열정* -냉정*' in boolean mode) 은 열정은 꼭 포함되고 냉정은 없어하는 조건이다 ex => '냉정'이들어간 영화제목들.
  select * from movie where match(title) against('열정*, 냉정*' in boolean mode) 은 둘중에 하나라도 있는 것들을 모두 검색해준다.
  ``` 
  
  ### Group by
  > group by는 어떤한 항목별로 조회할경우 사용된다. 
  ``` 
  salarie 테이블
  +-----------+---------+------+-----+---------+-------+
| Field     | Type    | Null | Key | Default | Extra |
+-----------+---------+------+-----+---------+-------+
| emp_no    | int(11) | NO   | PRI | NULL    |       |
| salary    | int(11) | NO   |     | NULL    |       |
| from_date | date    | NO   | PRI | NULL    |       |
| to_date   | date    | NO   |     | NULL    |       |
+-----------+---------+------+-----+---------+-------+

  employees 테이블
  +------------+---------------+------+-----+---------+-------+
| Field      | Type          | Null | Key | Default | Extra |
+------------+---------------+------+-----+---------+-------+
| emp_no     | int(11)       | NO   | PRI | NULL    |       |
| birth_date | date          | NO   |     | NULL    |       |
| last_name  | varchar(16)   | NO   | MUL | NULL    |       |
| gender     | enum('M','F') | NO   |     | NULL    |       |
| hire_date  | date          | NO   |     | NULL    |       |
+------------+---------------+------+-----+---------+-------+

dept_emp 테이블
+-----------+---------+------+-----+---------+-------+
| Field     | Type    | Null | Key | Default | Extra |
+-----------+---------+------+-----+---------+-------+
| emp_no    | int(11) | NO   | PRI | NULL    |       |
| dept_no   | char(4) | NO   | PRI | NULL    |       |
| from_date | date    | NO   |     | NULL    |       |
| to_date   | date    | NO   |     | NULL    |       |
+-----------+---------+------+-----+---------+-------+

 department 테이블
 +------------+---------------+------+-----+---------+-------+
| Field      | Type          | Null | Key | Default | Extra |
+------------+---------------+------+-----+---------+-------+
| emp_no     | int(11)       | NO   | PRI | NULL    |       |
| birth_date | date          | NO   |     | NULL    |       |
| last_name  | varchar(16)   | NO   | MUL | NULL    |       |
| gender     | enum('M','F') | NO   |     | NULL    |       |
| hire_date  | date          | NO   |     | NULL    |       |
+------------+---------------+------+-----+---------+-------+
  ```
   * ex 사원별 최고 연봉 쿼리 : 
   ```
   select emp_no, max(salary) max_salary , min(salary) min_salary from salaries group by emp_no order by max_salary desc limit 10; => 사원들중 연봉이 제일 높은 사원순으로 10개를 조회하는 쿼리. '사원'으로 데이터가 묶여 최다연봉기준으로 출력된다.
   ```
   * ex 부서별 최고 연봉 쿼리 :
   ``` 
   select dept_no, max(salary) max_salary , min(salary) min_salary from salaries join dept_emp using(emp_no) group by dept_no order by max_salary; => 부서들중 연봉이 제일 높은 부서 순으로 조회하는 쿼리. '부서'별로 데이터가 묶여 연봉이 계산되 출력된다. 
   ```
   * ex 개인별 연봉 누적 총액 (단 1996년 이후 , 누적연봉 100만 달러이상만) : 
   ```
   select emp_no,last_name, sum(salary) sum_salary,from_date
   from salaries join employees using(emp_no) 
   where from_date >= '1996-01-01' 
   group by emp_no 
   having sum_salary >= 1000000 
   order by sum_salary desc 
   limit 10;
   => 조금 복잡하지만 찬찬히 본다면 1996년 이후라는 조건은 where 절에, 누적연봉 100달러 이상은 having 조건에 들어간다. (참고로 having은 group by에 대한 조건문이다.) 누적연봉 sum_salary 컬럼은 sum함수를 사용하며 준 임시 컬럼이름이다 where절은 기존 테이블의 컬럼을 조회하기 때문에 sum_salary를 인식할수 없다. 그렇기에 having에 묶어주어야 조건을 만족시킬수 있다. 
   ```

## CHAR과 VARCHAR에 대해
> char(n)은 고정길이 n개의 바이트를 말하고 varchar(n)은 가변길이 최대 n개의 바이트를 말한다. 예를 들어서 char(50)의 경우 50자리 까지 넣을수 있는 고정문자열이 생성되고 varchar(50)은 50자리까지 넣을수있는 가변길이 문자열이 된다. 즉 'abcde'라는 문자열을 해당 필드에 넣을때 char의 경우 abcde가 입력된 후 입력값을 제외한 45자리가 남게되고 varchar는 abcde 딱 5개의 문자만 입력되고 존재하게 된다.

## JOIN이란
> 관계형 DB에선 중복 데이터를 피하기 위해 데이터의 속성을 분류해 여러 테이블로 나누어 놓는 '정규화' 작업을 한다. 이렇게 정규화된 데이터에서 원하는 결과를 도출하기 위해 여러 테이블을 조합할 필요성이 생기는데 이런경우 사용하는 명령어가 컬럼을 기준으로 행을 합쳐 가상의 테이블 처럼 만들어 결과를 보여주는 연산인 **JOIN** 이다.  
+ JOIN관계의 두 테이블이 n:1의 경우엔 n쪽에서 1쪽으로 JOIN하는게 속도가 빠르다.

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
## 트랜잭션
> 트랜잭션은 데이터베이스의 상태를 변화시키기 위하여 논리적 기능을 수행하는 하나의 작업 단위를 말하며 한꺼번에 모두 수행되어야 할 일련의 데이터베이스 연산이다. 사용자의 시스템에 대한 서비스 요구시 시스템의 상태 변환 과정의 작업 단위이고, 데이터베이스 시스템에서 병행제어 및 회복 작업의 논리적 작업단위 이며, 하나의 트랜잭션은 Commit되거나 Rollback이 되어야 한다.  예) 이체: 보내는 계좌에서 차감 -> 받는 계좌에서 증액 ,  영화 예매 : 좌석 점유 -> 포인트 사용 -> 신용카드 결제

* 만약 내가 친구에게 10만원을 이체하는 경우.
 1) 내 통장의 잔고를 조회해야 한다
 2) 잔액을 조회후 친구에게 10만원을 보내기 위해 이체 시킨다. 이체후 남은 금액이 계산 되어야 한다.
 3) 친구에게 보내고 나서 남은 금액을 기록한다. 
 4) 친구의 통장이라고 가정하고 친구의 잔액을 조회한다.
 5) 이체된 금액을 더하고 그합을 다시 저장하면 계좌이체가 완료된다.
 6) 위 과정은 조금더 상세하겐 내 계좌와 친구계좌의 값을 하드디스크(DB)에서 주기억장치 버퍼로 읽어오고 내 계좌에서 10만원 인출한 값을 저장하고 친구계좌에 10만원 입금한 값을 저장한후 내 계좌와 친구계좌에 주기억장치버퍼에서 하드디스크(DB)에 기록하는 과정을 거친다.
 * 이러한 과정이 모두 합쳐져 계좌 이체라는 하나의 작업단위를 구성한다. 
 * **데이터베이스에서는 이와 같은 하나의 논리적인 작업 단위를 구성하는 연산들의 집합을 '트랜잭션' 이라고 한다.** 이런 관점에서 **데이터베이스 응용 프로그램은 트랜잭션들의 집합으로 정의할 수 있다.**
<img src="https://t1.daumcdn.net/cfile/tistory/9978DA4F5ADE84AD15"/>

 ### 트랜잭션의 필요성
 > 위의 계좌이체를 생각해보면 이체도중 예기치 않은오류가 발생하는 경우 최악의 경우는 내 계좌에선 금액이 빠져나갔지만 친구의 계좌엔 이체가 안된 즉 돈이 증발한 상황이다. **트랜잭션은 이러한 문제가 발생하지 않도록 하는 강력한 수단을 제공한다. 이체라는 동작하나가 트랜잭션 단위로 동작해 중간 오류가 발생하면 즉시 동작전 상태로 돌아가게 하는것이 가능하다.**  

 ### 트랜잭션의 특성(ACID 성질)
 1) 원자성 : 하나의 트랜잭션은 원자처럼 더이상 쪼개지지않는 하나의 단위로 처리되어야 한다. 어떤 트랜잭션이 A,B로 구성되어있고 항상 A,B의 처리결과는 동일한 결과여야 한다. 즉 트랜잭션의 결과는 모두 성공 or 트랜잭션 실행전 상태 이다(= ALl or Nothing). **트랜잭션내의 모든 연산,작업은 반드시 한꺼번에 완료되어야 하며 어떤 작업이 잘못되는경우 모든것은 다시 원점으로 되돌아가야만 한다.**
 2) 일관성 : 트랜잭션이 성공했다면 데이터베이스의 모든 데이터는 일관성을 유지해야 한다. 트랜잭션 수행전과 수행 완료 후의 성질이 같아야 한다는 것이다. 즉, a에서 b로 계좌 이체를 했다면 a 잔액의 합과 b잔액의 합이 전과 같아야 한다.
 3) 격리성 : 트랜잭션으로 처리되는 중간에 외부에서의 간섭은 없어야 한다. 또한 둘이상의 트랜잭션이 동시에 병행실행 되는 경우 하나의 트랜잭션 실행중 다른 트랜잭션의 연산이 끼어들 수 없으며 트랜잭션 T1과 T2에 대해서 T1이 시작 되기 전에 T2가 끝나든지 T1이 끝난후 T2가 시작되든지 해야한다는 성질이다.
 4) 영속성 : 트랜잭션이 일단 해당 작업을 성공하면 그 결과는 계속 유지되어야 한다는 성질이다. 즉 트랜잭션이 정상적으로 커밋된 경우 버퍼의 내용을 하드디스크(DB)에 확실히 기록해야 하며 부분환료 된경우 작업을 취소하여야 한다. 
 
 ### 트랜잭션과 DBMS
 * DBMS는 원자성을 유지하기 위해 회복 관리자 프로그램을 작동시킨다
 * DBMS는 일관성을 유지하기 위해 동시성 제어 알고리즘과 무결성 제약조건을 활용한다
 * DBMS는 고립성을 유지하기 위해 동시성 제어 알고리즘을 작동시킨다.
 * DBMS는 지속성을 유지하기 위해 회복 관리자 프로그램을 이용한다.

 > 어떤 트랜잭션이 실행되다 장애에 의해 부분 완료되는 상황은 원자성과 지속성이라는 속성에 위배된다.그래서 DBMS는 이를 유지하기 위해 '회복 관리자 프로그램'을 이용하는데 일부만 진행된 트랜잭션을 취소시켜 원자성을 유지할 뿐 아니라 값을 트랜잭션 이전의 상태로 복원시켜 지속성을 유지시켜줍니다. 또한 일관성과 고립성을 유지하기 위해서 값에 동시에 접근하지 않도록 하므로 '동시성제어(Loking)'를 활용하여 이를 해결한다.파일 시스템과 같은 경우처럼 값이 덮어씌워지는 경우 일관성이 무너질수 있고 그러한 경우 고립성에 위배되는 경우이므로 동시성제어를 하여 이를 만족시킨다. 여기에 더해 DBMS는 잘못된 값에 대한 입력이 오면 일관성이 무너질수 있으므로 이를 유지시키기 위해 '무결성 제약조건'도 활용한다
 
 <img src="https://t1.daumcdn.net/cfile/tistory/994CAA425A2F96501C"/>
 
 ### 트랜잭션의 연산
 1) COMMIT 연산
  * 모든 작업을 정상적으로 처리하겠다고 확정하는 명령어로 처리과정을 DB에 영구저장 하는것이다.
  * Commit은 하나의 트랜잭션 과정을 종료하는 것이고 이전 데이터가 완전히 수정된다.
  <img src="https://t1.daumcdn.net/cfile/tistory/995E053D5ADE8AC410"/>
  * 위 그림중 첫번쨰 커밋후 뒤 update,delete,insert 명령을 진행한다. 만약 3-4-5과정이 오류없이 수행되었다면 지금까지 실행한 3-4-5작업을 한번에 DB에 적용하는 명령으로 COMMIT을 수행한다.
 
 2) Rollback 연산
  * 작업중 문제가 발생되어 트랜잭션 처리과정에서 발생한 변경사항을 취소하는 명령어이다.
  * 트랜잭션이 시작되기 이전 상태로 되돌린다
  * 커밋하여 저장한것만 복구한다
  <img src="https://t1.daumcdn.net/cfile/tistory/998AAF395ADE8C141C"/>
  * 위 그림에서 Rollback 명령은 마지막으로 수행한 커밋 명령(1,2)까지만 처리된상태로 유지한다
  * 이후 실행한 3-4-5작업은 취소시켜 이전 상태(1,2)로 복구시킨다.
  * 트랜잭션은 이렇게 ALL-OR-Noting(수행하거나 하지않거나)방식으로 DML명령어 들을 처리한다.
 
 3) SAVEPOINT 
 * 트랜잭션 단위 내의 임시저장위치 이다.
 * 보통 Rollback을 명시하면 트랜잭션 내에서 실행되었던 작업 전체가 취소 되는데 전체가 아닌 특정 부분에서 트랜잭션을 취소 시킬수 있다.
 * SAVEPOINT를 쓰면 현재의 트랜잭션을 작게 분할 가능하다.
 * SAVEPOINT는 여러 쿼리를 수행하는 트랜잭션의 경우 사용자가 중간중간 SAVEPOINT를 지정할 수 있다
 * SAVEPOINT를 쓰려면 취소하는 지점을 명시한뒤 그 지점까지 작업을 취소하는 식으로 사용하는데 이 지점을 SAVEPOINT라고 한다.
 * SAVEPOINT를 지정한뒤 Rollback to SAVEPOINT이름 ; 을 실행하면 해당 SAVEPOINT지점까지 처리한 작업이 롤백된다.
<img src="https://t1.daumcdn.net/cfile/tistory/99BFDC365ADE935908"/>

### 트랜잭션의 상태
<img src="https://t1.daumcdn.net/cfile/tistory/991020485ADE85BF0D"/> 
1) 활동 : 트랜잭션이 시작하였거나 실행중에 있는 상태.
2) 부분완료 : Commit연산이 실행되기 직전의 상태로 마지막 명령을 수행한 직후의 상태라고도 볼수 있다
3) 완료 : 트랜잭션이 성공적으로 종료되 Commit연산을 실행한 후의 상태
4) 실패 : 트랜잭션이 실행에 오류가 발생하여 중단된 상태
5) 철회 : 트랜잭션이 비정상적으로 종료되어 Rollback연산을 수행한 상태

### 동시성 제어
**https://mangkyu.tistory.com/30 게시글로 공부후 복기**

* 다중 사용자 환경에서 둘 이상의 트랜잭션이 동시에 수행될때, 일관성을 해치지 않도록 트랜잭션의 데이터접근을 제어하는것.
* 다중 사용자 환경을 지원하는 DBMS의 경우 반드시 지원해야 하는 기능이다.
> 만약 2개이상의 트랜잭션이 하나의 값에 접근하는 경우 둘다 읽기만하면 문제가 되지 않지만 트랜잭션1은 읽고 2는 쓴다면? 상황에 따라 '더티리드', '반복 가능하지 않은 조회', '팬텀리드'문제가 발생하게 되고 또한 둘다 쓰게된다면? 수정손실, 모순성, 연쇄복귀등의 문제가 발생할 수 있다.

<img src="https://t1.daumcdn.net/cfile/tistory/9968854D5A2F9E5E02"/>

 #### 수정 손실 (LOST Update)
 * 트랜잭션1이 갱신한 내용을 트랜잭션2가 다른값으로 덮어씀으로써 수정이 무효화가 되는것을 의미한다.
 * 두개의 트랜잭션이 한개의 데이터를 동시에 수정할떄 발생한다.
 * DB에서 절대 발생하면 안되는 현상
 
 > 수정손실은 하나의 값에 계속해서 덮어쓰기하여 데이터 갱신이 무효화 되는 현상이다. x= 1000 이고 트랜잭션1은 X+=300, 트랜잭션2는 x-=500이라고 하때 동시성제어를 해주지 않으면 1000이라는 값이 트1에 의해 1300이 된 상태에서 트2가 아직 1300으로 기록되지 전인 x=1000을 조회하여 1300-500이 아닌 1000 -500을 수행해 결국 800이어야 하는 값이 500이 되버리는 +300이라는 **연산의 값이 소실되버리는 현상을 갱신손실(수정손실)**이라고 한다.
 
 #### 모순성
 * 다른 트랜잭션들이 해당 항목 값을 갱신하는 동안 한 트랜잭션이 두개의 항목 값중 어떤것은 갱신되기 전의 값을 읽고 다른것은 갱신된 후의 값을 읽게 되어 데이터의 불일치가 발생하는 

> 초기값 x=150, y=100이 있고 트랜잭션T1은 x,y를 30씩 증가, T2는 x,y를 3배씩 증가시킨다.T1이 수행시 x,y는 각각 180,130이 되야 하지만 x의 값을 180으로 증가시키고 기록한다음 y를 수행하는것이아닌 T2가 수행된다면 x,y는 540,300이 되어버리고 T1의 y를 조회하는 과정에서 100이 아닌 300이 조회되버린다. 이렇게 **어떤 값을 갱신 전의 값을, 다른값은 갱신후의 값을 읽어 데이터가 불일치하는것을 모순성**이라고 한다.
 
 #### 연쇄복귀
 * 두 트랜잭션이 동일한 데이터 내용을 접근할 때 발생
 * 한 트랜잭션이 데이터를 갱신한 다음 실패하여 Rollback연산을 수행하는 과정에서 갱신과 Rollback연산을 실행하고 있는 사이에 해당 데이터를 읽어서 사용할때 발생할 수 있는 문제이다
 
 > 초기값 x=1500 ,y=1000과 x를 300 증가시키고 y를 200 감소시키는 트랜잭션T1과 x를 3배 증가시키는 T2가 있다고 할때 T1이 x를 300 증가시키고 기록하여 1800이 된 상황에서 T2 트랜잭션이 실행되어 x를 3배하여 기록한후 종료되버리면 T1이 Rollback 연산을 하여 x를 1500으로 돌려놓으려고 해도 T2가 실행후 커밋되어버렸기 때문에 원래 상태로 돌아갈수 없게 되버리는 문제가 발생하고 이것을 연쇄복귀라고 한다.
 

### 트랜잭션 스케줄
* 직렬 스케줄
* 비직렬 스케줄
* 직렬가능 스케줄
> 트랜잭션들은 삽입,수정,삭제 등과 같은 연산들로 이루어져 있는데 여기서 트랜잭션 스케줄이란 그 연산들의 실행 순서를 의미한다. 
> 직렬 스케줄은 트랜잭션의 연산을 모두 순차적으로 실행하는 것이다. 그러므로 하나의 트랜잭션이 실행되면 해당 트랜잭션이 완료되야함 다른 트랜잭션이 실행될수 있다. 다만 성능이 떨어지게 된다. 
> 비직렬 스케줄은 트랜잭션 순서와 상관없이 병행수행하는 스케줄을 의미한다. 그러므로 한 트랜잭션이 진행중이어도 다른 트랜잭션도 실행될수 있다.
> 마지막 직렬 가능 스케줄은  서로 영향을 주지 않는 직렬스케줄을 비직렬적으로 수행하겠다는 것이다?
 * 두개의 트랜잭션이 Read 연산 만을 수행할 것이라면 상호 간섭이 없으며 연산 순서도 중요x
 * 두개의 트랜잭션이 같은 데이터항목에 접근하지 않는다면 상호 간섭이 없으며 연산 순서도 중요x
 * T1이 x에 write연산을 하고 T2가 x에 read또는 write연산을 한다면 실행순서는 중요하다.

### 락
 * 로킹(Locking) 기법 : 트랜잭션들이 동일한 데이터 항목에 대해 임의적인 병행 접근을 하지 못하도록 제어하는것.
 * 트랜잭션 T가 데이터항목 x에 대해 read(x) or write(x)연산을 수행하려면 반드시 lock(x) 연산을 해주어야한다.
 * 트랜잭션 T가 실행한 lock(x)에 대해서는 해당 트랜잭션이 종료되기 전에 반드시 unlock(x) 연산을 해주어야 한다.
 * 트랜잭션 T는 다른 트랜잭션에 의해 이미 lock이 걸려있는 x에 대해 다시 lock(x)을 수행하지 못한다.
 * 트랜잭션 T가 x에 lock을 걸지 않았다면 unlock(x)를 수행하지 못한다.

> 여러개의 트랜잭션들이 하나의 데이터로 동시에 접근하려고 할 때 이를 제어해주는 도구가 바로 lock이다. 락은 트랜잭션이 '읽기를 할 때 사용하는 공유락(LS, Shared Lock)'과 '읽고 쓰기를 할때 사용하는 베타락(LX, Exclusive Lock)'으로 나뉜다. 트랜잭션 T가 데이터항목 x에 대해서 공유락을 설정할 경우 트랜잭션 T는 해당 데이터 항목에 대해서 읽을 수 있지만 write 할 수 없다. 그리고 Read는 서로 영향을 주지 않으므로 다른 트랜잭션도 공유락이 설정된 x에 대해서 공유락을 동시에 설정할 수 있다. 트랜잭션 T가 데이터 항목 x에 대해서 베타락을 할 경우 트랜잭션 T는 해당 데이터 항목에 대해서 Read 할 수도 있고 write할 수도 있다. write는 영향을 주는 작업이므로 다른 트랜잭션은 베타락이 설정된 데이터항목x에 대해서 어떠한 lock도 할 수 없다.

 #### 공유락과 베타락을 사용하는 규칙
  * 데이터에 락이 걸려있지 않으면 트랜잭션은 데이터에 락을 걸수 있다.
  * 트랜잭션이 데이터 x를 읽기만 할 경우 공유락을 요청하고 읽거나 쓸 경우 베타락을 요청한다.
  * 다른 트랜잭션이 데이터에 공유락을 걸어둔 경우 공유락 요청은 허용하고 베티락은 허용하지 않는다
  * 다른 트랜잭션이 데이터에 베타락을 걸어둔 경우 공유락,베타락모두 허용하지 않는다
  * 트랜잭션이 락을 허용받지 못하면 대기 상태가 된다.

### 트랜잭션의 버퍼 관리자 & 버퍼 관리 정책
 * 데이터베이스 시스템은 보통 비휘발성 저장장치인 디스크에 데이터를 저장한다. 데이터베이스의 일부분은 메인 메모리에 유지되기도 한다. 
 * DBMS에서는 데이터를 고정길이의 페이지로 저장하며 페이지는 데이터가 입출력되는 단위가 된다.
 * 이렇게 데이터를 저장하고 있는 다량의 페이지들을 관리하는 모듈을 '페이지 버퍼관리자 or 버퍼 관리자'라고 한다. 
 * 버퍼관리자는 DBMS의 모듈중 일부이다. DBMS는 크게 질의처리기와 저장시스템으로 구성되어 있으며 버퍼 관리자는 저장시스템 구성의 일부이다. (저장시스템은 DB엔진(innoDB,myisam등)같은 것)
 * 버퍼 관리자는 버퍼 관리 정책에 따라 트랜잭션의 UNDO복구와 REDO복구가 요구되거나 그렇지 않게 된다.

### 회복
1) 회복
> 회복은 트랜잭션을 실행하는 도중 장애가 발생하여 데이터베이스가 손상되었을 경우 손상되기 이전의 상태로 복구하는 작업으로서 데이터베이스를 관리하는데 있어 매우 중요한 기법이다. 다만 데이터베이스 자체가 손상이 되면 복구가 어렵다.
2) 중복저장기법
> DBMS는 데이터베이스에 포함된 정보를 시스템 내에 별도로 중복 저장해두었다가 장애발생시 이 정보를 이용하여 회복시킨다
 1) 덤프 : 주기적을 데이터베이스 전체를 다른 저장장치에 복제해두는 기법이다.
 2) 로그 : 데이터베이스가 변경될때마다 변경되는 데이터 항목의 이전값,이후값을 별도로 기록하는 기법이다.
3) 회복의 원리 
 1) Redo(재수행) : DBMS에서 이루어지는 작업은 REDO log에 기록된다.(이 기록엔UNDO의 내용도 포함된다) 시스템이 장애가 발생할 경우 **Redo log에 기록된 내용을 기반으로 check point 장애지점까지의 DB 버퍼 캐시를 복구**하게 된다 즉 복구를 위해 log기록을 재실행하는 행위가 'REDO' 이다. 이과정이 완료되면 UNDO 과정을 통해 commit되지 않은 데이터를 복구한다. 
 2) UNDO(ROllback) : 수정된 페이지들은 버퍼 교체 알고리즘에 의해 디스크에 출력되고 버퍼는 버퍼의 상태에 따라 교체된다.
  1) 트랜잭션이 실행되면 수정된 페이지들이 디스크에 출력될 수 있는 상태가 되어야 한다.
  2) 트랜잭션이 진행되며 수정한 페이지들도 디스크에 출력될 수 있기 때문에 중간에 트랜잭션이 실패한 경우 변경된 페이지들은 원상복구 되어야 한다. 
 * 이렇게 진행중이던 트랜잭션 과정을 원상태로 복구시키는 과정을 UNDO라고 한다.
 * UNDO의 정책은 두가지로 나뉘어진다
  1) 수정된 페이지를 언제든지 디스크에 쓸 수 있는 정책
  2) 수정된 페이지들을 최소한 트랜잭션 종료시점까지는 버퍼에 유지하는 정책
 * 2)번이 편하긴 하지만 많은 양의 버퍼가 필요하게 되므로 메모리 문제가 발생해 DBMS는 1)번 정책을 상ㅇ한다 
4) 회복 기법의 종류
> 회복 기법에는 즉시갱신(Immediate Update), 지연갱신(Deferred Modification), 검사 시점(Check Point) 총 3개의 기법이 있다.
 1) 즉시 갱신
 > 즉시 갱신은 트랜잭션이 연산을 실행하고 있는 활동 상태에서 데이터의 변경 결과를 데이터베이스 즉시 반영하는 기법이다. 
 
 | 트랜잭션 | 로직 |
 |---|---|
 | T1: | Read(A) -> A = A -100 -> Write (A) Read (B) -> B = B + 100 -> Write(B) |
 | T2: | Read(C) -> C = C - 200 -> Write(C) |
 
 * T1 
  * A를 읽어 온다 (A=1000)
  * 1000 - 100 의 값을 A에 저장
  * 1000 - 100 이 계산값을 기록 
  * B를 읽어 온다 (B = 2000)
  * 2000 + 100의 수행값을 B에 저장
  * 2000 + 100의 계산값을 기록
 * T2 
  * C를 읽어온다 (C에 들어 있는 값은 3000이라고 가정)
  * 3000 - 200의 수행값을 다시 C에 넣는다
  * 3000 - 200 이 계산된 값 2800을 기록한다
 
  |---|---|
  | 로그파일 | <T1, start> -> <T1,A,1000,900> -> <T1,B,2000,2100> -> <T1,Commit> -> <T2,start> -> <T2,C,3000,2800> -> <T2,commit>| 
  
  * 로그파일에는 위와 같이 T1,T2가 수행한 연산을 기록하는데 T1수행 내용을 Commit명령으로 로그에 기록하고 또 T2의 연산 결과를 Commit명령으로 로그에 기록하는 원리 이다. 
  **즉 그때 그때 마다 나온 연산의 결과를 로그파일에 기록해 하고 데이터베이스에 저장하는 것을 즉시 갱신이라고 한다.**
  다만 커밋 발생 이전의 갱신은 원자성이 보장되지 않기 때문에 장애발생시 UNDO필요 
 
 2) 지연 갱신
 > 지연갱신은 트랜잭션이 실행되는 동안 변경된 내용을 로그에 보관하다가 트랜잭션의 부분완료 시점에 저장되는 방법이다. 
  * 트랜잭션의 부분 완료 상태에선 변경 내용을 로그 파일에만 저장한다.
  * 커밋이 발생하기 전까진 데이터베이스에 저장하지 않는다
  * 중간에 장애가 발생하더라도 데이터 베이스에 기록되지 않았으므로 UNDO가 필요없음

 3) 검사점 회복 기법
  * 체크포인트 회복 기법이라고도 한다
  * 트랜잭션이 실행하는 동안 변경 내용이나 시스템 상황등의 정보와 함께 검사시점을 주기적으로 로그에 보관하다가 장애 발생시 로그내의 가장 최근의 검사시점으로부터 회복작업을 수행한다.
  *  로그 전체를 조사할 필요가 없으므로 회복시간을 단축 시킬수 있다. 
 4) 그림자 페이징
  * 그림자페이징은 로그를 이용하지 않는다.
  * 트랜잭션이 실해되는 동안 데이터베이스를 일정 크기의 페이지와 그 복사본인 그림자 페이지로 보관하는 기법이다. 
  * 데이터 변경시 현 페이지 테이블만 변경하며 회복시 현 페이지 테이블을 그림자 페이지 테이블로 대체한다

 ### 트랜잭션의 격리 상태
 
  #### dirty read (커밋되지 않은 데이터 쓰기)
   * 만약 사용자 a가 db의 product 테이블에 product를 1개 추가후 cnt값도 추가한다고 가정할때
   1) a가 product를 1개 추가하는 insert쿼리를 날린다.
   2) 이제 cnt값을 1 늘리는 update쿼리는 날려야 하는데
   3) 사용자 b가 중간에 product개수를 조회하니 2가 나온다.
   4) 마찬가지로 cnt값을 조회했는데 1이 나온다?
   5) 이후 a가 cnt값을 1늘리는 update쿼리를 날렸지만 이미 b는 데이터 무결성이 꺠졌다고 판단한다.
   6) 또한 a의 작업이 롤백된다면 데이터의 정확성또한 떨어진다.
   > 즉 생성,갱신,삭제중에 커밋되지 않은 데이터 조회를 허용함으로써 트랜잭션이 종료되면 더이상 존재하지 않거나 롤백되었거나, 저장 위치가 바뀌었을 수도 있는 데이터를 읽어들이는 현상이다.
  #### dirty write (커밋되지 않은 데이터 덮어쓰기)
   * 만약 사용자 a가 db의 product 테이블에 기존 product p1,p2의 회사명을 'A'로 바꾸려고 한다고 할때
   1) a가 p1의 회사명을 A로 바꾸는 update쿼리를 날린다
   2) 그런데 b가 갑자기 p1의 회사명을 B로 바꿔버린다
   3) 또 b가 p2의 회사명도 B로 바꿔버린다
   4) 이후 원래대로 a가 p2의 회사명을 A로 바꾼다
   5) 기존에 a가 기대하던 값은 p1,p2의 회사명이 A인것이지만 실제론 p1 = B ,p2 = A가 되어있다
   6) 또한 b역시 기대하던 값은 p1,p2의 회사명이 B인것이지만 실제론 p1 = B ,p2 = A가 되어있다

  #### 반복 불가능 읽기(Non-repeatable Read)
   * 트랜잭션1이 데이터를 읽고 트랜잭션2가 데이터를 update하고 트랜잭션1이 다시 한번 데이터를 읽을 때 생기는 문제
   * 트랜잭션 1이 읽기 작업을 다시 한번 반복할 경우 이전의 결과와 다른 결과가 나오는 현상
   > 만약 product p1의 갯수가 3인 상황에 트랜잭션 t1이 p1을 조회해쓸때 3이 나오는데 이때 t2가 값을 5로 바꾸어버리고 t1이 다시 p1을 조회하게 되면 5가 조회되어 바로전 읽은 값이 달라져 버리는데 이것을 '반복불가능 읽기'라고한다

 #### 팬텀 리드 (Phantom Read)
  * 트랜잭션1이 데이터를 읽고 트랜잭션2가 데이터를 쓰고 트랜잭션1이 다시 한번 데이터를 읽을 때 생기는 문제
  * 트랜잭션 1이 읽기 작업을 다시 반복할 경우 이전에 없던 데이터(유령데이터)가 나타나는 현상이다.
 > 만약 product는 p1만 있는 상황에 트랜잭션 t1이 product를 조회하면 p1만 나오는데 이때 t2가 product에 p2를 insert하고 t1이 다시 product를 조회하면 p1,p2가 나오는데 p2는 방금전 조회엔 없었던 데이터고 이것을 '팬텀리드'라고 한다.


 > 트랜잭션의 네가지 주요 성질인 원자성,일관성,고립성,영속성 고립성(격리성)을 구현하는 개념이다. 격리수준은 각기 다른 트랜잭션들이 서로에게 어느정도 격리 되어 있는지를 나타낸다.
* 여러 클라이언트가 같은 데이터에 접근할 때 문제 발생. 더티리드, 반복불가능읽기, 팬텀리드와 같은 문제를 직면할 수 있다. **그래서 Lock보다는 완화된 방법으로 트랜잭션을 동시에 실행시키면서 발생하는 문제를 해결하기 위해 DBMS가 제공하는 명령어**가 바로 트랜잭션 격리수준이다.
* 가장 쉬운방법은 트랜잭션을 순서대로 실행하는 것이다. 이 방법은 동시접근 문제는 아예없지만 한번에 한개의 트랜잭션만 처리하므로 성능(처리량) 저하가 가능하다
* 이에따라 데이터 베이스틑 4가지의 격리수준을 지원한다
<img src="https://t1.daumcdn.net/cfile/tistory/99958E475A2FEAB22C"/>

 #### Read Uncommitted
 * 잠금을 일정 실행하지 않아 미처 커밋되지 않고 트랜잭션이 진행중인 기록조차도 조회할 수 있도록 하는 격리 수준이다. 네가지 격리 수준중 트랜잭션의 고립성을 가장 덜 구현하는 가장 느슨한 형태다
 * Read Uncommitted는 더티리드를 유발한다. 대신 DB나 페이지, 열등에 잠금을 유지하는데에 드는 간접비용이 제일 적고 교착 상태에 빠질 위험이 적어 성능은 빠르고 우수하다.
 결론 => 
  1) 데이터 무결성을 위해 되도록 이면 사용하지 않는 것이 이상적이다.
  2) 사용하더라도 갱신되지 않을 과거자료 열람이나 거대한 양의 데이터를 어림잡아 집계하는 데에만 사용하는게 바람직하다.

 #### Read Committed
 * 고립 수준이 1 인 명령어로  커밋이 완료된 데이터에 대해서만 조회를 허용한다. 여러 RDBM에서 기본값으로 설정되어있다. mysql은 x.
 * 더티리드가 방지된다
 * 팬텀 리드와 반복 가능하지 않은 조회가 발생할 수 있다.
 * mysql의 innoDB에서는 행 단위로 잠가 교착 상태를 최대한 방지한다.
 > 커밋한 값만 읽는 만큼 더티리드 현상은 방지되지만 같은 조회 명령문의 다른 조회 결과를 불러오는 팬텀리드가 발생할 수 있다.  
 결론 => 
  1) 더티리드를 방지할수 있다는 점에서 고립수준이 올라감
  2) 잠금이 발생하는 만큼 속도나 성능에 있어서는 좀더 느려질수 있으며 교착상태도 벌어질수 있다
  3) 트랜잭션간 고립성을 완정히는 보장하지 못해 팬텀리드, 반복가능하지 않은 조회 등이 여전히 발생할 수 있다.
  4) 이는 일반 웹 애플리케이션 구동에는 큰 문제가 없을수 있어도 은행계좌 정보 조회처럼 각 트랜잭션의 정확도가 생명이라면 적합하지 않다.
 <img src="https://t1.daumcdn.net/cfile/tistory/9950383F5A2FEEB209"/>
 
 #### Repeatable Read
 * 고립수준이 2 인 명령어로 자신의 데이터에 설정된 공유락과 배타락을 트랜잭션이 종료될때 까지 유지하여 다른 트랜잭션이 다신의 데이터를 갱신할수 없도록 한다.
  * select시(공유락시) 특징 : 멀티버전 동시성제어라는 것을 통해 특정 시점의 데이터베이스 스냅샷을 남긴다. 그러면 쿼리문은 그 시점과 그 이전의 모든 변경점을 보고 반영한다. 쿼리문은 그 이후의 트랜잭션은 반영하지 못하지만 현재 그 쿼리문이 담긴 트랜잭션내의 다른 명령문은 볼수 있다.(if 트랜잭션 상단에서 update문을 실행했으면 아직 커밋이 일어나지 않았음에도 밑의 select문은 update가 반영된 기록을 조회한다.) 쿼리를 마치고 커밋을 함으로써 최신 스냅샷을 사용할 수 있다.
  * update나 delete시(베타락시) : Repeatable Read는 Read Committed와 달리 작업을 수행하지 않은 열도 잠근다. 커밋이나 롤백이 일어나기 전까지 모두 잠겨있다. 커밋이나 롤백이 일어나기 전까지 잠겨있다
 결론 =>
  1) 반복가능하지 않은 조회를 방지할 수 있다는 점에서는 Read Committed의 단점을 보완한다.
  2) 잠금이 적용되는 범위가 더욱 넓어져 성능과 속도가 느려진다
  3) 원래는 팬텀리드도 발생하지만 mysql의 innoDB는 멀티버전 동시성 제어를 통해 팬텀리드도 어느정도 극복한다.
  
 <img src="https://t1.daumcdn.net/cfile/tistory/995996435A2FF24F3C"/>

 #### Serializable
 * 고립수준이 3 인 가장 높은 명령어로 실행중인 트랜잭션은 다른 트랜잭션으로 부터 완변하게 분리되어 가장 높은 고립성을 띄지만 동시성과 성능은 그만큼 낮아진다. 작
 * 작업중인 트랜잭션이 완전히 종료될때 까지 다른 어떤 작업도 허용하지 않아 더티리드, 반복가능하지않은 조회, 팬텀리드를 완벽히 방지한다.

==> 어렵고 햇갈린다..

## 데이터베이스 이상현상(anomaly)
> 이상이란 테이블에서 일부 속성들의 종속이나 데이터중복으로 인해 데이터 조작시 불일치가 발생하는 것을 말한다. 즉, 테이블을 설계할때 잘못 설계하여 데이터를 삭제,수정,삽입 할때 논리적으로 오류가 생기는 것을 말한다. 대부분의 경우 데이터 중복때문에 발생하는데 이런 이상을 줄이기 위해 정규화를 진행한다.
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcbQKYI%2FbtqHGTyd46J%2FR3OvsR371XQeWYZAqwmHek%2Fimg.png"/>

이상의 종류에는 삽입이상, 삭제이상, 갱신이상이 있다.
 1) 삽입이상 : **튜플을 삽입할때 의도하지 않은 데이터까지 삽입해야만 튜플을 테이블에 추가할 수 있는 현상**이다. 강의를 아직 수강하지 않은 새로운 학생을 삽입할 경우 강의 코드속성에는 null값이 들어가야 하는 문제가 생긴다.  결국 강의코드는 외래키이기 때문에 외래키에 null이 입력될수 없고 '미수강' 같은 코드를 만들어야 삽입이 가능해져 버린다.
 2) 갱신이상 : **중복된 데이터중 일부만 수정되어 데이터 모순이 일어나는 현상**이다. 강의코드가 'AAC3'인 서준호의 전화번호를 수정할 경우 3번쨰 튜플의 데이터만 수정되지만 3,4는 같은 사용자 데이터임에도 불구하고 전화번호가 달라져 버린다.
 3) 삭제 이상 : **어떤 정보를 삭제하면 유용한 다른 정보까지 삭제되어 버리는 이상이다.** 강의코드가 AAC1인 데이터베이스 개론 강의를 삭제하게 되면 김영호 학생의 데이터까지 삭제되어 버린다.
 => 데이터 정규화가 필요한 대표적 이유중 하나이고 개인적으로 갱신 이상이 제일 치명적이라고 생각한다. 

## SQL vs NOSQL
### SQL(구조화된 쿼리언어)
> sql을 사용하면 관계형 데이터베이스 관리시스템에서 데이터를 저장,수정,삭제,검색 가능하다.
 * 특징
  * 데이터는 정해진 데이터 스키마를 따라 db테이블에 저장된다
  * 데이터는 관계를 통해서 연결된 여러개의 테이블에 분산된다.
 * 엄격한 스키마
  * 데이터는 테이블에 레코드로 저장되며 각 테이블에는 명확하게 정의된 구조가 있다
  * 구조 : 어떤 데이터가 테이블에 들어가고 어떤 데이터가 그렇지 않음을 정의하는 필드 집합
  * 구조는 필드의 이름과 데이터의 유형으로 정의
  * 관계형DB에서는 스키마를 준수하지 않는 레코드는 추가할 수 없다. 즉, 더 많은 필드를 가지고 싶다면, 다른 테이블을 만들어 넣거나, 스키마를 뜯어 고쳐서 필드에 추가해야한다.
 * 관계
  * 데이터들은 여러개의 테이블에 나누어서, 데이터들의 중복을 피할 수 있다. 
  * 만약 사용자가 구입한 상품들을 나타내기 위해서는 user,product,order 같은 여러 테이블을 만들어야 하지만 각각 테이블들은 다른 테이블에 저장되지 않은 데이터만을 가진다.(중복데이터가 없다).
  * 하나의 테이블에서 중복없는 하나의 데이터만을 관리하기 때문에 다른 테이블에서 부정확한 데이터를 다룰 위험이 없다(정규화로 인한 중복 컬럼이 없어 테이블간 독립성 유지)
### NOSQL
> nosql은 기본적으로 sql과 반대되는 접근 방식을 따른다
 * 스키마 없음
 * 관계없음
 * sql에서 데이터는 레코드라고 하지만 nosql에선 문서(document)라고 부른다.
 * sql에서는 정해진 스키마를 따르지 않으면 데이터를 추가할 수 없지만 no-sql에서는 다른 구조의 데이터를 같은 컬렉션(테이블)에 추가할 수 있다
 * nosql의 문서는 json데이터와 비슷한 형태를 가지고 있다. 일반적으로 관련 데이터를 동일한 컬렉션에 넣는다(sql처럼 여러 테이블에 나누어 담지 않는다). 즉 관계형 db에서 사용한 user,product정보 또한 orders에 포함하여 한번에 저장한다.
 * 이러한 방식은 데이터가 중복되기에 불아정한 측면이 있다. User,product에는 orders정보가 동시에 들어가는데 user의 order정보만 바뀔경우 user과 product의 동일한 order정보에 무결성이 깨진다.
 * 즉 데이터를 같이 사용하는 컬렉션에서 똑같은 데이터 업데이트를 수행하도록 해야한다.
 * 그럼에도 이러한 방식의 커다란 장점은 복잡한 조인을 사용할 필요가 없다는 것이다.
 * 특히 자주 변경되지 않는 데이터일때 더 큰 장점이 있다.

### 비교
#### 수직적 확장
 * db서버의 성능 확장( ex. CPU업그레이드 등)
 * sql,nosql 둘다 가능
#### 수평적 확장
 * 데이터가 관계적으로 저장되기에 sqldb는 수평적 확장은 지원하지 않는다 
 * nosql만이 수평확장을 지원한다
 * 더많은 서버가 추가,db가 전체적으로 분산됨

### 장점
* sql
 * 명확하게 정의된 스키마 : 데이터 무결성 보장
 * 관계는 각 데이터를 중복없이 한번만 저장
* nosql
 * 스키마 없기에 훨씬 유연, 언제든지 저장된 데이터를 조정하고, 새로운 필드 추가 가능
 * 데이터의 저장은 앱이 필요한 부분에 유동적으로 저장 => 속도 빨라진다.
 * 수직,수평 확장 가능함으로 db가 앱에서 발생하는 모든 읽기/쓰기 요청 처리가능
### 단점
* sql 
 * 덜유연, 데이터 스키마는 사전에 계획되고 알려져야함 (수정하기 매우 힘들다)
 * 관계를 맺기에 JOIN문이 많은 복잡한 쿼리 생성
 * 수평적 확장 불가, 수직적 확장만 가능. 즉, 어느 시점에서 확장의 한계에 직면
* nosql
 * 중복된 데이터가 변경된 경우 여러개의 컬렉션에서 데이터를 바꿔야 한다.  
 * 데이터 중복을 계속업데이트 해야한다.

* sql 데이터베이스 사용이 더 좋을때
 * 관계를 맺고 있는 데이터가 자주 변경되는 어플리케이션의 경우
 * 변경될 여지가 없고, 명확한 스키마가 사용자와 데이터에게 중요한 경우
* nosql 데이터베이스 사용이 더 좋을때
 * 정확한 데이터 구조를 알 수 없거나 변경/확장 될 수 있는 경우 
 * 읽기를 자주 하지만, 데이터 변경은 자주 없는경우
 * 데이터베이스를 수평으로 혹장해야 하는 경우 
 
 **완정한 정답이아닌 결국 둘다 '설계를 재대로해서 단점을 없앨수 있다'**

## 데드락(교착상태)
* 데이터베이스에서 교착 상태란 **여러개의 트랜잭션들이 실행하지 못하고 서로 무한정 기다리는 상태**를 의미한다.
* 기본적으로 데이터베이스에서는 트랜잭션들의 동시성을 제어하기 위해 로킹(Locking)을 사용한다.로킹으로 데이터가 꼬이는걸 예방해주지만 그 부작용으로 교착상태를 일으킬수 있다.
* 교착 상태 해결 방법은 크게 예방기법과 회피기법이 있다
1) 예방기법
  * 각 트랜잭션이 실행되기 전에 필요한 데이터를 모두 로킹해주는 것이다.
  * 다만 필요한 모든 데이터를 전부 로킹해야 함으로 트랜잭션의 병행성을 보장하지 못한다 
  * 또한 몇몇 트랜잭션은 계속해서 처리하지 못하는 기아상태가 발생할 수 있다
2) 회피기법
  * 자원을 할당할때 시간 스탬프를 사용하여 교착 상태가 일어나지 않도록 회피하는 방법이다. 
  * Wait-Die방식과 Wound-Wait 방식이 있다.
    * Wait-Die방식 : 트랜잭션 T1가 T2에 의해 로킹된 데이터를 요청할떄 T1이 먼저들어온 트랜잭션이 라면 기다리고 T1이 나중에 들어온 트랜잭션이라면 포기(Die)하고 나중에 다시 요청한다 다른 트랜잭션이 데이터를 점유하고 있을때 기다리거나(Wait) 포기(Die)하는 방식이다.
    * Wound-Wait 방식 : 트랜잭션 T1가 T2에 의해 로킹된 데이터를 요청할떄 T1이 먼저 들어온 트랜잭션이라면 데이터를 선점(Wound)하고 반면 T1가 나중에 들어온 트랜잭션이라면 기다린다.(Wait) 즉 다른 트랜잭션ㅇ 데이터를 점유하고 있을때 뺴앗거나(Wound) 기다리는(Wait) 방식이다.
