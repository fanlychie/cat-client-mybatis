> 对`MyBatis`进行拦截，并加入到`CAT`监控。

源码源自[CAT](https://github.com/dianping/cat)的[框架埋点方案集成/mybatis](https://github.com/dianping/cat/tree/master/框架埋点方案集成/mybatis)。源码改动内容有如下：

- [x] 构建成`Maven`项目
- [x] 重写`getSqlURL`方法
- [x] 修复SQL的URL`jdbc:mysql://unknown:3306/%s?useUnicode=true`的问题
- [x] 扩展支持常见的数据源`druid`、`dbcp`、`dbcp2`、`c3p0`、`HikariCP`、`BoneCP`

---

安装到本地仓库命令：

```sh
mvn clean install
```

客户端依赖声明方式：

```xml
<dependency>
    <groupId>com.dianping.cat</groupId>
    <artifactId>cat-client-mybatis</artifactId>
    <version>2.0.0</version>
</dependency>
```

---

或者使用我托管的仓库`fanlychie-maven-repo`直接声明依赖：

```xml
<repositories>
    <repository>
        <id>fanlychie-maven-repo</id>
        <url>https://raw.github.com/fanlychie/maven-repo/releases</url>
    </repository>
</repositories>
<dependencies>
    <dependency>
        <groupId>com.dianping.cat</groupId>
        <artifactId>cat-client-mybatis</artifactId>
        <version>2.0.0</version>
    </dependency>
</dependencies>
```

---

接入方式：

```xml
<bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
    <property name="dataSource" ref="dataSource"/>
    <property name="typeAliasesPackage" value="org.fanlychie.entity"/>
    <property name="configLocation" value="classpath:mybatis-config.xml"/>
    <property name="mapperLocations" value="classpath*:mapper/*.xml"/>
    <!-- MyBatis 接入 CAT -->
    <property name="plugins">
        <array>
            <bean class="com.wanda.cat.sample.plugins.CatMybatisPlugin"></bean>
        </array>
    </property>
</bean>
```

效果图：

![image](https://raw.githubusercontent.com/fanlychie/mdimg/master/cat-client-mybatis.png)