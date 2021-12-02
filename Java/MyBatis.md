# MyBatis

## 1. 简介

### 1.1 什么是Mybatis

`MtBatis`是一款优秀的`持久层`框架，MyBatis 本是apache的一个开源项目iBatis, 2010年这个项目由apache software foundation 迁移到了「google code」，并且改名为MyBatis 。2013年11月迁移到「Github」

**mvn坐标：**

```xml
<!-- https://mvnrepository.com/artifact/org.mybatis/mybatis -->
<dependency>
    <groupId>org.mybatis</groupId>
    <artifactId>mybatis</artifactId>
    <version>3.5.6</version>
</dependency>
```

### 1.2 持久化

**数据持久化**

- 持久化就是将程序的数据持久状态和瞬时状态转化的过程
- 内存：==断电即失==
- 数据库(jdbc)：io持久化
- 生活：罐头，冷藏

**为什么需要持久化？**

- 有一些对象不能让他丢掉
- 内存费用太高了

### 1.3 持久层

Dao层、Service层、Controller层...

- 完成持久化工作的代码块
- 层界限十分明显

### 1.4 为什么需要MyBatis

- 帮助程序员将数据存入数据库中
- 方便、自动化
- 传统的JDBC代码十分复杂
- 不用也可以，用JDBC
- 目前主流技术没办法

**优点**

- 简单易学：本身就很小且简单。
- 灵活：sql写在xml里，便于统一管理和优化。通过sql语句可以满足操作数据库的所有需求。
- 解除sql与程序代码的耦合：通过提供DAO层，将业务逻辑和数据访问逻辑分离，使系统的设计更清晰，更易维护，更易单元测试。sql和代码的分离，提高了可维护性。
- 提供映射标签，支持对象与数据库的orm字段关系映射
- 提供对象关系映射标签，支持对象关系组建维护
- 提供xml标签，支持编写动态sql。

## 2. 第一个MyBatis

思路：搭建环境->导入MyBatis->编写代码->测试。

### 2.1 搭建环境

编写mybatis核心配置文件

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <environments default="development">
        <environment id="development">
            <transactionManager type="JDBC"/>
            <dataSource type="POOLED">
                <property name="driver" value="com.mysql.cj.jdbc.Driver"/>
                <property name="url" value="jdbc:mysql://localhost:3306/mybatis?useSSL=true&amp;useUnicode=true&amp;characterEncoding=UTF-8"/>
                <property name="username" value="root"/>
                <property name="password" value="root"/>
            </dataSource>
        </environment>
    </environments>
