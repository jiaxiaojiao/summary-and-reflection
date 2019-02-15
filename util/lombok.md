# Lombok
>Lombok 是一种 Java™ 实用工具。
 可用来帮助开发人员消除 Java 的冗长，尤其是对于简单的 Java 对象（POJO）。
 Lombok 采取的注解形式的，在编译后，自动生成相应的方法
## 步骤
- 添加依赖
```text
    <!-- 在 pom.xml 文件中添加相关依赖 -->
    <lombok.version>1.16.20</lombok.version>
    
    <!-- https://mvnrepository.com/artifact/org.projectlombok/lombok -->
    <dependency>
        <groupId>org.projectlombok</groupId>
        <artifactId>lombok</artifactId>
        <version>${lombok.version}</version>
        <scope>provided</scope>
    </dependency>
```

- 安装插件
>  为了IDE不报错，需要安装插件支持它
```text
IDEA :  File > Settings > Plugins > 搜索安装Lombok plugin 
```


## 常用的注解
```text
@Getter
@Setter
@ToString
@EqualsAndHashCode
构造函数
@AllArgsConstructor
会生成一个包含所有变量，同时如果变量使用了NotNull annotation ， 会进行是否为空的校验， 
全部参数的构造函数的自动生成，该注解的作用域也是只有在实体类上，参数的顺序与属性定义的顺序一致。
@NoArgsConstructor
无参构造函数
@RequiredArgsConstructor
会生成一个包含常量（final），和标识了@NotNull的变量 的构造方法。
```

### 使用注解
#### @Data
使用 @Data 注解就可以有下面几个注解的功能： @ToString、@Getter、@Setter、@EqualsAndHashCode、@NoArgsConstructor

#### @Slf4j
直接调用log

#### @Log
使用的是 java.util.logging.Logger ，直接使用 变量 log。

#### @Builder
bulder 模式构建对象

#### @Cleanup
自动化关闭流，相当于 jdk1.7 种的 try with resource
```text
@Cleanup 
InputStream in = new FileInputStream(args[0]);
@Cleanup 
OutputStream out = new FileOutputStream(args[1]);
```

#### @NonNull
```text
public NonNullExample(@NonNull Person person) {
    this.name = person.getName();
}
转换后：
public NonNullExample(@NonNull Person person) {
    if (person == null) {
        throw new NullPointerException("person");
    }
    this.name = person.getName();
}
```
#### @SneakyThrows
暗中抛出异常，当我们需要抛出异常，在当前方法上调用，不用显示的在方法名后面写 throw
```text
@SneakyThrows(Exception.class)
```
#### @Synchronized
>方法中所有的代码都加入到一个代码块中，默认静态方法使用的是全局锁，普通方法使用的是对象锁，当然也可以指定锁的对象。
```text
private final Object lock = new Object();
@Synchronized("lock")
public void foo() {
    // Do something
}
```