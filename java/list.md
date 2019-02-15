# 集合类



### List 数组转换
#### List转换为Array
```text
ArrayList<String> list=new ArrayList<String>();
String[] strings = new String[list.size()];
list.toArray(strings);
```

#### 数组转换List
```text
String[] s = {"a","b","c"};
List list = java.util.Arrays.asList(s);
```