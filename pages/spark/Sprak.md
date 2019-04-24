# 初学Spark
Spark: 大数据处理框架
## 1、安装


## 2、创建项目
### 方式一：maven创建
新建maven项目，加载如下maven依赖
```maven
 <!-- 引入spark包 start,需要与scala的jdk版本一致 -->
        <dependency>
            <groupId>org.apache.spark</groupId>
            <artifactId>spark-core_2.11</artifactId>
            <version>2.2.1</version>
            <exclusions>
                <exclusion>
                    <artifactId>httpclient</artifactId>
                    <groupId>org.apache.httpcomponents</groupId>
                </exclusion>
            </exclusions>
        </dependency>
        <dependency>
            <groupId>org.apache.spark</groupId>
            <artifactId>spark-sql_2.11</artifactId>
            <version>2.2.1</version>
        </dependency>
        <dependency>
            <groupId>org.apache.spark</groupId>
            <artifactId>spark-hive_2.11</artifactId>
            <version>2.2.1</version>
            <exclusions>
                <exclusion>
                    <artifactId>httpclient</artifactId>
                    <groupId>org.apache.httpcomponents</groupId>
                </exclusion>
            </exclusions>
        </dependency>
        <dependency>
            <groupId>org.apache.spark</groupId>
            <artifactId>spark-streaming_2.11</artifactId>
            <version>2.2.1</version>
            <scope>provided</scope>
        </dependency>
        <!-- 引入spark包 end -->
```
