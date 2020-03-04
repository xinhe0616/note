# idea新建java

src右键创建包pakpage，包右键创建类

psvm创建main，sout 输出，右击run

# 项目打包

project struct

artfile添加项目或者选各中，选择jar，ok。build对jarbuild

java -cp jar包 包名.类名

# idea自动导包、自动编译

 set-编辑-自动包两个打勾

set-build-compier两个勾

# idea快捷键

复制行ctrl D

代码生成

alt /代码自动补全

alt ins构造函数生成

ctrl j 自动代码模板

# 跳过直接看maven

 

# 删除数据库

cmd里面输入  **sc delete mysql**

mysql安装是不需要新建data文件夹

# 新建一个数据库程序

在maven中添加mysql依赖，同步完之后在mysql驱动设置导入maven下载的MySQL驱动，cmd 设置MySQL时区，idea添加mysql 名称为数据库名称，所以cmd新建一个数据库名字。注意这里使用的不是数据库服务名字。

# 新建一个spring boot

下载spring boot失败，在创建工程的时候报错需要修改http

pol. xml 中spring-boot-maven-plugin 报错

# tryleaf

模板引擎

# 制作一个登录界面

用到的知识点有

* spring boot创建项目
* 数据库
* 登录页面制作模板

1. 用AdminLTE3模板写出登录界面，前端范畴

   1. 新建一个spring boot的项目,实现thymeleaf

   2. 在templates下面新建一个index.html和login.html。把新蜂的文件拷贝进来。

   3. 新建Admincontorller类

      1. 设置自动导包和自动删包

      2. 

         1. ```java
                @GetMapping({"/login"})
                public String login() {
                    return "admin/login";
                }
            ```

            这时候的可以显示登录界面了，只是不够完善

            ![image-20200218103741973](C:\Users\babshr\AppData\Roaming\Typora\typora-user-images\image-20200218103741973.png)

            把AdminLTE的前端文件的dist和plugins拷贝到项目目录中

            ![image-20200218105314449](C:\Users\babshr\AppData\Roaming\Typora\typora-user-images\image-20200218105314449.png)

            修改login.html

            1. 浏览器显示title
            2. 提示语句Let's

         2. ```java
                @GetMapping({"/index"})
                public String index() {
                    return "admin/index";
                }
            ```

            就可以访问验证成功了

         3. 怎么按键跳转呢卡住了
         
            看了一星期的狂神说java，学习了java基础，看了
         
            1. html css js
            2. spring + spring mvc + spring boot 
            3. mybatis + thymeleaf 
         
            做了一个大概的了解
         
            现在开始继续谢我的登录界面
         
            按键跳转
         
            在html页面上点击按钮能够跳转到新页面，通过spring
         
            ```java
            @Controller
            @RequestMapping({"/admin"})
            public class Admincontrpller {
                @GetMapping({"/login"})
                public String login() {
                    return "admin/login";
                }
            
                @PostMapping(value = "/login")
                public String login(@RequestParam("userName") String userName,
                                    @RequestParam("password") String password,
                                    @RequestParam("verifyCode") String verifyCode,
                                    HttpSession session) {
                    System.out.println("username:" + userName);
                    System.out.println("password:" + password);
                    System.out.println("verifyCode:" + verifyCode);
            //        return userName;
                    return "admin/index";
                }
            
            }
            ```
         
            @Controller注解
         
            表示这是个控制器
         
            程序开始扫描到@GetMapping({"/login"})，浏览器输入路径login，
         
            ```java
            public String login() {   
                return "admin/login";
            }
            ```
         
            跳转到login.html，用户输入用户信息，点击提交按钮
         
            ```html
            <form th:action="@{/admin/login}" method="post">
            ```
         
            表单跳转到login，回到控制器，
         
            @PostMapping(value = "/login")
         
            接受请求，同时获得参数
         
            * 这里使用@RestController，可以用return语句直接在html上将参数显示
         
            直接
         
            ```java
            return "admin/index";
            ```
         
            进入index.html
         
            跳转成功
         
         4. 添加数据库实现用户验证
         
            1. 创建数据库
         
               1. ```mysql
                  CREATE DATABASE mybatis_demo01;
                  
                  USE `mybatis_demo01`;
                  CREATE TABLE users(
                    id INT(20) NOT NULL PRIMARY KEY,
                    `name` VARCHAR(30) DEFAULT NULL,
                    pwd VARCHAR(30) DEFAULT NULL
                  )ENGINE=INNODB DEFAULT CHARSET=utf8;
                  
                  INSERT INTO users (id, `name`, pwd) VALUES
                  (1, '张三', '123456'),
                  (2, '李四', '123456'),
                  (3, '王五', '123456')
                  ```
         
            2. 创建普通maven项目
         
               1. 添加依赖
         
                  ```xml
                  <dependencies>
                      <dependency>
                          <groupId>org.mybatis</groupId>
                          <artifactId>mybatis</artifactId>
                          <version>3.5.4</version>
                      </dependency>
                  
                      <dependency>
                          <groupId>junit</groupId>
                          <artifactId>junit</artifactId>
                          <version>4.12</version>
                          <scope>test</scope>
                      </dependency>
                          <!-- https://mvnrepository.com/artifact/mysql/mysql-connector-java -->
                          <dependency>
                              <groupId>mysql</groupId>
                              <artifactId>mysql-connector-java</artifactId>
                              <version>8.0.15</version>
                          </dependency>
                  
               </dependencies>
                  ```
         
                  
            
            3. 配置数据库
            
               1. mybatis配置文件
            
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
                                  <property name="driver" value="com.mysql.jdbc.Driver"/>
                                  <property name="url" value="jdbc:mysql://localhost:3306/mabatis_demo01"/>
                                  <property name="username" value="root"/>
                                  <property name="password" value="1"/>
                              </dataSource>
                       </environment>
                      </environments>
               </configuration>
                  ```
         
               2. 加载配置文件新建一个包
            
                  ```java
               //SqlSessionFactory-> sqlSession
                  public class MybatisUtils {
                   private  static SqlSessionFactory sqlSessionFactory;
                      //静态代码库初始加载
                   static{
                          try {
                           String resource = "mybatis-config.xml";
                              InputStream inputStream = Resources.getResourceAsStream(resource);
                               sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
                          } catch (IOException e) {
                           e.printStackTrace();
                          }
                   }
                  
                      public static SqlSession getSession(){
                          return sqlSessionFactory.openSession();
                      }
                  }
                  
                  ```
            
            4. 创建实体类
            
               entity/AdminUser
         
               ```java
               private Integer adminUserId;private String loginUserName;private String loginPassword;private String nickName;private Byte locked;
               ```
            
               alt + insert
            
               win + shift + s截图
            
               ![image-20200225140401919](C:\Users\babshr\AppData\Roaming\Typora\typora-user-images\image-20200225140401919.png)
            
               1. 构造函数无参有参
               2. gettet and setter自动生成
               3. 和tostring
            
            5. UserMapper
            
               1. 配置文件
            
                  ```xml
                  <?xml version="1.0" encoding="UTF-8" ?>
                  <!DOCTYPE mapper
                    PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
                    "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
                  <mapper namespace="org.mybatis.example.BlogMapper">
                    <select id="selectBlog" resultType="Blog">
                      select * from Blog where id = #{id}
                    </select>
                  </mapper>
                  ```
            
               2. Dao接口
            
                  ```java
                  public interface UserDao {
                      List<User> getUserList();
                  }
                  
                  ```
            
               3. Mapper接口实现
            
                  ```xml
                  <?xml version="1.0" encoding="UTF-8" ?>
                  <!DOCTYPE mapper
                          PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
                          "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
                  <mapper namespace="com.babashr.dao.UserDao">
                      <select id="getUserList" resultType="com.babashr.pojo.User">
                      select * from mybatis_demo01.users;
                    </select>
                  </mapper>
                  ```
            
               4. 资源文件扫描
            
                  ```xml
                  <build>
                          <resources>
                              <resource>
                                  <directory>src/main/java</directory>
                                  <includes>
                                      <include>**/*.properties</include>
                                      <include>**/*.xml</include>
                                  </includes>
                              </resource>
                              <resource>
                                  <directory>src/main/resources</directory>
                                  <includes>
                                      <include>**/*.*</include>
                                  </includes>
                              </resource>
                          </resources>
                      </build>
                  ```
            
               5. 增删改查
            
                  
            
               
            
               

