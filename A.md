### 创建项目

#### 1. 新建项目

 1. 创建spring-boot web

 2. 下载所需要的文件

    1. 前端模板

       ![image-20200229200053289](C:\Users\babshr\AppData\Roaming\Typora\typora-user-images\image-20200229200053289.png)

    2. 创建文件夹架构

       1. java

          1. controller
          2. pojo
          3. mapper
          4. service

       2. resources

          1. mapper

          2. static

          3. templates

             

#### 2. 添加依赖

~~~xml
 <dependencies>
        <!--shiro-->
        <dependency>
            <groupId>org.apache.shiro</groupId>
            <artifactId>shiro-spring</artifactId>
            <version>1.4.1</version>
        </dependency>
        <dependency>
            <groupId>com.github.theborakompanioni</groupId>
            <artifactId>thymeleaf-extras-shiro</artifactId>
            <version>2.0.0</version>
        </dependency>

        <!--thymeleaf-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-thymeleaf</artifactId>
        </dependency>

        <!--mybatis-->
        <dependency>
            <groupId>org.mybatis.spring.boot</groupId>
            <artifactId>mybatis-spring-boot-starter</artifactId>
            <version>2.1.1</version>
        </dependency>
            <!--数据库-->
            <dependency>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-starter-jdbc</artifactId>
            </dependency>
            <dependency>
                <groupId>mysql</groupId>
                <artifactId>mysql-connector-java</artifactId>
                <scope>runtime</scope>
        </dependency>

        <!--lombok-->
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <version>1.16.10</version>
        </dependency>



        <!--spring boot web-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
            <exclusions>
                <exclusion>
                    <groupId>org.junit.vintage</groupId>
                    <artifactId>junit-vintage-engine</artifactId>
                </exclusion>
            </exclusions>
        </dependency>
    </dependencies>
~~~

运行测试

这里因为没有设置数据库，所以先屏蔽掉数据库相关内容

~~~xml
<!--        &lt;!&ndash;mybatis&ndash;&gt;-->
<!--        <dependency>-->
<!--            <groupId>org.mybatis.spring.boot</groupId>-->
<!--            <artifactId>mybatis-spring-boot-starter</artifactId>-->
<!--            <version>2.1.1</version>-->
<!--        </dependency>-->
<!--            &lt;!&ndash;数据库&ndash;&gt;-->
<!--            <dependency>-->
<!--                <groupId>org.springframework.boot</groupId>-->
<!--                <artifactId>spring-boot-starter-jdbc</artifactId>-->
<!--            </dependency>-->
<!--            <dependency>-->
<!--                <groupId>mysql</groupId>-->
<!--                <artifactId>mysql-connector-java</artifactId>-->
<!--                <scope>runtime</scope>-->
<!--        </dependency>-->
~~~

或者先按照 4.数据库操作先idea连上数据库

测试不报错就下一步。

