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
      1. Single Server에 모든 데이터가 존재하기 때문에 Simple하고 관리가 용이하다.
    - 단점
      1. Multiple Query들을 동시에 수행하기 어렵다.
      2. 서버의 Maximum Load를 초과하면, Downtime(중단시간) 확률이 높아진다.
  - Horizontal Scale up
    - 장점
      1. Query는 특정한 서버에서 수행되기 때문에 server에 Load를 줄이고 better performanc를 준다.
      2. Vertical Scaling에 비해 저렴하다.
      3. Downtime 확률이 더 적다. Maximum Load가 될 확률이 적기 때문에.

    - 단점
      1. Cross-server communication이 포함될 수 있기 때문에 Join을 만들기 어렵다.
      2. Cosistency만 보장해주기 때문에, 동시에 발생하는 은행의 Transaction에 적절하지 않다.
      3. 각 기능을 서버별로 쉽게 분류할 수 없다. 때때로 이미지는 단일서버가 처리할 수 있는 것보다 더 많은 공간을 차지할 수 있다.
