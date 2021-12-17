# Database
<h3>RDBMS가 확장성이 용이하지 '않는' 이유</h3>

 1. Column이 추가됐을 때, 기존 테이블에 들어있는 데이터들에 대해서 추가된 Column 값을 채워줘야 한다. 이 때, 기존 테이블에 있는 데이터들의 개수가 10억건이라면? -> 굉장히 비효율적!
 
 > **Solution** 1. 기존 테이블에 Column을 추가하는 것이 아닌, 기존 테이블 + 별도로 추가된 Column의 테이블을 만들어 관리한다.
 
 2. 새로운 테이블을 하나 더 만들었을 때, 기존 테이블들과의 관계를 맺어줘야하기 때문이다.

---

<h3>RDBMS vs No-sql</h3>
1. Sale up 방식의 차이

- **Vertical(RDBMS) vs Horizontal(No-sql)**
  - 비유) 4인승 소나타(Server)가 있다. 여행을 가는데 8명의 친구가 차량에 탑승해야 하는 상황이다.
    - Vertical Scale up : 8인승 카니발 1대를 새로 구입한다.
    > Transaction의 ACID 성질을 보장한다.
    
    > machine의 수가 아닌, machine의 성능을 높이는 방식이다.
    
    - Horizontal Scale up : 4인승 소나타 1대를 더 구입한다.
    > data set을 나누고 multiple surver로 data를 분산한다. 
    
    > 각 서버들은 database에 독립적이다.
    
    > Vertical scaling은 power와 memory 증가에 집중한 반면, Horizontal Scaling은 machine의 수의 증가에 집중한다.
    
    > 인스타그램을 예시로 들면, 하나의 서버는 User Profile 정보를 저장하고 또 다른 서버는 스토리와 hightlihgt, 그리고 또다른 서버는 이미지를 저장한다.


  - Vertical Scale up
    - 장점
      1. 정해진 스키마에 따라 데이터가 저장되므로 명확한 데이터 구조를 보장한다.
    - 단점
      1. 테이블 간 관계를 맺고 있기 때문에 시스템이 커질 경우 JOIN문이 많은 복잡한 쿼리가 만들어질 수 있다.
      2. Vertical Scale up으로 인해 성능 향상 비용이 굉장히 비싸다.
      3. 스키마로 인해 데이터가 유연하지 못하고 스키마 변경이 어렵다.
  - Horizontal Scale up
    - 장점
      1. 스키마가 존재하지 않기 때문에 유연하고 자유로운 데이터 구조를 갖는다. 때문에 언제든 저장된 데이터를 조정하고 새로운 필드를 추가할 수 있다.
      2. 데이터 분산이 용이하며, Vertical Scaling에 비해 저렴하다.
      3. Downtime 확률이 더 적다. Maximum Load가 될 확률이 적기 때문에.

    - 단점
      1. 테이블 간 Join을 할 수 없다.
      2. Cosistency만 보장해주기 때문에, 동시에 발생하는 은행의 Transaction에 적절하지 않다.
      3. 각 기능을 서버별로 쉽게 분류할 수 없다. 때때로 이미지는 단일서버가 처리할 수 있는 것보다 더 많은 공간을 차지할 수 있다.


 ***Atomic Transaction이 필요하다면 Vertical Sacling, 중복성을 허용하고 Join이 less하다면 Horizontal Scaling이 유리하다.***
 
 :question: ***RDBMS, NoSQL 언제 사용해야 될까??***
 
   - RDBMS : 데이터 구조가 변경될 여지가 없고 명확한 스키마가 필요한 경우 사용한다. 또한 중복된 데이터가 없어 데이터 변경이 용이하기 때문에 관계를 맺고 있는 데이터가 자주 변경되는 시스템에 적합하다.

   - NoSQL : 정확한 데이터 구조를 정의하기 힘들고, 데이터가 변경/확장 될 수 있는 경우에 사용한다. 또한 데이터 중복이 가능하기 때문에 중복된 데이터가 변경될 시에는 모든 컬렉션(=SQL에서의 테이블)에서 수정을 해야 한다.  이러한 이유로 Update가 많이 이루어지지 않는 시스템에 적합하며 Horizontal Scale up이 가능하다는 장점을 활용해 대용량의 데이터를 저장해야하는 시스템에 사용하면 적합하다.

--- 

<h2>Index</h2>

<h3>Clusterd Index vs Non-Clustered Index</h3>

https://lalwr.blogspot.com/2016/02/db-index.html


- Clustered Index
 > 테이블 당 1개만 가질 수 있다. 
 
 > Non-clusted Index와는 달리, Clustered Index를 기준으로 물리적으로 행을 정렬한다.
 
 > data가 update 되거나 insert 될 때마다 물리적으로 row를 정렬한다. 때문에 매번 update or inserrt 시, 정렬 비용이 발생하므로 잦은 insert, update 시 성능 이슈가 발생한다. 그러나, **read-only application**에 적용한다면 data를 빠르게 read 할 수 있으므로 이럴 경우엔 **clustered Index**를 사용하는 것이 좋다. 하지만, insert/update가 잦은 application엔 부적절하다.

 - Non-Clustered Index
  > 테이블 당 여러개의 Index를 가질 수 있다.
  
  > '이름', '생일'로 Non-clustered Index를 만들게 되면, 이것을 기준으로 Column들을 Indexing 해놓은 별도의 Index Page가 만들어진다. 그리고 이것 외의 Non-Clustered Index들을 구별하기 위해 Root Node가 만들어진다.
  
  > Root Node를 통해 '이름', '생일'로 Indexing한 Index Page의 정보를 얻고, 얻은 Index Page 정보를 통해 Data Node를 찾아가 해당하는 Row를 찾는다.
  
  > 책의 '주제별 인덱스', '단어 인덱스', '기능별 인덱스'와 같은 것들이 Non-Clusterd Index에 해당한다.
  
  > 매번 Database를 조회할 때마다 테이블 전체를 Scan하면 시간이 오래 걸리므로, 자주 사용하는 Column들을 묶어 Non-Clustered Index로 관리해 탐색 시간을 줄일 수 있다.
 