#### 3. 页面跳转

 1. MyController控制类

    取名字的时候不要和包的名字重名

    ~~~java
    @Controller
    public class MyController {
        @RequestMapping({"/","index"})
        public String index(){
            return "index";
        }
        @RequestMapping("/login")
        public String login(){
            return "login";
        }
        @RequestMapping("/user/add")
        public String add(){return "/user/add"; }
        @RequestMapping("/user/update")
        public String update(){
            return "/user/update";
        }
    }
    ~~~

    资源文件下面

    	1. templates放index.html和login.html

       	2. user下放add.html和update.html

    login

    ~~~html
    <!DOCTYPE html>
    <html xmlns:th="http://www.thymeleaf.org">
    <head>
        <meta charset="utf-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <title>newbee-mall管理系统 | Log in</title>
        <!-- Tell the browser to be responsive to screen width -->
        <meta name="viewport" content="width=device-width, initial-scale=1">
        <link rel="shortcut icon" th:href="@{/dist/img/favicon.png}"/>
        <!-- Font Awesome -->
        <link rel="stylesheet" th:href="@{/dist/css/font-awesome.min.css}">
        <!-- Ionicons -->
        <link rel="stylesheet" th:href="@{/dist/css/ionicons.min.css}">
        <!-- Theme style -->
        <link rel="stylesheet" th:href="@{/dist/css/adminlte.min.css}">
        <style>
            canvas {
                display: block;
                vertical-align: bottom;
            }
            #particles {
                background-color: #F7FAFC;
                position: absolute;
                top: 0;
                width: 100%;
                height: 100%;
                z-index: -1;
            }
        </style>
    </head>
    <body class="hold-transition login-page">
    <div id="particles">
    </div>
    <div class="login-box">
        <div class="login-logo" style="color: #1baeae;">
    <!--        <img th:src="@{/image/new-bee-logo-3.png}" style="    height: 58px;float: left;margin-left: 10px;">-->
            <h1>管理系统登陆</h1>
        </div>
        <!-- /.login-logo -->
        <div class="card">
            <div class="card-body login-card-body">
                <p class="login-box-msg"> NewBee MALL , Let's Go !</p>
                <form th:action="@{/user/login}" method="get">
                    <div th:if="${not #strings.isEmpty(msg)}" class="form-group">
                        <div class="alert alert-danger" th:text="${msg}"></div>
                    </div>
                    <div class="form-group has-feedback">
                        <span class="fa fa-user form-control-feedback"></span>
                        <input type="text" id="userName" name="userName" class="form-control" placeholder="请输入账号"
                               required="true">
                    </div>
                    <div class="form-group has-feedback">
                        <span class="fa fa-lock form-control-feedback"></span>
                        <input type="password" id="password" name="password" class="form-control" placeholder="请输入密码"
                               required="true">
                    </div>
                    <div class="row">
                        <div class="col-6">
                            <input type="text" class="form-control" name="verifyCode" placeholder="请输入验证码" required="true">
                        </div>
                        <div class="col-6">
                            <img alt="单击图片刷新！" class="pointer" th:src="@{/common/kaptcha}"
                                 onclick="this.src='/common/kaptcha?d='+new Date()*1">
                        </div>
                    </div>
                    <div class="form-group has-feedback"></div>
                    <div class="row">
                        <div class="col-8">
                        </div>
                        <div class="col-4">
                            <button type="submit" class="btn btn-primary btn-block btn-flat">登录
                            </button>
                        </div>
                    </div>
                </form>
    
            </div>
            <!-- /.login-card-body -->
        </div>
    </div>
    <!-- /.login-box -->
    
    <!-- jQuery -->
    <script th:src="@{/plugins/jquery/jquery.min.js}"></script>
    <!-- Bootstrap 4 -->
    <script th:src="@{/plugins/bootstrap/js/bootstrap.bundle.min.js}"></script>
    <script th:src="@{/dist/js/plugins/particles.js}"></script>
    <script th:src="@{/dist/js/plugins/login-bg-particles.js}"></script>
    </body>
    </html>
    
    ~~~

    index

    ~~~html
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>Title</title>
    </head>
    <body>
    成功登录欢迎您！
    </body>
    </html>
    ~~~

    add

    ~~~xml
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>Title</title>
    </head>
    <body>
    这里添加操作
    </body>
    </html>
    ~~~

    update

    ~~~html
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>Title</title>
    </head>
    <body>
    这里更新操作
    </body>
    </html>
    ~~~

    

    打开屏蔽的数据库相关maven依赖