<!--    <mappers>-->
<!--        <mapper resource="org/mybatis/example/BlogMapper.xml"/>-->
<!--    </mappers>-->
</configuration>
```

### 2.2 编写代码

- 创建接口

  ```java
  /**
  * 查询用户列表
  * @return
  */
  List<User> getUserList();
  ```

- 接口实现类由原来的`UserDaoImpl`转变为一个`UserDaoMapper`配置文件

  ```xml
  <?xml version="1.0" encoding="UTF-8" ?>
  <!DOCTYPE mapper
          PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
          "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
  <!-- namespace:绑定方法 -->
  <mapper namespace="com.huawei.dao.UserDao">
      <!-- id：方法名 resultType：返回值类型 -->
      <select id="getUserList" resultType="com.huawei.pojo.User">
          SELECT * FROM USER;
      </select>
  </mapper>
  ```
  
- 编写MybatisUtil，读取Mybatis配置

  ```java
  public class MybatisUtil {
      private static InputStream is;
      private static SqlSessionFactory build;
  
      static {
          try {
              is = Resources.getResourceAsStream("mybatis-config.xml");
              build = new SqlSessionFactoryBuilder().build(is);
          } catch (IOException e) {
              e.printStackTrace();
          }
      }
  
      public static SqlSession getSqlSession(){
          // 传入true自动提交事务
          return build.openSession(true);
      }
  }
  ```
  
- 测试

  ```java
  @Test
  public void test(){
      // 1. 获取sqlSession
      SqlSession sqlSession = MybatisUtils.getSqlSession();
      // 2. 执行 这里用了反射得到文件对象
      UserDao mapper = sqlSession.getMapper(UserDao.class);
      List<User> userList = mapper.getUserList();
  
      userList.forEach(System.out::println);
  
      // 关闭sqlSession
      sqlSession.close();
  
  }
  ```


**常见错误**

- 没有绑定到`Mapper.xml`

  ```java
  org.apache.ibatis.binding.BindingException: Type interface com.huawei.dao.UserDao is not known to the MapperRegistry.
  ```

- 解决`Maven`资源过滤问题

  ```java
  <build>
     <resources>
         <resource>
             <directory>src/main/java</directory>
             <includes>
                 <include>**/*.properties</include>
                 <include>**/*.xml</include>
             </includes>
             <filtering>false</filtering>
         </resource>
         <resource>
             <directory>src/main/resources</directory>
             <includes>
                 <include>**/*.properties</include>
                 <include>**/*.xml</include>
             </includes>
             <filtering>false</filtering>
         </resource>
     </resources>
  </build>
  ```


## 3.MyBatis配置文件优化

### 3.1 数据库字段与实体不一样映射

- 在Mapper.xml中使用「resultMap」标签

  ```xml
  <!--设置实体和表字段映射 可以避免驼峰命名等和数据库不对应的情况 -->
  <resultMap id="UserMap" type="user">
      <result column="ID" property="id"/>
      <result column="USERNAME" property="userName"/>
      <result column="PASSWORD" property="password"/>
  </resultMap>
  ```

- 在mybatis-condig中配置「驼峰命名规则映射」

  ```xml
  <settings>
      <setting name="mapUnderscoreToCamelCase" value="true"/>
  </settings>
  ```

### 3.2 实体类自动设置别名

```XML
<typeAliases>
    <package name="com.huawei.pojo"/>
