#### HTTP 특성(비연결성, 무상태)과 구성요소 그리고 Restful API ####

[설명](https://webcache.googleusercontent.com/search?q=cache:CgSTegd2dUsJ:https://victorydntmd.tistory.com/286+&cd=1&hl=ko&ct=clnk&gl=kr)

#### Spring Framework ###

- DI란? 
  > DI는 '부품 조립'이라고 밀할 수 있습니다. 컴퓨터를 하나의 큰 프로그램으로 가정했을 때, 컴퓨터 부품 하나하나는 '객체'라고 볼 수 있습니다. 이 부품들은 서로 어떠한 관계를 갖고, 컴퓨터 정상적으로 동작시키기 위해 관계를 갖는 부품들끼리 조립해주는 것, 이것이 의존성 주입입니다. Spring Framework의 등장 이전에는 개발자들이 직접 코드를 수정하여 의존성 주입을 했지만, Spring Framework가 등장하면서 개발자들은 직접 코드를 수정하는 것이 아닌 XML, Annotaion을 통해 의존성 주입을 할 수 있게 되었습니다.
  
  
  ❓Spring Framework에서 생성자 주입을 권하는 이유는? [이유](https://jgrammer.tistory.com/entry/springboot-의존성-주입-방식-결정)
  
 
#### 끄적끄적 ####
  의존성을 바꿔줄 때, 소스코드 변경없이 XML을 이용한 설정만 바꾸면 바꿀 수 있었다. 이후, XML 대신 메타데이터인 '어노테이션'을 통해 더 편하게 설정을 바꿀 수 있게 되었다.
  
  Field Annotation : 기본생성자가 생성될 때 함께 주입된다. 때문에 Overloading 생성자는 있고 기본 생성자는 없을 때, Field Annotation을 사용하면 에러가 발생한다.
  
  Overloading 생성자 Annotation: Overloading 생성자 호출 시 함께 주입된다.
  
  Setter Annotation : Setter함수 호출 시 함께 주입된다.
  
  비록 기능적인 측면에선 다소 부족해보일 수 있으나, Web의 가장 기본적인 동작인 CRUD를 구현하는 과정을 통해 Spring Framework가 왜 탄생했고, 이것이 가진 강점이 무엇인지, 그리고 어떻게 동작하는지를 이해할 수 있었습니다. 이 과정은 이후 제가 Spring Framework를 사용하는 어떤 프로젝트에 투입됐을 때, 프로젝트 구조를 더 빠르게 이해하고 Spring Framework가 가진 강점을 통해 프로그램의 고도화를 이뤄내는 밑거름이 되어줄 것이라 생각합니다.