#### 4. 数据库

 1. 创建数据库

    ~~~mysql
    CREATE DATABASE project01;
    
    USE project01;
    
    CREATE TABLE IF NOT EXISTS `users`(
       `id` INT UNSIGNED AUTO_INCREMENT,
       `name` VARCHAR(20) NOT NULL,
       `pwd` VARCHAR(20) NOT NULL,
       `perms` VARCHAR(20) NOT NULL,
       PRIMARY KEY ( `id` )
    )ENGINE=INNODB DEFAULT CHARSET=utf8;
    
    INSERT INTO users ( id,`name`,pwd, perms)
                           VALUES
                           ( 1,"阿毛", "1" , "vip1"),
                           ( 2,"小王", "2"  , "vip1"),
                           ( 3,"小鑫", "3"  , "vip1"),
                           ( 4,"小刘", "4"  , "vip1"),
                           ( 5,"小小刘", "5"  , "vip2"),
                           ( 6,"小李", "6"  , "vip3"),
                           ( 7,"小黄", "7"  , "vip3")       
                           ;
                           
    INSERT INTO users ( id,`name`,pwd, perms)
                           VALUES
                           ( 8,"张三", "8","");
                           
    SELECT * FROM users;
    
    SELECT * FROM users WHERE id=1;
    
    UPDATE users SET NAME="李四", pwd= "123" WHERE id=8;
    
    DELETE FROM users WHERE id=8;
    ~~~

 2. idea插件连接数据库

    只要输入这三个

    账号：root

    密码：1

    url:

    ~~~xml
    jdbc:mysql://localhost:3306/?serverTimezone=UTC&useUnicode=true&characterEncoding=utf-8
    ~~~

    ![image-20200229204559209](C:\Users\babshr\AppData\Roaming\Typora\typora-user-images\image-20200229204559209.png)

    配置application.yml

    ~~~xml
    spring:
      datasource:
        username: root
        password: 1
        url: jdbc:mysql://localhost:3306/project01?serverTimezone=UTC&useUnicode=true&characterEncoding=utf-8
        driver-class-name: com.mysql.cj.jdbc.Driver
    mybatis:
      type-aliases-package: com.mao.pojo
      mapper-locations: classpath:mapper/*.xml
    ~~~

    到这里可以运行上文的测试

    创建实体类

    pojo.User

    ~~~java
    @Data
    @NoArgsConstructor
    @AllArgsConstructor
    public class User {
        private int id;
        private String lastname;
        private String pwd;
        private String perms;
    }
    
    ~~~

    mapper.UserMapper接口

    ~~~java
    @Repository
    @Mapper
    public interface UserMapper {
        public User getByName(String name);
    }
    ~~~

    UserMapper.xml

    需要修改

    	1. namespace

       	2. mysql语句 id里面写UserMapper接口里面的函数

    ~~~xml
    <?xml version="1.0" encoding="UTF-8" ?>
    <!DOCTYPE mapper
            PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
            "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
    <mapper namespace="com.mao.mapper.UserMapper">
        <select id="getNameById" parameterType="String" resultType="User">
        select * from users where name = #{name}
       </select>
    </mapper>
    ~~~

    测试函数测试

    ~~~java
        @Autowired
        UserMapper userMapper;
        @Test
        void contextLoads() {
            System.out.println(userMapper.getNameById("阿毛"));
        }
    ~~~

    ![image-20200229212414376](C:\Users\babshr\AppData\Roaming\Typora\typora-user-images\image-20200229212414376.png)

    测试成功

#### 5. 用户认证

​	注解不要忘记加

		1. @Mapper @Repository

   2. @Configuration

           		3. @Controller
                     		4. @Service

 3. 用户认证基本配置

    新建config.ShiroRealm和config.ShiroConfig

    ~~~java
    public class ShiroRealm extends AuthorizingRealm {
        @Override
        protected AuthorizationInfo doGetAuthorizationInfo(PrincipalCollection principalCollection) {
            return null;
        }
    
        @Override
        protected AuthenticationInfo doGetAuthenticationInfo(AuthenticationToken authenticationToken) throws AuthenticationException {
            return null;
        }
    }
    ~~~

    ~~~java
    public class ShiroConfig{
        //shiro工厂bean
        @Bean
        public ShiroFilterFactoryBean shiroFilterFactoryBean(@Qualifier("DSManager") DefaultWebSecurityManager defaultWebSecurityManager){
            ShiroFilterFactoryBean factoryBean = new ShiroFilterFactoryBean();
            factoryBean.setSecurityManager(defaultWebSecurityManager);
            return factoryBean;
        }
    
        //默认web安全控制
        @Bean(name = "DSManager")
        public DefaultWebSecurityManager defaultWebSecurityManager(@Qualifier("shiroRealm") ShiroRealm shiroRealm){
            DefaultWebSecurityManager defaultWebSecurityManager = new DefaultWebSecurityManager();
            defaultWebSecurityManager.setRealm(shiroRealm);
            return defaultWebSecurityManager;
        }
        //ShiroConfig
        @Bean
        public ShiroRealm shiroRealm()
        {
            return new ShiroRealm();
        }
    }
    ~~~

 4. 拦截

    1. 登录拦截跳转首页

       修改ShiroConfig

       ~~~java
       /拦截代码
       
               /*
                * anon:无需认证
                * authc：认证访问
                * user： 记住我可访问
                * perms：拥有资源访问
                * role：角色访问
                * */
               HashMap<String, String> map = new HashMap<>();
               //首页登录拦截
               map.put("/user/*","authc");
               factoryBean.setFilterChainDefinitionMap(map);
               factoryBean.setLoginUrl("/toLogin");
       ~~~

 5. 认证

    1. 设置认证密码

       修改ShiroRealm

       ~~~java
           @Override
           protected AuthenticationInfo doGetAuthenticationInfo(AuthenticationToken authenticationToken) throws AuthenticationException {
               System.out.println("认证");
               String name = "root";
               String pwd = "1";
               //Auth
               return new SimpleAuthenticationInfo("",pwd,"");
           }
       ~~~

    2. 前端获取账号密码

    3. 控制把账号密码传给Shiro

       ~~~java
           @RequestMapping("/toLogin")
           public String toLogin(String userName, String password){
               System.out.println("账号："+"密码："+userName+password);
               //安全工具
               Subject subject = SecurityUtils.getSubject();
               UsernamePasswordToken token = new UsernamePasswordToken(userName, password);
               try{
                   subject.login(token);
                   return "index";
               }catch (UnknownAccountException e){
                   System.out.println("用户不存在");
                   return "login";
               }catch (IncorrectCredentialsException e) {
                   System.out.println("密码错误");
                   return "login";
               }
       
           }
       ~~~

 6. 从数据库获取用户认证码

    新建接口service.UserService和service.UserServiceImpl

    

    ~~~java
    public interface UserService {
        public User getNameById(String name);
    }
    ~~~

    ~~~java
    @Service
    public class UserServiceImpl implements UserService{
        @Autowired
        UserMapper userMapper;
        @Override
        public User getNameById(String name) {
            return userMapper.getNameById(name);
        }
    }
    ~~~

    1. 修改ShiroRealm

       ~~~java
               System.out.println("认证");
               System.out.println(authenticationToken);
       //        String name = "root";
       //        String pwd = "1";
               UsernamePasswordToken token = (UsernamePasswordToken) authenticationToken;
               User user = userMapper.getNameById(token.getUsername());
               if(user==null){
                   return null;
               }
               return new SimpleAuthenticationInfo("",user.getPwd(),"");
       ~~~

 7. 无权限拦截

    ~~~java
            map.put("/user/add","perms[vip1]");
            map.put("/user/update","perms[vip2]");
            factoryBean.setUnauthorizedUrl("/user/stop");
            factoryBean.setFilterChainDefinitionMap(map);
    ~~~

  		8. 授权

       授权代码

       ~~~java
        System.out.println("授权");
               SimpleAuthorizationInfo info = new SimpleAuthorizationInfo();
       //        info.addStringPermission("user:add");
               //得到当前用户
               Subject subject = SecurityUtils.getSubject();
               User user = (User) subject.getPrincipal();
       
               System.out.println(user);
               System.out.println(user.getPerms());
               info.addStringPermission(user.getPerms());
       //        return null;
               return info;
       ~~~

       别忘了修改认证时传递的数据参数

       ~~~java
               System.out.println("认证");
               System.out.println(authenticationToken);
       //        String name = "root";
       //        String pwd = "1";
               UsernamePasswordToken token = (UsernamePasswordToken) authenticationToken;
               User user = userMapper.getNameById(token.getUsername());
               if(user==null){
                   return null;
               }
       
               return new SimpleAuthenticationInfo(user,user.getPwd(),"");
       ~~~

  		9. 添加注销

       ~~~java
           @RequestMapping("/user/logout")
           public String logout(){
               Subject subject = SecurityUtils.getSubject();
               subject.logout();
               return "/login";
           }
       ~~~

       完整控制代码

       ~~~java
       @Controller
       public class MyController {
           @RequestMapping({"/","index"})
           public String index(){
               return "index";
           }
           @RequestMapping("/user/login")
           public String login(){return "/login"; }
           @RequestMapping("/user/add")
           public String add(){return "/user/add"; }
           @RequestMapping("/user/update")
           public String update(){
               return "/user/update";
           }
           @RequestMapping("/user/stop")
           public String stop(){
               return "/user/stop";
           }
       
       
           @RequestMapping("/user/logout")
           public String logout(){
               Subject subject = SecurityUtils.getSubject();
               subject.logout();
               return "/login";
           }
           @RequestMapping("/toLogin")
           public String toLogin(String userName, String password){
               System.out.println("账号："+userName+"密码："+password);
               //安全工具
               Subject subject = SecurityUtils.getSubject();
               UsernamePasswordToken token = new UsernamePasswordToken(userName, password);
               try{
                   subject.login(token);
                   return "index";
               }catch (UnknownAccountException e){
                   System.out.println("用户不存在");
                   return "login";
               }catch (IncorrectCredentialsException e) {
                   System.out.println("密码错误");
                   return "login";
               }
       
           }
       
       }
       ~~~

  		10. 首页根据用户登录情况显示

        添加thymeleaf和shiro依赖

        ~~~html
        <html lang="en"
              xmlns:th="http://www.thymeleaf.org"
              xmlns:shiro="http://www.pollix.at/thymeleaf/shiro">
        ~~~

        1. 登录错误信息

           ~~~java
               @RequestMapping("/toLogin")
               public String toLogin(String userName, String password, Model model){
                   System.out.println("账号："+userName+"密码："+password);
                   //安全工具
                   Subject subject = SecurityUtils.getSubject();
                   UsernamePasswordToken token = new UsernamePasswordToken(userName, password);
                   try{
                       subject.login(token);
                       return "index";
                   }catch (UnknownAccountException e){
                       System.out.println("用户不存在");
                       model.addAttribute("msg","用户不存在");
                       return "login";
                   }catch (IncorrectCredentialsException e) {
                       System.out.println("密码错误");
                       model.addAttribute("msg","密码错误");
                       return "login";
                   }
           ~~~

        2. index显示

           ~~~html
           <div th:if="${session.userLogin==null}">
               <a href="/user/login">登录</a>
           </div>
           ~~~

  		11. 根据授权显示首页信息

        首页

        ~~~html
        <!DOCTYPE html>
        <html lang="en"
              xmlns:th="http://www.thymeleaf.org"
              xmlns:shiro="http://www.pollix.at/thymeleaf/shiro">
        <head>
            <meta charset="UTF-8">
            <title>Title</title>
        </head>
        <body>
        <h1>这里是首页</h1>
        <p shiro:hasPermission="vip1"><li>这是svip能看到的p标签</li></p>
        <div th:if="${session.userLogin==null}">
            <a href="/user/login">登录</a>
        </div>
        <p></p>
        <div shiro:hasPermission="vip1">
            <a href="/user/add">添加</a>
        </div>
        <p></p>
        <div shiro:hasPermission="vip2">
            <a href="/user/update">更新</a>
        </div>
        <div th:if="!${session.userLogin==null}">
            <a href="/user/logout">注销</a>
        </div>
        
        
        
        </body>
        </html>
        ~~~

        ShiroConfig

        ~~~java
            @Bean
            public ShiroDialect shiroDialect(){
                return new ShiroDialect();
            }
        ~~~

        到这里第一部分完了