</typeAliases>
```

配置完后在「Mapper」中可以直接使用`类名`首字母小写，作为参数类型。

比如`User`类，可以使用`user`作为「Mapper.xml」中的参数使用，而不是`com.xxx.pojo.User`

## 4.日志

### 4.1 LOG4J

**什么是LOG4J**

Log4j是Apache的一个开源项目，通过使用Log4j，我们可以控制日志信息输送的目的地是控制台、文件、GUI组件，甚至是套接口服务器NT的事件记录器、UNIX、Syslog、守护进程等；我们也可以控制每一条日志的输出格式；通过定义每一条日志信息的级别，我们能够更加细致地控制日志的生成过程。最令人感兴趣的就是，这些可以通过一个配置文件来灵活地进行配置，而不需要修改应用的代码。

1. 配置log4j的实现

   ```xml
   <settings>
           <setting name="logImpl" value="LOG4J"/>
   </settings>
   ```

2. 导入依赖

   ```xml
   <!-- https://mvnrepository.com/artifact/log4j/log4j -->
   <dependency>
       <groupId>log4j</groupId>
       <artifactId>log4j</artifactId>
       <version>1.2.17</version>
   </dependency>
   ```

3. 创建log4j.properties配置文件

   ```protobuf
   ### 将DEBUG等级日志，输出到console，file ###
   log4j.rootLogger=DEBUG,console,file
   
   #控制台输出的相关设置
   log4j.appender.console = org.apache.log4j.ConsoleAppender
   log4j.appender.console.Target = System.out
   log4j.appender.console.Threshold=DEBUG
   log4j.appender.console.layout = org.apache.log4j.PatternLayout
   log4j.appender.console.layout.ConversionPattern=[%c]-%m%n
   
   #文件输出的相关设置
   log4j.appender.file = org.apache.log4j.RollingFileAppender
   log4j.appender.file.File=./log/logging.log
   log4j.appender.file.MaxFileSize=10mb
   log4j.appender.file.Threshold=DEBUG
   log4j.appender.file.layout=org.apache.log4j.PatternLayout
   log4j.appender.file.layout.ConversionPattern=[%p][%d{yy-MM-dd}][%c]%m%n
   
   #日志输出级别
   log4j.logger.org.mybatis=DEBUG
   log4j.logger.java.sql=DEBUG
   log4j.logger.java.sql.Statement=DEBUG
   log4j.logger.java.sql.ResultSet=DEBUG
   log4j.logger.java.sql.PreparedStatement=DEBUG
   ```

4. 使用

   ```java
   public class LogTest {
   	static Logger logger = Logger.getLogger(UserDaoTest.class);
   	/**
   	 * 在方法中调用就可以了
   	*/
       @Test
       public void testLog4j() {
           logger.info("info进入了testLog4j");
           logger.debug("info进入了testLog4j");
           logger.error("info进入了testLog4j");
       }
   }
   ```

## 5.分页

**为什么要分页？**

- 减少数据的处理量
- 内存太贵了

**使用Limit分页**

```mysql
SELECT * FROM USER LIMIT 起始下标，页数;
SELECT * FROM USER LIMIT 页数;
```

**使用MyBatis分页**

1. 接口

   ```JAVA
   List<User> getUserByLimit(Map<String,Integer> map);
   ```

   

2. Mapper.xml

   ```XML
   <select id="getUserByLimit" parameterType="map" resultMap="UserMap">
           SELECT * FROM USER LIMIT #{startIndex},#{pageSize};
   </select>
   ```

   

3. 测试

   ```JAVA
   @Test
       public void getUserLimit(){
           // 1. 获取sqlSession
           SqlSession sqlSession = MybatisUtils.getSqlSession();
           // 2. 执行 这里用了反射得到文件对象
           UserMapper mapper = sqlSession.getMapper(UserMapper.class);
           HashMap<String, Integer> map = new HashMap<>();
           map.put("startIndex",1);
           map.put("pageSize",2);
           List<User> userByLimit = mapper.getUserByLimit(map);
           userByLimit.forEach(System.out::println);
           // 关闭sqlSession
           sqlSession.close();
   
       }
   ```

**使用插件**

[PageHelper](https://pagehelper.github.io/)

## 6.使用注解开发

### 6.1 面向接口编程

根本原因：`解耦`，可以扩展

接口可以反映系统设计人员对抽象的理解

## 7.动态SQL

- 使用`IF`标签判断，进行模糊查询

```xml
<select id="getBlog2" parameterType="map" resultType="blog">
    <!-- 正常开发不要写1=1！！！！ -->
    SELECT * FROM BLOG WHERE 1=1
    <if test="title != null">
        AND TITLE LIKE "%"#{title}"%"
    </if>
    <if test="author != null">
        AND AUTHOR LIKE "%"#{author}"%"
    </if>
</select>
```

- 使用`choose`和`when`标签

  ```xml
  <select id="getBlog2" parameterType="map" resultType="blog">
          SELECT * FROM BLOG
          <where>
              <choose>
                  <when test="title != null">
                      AND TITLE LIKE "%"#{title}"%"
                  </when>
                  <when test="author != null">
                      AND AUTHOR LIKE "%"#{author}"%"
                  </when>
                  <otherwise>
                      and VIEWS = #{views}
                  </otherwise>
              </choose>
          </where>
      </select>
  ```

  1. 相比第一个案例使用`where 1=1`，第二个案例会更合理。

  2. 使用`choose`标签会自动匹配其中的条件，`when`标签在条件成立时才会生效且只会选择一条，类似于`java`中的`switch catch`，某一条成立则后面的不会生效了。
  3. `otherwise`标签是最后一个条件，可以理解为`switch`中的`default`。

## 8. MyBatis如何防止SQL注入

[mybatis是如何防止SQL注入的 - 王的微笑 - 博客园 (cnblogs.com)](https://www.cnblogs.com/jokmangood/p/11705850.html)

