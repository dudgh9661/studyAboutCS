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
