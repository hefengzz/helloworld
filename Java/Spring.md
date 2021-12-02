# Spring

## 两大核心思想 IOC/AOP

学习Spring主要是学思想，Spring是一个轻量级的IOC和AOP的框架

## 1. Spring配置

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">

</beans>
```

### 1.1 beans.xml

在`Spring`中，所有的对象都由spring创建，管理，装配。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">

    <!--
        id: bean的唯一标识符，相当于对象名。
        class: bean 对象所对应的全限定名： 包名 + 类型
        name: 也是别名
     -->
    <bean id="hello" class="com.hefeng.pojo.Hello" name="hello" />

    <bean id="hello" class="com.hefeng.pojo.Hello">
        <!-- 通过set -->
        <property name="name" value="黑猫警长" />
<!--         通过下标赋值，实际上是通过有参构造，所以必须创建有参的构造方法 -->
        <constructor-arg index="0" value="java" />
<!--         通过参数赋值，实际上是通过有参构造，所以必须创建有参的构造方法 -->
        <constructor-arg name="name" value="你好Java" />
    </bean>

    <!-- 别名 -->
    <alias name="hello" alias="h1"/>
</beans>
```

### 1.2 applicationContext.xml

项目开发时，可能是多人协作开发的，所以会出现多个配置文件的情况，此时就可以通过`applicationContext.xml`将其它配置文件整合起来。

这样只需要读取一个配置文件，Spring可以管理所有的对象「beans」

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">

    <!-- 在一个项目中，可能是多人开发，可以通过applicationContext将其它配置文件合并起来，这样就只需要一个配置文件 -->
    <import resource="beans.xml" />
    <import resource="beans2.xml" />
    <import resource="beans3.xml" />
</beans>
```

## 2. 依赖注入

### 2.1 构造器注入

前面的Spring配置已经有案例

### 2.2 Set注入

- 依赖注入：Set注入！
  - 依赖：bean对象的创建依赖于容器
  - 注入：bean对象中的所有属性，由容器来注入

【环境搭建】

1. 复杂类型

   ```java
   public class Address {
       private String address;
   
       @Override
       public String toString() {
           return "Address{" +
                   "address='" + address + '\'' +
                   '}';
       }
   
       public String getAddress() {
           return address;
       }
   
       public void setAddress(String address) {
           this.address = address;
       }
   }
   ```

2. 真实测试对象

   ```java
   public class Student {
       private String name;
       private Address address;
       private String[] books;
       private List<String> hobbys;
       private Map<String, String> map;
       private Set<String> games;
       private String wife;
       private Properties info;
   }
   ```

3. 配置文件

   ```XML
   <?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://www.springframework.org/schema/beans
           https://www.springframework.org/schema/beans/spring-beans.xsd">
   
       <bean id="address" class="com.hefeng.pojo.Address">
           <property name="address" value="长沙" />
       </bean>
   
       <bean id="student" class="com.hefeng.pojo.Student">
           <!-- 1. 普通值注入 -->
           <property name="name" value="薇恩" />
   
           <!-- 2. bean注入 -->
           <property name="address" ref="address" />
   
           <!-- 3. 数组注入 -->
           <property name="books">
               <array>
                   <value>红楼梦</value>
                   <value>三国演义</value>
                   <value>水浒传</value>
                   <value>西游记</value>
               </array>
           </property>
   
           <!-- 4. List注入 -->
           <property name="hobbys">
               <array>
                   <value>听歌</value>
                   <value>打游戏</value>
                   <value>敲代码</value>
                   <value>看电影</value>
                   <value>打球</value>
               </array>
           </property>
   
           <!-- 5. Map注入 -->
           <property name="card">
               <map>
                   <entry key="身份证号" value="430111111111111111" />
                   <entry key="央行卡" value="4444444444444444" />
               </map>
           </property>
   
           <!-- 6. Set注入 -->
           <property name="games">
               <set>
                   <value>LOL</value>
                   <value>COD</value>
                   <value>APEX</value>
                   <value>DOTA</value>
               </set>
           </property>
   
           <!-- 7. Null值注入 -->
           <property name="wife">
               <null/>
           </property>
   
           <!-- 8. Properties注入 -->
           <property name="info">
               <props>
                   <prop key="driver">com.jdbc.cj.mysql.Driver</prop>
                   <prop key="url">jdbc:mysql://localhost:3306/spring?useSSL=true&amp;useUnicode=ture&amp;characterEncoding=UTF-8&amp;serverTimezone=UTC</prop>
                   <prop key="username">root</prop>
                   <prop key="password">root</prop>
               </props>
           </property>
       </bean>
   </beans>
   ```

   



### 2.3 拓展方式注入

## 3. Bean的作用域

1. 单例模式(Spring默认机制)

   ```xml
   <bean id="accountService" class="com.something.DefaultAccountService"/>
   
   <!-- the following is equivalent, though redundant (singleton scope is the default) -->
   <bean id="accountService" class="com.something.DefaultAccountService" scope="singleton"/>
   ```

2. 原型模式

   ```xml
   <bean id="accountService" class="com.something.DefaultAccountService" scope="prototype"/>
   ```

3. 其余的request、session、application这些只能在web中使用到。

## 4. Bean的自动装配

- 自动装配是Spring满足bean依赖的一种方式
- Spring会在上下文中自动寻找，并且自动给bean装配属性

**在Spring中有三种装配方式**

1. 在xml显示的配置

2. 在java中显示的配置

3. 隐式的自动装配bean【重要】

   **开启注解支持**

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
           https://www.springframework.org/schema/beans/spring-beans.xsd
           http://www.springframework.org/schema/context
           https://www.springframework.org/schema/context/spring-context.xsd">
   	<!-- 开启注解支持 -->
       <context:component-scan base-package="com.huawei.pojo"/>
       <context:annotation-config/>
   
   </beans>
   ```

