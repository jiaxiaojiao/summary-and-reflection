# String 字符串

#### 对比 String StringBuffer StringBuilder
```text
String 字符串长度不可变，底层使用final char[] value，不可以继承。
StringBuffer StringBuilder 字符串长度可变，底层使用char[] value，

拼接字符串
String 需要创建多个，效率低
StringBuilder  线程不安全，
Stringbuffer  线程安全，synchronized

效率 String < StringBuffer < StringBuilder
```

#### hashCode()  equals()
```text
hashCode() 相等，equals() 可能相等。
equals() 相等，  hashCode() 肯定相等。
```
