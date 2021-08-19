# Operating System

<h2>Process vs Thread</h2>

> 피자에 비유해보자!
>> 피자 레시피 <-> 프로그램 ( 코드로 이루어진 파일 )
>> 
>> 피자 레시피로 만든 피자 <-> 프로세스 ( 프로그램이 실행된 상태 )

---

### _Program이 Process가 되기 위해선, '메모리'에 올라가야하고 'PCB'가 만들어져야 한다.!_***

#### Process 메모리 구조

- ***Code*** : 실행 명령을 포함하는 코드들
- ***Data*** : Static 변수 혹은 Global 변수
- ***Heap*** : 동적 메모리 영역
- ***Stack*** : 지역변수, 매개변수, 반환 값등 일시적인 데이터

#### PCB 메모리 구조

- ***Pointer*** : Process의 준비상태, 대기상태의 큐를 구현하기 위한 구역
- ***Process State*** : 현재 Process 상태를 저장
- ***PID*** : Process의 고유 번호
- ***Program Count*** :: 다음 명령어를 가리킨다

