# 목차
[1. Java String](#java-string)

[2. IS-A vs HAS-A](#is-a-vs-has-a)

[3. Overriding vs Overloading](#overriding-vs-overloading)

[4. Java, Call by Value? Call by Reference](https://jackjeong.tistory.com/37)

## Java String
- Java에서 String은 char values의 sequence를 표현하는 Object(객체)이다. 
```
char[] ch={'j','a','v','a','t','p','o','i','n','t'};  
String s=new String(ch);  
```
is same as:
```
String s = "javatpont";
```
- The java.lang.String class implements Serializable, Comparable and CharSequence interfaces
- The CharSequence interface is used to represent the sequence of characters. String, StringBuffer and StringBuilder classes implement it. 
  It means, we can create strings in Java by using these three classes.
 - The Java String is **immutable** which means it cannot be changed. **Whenever we change any string, a new instance is created**. 
   For **mutable** strings, you can use **StringBuffer and StringBuilder classes.**

### How to creat a String object?
 1. By ***String literal***
    - Each time you create a string literal, the JVM checks the **string constant pool"** first.
    If the string already exists in the pool, a reference to the pooled instance is returned. If the string doesn't exist in the pool, a new string instance is created and placed in the pool. 
      - For example:
          ```
          String s1 = "welcome";
          String s2 = "welcome"; 
          ```
          > In the above example, only one object will be created. Firstly, JVM will not find any string object with the value "Welcome" in string constant pool, that is why it will           create a new object. **After that it will find the string with the value "Welcome" in the pool,** it will **not create a new object** but will **return the reference to             the same instance.**
          
          ***즉, s1과 s2는 같은 reference value of instance를 갖는다.***
          
          :point_right: **Note: String objects are stored in a special memory area known as the "string constant pool".**
          
          :point_right: Heap Memory 안에 string constant pool 공간이 있고 그 안에 **String object**를 저장!
          > 그럼 왜 Java는 String literal 컨셉을 사용하나?
          >> 만약 "string constant pool" 안에 이미 해당 문자열이 있다면, 새로운 object를 생성하지 않아도 되기 때문에 memory를 효율적으로 사용할 수 있기 때문이다!
               
 2. By ***new*** keyword 
    ```
    String s = new String("Welcome"): //creates two objects and one reference variable
    ```
    - In such case, JVM will create a new string object in normal (non-pool) heap memory, and the literal "Welcome" will be placed in the string constant pool. The variable s will refer to the object in a heap (non-pool).

 :pushpin: **결론** 
 - literal로 생성했을 때, 문자열이 같으면 변수명이 다르더라도 같은 참조값을 갖는다.
 - new String으로 생성했을 때, 문자열이 같아도 변수명이 다르면 다른 참조값을 갖는다.

## IS-A vs HAS-A
 ### IS-A
  - JAVA에서의 상속은 Parent Object의 behaviors, properties를 다른 object가 습득하는 mechanism이다.
    > JAVA의 상속 덕분에 parent class의 methods와 fields를 reuse 할 수 있다. 뿐만 아니라, new methods와 field를 추가해서 사용할 수 있다.

    :point_right: 상속(Inheritance)는 parent-child relationship으로 알려진, **IS-A relationshop**이다.
    
    :question: **Why use inheritance in Java?**
      1. For ***Method Overriding***(So, runtime polymorphism can be achieved)
      2. For ***COde Reusability***
 ### HAS-A
 - 만약 class가 entity reference를 가진다면, 이것은 Aggregation이다. Aggregation은 **HAS-A relationship**을 나타낸다.
    > 뭔소리냐구요..? 설명해드릴게요
  
  Employee object에 id,name, emailId와 같은 정보들이 있다고 가정합니다.
  
  이 Object는 'Address Object'(city, state, country와 같은 정보를 가진)를 포함하고 있습니다.
  ```
  class Employee{  
  int id;  
  String name;  
  Address address;//Address is a class  
  ...  
  }  
  ```
  :point_right: In such case, Employee has an entity reference address. **So relationship is Employee HAS-A address.**
  
  :question: **Why use Aggregation in Java?**
   
   - For Code Reusability
  
  
  > Example of Aggregation
  ```
  class Operation{  
    int square(int n){  
    return n*n;  
    }  
  }  
  
  class Circle{  
    Operation op;//aggregation  
    double pi=3.14;  
    
  double area(int radius){  
    op=new Operation();  
    int rsquare=op.square(radius);//code reusability (i.e. delegates the method call).  
    return pi*rsquare;  
  }  
  
     
    
  public static void main(String args[]){  
    Circle c=new Circle();  
    double result=c.area(5);  
    System.out.println(result);  
    }  
  }  
```

## Overriding vs Overloading
### Overriding과 Overloading이 무엇인가요?
  - 같은 calss 내 2개 이상의 같은 이름을 가진, **but different parameters**인 methodss, 이것이 **Overloading**이다.
  - In the parent class and child class, **the method signature(이름, 파라미터) are the same**. 이것이 **Overriding**이다.

### Overriding vs Overloading
 1. ***Overriding***은 **Runtime Polymorphsim**을 구현한다. 하지만, ***Overloading***은 **Compile time Polymorphism**을 구현한다.
 2. The method Overriding은 superclass와 subclass 사이에서 일어난다. Overloading은 같은 class 내의 method에서 일어난다.
 3. Overriding methods는 같은 signature(i.e name and method parameters)를 갖는다. Overloaded methods는 메소드명은 같으나, 파라미터가 다르다. 
    > Java 5.0 이전의 overriding method는 파라미터와 return type 둘 다 같아야 했지만, Java 5.0에선 ***covariant return type***을 도입했다.
    >> 이로 인해, overriding method는 same signature를 가져야 하지만, return type은 subclass를 가질 수 있다.
    >>> 즉, Subclass안에 있는 overriding method는 같은 signature를 갖는 superclass 함수의 return type의 subclass type을 return type으로 가질 수 있다.
    >>>> 단, 그 return type은 **Non-Primitive**이어야 한다.
      - Example
        ```
         부모 class의 display() function has return type ——- Object
         자식 class의 display() function has return type ——- String
  
        Just like every other class in Java, String class extends the Object class i.e. String is a sub-type of Object. 
        Hence we can use it as return type in overridden display() function instead of type Object as in Base class.
        ```
  
           :point_right: Basically 부모 class의 display() method has a covariant return type.
           
  4. With **Overloading**, 호출된 method는 **compile-time**에 결정된다. With **Overriding**, method call is determined at the **runtime** based on the object type.
  5. ***만약 overriding이 break 된다면***, 이것은 프로그램에 심각한 이슈를 발생시킨다. 왜냐하면 그 effect는 **runtime**에 보이기 때문이다. 
    
      ***반면에, overloading이 break 된다면,*** **compile-time**에 error를 발생시킬 것이고, 때문에 에러를 해결하기 더 쉽다.
          
        > [Compile time과 Runtime은 뭘까요??](#compile-time-and-runtime)


### Compile time and Runtime
 - Compile time 
    > At compile time, The java file is compiled by ***Java Compiler***(It does not interact with OS) and converts ***the Java code*** into ***bytecode.***
    
    Ex] Java Code(Simple.**java**) -> Java Compiler -> Byte Code(Simple.**class**)
    
  - Runtime
      
      런타임에서 다음과 같은 일들이 일어납니다!
      
       > Class File -> Classloader -> Bytecode Verified -> Interpreter -> Runtime -> Hardware
       
       - Classloader : class file들을 load하기 위해 사용하는 JVM의 subsystem.
       - Bytecod Verifier : 객체에 대한 접근 권한들을 위반하는지를 check.
       - Interpreter : bytecode stream을 읽고, 명령어들을 실행.

## 예외처리

## Static 
  -  메모리에 고정적으로 할당되어, 프로그램이 종료될 때 해제되는 변수
      > 일반적으로 우리가 만든 Class는 Static 영역에 생성되고, new 연산을 통해 생성한 객체는 Heap영역에 생성됩니다. 객체의 생성시에 할당된 Heap영역의 메모리는 Garbage Collector를 통해 수시로 관리를 받습니다. 하지만 Static 키워드를 통해 Static 영역에 할당된 메모리는 모든 객체가 공유하는 메모리라는 장점을 지니지만, Garbage Collector의 관리 영역 밖에 존재하므로 Static을 자주 사용하면 프로그램의 종료시까지 메모리가 할당된 채로 존재하므로 자주 사용하게 되면 시스템의 퍼포먼스에 악영향을 주게 됩니다
      
 :question: 언제 사용하면 좋을까?
 
  하나의 클래스에 ***여러번 사용되는 함수***들을 static 키워드를 이용해 관리한다.
  > Ex) Util

### Reflection

https://dublin-java.tistory.com/53

### equals(), hashCode()를 재정의해야하는 이유

https://jisooo.tistory.com/entry/java-hashcode와-equals-메서드는-언제-사용하고-왜-사용할까