**@Autowire和@Resource的区别**

- 都是用来自动装配的，都可以放在属性字段上

- @Autowire默认通过bytype的方式实现，而且必须要求这个对象存在【常用】

- @Resource默认通过byname的方式实现，如果找不到名字，则通过bytype的方式实现！如果两种都找不到的情况就报错。【常用】

## 5. 使用注解开发

在Spring4之后，要使用注解开发，必须要保证aop的包导入了

![image-20210521115345291](../../../pic/Spring笔记/image-20210521115345291.png)

使用注解需要导入`context`约束，开启注解的支持。[自动装配](Bean的自动装配)中有配置过。

1. 对象注入和属性注入

```java
// 等价于 <bean id="user" class="com.huwei.pojo.User" />
@Component
public class User {
    // 等价于 <property name="name" value="薇恩" />
    @Value("薇恩")
    private String name;

    @Override
    public String toString() {
        return "User{" +
                "name='" + name + '\'' +
                '}';
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}
```

2. 衍生注解

   `@Component`有几个衍生注解，在web开发中，会按照MVC三层架构分层。

   - dao `@Repostiory`
   - service `@Service`
   - controller `@Controller`

3. 作用域

   @Scope

## 6. 小结

Xml和注解的区别：

- XML更加灵活，适用于任何场景，方便维护。
- 注解不是自己类是用不了，维护相对复杂。

## 7. AOP(面向切面编程)

### 动态代理

- 动态代理和静态代理角色一样
- 动态代理的代理类是动态生成的，不是我们直接写好的。
- 动态代理分为两大类：基于接口的动态代理，基于类的动态代理
  - 基于接口：JDK
  - 基于类：chlib
  - Java字节码实现：JAVAAssist

==需要了解两个类：Proxy、InvocationHandler==

动态代理的好处：

- 可以使真实角色的操作更加纯粹，不用去关注一些业务
- 公共业务交给代理角色，实现了业务的分工
- 公共业务发生扩展的时候，方便集中管理
- 一个动态代理类代理的是一个接口，一般就是对应的一类业务
- 一个动态代理类可以代理多各类，只是实现了同一个接口即可



### 7.1 使用Spring实现AOP

==使用AOP织入，需要导入一个依赖包==

```JAVA
<!-- https://mvnrepository.com/artifact/org.aspectj/aspectjweaver -->
<dependency>
    <groupId>org.aspectj</groupId>
    <artifactId>aspectjweaver</artifactId>
    <version>1.9.6</version>
</dependency>
```

方式一：使用Spring的API接口【主要SpringAPI接口实现】

方式二：自定义来实现AOP【主要是切面定义】

方式三：使用注解实现

> 案例在代码中的注释有标注序号

## 8 整合Mybatis

1. 编写实体类
2. 编写配置文件
3. 编写接口
4. 编写Mapper.xml
5. 测试

## 9.Mybatis-Spring

> 详情可以百度mybatis-spring官网

1. 新增一个==spring-dao.xml==编写配置,`Spring`整合`Mybatis`后数据库的配置就被Spring的配置代替了

   ```XML
   <?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://www.springframework.org/schema/beans
           https://www.springframework.org/schema/beans/spring-beans.xsd">
   
       <!-- DATASource：使用Spring的数据源替换Mybatis的配置 c3p0 dbcp druid
        这里使用的是Spring提供的JDBC：org.springframework.jdbc.datasource-->
       <bean id="dataSource" class="org.springframework.jdbc.datasource.DriverManagerDataSource">
           <property name="driverClassName" value="com.mysql.cj.jdbc.Driver"/>
           <property name="url" value="jdbc:mysql://localhost:3306/mybatis?useSSL=true&amp;useUnicode=true&amp;characterEncoding=UTF-8&amp;serverTimezone=UTC"/>
           <property name="username" value="root"/>
           <property name="password" value="root"/>
       </bean>
       <!-- SqlSessionFactory -->
       <bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
           <property name="dataSource" ref="dataSource" />
           <!-- mybatis配置文件 -->
           <property name="configLocation" value="classpath:mybatis-config.xml"/>
           <property name="mapperLocations" value="classpath:com/huawei/mapper/*.xml"/>
       </bean>
   
       <!-- MyBatis-spring核心 -->
       <bean id="sqlSessionTemplate" class="org.mybatis.spring.SqlSessionTemplate">
           <!-- 这里使用构造器注入，因为源码中没有set方法 -->
           <constructor-arg index="0" ref="sqlSessionFactory"/>
       </bean>
   </beans>
   ```

