# log4j和log4j2的区别

1.配置文件类型 \
log4j是通过一个_.properties的文件作为主配置文件的，而现在的log4j 2则已经弃用了这种方式，采用的是_.xml，_.json或者_.jsn这种方式来做，可能这也是技术发展的一个必然性，毕竟properties文件的可阅读性真的是有点差。

2.核心JAR包 \
log4j只需要引入一个jar包即可，

```xml
<dependency>
    <groupId>log4j</groupId>
    <artifactId>log4j</artifactId>
    <version>1.2.17</version>
</dependency>
```

&#x20;

而log4j 2则是需要2个核心

```xml
<dependency>
    <groupId>org.apache.logging.log4j</groupId>
    <artifactId>log4j-core</artifactId>
    <version>2.5</version>
</dependency>
<dependency>
    <groupId>org.apache.logging.log4j</groupId>
    <artifactId>log4j-api</artifactId>
    <version>2.5</version>
</dependency>
```

&#x20;

&#x20;

大家发现没，log4j和log4j 2的包路径是不同的，Apache为了区分，包路径都更新了
