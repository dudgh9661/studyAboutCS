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
 1. By String literal //String s = "string";
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
               
 3. By ***new*** keyword