2. 不过为了清晰的知道整合了Mybatis，`<Seting/>`的配置还是会保留在==mybatis-config.xml==里，当然也可以全在`spring`里配置，完全舍弃掉`mybatis`的配置文件。

   ```XML
   <?xml version="1.0" encoding="UTF-8" ?>
   <!DOCTYPE configuration
           PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
           "http://mybatis.org/dtd/mybatis-3-config.dtd">
   <configuration>
       <settings>
           <setting name="mapUnderscoreToCamelCase" value="true"/>
       </settings>
       <typeAliases>
           <package name="com.huawei.pojo"/>
       </typeAliases>
   </configuration>
   ```

   

3. 由于`spring`的配置很多，所以可以用一个XML(applicationContext.xml)来管理他们。

   ```XML
   <?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xmlns:aop="http://www.springframework.org/schema/aop"
          xsi:schemaLocation="http://www.springframework.org/schema/beans
           https://www.springframework.org/schema/beans/spring-beans.xsd
           http://www.springframework.org/schema/aop
           https://www.springframework.org/schema/aop/spring-aop.xsd">
   
       <import resource="spring-dao.xml"/>
       <!-- 方法一 -->
       <bean id="userMapper" class="com.huawei.mapper.UserMapperImpl">
           <property name="sqlSessionTemplate" ref="sqlSessionTemplate"/>
       </bean>
       <!-- 方法二：使用这种方式，可以省略掉SqlSessionTemplate的注入配置 -->
       <bean id="userMapper2" class="com.huawei.mapper.UserMapperImpl2">
           <property name="sqlSessionFactory" ref="sqlSessionFactory"/>
       </bean>
   </beans>
   ```

   ## 10 声明式事务

   ### 1. 回顾事务

   - 把一组事务当作一个业务来做，要么都成功，要么都失败。
   - 事务在项目开发中，十分的重要，涉及到的数据一致性问题，不能马虎。
   - 确保完整的一致性。

   事务的ACID原则：

   - 原子性
   - 一致性
   - 隔离性：多个业务可能操作一个数据，防止数据损坏
   - 持久性：事务一旦提交，无论系统发生什么问题，都不会在被影响，被持久化的写到存储器中

   ### 2. Spring中事务的管理

   1. 配置事务注入
   
      ```XML
      <!-- 配置声明式事务 -->
      <bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
          <property name="dataSource" ref="dataSource"/>
      </bean>
      ```
   
   2. Spring的7种事务传播行为
   
      1. `PROPAGATION_REQUIRED`：如果当前没有事务，就创建一个新事务，如果当前存在事务，就加入该事务，该设置是最==常用==的设置。
   
      2. `PROPAGATION_SUPPORTS`：支持当前事务，如果当前存在事务，就加入该事务，如果当前不存在事务，就以非事务执行。
   
      3. `PROPAGATION_MANDATORY`：支持当前事务，如果当前存在事务，就加入该事务，如果当前不存在事务，就抛出异常。
   
      4. `PROPAGATION_REQUIRES_NEW`：创建新事务，无论当前存不存在事务，都创建新事务。
   
      5. `PROPAGATION_NOT_SUPPORTED`：以非事务方式执行操作，如果当前存在事务，就把当前事务挂起。
   
      6. `PROPAGATION_NEVER`：以非事务方式执行，如果当前存在事务，则抛出异常。
   
      7. `PROPAGATION_NESTED`：如果当前存在事务，则在嵌套事务内执行。如果当前没有事务，则执行与`PROPAGATION_REQUIRED`类似的操作。
   
   3. 配置事务的切入
   
      ```XML
      <!-- 结合AOP实现事务的织入 -->
      <!-- 配置事务的传播性 -->
      <tx:advice id="txAdvice" transaction-manager="transactionManager">
          <tx:attributes>
              <tx:method name="add" propagation="REQUIRED"/>
              <tx:method name="delete" propagation="REQUIRED"/>
              <tx:method name="update" propagation="REQUIRED"/>
              <tx:method name="query" read-only="true"/>
              <tx:method name="*" propagation="REQUIRED"/>
          </tx:attributes>
      </tx:advice>
      
      <!-- 配置事务切入 -->
      <aop:config>
          <aop:pointcut id="txPointCut" expression="execution(* com.hefeng.mapper.*.*(..))"/>
          <aop:advisor advice-ref="txAdvice" pointcut-ref="txPointCut"/>
      </aop:config>
      ```
   
   4. 为什么需要事务
   
      - 如果不配置事务，可能在数据提交不一致的情况；
      - 如果我们不在Spring中去配置声明事务，就需要在代码中手动配置事务！
      - 事务在项目的开发中有着不可撼动的地位，涉及到数据的一致性和完整性问题，不容马虎！
   
   