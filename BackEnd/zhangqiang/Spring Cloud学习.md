<a name="sbx1l"></a>
# 1、相关技术了解
<a name="M72r6"></a>
## 1.1 服务注册中心
Eureka（停止更新）、Zookeeper（算好用）、Consul（go语言开发，不推荐）、Nacos（好用比较推荐）
<a name="jMr2m"></a>
## 1.2 服务调用
Ribbon（停更边缘）、LoadBalancer（会慢慢取代Ribbon）、Feign（停止更新）、OpenFegin（Spring官方发布）
<a name="VmWfA"></a>
## 1.3服务降级
Hystrix（停止更新，不推荐）、resilience4j（推荐使用，国内使用较少）、Sentinel（强推，阿里推出框架）
<a name="zJb0f"></a>
## 1.4 服务网关
Zuul（停止更新）、gateway（推荐）
<a name="Q4NHx"></a>
## 1.5 服务配置
Config（停止更新，不再使用）、Nacos（阿里，推荐使用）
<a name="U72GX"></a>
## 1.6 服务总线
Bus（停更，弃用）、Nacos（阿里，推荐使用）
<a name="Xnfhh"></a>
# 2、Cloud服务搭建过程
<a name="FADy4"></a>
## 2.1 新建maven项目，并加入简单的maven框架
![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1620385004865-21230b95-fe7d-4891-9cd9-b3418317075f.png#clientId=u30401bea-0686-4&from=paste&height=782&id=ud97c232d&margin=%5Bobject%20Object%5D&name=image.png&originHeight=782&originWidth=818&originalType=binary&size=154755&status=done&style=none&taskId=u0517965b-b538-4254-93d8-670836c671b&width=818)<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1620385076660-a08ec5a7-90e6-4e93-976d-440fb8451ea2.png#clientId=u30401bea-0686-4&from=paste&height=782&id=u3685dc45&margin=%5Bobject%20Object%5D&name=image.png&originHeight=782&originWidth=818&originalType=binary&size=63668&status=done&style=none&taskId=u47413b0b-701d-4d9d-8524-e177b9ec562&width=818)<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1620385100918-330f0340-50ec-4b10-9b12-09949931a9fa.png#clientId=u30401bea-0686-4&from=paste&height=782&id=u98927d8f&margin=%5Bobject%20Object%5D&name=image.png&originHeight=782&originWidth=818&originalType=binary&size=64282&status=done&style=none&taskId=u17543b79-57f8-419c-9c53-dba329de7a6&width=818)
<a name="rGt9I"></a>
## 2.2 项目基础设置
<a name="QFvdL"></a>
### 2.2.1 工程编码设置
![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1620385266433-776cbbd8-8945-44e0-a700-7da9d630f030.png#clientId=u30401bea-0686-4&from=paste&height=738&id=ua3b172ed&margin=%5Bobject%20Object%5D&name=image.png&originHeight=738&originWidth=998&originalType=binary&size=111277&status=done&style=none&taskId=ud4748c91-ceeb-4976-947d-2644c45e5af&width=998)
<a name="qmISA"></a>
### 2.2.2 注解生效激活
![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1620385333929-dcb24463-a89d-405e-8ec6-07f9fbef9651.png#clientId=u30401bea-0686-4&from=paste&height=738&id=u3c338ce2&margin=%5Bobject%20Object%5D&name=image.png&originHeight=738&originWidth=998&originalType=binary&size=115167&status=done&style=none&taskId=u96bff531-156a-4bb5-95c1-511f57aa9cb&width=998)
<a name="jM0oM"></a>
### 2.2.3 选择JDK编译版本
![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1620385488404-37e346b8-90be-48dc-90ef-ce7fab151d9a.png#clientId=u30401bea-0686-4&from=paste&height=738&id=u87fd4f6a&margin=%5Bobject%20Object%5D&name=image.png&originHeight=738&originWidth=998&originalType=binary&size=115883&status=done&style=none&taskId=u3a2b238e-988e-442e-baf2-27beaac3f3a&width=998)
<a name="ZNnlO"></a>
### 2.2.4 父级项目POM文件指定packing为pom
![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1620388018655-f61e821d-1e08-4894-a714-aaefbceaea55.png#clientId=u30401bea-0686-4&from=paste&height=196&id=ub75ae88e&margin=%5Bobject%20Object%5D&name=image.png&originHeight=196&originWidth=572&originalType=binary&size=22534&status=done&style=none&taskId=u393021bb-cc39-48d3-be25-ea6ffe53bdd&width=572)
<a name="Xoteo"></a>
### 2.2.5 删除项目目录下的src文件夹
![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1620388119999-e7f06cc9-92d5-4c74-8371-4f97b39ddb61.png#clientId=u30401bea-0686-4&from=paste&height=179&id=ufb4af536&margin=%5Bobject%20Object%5D&name=image.png&originHeight=179&originWidth=445&originalType=binary&size=12520&status=done&style=none&taskId=u523bce0a-1d6c-4a8f-8fc9-77d75f45ed2&width=445)
<a name="YeCwL"></a>
### 2.2.6 粘贴统一jar包管理
```xml
<!--统一管理jar包版本-->
  <properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <maven.compiler.source>1.8</maven.compiler.source>
    <maven.compiler.target>1.8</maven.compiler.target>
    <junit.version>4.12</junit.version>
    <log4j.version>1.2.17</log4j.version>
    <lombok.version>1.16.18</lombok.version>
    <mysql.version>5.1.47</mysql.version>
    <druid.version>1.1.16</druid.version>
    <mybatis.spring.boot.version>1.3.0</mybatis.spring.boot.version>
  </properties>

  <!--子模块继承之后，提供作用：锁定版本+子module不用groupId和version-->
<!--只是用于父工程管理依赖的，用于统一管理jar的版本。子工程需要使用相应的jar引入
依赖即可，这时才真正的使用到相应jar-->
<dependencyManagement>
  <dependencyManagement>
    <dependencies>
      <!--spring boot 2.2.2-->
      <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-dependencies</artifactId>
        <version>2.2.2.RELEASE</version>
        <type>pom</type>
        <scope>import</scope>
      </dependency>
      <!--spring cloud Hoxton.SR1-->
      <dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-dependencies</artifactId>
        <version>Hoxton.SR1</version>
        <type>pom</type>
        <scope>import</scope>
      </dependency>
      <!--spring cloud alibaba 2.1.0.RELEASE-->
      <dependency>
        <groupId>com.alibaba.cloud</groupId>
        <artifactId>spring-cloud-alibaba-dependencies</artifactId>
        <version>2.1.0.RELEASE</version>
        <type>pom</type>
        <scope>import</scope>
      </dependency>
      <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <version>${mysql.version}</version>
      </dependency>
      <dependency>
        <groupId>com.alibaba</groupId>
        <artifactId>druid</artifactId>
        <version>${druid.version}</version>
      </dependency>
      <dependency>
        <groupId>org.mybatis.spring.boot</groupId>
        <artifactId>mybatis-spring-boot-starter</artifactId>
        <version>${mybatis.spring.boot.version}</version>
      </dependency>
      <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>${junit.version}</version>
      </dependency>
      <dependency>
        <groupId>org.projectlombok</groupId>
        <artifactId>lombok</artifactId>
        <version>${lombok.version}</version>
        <optional>true</optional>
      </dependency>
    </dependencies>
  </dependencyManagement>

  <build>
    <plugins>
      <plugin>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-maven-plugin</artifactId>
        <configuration>
          <fork>true</fork>
          <addResources>true</addResources>
        </configuration>
      </plugin>
    </plugins>
  </build>
</project>
```
<a name="jcGh2"></a>
## 2.3 父工程发布
父工程创建完成后使用maven:install发布到仓库方便子工程继承，如不需要再执行clean即可清除<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1620455815402-ad24078c-d42a-4357-9df9-9f3680350898.png#clientId=ucc40c15a-f785-4&from=paste&height=422&id=u7085f3f9&margin=%5Bobject%20Object%5D&name=image.png&originHeight=422&originWidth=589&originalType=binary&size=27866&status=done&style=none&taskId=ue37524f8-7d31-4fcb-9816-402d630bca0&width=589)
<a name="tUnfa"></a>
# 3、 Maven知识概念
<a name="MLyFg"></a>
## 3.1 Maven中的DependencyManagement和Dependencies
1、通常会在一个组织或项目的最顶层的父POM中看到dependencyManagement；<br />2、使用pom.xml中的dependencyManagement元素能让所有在子项目中引用一个依赖而不用显式的列出版本号。Maven会沿着父子层次向上走，直到找到一个拥有dependencyManagement元素的项目，然后他就会使用这个dependencyManagement元素中指定的版本号；<br />**3、dependencyManagement里只是声明依赖，并不实现引入，因此子项目需要显式的声明dependencies需要用的依赖**<br />**4、如果不在子项目中声明依赖，是不会从父项目中继承下来的；只有在子项目中卸了该依赖项，并且没有指定具体版本，才会从父项目中继承该项，并且version和scope都读取自父POM**<br />
<br />

```xml
例如在父项目中：
<dependencyManagement>
    <dependencies>
      <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <version>5.1.2</version>
      </dependency>
     </dependencies>
</dependencyManagement>
然后在子项目中就添加mysql-connector-java可以不指定版本号，例如
<dependencies>
      <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
      </dependency>
</dependencies>

```
<a name="kLCLl"></a>
## 3.2 Maven跳过单元测试
点上闪电符号Maven生命周期的test会变为不可用<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1620455601387-2b87f978-00ee-49a2-a315-c31a81518e6c.png#clientId=ucc40c15a-f785-4&from=paste&height=466&id=u5e2d8ac3&margin=%5Bobject%20Object%5D&name=image.png&originHeight=466&originWidth=487&originalType=binary&size=26953&status=done&style=none&taskId=uca9105f8-e685-4490-bbc8-309ccc4d068&width=487)
<a name="SxD2h"></a>
# 4、微服务建立
<a name="AXfzW"></a>
## 4.1 服务端项目建立顺序流程
<a name="SIhUE"></a>
### 4.1.1 建Module
1、鼠标右键父工程建module<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1620456371090-872031e7-0f5c-498b-b827-05cdaabf290b.png#clientId=ucc40c15a-f785-4&from=paste&height=660&id=ufc222642&margin=%5Bobject%20Object%5D&name=image.png&originHeight=660&originWidth=854&originalType=binary&size=126789&status=done&style=none&taskId=u3fb66e2f-348d-4eb2-94dc-f1074f5fa24&width=854)<br />2、只需定义子工程的ArtifactId即可<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1620456675306-a3b83fc0-76b1-4c21-94a4-31e2fa30b03b.png#clientId=ucc40c15a-f785-4&from=paste&height=681&id=u72e8a419&margin=%5Bobject%20Object%5D&name=image.png&originHeight=681&originWidth=734&originalType=binary&size=61669&status=done&style=none&taskId=uc918f1c1-cb66-4e5a-8f37-81df510897f&width=734)<br />3、创建成功后父工程pom中会多出子module信息<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1620456845928-8e7e84f0-82ca-499e-84fa-75f384bef76a.png#clientId=ucc40c15a-f785-4&from=paste&height=288&id=u559655e5&margin=%5Bobject%20Object%5D&name=image.png&originHeight=288&originWidth=633&originalType=binary&size=35284&status=done&style=none&taskId=u8286f865-f3ed-47e0-ba5c-80aa70a73dc&width=633)
<a name="q76WG"></a>
### 4.1.2 改POM
```xml
将子类需要pom依赖加入
<artifactId>cloud-provider-payment8001</artifactId>

    <dependencies>
        <!--包含了sleuth+zipkin-->
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-zipkin</artifactId>
        </dependency>
        <!--eureka-client-->
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
        </dependency>
        <!--引入自己定义的api通用包，可以使用Payment支付Entity-->
        <dependency>
            <groupId>com.atguigu.springcloud</groupId>
            <artifactId>cloud-api-commons</artifactId>
            <version>${project.version}</version>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>
        <dependency>
            <groupId>org.mybatis.spring.boot</groupId>
            <artifactId>mybatis-spring-boot-starter</artifactId>
        </dependency>
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>druid-spring-boot-starter</artifactId>
            <version>1.1.10</version>
        </dependency>
        <!--mysql-connector-java-->
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-jdbc</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>
</project>
```
<a name="GPG4s"></a>
### 4.1.3 写YML
1、子工程新建YAML<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1620457715526-98e9584f-c1a3-4e27-947c-744b2371cb0f.png#clientId=ucc40c15a-f785-4&from=paste&height=136&id=u8b22a438&margin=%5Bobject%20Object%5D&name=image.png&originHeight=136&originWidth=275&originalType=binary&size=6418&status=done&style=none&taskId=u1fa17e47-0f63-4d7c-85f5-24ae7eb2cf4&width=275)<br />2、加入相关配置
```yaml
server:
  port: 8001

spring:
  application:
    name: cloud-provider-service

  datasource:
    type: com.alibaba.druid.pool.DruidDataSource      #当前数据源操作类型
    driver-class-name: org.gjt.mm.mysql.Driver        #mysql驱动包
    url: jdbc:mysql://localhost:3306/db2019?useUnicode=true&characterEncoding=utf-8&useSSL=false
    username: root
    password: root
  zipkin:
    base-url: http://localhost:9411
  sleuth:
    sampler:
      probability: 1

eureka:
  client:
    #表示是否将自己注册进EurekaServer默认为true
    register-with-eureka: true
    #是否从EurekaServer抓取已有的注册信息，默认为true。单节点无所谓，集群必须设置为true才能配合ribbon使用负载均衡
    fetch-registry: true
    service-url:
      defaultZone: http://localhost:7001/eureka #单机版
      #defaultZone: http://eureka7001.com:7001/eureka,http://eureka7002.com:7002/eureka  #集群版
  instance:
    instance-id: payment8001
    prefer-ip-address: true #访问路径可以显示IP地址
    #Eureka客户端向服务端发送心跳的时间间隔，单位为秒（默认是30秒）
    #lease-renewal-interval-in-seconds: 1
    #Eurekaf服务端在收到最后一次心跳后等待时间上限，单位为秒（默认是90秒），超时将剔除服务
    #lease-expiration-duration-in-seconds: 2


mybatis:
    mapper-locations: classpath:mapper/*.xml
    type-aliases-package: com.atguigu.springcloud.entities       #所有Entity别名类所在包
```
<a name="r746w"></a>
### 4.1.4 主启动
创建主启动类<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1620459877386-3dfff4bb-f2cd-473f-b2f9-cfb4e7dfabf0.png#clientId=ucc40c15a-f785-4&from=paste&height=400&id=u1217da81&margin=%5Bobject%20Object%5D&name=image.png&originHeight=400&originWidth=1293&originalType=binary&size=84072&status=done&style=none&taskId=u5fcb2273-e50d-4d59-9b0c-16ea116eda2&width=1293)
<a name="OqjVp"></a>
### 4.1.5 写业务
```java
/**
 * 通用返回传给前端的类
 */
@Data
@AllArgsConstructor
@NoArgsConstructor
public class CommonResult<T> {
    //返回请求状态码
    private Integer code;
    //返回消息
    private String msg;
    //实体类
    private T date;

    public CommonResult(Integer code,String msg){
        this(code,msg,null);
    }
}
```
服务端Controller
```java
@RestController
@Slf4j
public class PaymentController {
    @Autowired
    PaymentService paymentService;

    @GetMapping("/service/selectPaymentById/{id}")
    public CommonResult selectPaymentById(@PathVariable("id") Long id){
        Payment payment = paymentService.selectById(id);
        if(payment != null){
            log.info("查询成功"+payment);
            return new CommonResult(200,"查询成功",payment);
        }else{
            log.info("查询失败");
            return new CommonResult(444,"查询失败",null);
        }
    }

    @PostMapping("/service/addPayment")
    public CommonResult addPayment(@RequestBody Payment payment){
        int result = paymentService.add(payment);
        if(result > 0){
            log.info("添加成功");
            return new CommonResult(200,"入库成功");
        }else{
            log.info("添加失败");
            return new CommonResult(444,"入库失败");
        }
    }
}
```
<a name="sVTMz"></a>
## 4.2 客户端项目建立
与服务端建立相同，只需配置文件指定80端口和编写bean实体和Controller层调用服务就OK
<a name="w4aro"></a>
### 4.2.1 创建配置类配置RestTemplate
```java
@Configuration
public class ApplicationContextConfig {
    @Bean
    public RestTemplate getRestTemplate(){
        return new RestTemplate();
    }
}
```
<a name="g9Hb6"></a>
### 4.2.2 Controller中注入并实例化RestTemplate
```java
@RestController
@Slf4j
public class OrderController {
    //服务端地址
    public static final String PAYMENT_URL="http://localhost:8001";

    @Autowired
    RestTemplate restTemplate;

    @GetMapping("order/addPayment")
    public CommonResult<Payment> addPayment(Payment payment){
        return restTemplate.postForObject(PAYMENT_URL+"/service/addPayment",payment,CommonResult.class);
    }

    @GetMapping("order/selectPaymentById")
    public CommonResult selectPaymentById(@RequestParam("id") Long id) {
        return restTemplate.getForObject(PAYMENT_URL + "/service/selectPaymentById/" + id, CommonResult.class);
    }
}
```
<a name="XcOcO"></a>
## 4.3 IDEA2020.3版本Service服务窗口开启
![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1620480095282-6f1fd21b-106a-42d2-8861-63b59c484081.png#clientId=ucc40c15a-f785-4&from=paste&height=574&id=u18f3c4d3&margin=%5Bobject%20Object%5D&name=image.png&originHeight=574&originWidth=568&originalType=binary&size=87825&status=done&style=none&taskId=ue233758d-524f-4215-9d78-81806ae9c37&width=568)<br />弹出窗口选择SpringBoot<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1620480112919-ea1790d3-97ec-4a6a-8de3-04251f9ca5f3.png#clientId=ucc40c15a-f785-4&from=paste&height=110&id=u811333e8&margin=%5Bobject%20Object%5D&name=image.png&originHeight=110&originWidth=180&originalType=binary&size=4993&status=done&style=none&taskId=u3b81c673-6e82-44dc-8505-a2598a855fc&width=180)
<a name="JAveK"></a>
## 4.4 工程重构，去除冗余
<a name="ci0lR"></a>
### 4.4.1 新建通用类工程，将其他微服务重复代码抽取至新工程
![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1620482374533-ae5a3629-c494-42cc-b11c-e54a73cb6c35.png#clientId=ucc40c15a-f785-4&from=paste&height=247&id=ue03baae3&margin=%5Bobject%20Object%5D&name=image.png&originHeight=247&originWidth=424&originalType=binary&size=11359&status=done&style=none&taskId=u3a39eecb-12a6-41fc-938c-31025af7d41&width=424)
<a name="O4wiM"></a>
### 4.4.2 通用工程pom文件引入通用jar
```xml
<dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>cn.hutool</groupId>
            <artifactId>hutool-all</artifactId>
            <version>5.1.0</version>
        </dependency>
    </dependencies>
</project>
```
<a name="rN74k"></a>
###  4.4.3 通用工程打包
先clean，没有问题install安装打包<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1620482508573-880768df-dd10-48cd-a25e-b3fa10928aeb.png#clientId=ucc40c15a-f785-4&from=paste&height=331&id=u3e67e757&margin=%5Bobject%20Object%5D&name=image.png&originHeight=331&originWidth=373&originalType=binary&size=21539&status=done&style=none&taskId=ua8b17ed0-6cbd-421c-b5aa-3a8c19be1e2&width=373)
<a name="VMxAJ"></a>
### 4.4.4 其他微服务工程引入打包好的通用工程
![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1620482791373-8b8d140e-ed48-4df8-86ff-0940cbdf2dad.png#clientId=ucc40c15a-f785-4&from=paste&height=187&id=u51edc5ad&margin=%5Bobject%20Object%5D&name=image.png&originHeight=187&originWidth=667&originalType=binary&size=32614&status=done&style=none&taskId=u9318df95-855b-4ce6-8e3d-bc281b3a076&width=667)
<a name="eJlca"></a>
# 5、Eureka服务注册与发现(服务注册中心)
<a name="P9DDT"></a>
## 5.1 Eureka基础知识
<a name="Cfu1b"></a>
### 5.1.1 服务治理
Spring Cloud封装了Netflix公司开发的Eureka模块来实现服务治理；<br />在传统的rpc远程调用框架中，管理每个服务与服务之间依赖关系比较复杂，管理比较复杂，所以需要使用服务治理，管理服务与服务之间的依赖关系，可以实现服务调用、负载均衡、容错等，实现服务发现与注册。
<a name="xg0qc"></a>
### 5.1.2 服务注册与发现
       Eureka采用了CS的设计架构，Eureka Server作为服务注册功能的服务器，它是服务注册中心。而系统中的其他微服务，使用Eureka的客户端连接到Eureka Server并维持心跳链接，这样系统的维护人员就可以通过Eureka Server来监控系统中各个微服务是否正常运行。<br /> 在服务注册与发现中，有一个注册中心。当服务器启动的时候，会把当前自己服务器的信息比如服务器通讯地址等以别名注册到注册中心上。另一方（消费者|服务提供者），以该别名的方式去注册中心上获取到实际的服务通讯地址，然后在实现本地RPC远程调用框架核心的设计思想：在于注册中心，因为使用注册中心管理每个服务与服务之间的一个依赖关系（服务治理概念）。在任何rpc远程框架中，都会有一个注册中心（存放服务地址相关信息（接口地址））
<a name="WQQPh"></a>
### 5.1.3 Eureka系统架构与Dubbo架构对比
![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1620543096814-c76607d4-e097-46fb-88ae-b3a693bcf70b.png#clientId=ue4fded7f-337e-4&from=paste&height=374&id=u764d3bda&margin=%5Bobject%20Object%5D&name=image.png&originHeight=374&originWidth=1135&originalType=binary&size=143539&status=done&style=none&taskId=u40fd75dd-8881-4c76-9f68-c020d9047e0&width=1135)
<a name="rseTR"></a>
### 5.1.4 Eureka组件，Eureka Server和Eureka Client
**1、Eureka Server提供服务注册服务**<br />各个微服务节点通过配置启动后，会在EurekaServer中进行注册，这样EurekaServer中的服务注册表中将会存储所有可用服务节点的信息，服务节点的信息可以在界面中直观看到。（**新版Eureka Server已经集成了Ribbon**）<br />**2、EurekaClient通过注册中心进行访问**<br />是一个java客户端，用户简化Eureka Server的交互，客户端同时也具备一个内置的、使用轮询（round-robin）负载算法的负载均衡器。在应用启动后，将会向Eureka Server发送心跳（默认周期为30秒）。如果Eureka Server在多个心跳周期内没有接收到某个节点的心跳，EurekaServer将会从服务注册表中把这个服务节点移除（默认90秒）
<a name="QP7w6"></a>
## 5.2 建立Eureka Server
![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1620543914133-94646d79-2755-4b9c-b5e4-6dc527bd171e.png#clientId=ue4fded7f-337e-4&from=paste&height=681&id=u81446b29&margin=%5Bobject%20Object%5D&name=image.png&originHeight=681&originWidth=734&originalType=binary&size=63744&status=done&style=none&taskId=ub72099b2-31ca-45bb-8b62-7a30bcb906e&width=734)
```xml
引入Eureka Server依赖
				<dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>
        </dependency>
```
```java
@SpringBootApplication
@EnableEurekaServer //代表这是Eureka服务注册中心
public class Main7001 {
    public static void main(String[] args) {
        SpringApplication.run(Main7001.class,args);
    }
}
```
```yaml
server:
  port: 7001

eureka:
  instance:
    hostname: locahost #eureka服务端的实例名称
  client:
    #false表示不向注册中心注册自己
    register-with-eureka: false
    #false表示自己端就是注册中心，我的职责就是维护服务实例，并不需要去检索服务
    fetch-registry: false
    service-url:
      #设置与Eureka Server交互的地址查询服务和注册服务都需要依赖这个地址
      #defaultZone: http://eureka7002.com:7002/eureka/  #互相注册
      defaultZone: http://${eureka.instance.hostname}:${server.port}/eureka/ #单机模式
    #server:
    #关闭自我保护机制，保证不可用服务被及时剔除
    #enable-self-preservation: false
    #eviction-interval-timer-in-ms: 2000
```
运行项目访问localhost:7001出现页面即为成功<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1620545798189-deabb88d-3a69-4762-9880-44e9ac435aa0.png#clientId=ue4fded7f-337e-4&from=paste&height=1048&id=u55a89a7f&margin=%5Bobject%20Object%5D&name=image.png&originHeight=1048&originWidth=1920&originalType=binary&size=214256&status=done&style=none&taskId=uaaec9842-4553-4137-af5e-a8d19ca09ee&width=1920)
<a name="egbsc"></a>
## 5.3 注册微服务到Eureka Server
```xml
POM中加入配置
				<dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
        </dependency>
```
```yaml
配置文件中增加
eureka:
  client:
    #表示是否将自己注册进EurekaServer默认为true
   register-with-eureka: true
    #是否从EurekaServer抓取已有的注册信息，默认为true。单节点无所谓，集群必须设置为true才能配合ribbon使用负载均衡
    fetch-registry: true
    service-url:
      defaultZone: http://localhost:7001/eureka #单机版
```
```java
主启动类代码增加
@MapperScan("com.zq.cloud.dao")
@SpringBootApplication
@EnableEurekaClient //表示这是Eureka的连接端
public class Main8001 {
    public static void main(String[] args) {
        SpringApplication.run(Main8001.class,args);
    }
}
```
启动连接客户端程序然后查看Eureka监控页面出现服务名则启动成功<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1620546857999-4530799b-77ff-4f68-824c-122cd9e28881.png#clientId=ue4fded7f-337e-4&from=paste&height=1022&id=ufc4025db&margin=%5Bobject%20Object%5D&name=image.png&originHeight=1022&originWidth=1920&originalType=binary&size=198438&status=done&style=none&taskId=u5576a8c8-9020-4c6d-848b-a64ea3a623a&width=1920)
<a name="XXWDV"></a>
## 5.4 Eureka集群
<a name="yNVAD"></a>
### 5.4.1 原理
相互注册，互相守望，对外暴露一个整体<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1620547637700-877083b9-59c2-4d68-9090-8e12b138d802.png#clientId=ue4fded7f-337e-4&from=paste&height=382&id=u8dd68466&margin=%5Bobject%20Object%5D&name=image.png&originHeight=382&originWidth=1121&originalType=binary&size=228261&status=done&style=none&taskId=ua6bb2945-fc99-4dc7-b0d3-6676b6fa4c0&width=1121)
<a name="sYsRA"></a>
### 5.4.2 Eureka集群搭建
<a name="uDMHw"></a>
#### 1、修改服务器映射文件，学习拿本机windos举例
修改映射文件C:\Windows\System32\drivers\etc下的hosts文件，添加所有Eureka服务器IP<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1620548865430-a02aef84-287c-40d8-9b9f-6ca0892c6910.png#clientId=ue4fded7f-337e-4&from=paste&height=37&id=u878d12a9&margin=%5Bobject%20Object%5D&name=image.png&originHeight=37&originWidth=197&originalType=binary&size=1538&status=done&style=none&taskId=u3ecea502-c3cf-4ef6-a1b3-51af30c8da0&width=197)
<a name="jjCdx"></a>
#### 2、修改yaml配置文件
```yaml
更改hostname和defaultZone
server:
  port: 7001

eureka:
  instance:
    hostname: eureka7001.com #eureka服务端的实例名称
  client:
    #false表示不向注册中心注册自己
    register-with-eureka: false
    #false表示自己端就是注册中心，我的职责就是维护服务实例，并不需要去检索服务
    fetch-registry: false
    service-url:
      #设置与Eureka Server交互的地址查询服务和注册服务都需要依赖这个地址
      defaultZone: http://eureka7002.com:7002/eureka/  #互相注册，多个值逗号隔开
      #defaultZone: http://${eureka.instance.hostname}:${server.port}/eureka/ #单机模式
    #server:
    #关闭自我保护机制，保证不可用服务被及时剔除
    #enable-self-preservation: false
    #eviction-interval-timer-in-ms: 2000
```
<a name="tEfOw"></a>
#### 3、启动两台Eureka Server并访问Eureka页面
看到如下效果则代表成功<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1620549525978-053cb60e-6bd8-4c10-86d6-effdab1f0676.png#clientId=ue4fded7f-337e-4&from=paste&height=516&id=uab1b18f9&margin=%5Bobject%20Object%5D&name=image.png&originHeight=516&originWidth=420&originalType=binary&size=28116&status=done&style=none&taskId=u73be15df-820c-4c9b-b7d6-bba9eabf81e&width=420)<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1620549537791-036801b8-d85d-4f15-b8a5-a0acf4d1e0fd.png#clientId=ue4fded7f-337e-4&from=paste&height=572&id=u249f8fa7&margin=%5Bobject%20Object%5D&name=image.png&originHeight=572&originWidth=414&originalType=binary&size=35740&status=done&style=none&taskId=u67cb4d1a-2469-44c1-a112-24985b45f58&width=414)
<a name="vUNWt"></a>
#### 4、微服务注册到Eureka集群yaml配置修改
```yaml
eureka:
  client:
    #表示是否将自己注册进EurekaServer默认为true
    register-with-eureka: true
    #是否从EurekaServer抓取已有的注册信息，默认为true。单节点无所谓，集群必须设置为true才能配合ribbon使用负载均衡
    fetch-registry: true
    service-url:
      #单机版
      #defaultZone: http://localhost:7001/eureka
      defaultZone: http://eureka7001.com:7001/eureka,http://eureka7002.com:7002/eureka  #集群版
```
<a name="EkVnr"></a>
#### 5、客户端通过Eureka集群访问微服务
```java
服务请求地址不再写具体IP，只写微服务注册到Eureka中的服务名
//public static final String PAYMENT_URL="http://localhost:8001";
  public static final String PAYMENT_URL="http://CLOUD-PAYMENT-SERVICE";

//客户端注入RestTemplate配置类添加@LoadBalanced注解，开启RestTemplate的负载均衡能力
@Configuration
public class ApplicationContextConfig {
    @Bean
    @LoadBalanced
    public RestTemplate getRestTemplate(){
        return new RestTemplate();
    }
}
```
<a name="J7elO"></a>
#### 6、Eureka集群监控显示服务名和访问IP
```yaml
eureka配置中加入instance下的instance-id和prefer-ip-address
eureka:
  client:
    #表示是否将自己注册进EurekaServer默认为true
    register-with-eureka: true
    #是否从EurekaServer抓取已有的注册信息，默认为true。单节点无所谓，集群必须设置为true才能配合ribbon使用负载均衡
    fetch-registry: true
    service-url:
      #单机版
      #defaultZone: http://localhost:7001/eureka
      defaultZone: http://eureka7001.com:7001/eureka,http://eureka7002.com:7002/eureka  #集群版
  instance:
      instance-id: payment8002 #服务名显示
      prefer-ip-address: true #访问路径可以显示IP地址
```
测试结果如图显示即为成功<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1620553297398-520e67d3-5720-4a5f-b9c2-365d66268292.png#clientId=ue4fded7f-337e-4&from=paste&height=505&id=u5651f322&margin=%5Bobject%20Object%5D&name=image.png&originHeight=505&originWidth=1519&originalType=binary&size=76635&status=done&style=none&taskId=u7a5686aa-2f63-4e13-9e57-6f2c7ef5dca&width=1519)
<a name="A5G37"></a>
## 5.5 服务发现Discovery
```java
在主启动类上加上注解“@EnableDiscoveryClient”开启Discovery服务发现功能

在Controller中注入DiscoveryClient
@Autowired
private DiscoveryClient discoveryClient;
写一个Controller用于触发获取相应信息
/**
     * 获取当前微服务下的服务信息
     * @return
     */
    @GetMapping("/service/discoveryClient")
    public Object discovery(){
        //获取注册在Eureka中所用的微服务名称
        List<String> services = discoveryClient.getServices();
        for (String service: services ) {
            log.info("service:"+service);
        }
        //根据微服务名称获取该服务的所有相关服务信息
        List<ServiceInstance> instances = discoveryClient.getInstances("CLOUD-PAYMENT-SERVICE");
        for (ServiceInstance instance : instances) {
            log.info(instance.getServiceId()+"---"+instance.getUri()+"---"+instance.getHost()+"---"+instance.getPort());
        }
        return discoveryClient;
    }
```
<a name="Rqqzl"></a>
## 5.6 Eureka的自我保护
**概述**<br />保护模式主要用于一组客户端和Eureka Server之间存在网络分区场景下的保护。一旦进入保护模式<br />**自我保护机制：默认情况EurekaClient定时向EurekaServer端发送心跳包，如果Eurekaserver端在一定时间内（默认90秒）没有收到EurekaClient发送心跳包，便会直接从服务注册列表中剔除该服务，但是当Eureka Server节点在短时间（90秒内）丢失过多客户端时（可能发生网络分区故障），那么这个节点就会进入自我保护模式**<br />Eureka Server将会尝试保护其他服务注册表中的信息，不在删除服务注册表中的数据，也就是不会注销任何微服务<br />**简单来说：某时刻某一个微服务不可用了，Eureka不会立刻清理，依旧会对该微服务的信息进行保存**<br />**看到如图所示则代表Eureka进入了自我保护模式**<br />![](https://cdn.nlark.com/yuque/0/2021/png/12668119/1620562479779-3e10c027-6c37-4c63-9a29-27ca22f979ee.png#clientId=u2cd453e1-735a-4&from=paste&height=344&id=u27851ddb&margin=%5Bobject%20Object%5D&originHeight=344&originWidth=1354&originalType=url&status=done&style=none&taskId=u6d39a1f1-a381-4ac3-bc6a-618e3cafc40&width=1354)
<a name="O0wVN"></a>
## 5.7关闭Eureka自我保护机制
```xml
EurekaServer端配置文件
server:
    #关闭自我保护机制，保证不可用服务被及时剔除
    enable-self-preservation: false
		#设置多长时间之内没有接收到客户端心跳就剔除该服务
    eviction-interval-timer-in-ms: 2000
EurekaClient端配置文件
instance:
      
    #Eureka客户端向服务端发送心跳的时间间隔，单位为秒（默认是30秒）
    lease-renewal-interval-in-seconds: 1
    #Eurekaf服务端在收到最后一次心跳后等待时间上限，单位为秒（默认是90秒），超时将剔除服务
    lease-expiration-duration-in-seconds: 2
```
<a name="YLsO1"></a>
# 6、Ribbon(服务调用)入门介绍


<a name="kaqLi"></a>
## 6.1 基本概念
**负载均衡概念**<br />将用户的请求平摊的分配到多个服务上，从而达到系统的HA(高可用)<br />常见的负载均衡有软件Nginx，LVS，硬件F5等。<br />
<br />Spring Cloud Ribbon是基于Netflix Ribbon实现的一套客户端，负载均衡的工具。<br />简单的说，Ribbon是Netflix发布的开源项目，主要功能是提供**客户端的软件负载均衡算法和服务调用**。Ribbon客户端组件提供一系列完善的配置项如连接超时，重试等。简单的说，就是在配置文件中列出LoadBalancer后面所有的机器，Ribbon会自动帮助你基于某种规则（如简单轮询，随机连接等）区连接这些机器。我们很容易使用Ribbon实现自定义的负载均衡算法。<br />
<br />**Ribbon本地负载均衡客户端 VS Nginx服务端负载均衡区别**<br />Nginx是服务器负载均衡，客户端所有请求都会交给Nginx，然后由Nginx实现转发请求。即负载均衡是由服务端实现的。<br />Ribbon本地负载均衡，在调用微服务接口时候，会在注册中心上获取注册信息服务列表之后缓存到JVM本地，从而实现RPC远程服务调用技术。<br />**进程内负载均衡**<br />将负载均衡逻辑集成到消费方，消费方从服务注册中心获知有哪些地址可用，然后自己再从这些地址中选择出一个合适的服务器。<br />Ribbon就属于这种情况，它只是一个类库，集成于消费方进程，消费方通过它来获取到服务提供方的地址
<a name="EUp5H"></a>
## 6.2 Ribbon自带负载均衡策略
**轮询**<br />com.netflix.loadbalancer.RoundRobinRule<br />**随机**<br />com.netflix.loadbalancer.RandomRule<br />**先按照轮询策略获取服务，如果获取服务失败则在指定时间内会进行重试，获取可用服务**<br />com.netflix.loadbalancer.RetryRule<br />**对轮询的扩展，响应速度越快的实例选择权重越大，越容易被选择**<br />WeightedResponseTimeRule<br />**会先过滤掉由于多次访问故障而处于断路器跳闸状态的服务，然后选择一个并发量最小的服务**<br />BestAvailableRule<br />**先过滤掉故障实例，在选择并发较小的实例**<br />AvailabilityFilteringRule<br />**默认规则，复合判断server所在区域的性能和server的可用性选择服务器**<br />ZoneAvoidanceRule
<a name="BENoy"></a>
## 6.3 Ribbon负载规则替换
注意：该方案不能放在@ComponentScan注解可扫描的包及其子包以下，否则自定义配置类就会被所有客户端共享达不到单独配置的目的，所以要自己建新包不在@ComponentScan扫描范围。
```java
自定义配置类将Ribbon负载策略定义为随机
@Configuration
public class MyRule {
    @Bean
    public IRule myRule(){
        return new RandomRule();//定义为随机
    }
}
主启动类添加@RibbonClient指定访问服务使用的负载策略
@SpringBootApplication
@EnableEurekaClient
@RibbonClient(name="CLOUD-PAYMENT-SERVICE",configuration = MyRule.class)
public class Main80 {
    public static void main(String[] args) {
        SpringApplication.run(Main80.class,args);
    }
}
```
<a name="j2xDa"></a>
## 6.4 负载均衡算法
rest接口第几次请求数 **%（取余）** 服务器集群总数量 = 实际调用服务器位置下标，每次服务器重启后rest接口计数从1开始计算
<a name="PILx3"></a>
# 7、 OpenFeign(服务调用)
<a name="awxqN"></a>
## 7.1 概念
是一个声明式的Web服务客户端，让编写Web服务客户端变得非常容易，只需创建一个接口并在接口上添加注解即可<br />Feign旨在使编写Java Http客户端变得更容易<br />前面在使用Ribbon+RestTemplate时，利用RestTemplate对http请求的封装处理，形成了一套模板化的调用方法，但在实际开发中，由于对服务依赖的调用可能不止一处，**往往一个接口会被多处调用，所以通常都会针对每个微服务自行封装一些客户端来包装这些依赖服务的调用**，Feign在此基础上做了进一步封装，由他来帮助我们定义和实现依赖服务接口的定义。在Feign的实现下，**我们只需创建一个接口并使用注解的方式来配置它（以前是Dao接口上面标注Mapper注解，现在是一个微服务接口上面标注一个Feign注解即可**），即可完成对服务提供方的接口绑定，简化了使用Spring cloud Ribbon时，自动封装服务调用客户端的开发量<br />

<a name="wAHjo"></a>
## 7.2 GitHub地址
https://github.com/spring-cloud/spring-cloud-openfeign<br />
<br />Feign集成了Ribbon<br />利用Ribbon维护了Payment的服务列表信息，并且通过轮询实现了客户端的负载均衡。而与Ribbon不同的是，**通过feign只需要定义服务绑定接口且以声明式的方法**，优雅而简单的实现饿了服务调用
<a name="RF8kZ"></a>
## 7.3 OpenFeign使用
**Feign在客户端使用**
```xml
客户端pom加入插件
				<dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-openfeign</artifactId>
        </dependency>
```
```java
主启动类上加@EnableFeignClients注解开启Feign
@SpringBootApplication
@EnableFeignClients
public class MainFeign80 {
    public static void main(String[] args) {
        SpringApplication.run(MainFeign80.class,args);
    }
}
定义service接口加入@FeignClient使用Feign
@Component
@FeignClient("CLOUD-PAYMENT-SERVICE")
public interface PaymentFeignService {
    @GetMapping("/service/selectPaymentById/{id}")//此处接口地址定义是真正服务的地址
    public CommonResult<Payment> selectPaymentById(@PathVariable("id") Long id);
}
```
<a name="r8BGW"></a>
## 7.4 OpenFeign超时控制
**feign默认等待服务端返回结果为1秒钟，超时就会报错**
```java
服务端故意延时三秒返回
	@GetMapping("service/feign/timeout")
    public String paymentFeignTimeout(){
        try {
            TimeUnit.SECONDS.sleep(3);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        return serverPort;
    }
```
```yaml
feign默认集成了ribbon,所以超时控制也由ribbon来实现,配置文件中加入如下配置开启feign超时等待
#设置feign 客户端超时时间（openFeign默认支持ribbon）
ribbon:
#指的是建立连接所用的时间，适用于网络状况正常的情况下，两端连接所用的时间
  ReadTimeout: 5000
#指的是建立连接后从服务器读取到可用资源所用的时间
  ConnectTimeout: 5000
```
<a name="worSo"></a>
## 7.5 OpenFeign日志增强
Feign提供了日志打印功能，我们可以通过配置来调整日志级别，从而了解Feign中Http请求的细节。<br />**可以对Feign接口的调用情况进行监控和输出**<br />**日志级别：**<br />**NONE：默认，不显示任何日志**<br />**BASIC：仅记录请求方法、URL、响应状态码及执行时间；**<br />**HEADERS：除了BASIC中定义的信息之外，还有请求和响应的头信息**<br />**FULL：除了HEADERS中定义的信息之外，还有请求和响应的正文及元数据**
```java
加入配置日志Bean，新建config包当做配置类建立
import feign.Logger;//注意日志包要引入feign
@Configuration
public class FeignLogConfig {
    @Bean
    Logger.Level feignLoggerLevel(){
        return Logger.Level.FULL;
    }
}

```
```yaml
配置文件如下配置开启日志监控
logging:
  level:
    #feign日志以什么级别监控哪个接口
    com.zq.cloud.service.PaymentFeignService: debug
```
<a name="t271S"></a>
# 8、 Hystrix(服务降级、服务熔断、接近实时监控)
<a name="MZNye"></a>
## 8.1 服务雪崩概念
       多个微服务之间调用的时候，假设微服务A调用微服务B和微服务C，微服务B和微服务C又调用其他的微服务，这就是所谓的“扇出”如果扇出的链路上某个微服务的调用响应时间过长或者不可用，对微服务A的调用就会占用越来越多的系统资源，进而引起系统崩溃，所谓的“雪崩效应”。<br />       对于高流量的应用来说，单一的后端依赖可能会导致所有服务器上的所有资源都在几秒钟内饱和。比失败更糟糕的是，这些应用程序还可能导致服务之间的延迟增加，备份队列，线程和其他系统资源紧张，导致整个系统发生更多的级联故障。这些都表示需要对故障和延迟进行隔离和管理，以便单个依赖关系的失败，不能取消整个应用程序或系统。<br />       所以，通常发现一个模块下的某个实例失败后，这时候这个模块依然还会接收流量，然后这个有问题的模块还调用了其他的模块，这样就会发生级联故障，或叫雪崩。
<a name="Hkl8F"></a>
## 8.2 服务降级
**服务器忙，不让客户等待并立即返回一个友好提示**<br />发生降级的情况：<br />程序运行异常、超时、服务熔断发生的服务降级、线程池/信号量打满发生服务降级
<a name="Mu8V5"></a>
## 8.3 服务熔断
类比保险丝达到最大服务访问后，直接拒绝访问，拉闸限电，然后调用服务降级的方法并返回友好提示<br />就是保险丝，**服务降级->进而熔断->恢复调用链路**
<a name="MP7N1"></a>
### 8.3.1 断路器
一句话就是保险丝<br />涉及到断路器的三个重要参数：<br />1、快照时间窗：断路器确定是否打开需要统计一些请求和错误数据，而统计的时间范围就是快照时间窗，默认为最近的10秒。<br />2、请求总数阈值：在快照时间窗内，必须满足请求总数阈值才有资格熔断。默认为20，意味着在10秒内，如果该hystrix命令的调用次数不足20次即使所有的请求都超时或其他原因失败，断路器都不会打开<br />3、错误百分比阈值：当请求总数在快照时间窗内超过了阈值，比如发生了30次调用，如果在这30次调用中，有15次发生了超时异常，也就是超过50%的错误百分比，在默认设定50%阈值的情况下，这时候就会将断路器打开<br />4、当断路器被打开的时候（**再有请求调用则不会调用主逻辑，而直接调用fallback**）<br />5、一段时间后（默认是5秒），这个时候断路器是半开状态，会让其中一个请求进行转发，如果成功，则断路器关闭，若失败，则继续开启重复4-5步。
<a name="Y7Kx6"></a>
### 8.3.2 熔断机制概述
熔断机制是应对雪崩效应的一种微服务链路保护机制。当扇出链路的某个微服务出错不可用或者响应时间太长时，会进行服务降级，进而熔断该节点微服务的调用，快速返回错误的响应信息。<br />**当检测到该节点微服务调用响应正常后，恢复调用链路**<br />在Spring Cloud框架中，熔断机制通过Hystrix实现。Hystrix会监控微服务间调用的状况，当失败的调用到一定阈值，缺省是5秒内20次调用失败，就会启动熔断机制。熔断机制的注解是@HystrixCommand
<a name="YRe1r"></a>
## 8.4 服务限流
秒杀高并发等操作，严禁一窝蜂的过来拥挤，大家排队，一秒钟N个，有序进行
<a name="Du5Wm"></a>
## 8.5 HyStrix概念
       Hystrix是一个用于处理分布式系统的**延迟**和**容错**的开源库，在分布式系统里，许多依赖不可避免的会调用失败，比如超时、异常等。<br />       Hystrix能够保证在一个依赖出问题的情况下，**不会导致整体服务失败，避免级联故障，以提高分布式系统的弹性。**<br />       “断路器”本身是一种开关装置，当某个服务单元发生故障之后，通过断路器的故障监控（类似熔断保险丝），**向调用方返回一个符合预期的、可处理的备选响应（FallBack），而不是长时间的等待或者抛出调用方无法处理的异常**，这样就保证了服务调用方的线程不会被长时间、不必要地占用，从而避免了故障在分布式系统的蔓延，乃至雪崩。
<a name="kNI77"></a>
## 8.6 GitHub地址
https://github.com/Netflix/Hystrix/wiki/How-To-Use
<a name="RhBsE"></a>
## 8.7 服务降级配置
**一般服务降级放在客户端**<br />**服务端开启服务降级代码写法**
```java
服务端业务类启动注解@HystrixCommand
//fallbackMethod，timeOut方法异常或超时会找该配置下的方法作为兜底处理
//commandProperties配置@HystrixProperty，下面的意思为注解标注的方法三秒钟返回结果算正常，否则异常
@HystrixCommand(fallbackMethod = "timeOutHandler",commandProperties = {
   @HystrixProperty(name = "execution.isolation.thread.timeoutInMilliseconds",value = "3000")
})
    @Override
    public String timeOut(Integer id) {
        try {
            TimeUnit.SECONDS.sleep(3);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        return "线程池:"+Thread.currentThread().getName()+"timeout,id:"+id;
    }
    public String timeOutHandler(Integer id) {
        return "timeOut方法暂时异常，交由我来托管";
    }
服务端主启动类加注解@EnableCircuitBreaker激活服务降级功能
@SpringBootApplication
@EnableEurekaClient
@EnableCircuitBreaker
public class MainHystrix8001 {
    public static void main(String[] args) {
        SpringApplication.run(MainHystrix8001.class,args);
    }
}
```
**客户端开启服务降级代码写法**
```yaml
配置文件加入配置开启feign的hystrix服务降级
feign:
  hystrix:
    enabled: true
```
```java
主启动类加注解@EnableHystrix开启功能
@SpringBootApplication
@EnableFeignClients
@EnableHystrix
public class MainHystrixOrder80 {
    public static void main(String[] args) {
        SpringApplication.run(MainHystrixOrder80.class,args);
    }
}
Controller类加入如下配置
@GetMapping("/consumer/payment/hystrix/timeout/{id}")
    //配置客户端自己出错的兜底方法和调用服务端最大超时时间
@HystrixCommand(fallbackMethod = "paymentTimeOutFallBackMethod",commandProperties = {
   @HystrixProperty(name = "execution.isolation.thread.timeoutInMilliseconds",value = "1500")
    })
    public String paymentInfo_TimeOut(@PathVariable("id") Integer id){
        int age = 10/0;
        return paymentHystrixService.paymentInfo_TimeOut(id);
    }

    public String paymentTimeOutFallBackMethod(@PathVariable("id") Integer id){
        return "我是消费者80，对方支付系统繁忙，请稍后再试，o(╥﹏╥)o";
    }
```
<a name="sawhf"></a>
### 8.7.1 避免兜底方法过多和与业务混在一起的代码膨胀或混乱
**配置文件配置**
```yaml
feign:
  hystrix:
    enabled: true
```
**Controller层变化**
```java
可在类头配置@DefaultProperties指定该类下所有出错方法的统一兜底方法
@DefaultProperties(defaultFallback = "payment_Global_FallbackMethod")
public class OrderHystrixController {
在方法头配置
@HystrixCommand//如果没有特殊声明其他属性，则默认使用类头配置的兜底方法，如不写该方法则无法使用服务降级
public String paymentInfo_TimeOut(@PathVariable("id") Integer id){
```
**客户端Service层可做如下处理**
```java
在@FeignClient注解上使用fallback属性指定当前通过feign接口调用服务端方法异常后的兜底类
@Component
@FeignClient(value = "CLOUD-PROVIDER-HYSTRIX-PAYMENT" ,fallback = PaymentFallbackService.class)
public interface PaymentHystrixService {

    @GetMapping("/payment/hystrix/ok/{id}")
    public String paymentInfo_OK(@PathVariable("id") Integer id);

    @GetMapping("/payment/hystrix/timeout/{id}")
    public String paymentInfo_TimeOut(@PathVariable("id") Integer id);
}
新建PaymentFallbackService实现PaymentHystrixService接口，重写方法为兜底方法
@Component
public class PaymentFallbackService implements PaymentHystrixService {
    @Override
    public String paymentInfo_OK(Integer id) {
        return "----PaymentFallbackService fall back-paymentInfo_OK,o(╥﹏╥)o";
    }

    @Override
    public String paymentInfo_TimeOut(Integer id) {
        return "----PaymentFallbackService fall back-paymentInfo_TimeOut,o(╥﹏╥)o";
    }
}
```
<a name="gJOJS"></a>
## 8.8 服务熔断配置
服务端代码配置<br />**注解@HystrixCommand可配置的参数项查看HystrixCommandProperties类即可**
```java
//服务熔断
    @HystrixCommand(fallbackMethod = "paymentCircuitBreaker_fallback",commandProperties = {
    //是否开启断路器
    @HystrixProperty(name = "circuitBreaker.enabled",value = "true"),   
    //请求次数
    @HystrixProperty(name = "circuitBreaker.requestVolumeThreshold",value = "10"),  
    //时间范围，在设定时间范围达到失败率设置即跳闸
    @HystrixProperty(name = "circuitBreaker.sleepWindowInMilliseconds",value = "10000"), 
    //失败率达到多少后跳闸,跳闸后多次正确服务恢复正常
    @HystrixProperty(name = "circuitBreaker.errorThresholdPercentage",value = "60"),
    })
     public String paymentBreaker(Integer id){
        if (id > 5){
            throw new RuntimeException("id太大");
        }
        return "成功";
    }
    public String paymentCallBack(){
        return "id不能大于5";
    }
```
<a name="te16i"></a>
## 8.9 Hystrix所有配置项
![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1620725597023-a80e60d8-dd58-4619-b01b-b85a499dcabc.png#clientId=ub69c7711-2424-4&from=paste&height=453&id=u5976db0f&margin=%5Bobject%20Object%5D&name=image.png&originHeight=453&originWidth=905&originalType=binary&size=354835&status=done&style=none&taskId=ub7873d4c-6d6b-4335-9d1b-c0f35d03d33&width=905)<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1620725643426-ace6fecc-9677-418f-a678-4d91d8990bf0.png#clientId=ub69c7711-2424-4&from=paste&height=316&id=u7064d9ef&margin=%5Bobject%20Object%5D&name=image.png&originHeight=316&originWidth=769&originalType=binary&size=293799&status=done&style=none&taskId=u3a7a15ce-b95b-43c6-b05a-e9d045e04ef&width=769)<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1620725691713-7c6b6f0d-dd19-413f-8122-096acbe36153.png#clientId=ub69c7711-2424-4&from=paste&height=286&id=u4d7d6746&margin=%5Bobject%20Object%5D&name=image.png&originHeight=286&originWidth=916&originalType=binary&size=320190&status=done&style=none&taskId=ua0a02b22-318b-41a6-beb3-96933a9c9d9&width=916)<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1620725716344-b68702f3-110a-48e5-9109-6cae47cd85a9.png#clientId=ub69c7711-2424-4&from=paste&height=363&id=u418cc61f&margin=%5Bobject%20Object%5D&name=image.png&originHeight=363&originWidth=977&originalType=binary&size=353128&status=done&style=none&taskId=u4c317365-06a6-410b-9268-72c38dbc22d&width=977)<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1620725735531-a0b218ab-09c3-46dd-896e-de34eade4cfe.png#clientId=ub69c7711-2424-4&from=paste&height=251&id=u284d52e8&margin=%5Bobject%20Object%5D&name=image.png&originHeight=251&originWidth=863&originalType=binary&size=191660&status=done&style=none&taskId=u730b5be0-cf13-4a62-b6f4-e379739da9f&width=863)
<a name="DhMES"></a>
## 8.10 Hystrix过程原理
![a06c27c91d03498da3ed1260af94010a.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1620726352006-253a963c-acb3-402e-98b9-2890b40a9e68.png#clientId=ub69c7711-2424-4&from=ui&id=uca88ea17&margin=%5Bobject%20Object%5D&name=a06c27c91d03498da3ed1260af94010a.png&originHeight=667&originWidth=1372&originalType=binary&size=95406&status=done&style=none&taskId=udd47a170-2e95-44b5-9146-2d4b4cfcc20)<br />![bb23d62750ad174eef37c0a0e8cd1b5a.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1620726359266-88dfac9c-ad49-4c7d-a650-8368b9efa020.png#clientId=ub69c7711-2424-4&from=ui&id=ud059f08d&margin=%5Bobject%20Object%5D&name=bb23d62750ad174eef37c0a0e8cd1b5a.png&originHeight=617&originWidth=1764&originalType=binary&size=253349&status=done&style=none&taskId=u794cec12-bbaa-4f5a-8022-3d3808465e1)
<a name="JAwVU"></a>
## 8.11 Hystrix监控页面dashboard开启
pom文件引入
```xml
			<dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-netflix-hystrix-dashboard</artifactId>
        </dependency>
```
```java
主启动类加上注解@EnableHystrixDashboard开启监控页面功能
@SpringBootApplication
@EnableHystrixDashboard
public class Main9001 {
    public static void main(String[] args) {
        SpringApplication.run(Main9001.class,args);
    }
}
```
**访问ip:port/hystrix看到如下页面代表服务搭建成功**<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1620727184510-ae0ff363-bbf3-4945-a715-3a27da4bae58.png#clientId=u0f5488cd-a803-4&from=paste&height=560&id=u4c47e584&margin=%5Bobject%20Object%5D&name=image.png&originHeight=560&originWidth=1081&originalType=binary&size=120385&status=done&style=none&taskId=u64bb9e0f-a27a-41b8-ac85-7cb8fd0196e&width=1081)
<a name="YEjDt"></a>
## 8.12 Hystrix被监控端配置
pom中加入
```xml
<dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>
```
```java
主启动类加入
/**
     * 此配置是为了服务监控而配置，与服务容错本身无关,SpringCloud升级后的坑
     * ServletRegistrationBean因为springboot的默认路径不是"/hystrix.stream"，
     * 只要在自己的项目里配置上下面的servlet就可以了
     */
    @Bean
    public ServletRegistrationBean getServlet(){
        HystrixMetricsStreamServlet streamServlet = new HystrixMetricsStreamServlet();
        ServletRegistrationBean registrationBean = new ServletRegistrationBean(streamServlet);
        registrationBean.setLoadOnStartup(1);
        registrationBean.addUrlMappings("/hystrix.stream");
        registrationBean.setName("HystrixMetricsStreamServlet");
        return registrationBean;
    }
主启动类注解
@SpringBootApplication
@EnableEurekaClient
@EnableCircuitBreaker
```
<a name="R2O9s"></a>
## 8.13 Hystrix监控页面使用
![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1620728280338-ada01684-d881-4314-a2d9-2e42836f3be6.png#clientId=u0f5488cd-a803-4&from=paste&height=560&id=u44f33542&margin=%5Bobject%20Object%5D&name=image.png&originHeight=560&originWidth=1023&originalType=binary&size=117757&status=done&style=none&taskId=udc155240-ddd2-42b2-9606-012eaa62024&width=1023)<br />地址栏填入IP:port/hystrix.stream,Delay填2000，title随便填写<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1620728690685-7f612bd7-1a87-4fad-a787-4af41a2c2a91.png#clientId=u0f5488cd-a803-4&from=paste&height=483&id=ud1ebfbf5&margin=%5Bobject%20Object%5D&name=image.png&originHeight=483&originWidth=1122&originalType=binary&size=283351&status=done&style=none&taskId=u914f24ec-ff03-4b00-8474-62b9f6094fd&width=1122)
<a name="LmIY5"></a>
# 9、Gateway服务网关
<a name="LuLO4"></a>
## 9.1 概述简介
**核心逻辑：路由转发+执行过滤器链**<br />       SpringCloud Gateway是SpringCloud的一个全新项目，基于Spring 5.0+Spring Boot 2.0和project Reactor等技术开发的网关，它旨在为微服务架构提供一种简单有效的统一的API路由管理方式。<br />       SpringCloud Gateway作为Spring Cloud生态系统中的网关，目标是替代Zuul，在Spring Cloud2.0以上版本中，没有对新版本Zuul2.0以上最新高性能版本进行集成，仍然还是使用的Zuul1.x非Reactor模式的老版本。而为了提升网关的性能，SpringCloud Gateway是基于WebFlux框架实现的，而WebFlux框架底层则使用了高性能的Reactor模式通信框架Netty。<br />       SpringCloud Gateway的目标是提供统一的路由方式且基于Filter链的方式提供了网关基本的功能，例如：安全，监控/指标，和限流
<a name="fWNdU"></a>
## 9.2 为什么选用Gateway不用zuul
1、开发Zuul的公司不太靠谱，Zuul 2.x迟迟不发布<br />2、Zuul1，是一个基于阻塞I/O的API Gateway<br />3、Zuul1基于Servlet2.5使用阻塞架构，它不支持任何长连接（如WebSocket）Zuul的设计模式和Nginx较像，每次I/O操作都是从工作线程中选择一个执行，请求线程被阻塞到工作线程完成，但是差别是Nginx用C++实现Zuul用Java实现，而JVM本身会有第一次加载较慢的情况，使得Zuul的性能相对较差。<br />4、Spring Cloud Gateway建立在Spring Framework 5、Project Reactor和Spring Boot2之上，使用非阻塞API<br />5、Spring Cloud Gateway还支持WebSocket，并且与Spring紧密集成拥有更好的开发体验<br />6、Gateway是基于**异步非阻塞模型**上进行开发的，性能方面不需要担心，SpringCloud也没有整合Zuul2的计划
<a name="CXgmF"></a>
## 9.3 Spring Cloud Gateway特性
1、动态路由：能够匹配任何请求属性；<br />**路由是构建网关的基本模块，它由ID，目标URI，一系列的断言和过滤器组成，如果断言为true则匹配该路由**<br />2、可以对路由指定Predicate（断言）和Filter（过滤器）；<br />**断言：参考的是Java8的java.util.function.Predicate**<br />**开发人员可以匹配HTTP请求中的所有内容（例如请求头或请求参数），如果请求与断言相匹配则进行路由**<br />**过滤：指的是Spring框架中GatewayFilter的实例，使用过滤器，可以在请求被路由前或者之后对请求进行修改。**<br />3、集成Hystrix的断路器功能；<br />4、集成SpringCloud服务发现功能；<br />5、易于编写断言和过滤器；<br />6、请求限流功能；<br />7、支持路径重写
<a name="t8b2r"></a>
## 9.4 Spring Cloud Gateway WebFlux
传统Web框架，如struts2，springmvc等都是基于ServletApI与Servlet容器基础之上运行的。<br />**但是在Servlet3.1之后有了异步非阻塞的支持**。而WebFlux是一个典型的非阻塞异步框架，它的核心是基于Reactor的相关API实现的。相对于传统web框架来说，它可以运行在诸如Netty，Undertow及支持Servlet3.1的容器上。非阻塞式+函数式编程（spring5让你必须使用java8）<br />**Spring WebFlux是Spring5.0引入的新的响应式框架，区别于SpringMVC ，它不需要依赖ServletAPI，它是完全异步非阻塞的，并且基于Reactor来实现响应式流规范**
<a name="k3K29"></a>
## 9.5 Spring Cloud Gateway工作流程
客户端向Spring Cloud Gateway发出请求，然后在Gateway Handler Mapping中找到与请求相匹配的路由，将其发送到Gateway Web Handler。<br />Handler再通过指定的过滤器链来将请求发送到我们实际的服务执行业务逻辑，然后返回。<br />过滤器之间用虚线分开是因为过滤器可能会在发送代理请求之前（“pre”）或之后（“post”）执行业务逻辑。<br />Filter在“pre”类型的过滤器可以做参数校验、权限校验、流量监控、日志输出、协议转换等，<br />在“post”类型的过滤器可以做响应内容、响应头的修改，日志的输出，流量监控等有非常重要的作用
<a name="zfliy"></a>
## 9.6 Gateway配置及使用
```xml
pom中添加配置
<dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-gateway</artifactId>
        </dependency>
排除配置，不然Gateway无法启动
<dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>
```
**总结：无论是yml还是javaConfig配置中的id可以随便起，path为访问localhost:9527/path触发断言，然后进行路由，路由地址为uri+path组合而成**
```yaml
配置文件中添加
spring:
  application:
    name: cloud-gateway
  cloud:
    gateway:
      discovery:
        locator:
          enabled: true   #开启从注册中心动态创建路由的功能，利用微服务名进行路由
      routes:
        - id: payment_routh #payment_routh    #路由的ID，没有固定规则但要求唯一，简易配合服务名
          #uri: http://localhost:8001         #匹配后提供服务的路由地址
          uri: lb://cloud-provider-service   #匹配后提供服务的路由地址
          predicates:
            - Path=/service/selectPaymentById/**          #断言，路径相匹配的进行路由

        - id: payment_routh2 #payment_routh   #路由的ID，没有固定规则但要求唯一，简易配合服务名
          #uri: http://localhost:8001          #匹配后提供服务的路由地址
          uri: lb://cloud-provider-service     #匹配后提供服务的路由地址
          predicates:
            - Path=/service/discoveryClient/**             #断言，路径相匹配的进行路由
            #- After=2020-03-15T15:35:07.412+08:00[GMT+08:00]
            #- Cookie=username,zzyy
            #- Header=X-Request-Id, \d+ #请求头要有X-Request-Id属性并且值为整数的正则表达式
            #- Host=**.atguigu.com
            #- Method=GET
            #- Query=username, \d+ #要有参数名username并且值还要啥整数才能路由
```
```java
Java Config的方式配置路由
/**
     * 使用编码方式配置网关路由
     * @param routeLocatorBuilder
     * @return
     */
    @Bean
    public RouteLocator customRouteLocator(RouteLocatorBuilder routeLocatorBuilder){
        RouteLocatorBuilder.Builder routes = routeLocatorBuilder.routes();
        routes.route("path_route_zq",//路由的ID
                r -> r.path("/guonei")
                .uri("https://news.baidu.com")).build();
        //访问localhost:9527/guonei将会转发到https://news.baidu.com/guonei
        return routes.build();
    }
```
<a name="B6tuU"></a>
## 9.7 通过微服务名实现动态路由
```yaml
yaml配置文件中配置
spring:
  application:
    name: cloud-gateway
  cloud:
    gateway:
      discovery:
        locator:
          enabled: true   #开启从注册中心动态创建路由的功能，利用微服务名进行路由
      routes:
        - id: payment_routh #payment_routh    #路由的ID，没有固定规则但要求唯一，简易配合服务名
        #匹配后提供服务的路由地址,lb代表从服务注册获取服务，跟服务在注册中心的名字
          uri: lb://cloud-provider-service   
          predicates:
            - Path=/service/selectPaymentById/**          #断言，路径相匹配的进行路由

        - id: payment_routh2 #payment_routh   #路由的ID，没有固定规则但要求唯一，简易配合服务名
        #匹配后提供服务的路由地址,lb代表从服务注册获取服务，跟服务在注册中心的名字
          uri: lb://cloud-provider-service     
          predicates:
            - Path=/service/discoveryClient/**             #断言，路径相匹配的进行路由
            #- After=2020-03-15T15:35:07.412+08:00[GMT+08:00]
            #- Cookie=username,zzyy
            #- Header=X-Request-Id, \d+ #请求头要有X-Request-Id属性并且值为整数的正则表达式
            #- Host=**.atguigu.com,**.atguigu.com #多个地址用,号隔开
            #- Method=GET
            #- Query=aaa，请求参数必须有name为aaa的参数；Query=aaa, 111：请求参数必须有name为aaa的参数，且aaa参数的值为111；
```
<a name="gO8qh"></a>
## 9.8 Gateway常用的Predicate
**Predicate就是为了实现一组匹配规则，让请求过来找到对应的Route进行处理**<br />**After**后面配置时间，意思为给路由地址加了个时间条件如上配置文件的释义就是2020年3月15日下午3点35分之后配置的整个路由才会生效。注意用代码获取一个默认时区，同类配置还有**Before**（配置时间之前生效），**Between**（配置两个时间之间生效）<br />**Cookie**需要两个参数，一个是cookie name，一个是对应值，路由规则会通过获取对应的cookie name值和对应值去匹配，如果匹配上就会执行路由，没匹配上就不执行，如上配置需要带上Cookie username=zzyy才能够访问服务<br />**Header**，与**Cookie**配置一样，不同的是需要吧K-V条件放在请求头中<br />**Host**一组匹配的域名列表，这个模板是一个ant模板，用.号作为分隔符他通过参数中的主机地址做匹配规则<br />**Method**什么请求方式访问才能生效<br />**Query **Query=aaa，请求参数必须有name为aaa的参数；Query=aaa, 111：请求参数必须有name为aaa的参数，且aaa参数的值为111；
<a name="ICceP"></a>
## 9.10 Gateway Filter
生命周期：pre（发送代理请求前）、post（发送代理请求后）<br />种类：GatewayFilter（单一）、GlobalFilter（全局）
<a name="rxWO9"></a>
### 9.10.1 自定义全局GlobalFilter
```java
/**
 * 自定义全局Filter需要实现GlobalFilter, Ordered接口
 */
@Component
@Slf4j
public class MyLogGatewayFilter implements GlobalFilter, Ordered {

    @Override
    public Mono<Void> filter(ServerWebExchange exchange, GatewayFilterChain chain) {
        log.info("进入MyLogGatewayFilter");
        String uname = exchange.getRequest().getQueryParams().getFirst("uname");
        if (uname == null ){
            log.info("非法用户");
            exchange.getResponse().setStatusCode(HttpStatus.NOT_ACCEPTABLE);//放入拒绝状态码回传
            return exchange.getResponse().setComplete();
        }
        return chain.filter(exchange);
    }

    /**
     * 加载过滤器顺序，值越小，优先级越高
     * @return
     */
    @Override
    public int getOrder() {
        return 0;
    }
```
<a name="lwfuV"></a>
# 10、 SpringCloud Config分布式配置中心
<a name="fGorn"></a>
## 10.1 理念
       微服务意味着要将单体应用中的业务拆分成一个个子服务，每个服务的粒度相对较小，因此系统中会出现大量的服务。由于每个服务都需要必要的配置信息才能运行，所以一套集中式的、动态的配置管理设施是必不可少的，一处修改，处处生效。<br />       SpringCloud提供了ConfigServer来解决这个问题，为微服务提供集中化的外部配置支持，配置服务器为各个不同微服务应用的所有环境提供了一个中心化的外部配置。
<a name="RChsH"></a>
## 10.2 SpringCloud Config组成结构
SpringCloud Config分为服务端和客户端两部分。<br />**       服务端**也成为**分布式配置中心，它是一个独立的微服务应用**，用来连接配置服务器并未客户端提供获取配置信息，加密/解密信息等访问接口。<br />**       客户端**则是通过制定的配置中心来管理应用资源，以及与业务相关的配置内容，并在启动的时候从配置中心获取和加载配置信息配置服务器默认采用git来存储配置信息，这样就有助于对环境配置进行版本管理，并且可以通过git客户端工具来方便的管理和访问配置内容。
<a name="KVXDB"></a>
## 10.3 SpringCloud Config能做什么
**SpringCloud Config默认使用Git来存储配置文件（也有其他方式，比如支持SVN和本地文件），但最推荐的还是Git，而且使用的是http/https访问的形式**<br />1、集中管理配置文件<br />2、不同环境不同配置，动态化的配置更新，分环境部署比如dev/test/prod/beta/release<br />3、运行期间动态调整配置，不再需要在每个服务部署的机器上编写配置文件，服务会向配置中心统一拉取配置自己的信息<br />4、当配置发生变化时，服务不需要重启即可感知到配置的变化并应用新的配置<br />5、将配置信息以REST接口的形式暴露
<a name="lhHMr"></a>
## 10.4 官网地址
https://cloud.spring.io/spring-cloud-static/spring-cloud-config/2.2.1.RELEASE/reference/html
<a name="IaKAi"></a>
## 10.5 SpringCloud Config服务端配置
1、在自己的Github上新建一个名为springcloud-config的Repository<br />2、获得新建项目的git地址，使用SSH方式的地址<br />3、本地新建git仓库并clone自己刚才建的项目<br />4、新建Module模块cloud-config-cneter3344，它即为Cloud的配置中心模块cloudConfig Center
```xml
pom中添加依赖
				<dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-config-server</artifactId>
        </dependency>
```
```yaml
配置文件配置如下
spring:
  application:
    name: cloud-config-center
  cloud:
    config:
      server:
        git:
          uri: git@github.com:zhangshier0317/springcloud-config.git #github仓库上面的git仓库名字
          ##搜索目录
          search-paths:
            - springcloud-config
      #读取分支
      label: master
```
```java
主启动类加上@EnableConfigServer
@SpringBootApplication
@EnableEurekaClient
@EnableConfigServer //激活配置中心
public class MainConfig3344 {
    public static void main(String[] args) {
        SpringApplication.run(MainConfig3344.class,args);
    }
}
```
**访问ip:3344/master/config-dev.yml可以看到配置文件内容即为成功**<br />**读取规则IP:port/分支/配置文件名-配置文件环境，如果没写分支则默认读取master分支，或在配置文件中label可指定默认读取分支**
<a name="ORH3S"></a>
## 10.6 SpringCloud Config客户端配置
```xml
pom中加入依赖
<!--不带server了，说明是客户端-->
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-config</artifactId>
        </dependency>
```
```yaml
建立bootstrap.yml配置文件
application.yml是用户级的资源配置项
bootstrap.yml是系统级的，优先级更高
SpringCloud会创建一个"Bootstrap Context"，作为Spring应用的‘Application Context’的父上下文。初始化的
时候，‘Bootstrap Context’负责从外部加载配置属性并解析配置，这两个上下文共享一个从外部获取的‘Environment’
Bootstarp属性有高优先级，默认情况下，他们不会被本地配置覆盖。‘Bootstarp context’和‘Application Context’
有着不同的约定，所以新增一个‘bootstrap.yml’文件，保证‘Bootstrap Context’和‘Application Context’配置的
分离。
要将Client模块下的Application.yml改为bootstrap.yml很关键
因为bootstrap.yml是比application.yml先加载的。bootstrap.yml优先级高于application.yml
server:
  port: 3355

spring:
  application:
    name: config-client
  cloud:
    #Config客户端配置
    config:
      label: master #分支名称
      name: config #配置文件名称
      profile: dev #读取后缀名称 上述3个综合：master分支上config-dev.yml的配置文件被读取 http://config-3344.com:3344/master/config-dev.yml
      uri: http://localhost:3344 #配置中心地址
  #rabbit相关配置 15672是web管理界面的端口，5672是MQ访问的端口
  rabbitmq:
    host: localhost
    port: 5672
    username: guest
    password: guest

#服务注册到eureka地址
eureka:
  client:
    service-url:
      defaultZone: http://localhost:7001/eureka
```
**上述配置可做到基本功能，但是如果GitHub上面配置文件发生变化则客户端读取的还是变化前的数据，所以需要数据动态加载。**
<a name="hWikk"></a>
### 10.6.1 SpringCloud Config客户端数据动态加载
```xml
pom引入，自身有变化可以通知其他微服务
		<dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>
```
```yaml
配置文件中新增
#暴露监控端点
management:
  endpoints:
    web:
      exposure:
        include: "*"
```
```java
在业务类上加注解@RefreshScope使业务类具备刷新能力
@RestController
@RefreshScope
public class ConfigController {
    @Value("${name.name}")
    private String configPort;

    @GetMapping("/getConfig")
    public String getConfig(){
        return configPort;
    }
}
```
**以上全部完成后需要在Github端修改配置文件的人手动使用POST触发客户端的**[http://localhost:3355/actuator/refresh](http://localhost:3355/actuator/refresh)**刷新接口，客户端此时不用重启也可获取最新参数,但是机器多了也不方便，此时还需要消息总线BUS的帮忙**
<a name="D0AtO"></a>
# 11、SpringCloud BUS消息总线
<a name="FXgFK"></a>
## 11.1 概述
可以配合SpringCloud config实现配置的动态刷新<br />SpringCloud Bus是用来将分布式系统的节点与轻量级消息系统连接起来的框架，**它整合了Java的事件处理机制和消息中间件的功能。**支持两种消息代理：RabbitMQ和kafka<br />**总线：**<br />在微服务架构的系统中，通常会使用轻量级的消息代理来构建一个共用的消息主题。并让系统中所有微服务实例都连接上来。由于该主题中产生的消息会被所有实例监听和消费，所以称它为消息总线。在总线上的各个实例，都可以方便地广播一些需要让其他链接在该主题上的实例都知道的消息。<br />**基本原理：**<br />ConfigClient实例都监听MQ中同一个topic（默认是springCloudBus）。当一个服务刷新数据的时候，他会把这个信息放入Topic中，这样其他监听同一个Topic的服务就能得到通知，然后去更新自身的配置
<a name="JCrhd"></a>
## 11.2 全局广播设计思想
1、利用消息总线触发一个客户端/bus/refresh而刷新所有客户端的配置。<br />**2、利用消息总线触发一个ConfigServer的/bus/refresh的端点而刷新所有客户端的配置**<br />**2的设计思想更好，微服务本身是作为服务存在，不应该再给他加一些除服务之外的功能，所以全局广播放在configServer端更好**
<a name="qIgJt"></a>
## 11.3  消息总线配置支持
<a name="AuMdl"></a>
### 11.3.1 SpringCloud Config Server端
```xml
pom中添加依赖
<!--添加消息总线RbbitMQ支持-->
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-bus-amqp</artifactId>
        </dependency>
<!--凡是暴露监控、刷新的都要有actuator依赖-->
				<dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>
```
```yaml
配置文件中增加rabbitmq相关配置
#rabbit相关配置
rabbitmq:
  host: localhost
  port: 5672
  username: guest
  password: guest
  
#rabbitmq相关配置，暴露bus刷新配置的端点
management:
  endpoints:  #暴露bus刷新配置的端点
    web:
      exposure:
        include: 'bus-refresh'  #凡是暴露监控、刷新的都要有actuator依赖，bus-refresh就是actuator的刷新操作
```
<a name="MzWcP"></a>
### 11.3.2 SpringCloud Config Client端
```xml
pom中添加依赖
<!--添加消息总线RbbitMQ支持-->
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-bus-amqp</artifactId>
        </dependency>
<!--凡是暴露监控、刷新的都要有actuator依赖-->
				<dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>
```
```yaml
#rabbit相关配置 15672是web管理界面的端口，5672是MQ访问的端口
rabbitmq:
  host: localhost
  port: 5672
  username: guest
  password: guest
  
#暴露监控端点
management:
  endpoints:
    web:
      exposure:
        include: "*" #客户端不用刷新
```
<a name="QgA6y"></a>
### 11.3.3 触发消息总线完成全局通知
在修改完Git上配置文件的参数后，手动触发接口[http://localhost:3344/actuator/bus-refresh](http://localhost:3344/actuator/bus-refresh)通知SpringCloud Config Server端，然后server端会通过消息总线全局通知到每个Client端
<a name="pjnZ0"></a>
### 11.3.4 触发消息总线完成定点通知
接口公式：http://localhost:配置中心端口号/actuator/bus-refresh/{destination}<br />bus-refresh请求不再发送到具体的服务实例上，而是发给config server并通过destination参数类指定需要更新配置的服务或实例<br />[http://localhost:3344/actuator/bus-refresh/config-client:3355](http://localhost:3344/actuator/bus-refresh/config-client:3355)
<a name="yXKk6"></a>
## 11.4 流程总结
1、github上配置文件更新，ConfigServer可以获取到最新的，但是ConfigClient还是旧的信息<br />2、修改配置文件的人员可以通过ConfigServer的bus-refresh接口全局广播到每一台ConfigClient使他们的配置都更新到最新<br />3、也可以定点通知某几台服务更新到最新
<a name="OHDUq"></a>
# 12、 SpringCloud stream消息驱动
<a name="al4O7"></a>
## 12.1 概述
**什么是SpringCloudStream？**<br />屏蔽底层消息中间件差异，降低维护开发成本，统一消息编程模型，构建消息驱动微服务的框架<br />应用程序通过inputs或者outputs来与SpringCloudStream中的binder对象交互。<br />通过我们配置来binding（绑定），而SpringCloudStream的binder对象负责与消息中间件交互。<br />所以我们只需要清楚如何与SpringCloudStream交互就可以方便使用消息驱动的方式。<br />通过使用SpringIntegration来连接消息代理中间件以实现消息事件驱动。<br />SpringCloudStream为一些供应商的消息中间件产品提供了个性化的自动配置实现，引用了发布-订阅、消费组、分区的三个核心概念。<br />**目前仅支持RabbitMQ、Kafka**
<a name="fseW0"></a>
## 12.2 官网地址
[https://spring.io/projects/spring-cloud-stream#overview/](https://spring.io/projects/spring-cloud-stream#overview/)
<a name="G6wb5"></a>
### 12.2.1 Spring cloud stream中文指导手册
[https://m.wang1314.com/doc/webapp/topic/20971999.html](https://m.wang1314.com/doc/webapp/topic/20971999.html)
<a name="sbNdk"></a>
## 12.3 标准MQ与引入Spring cloud stream对比
<a name="v3uQm"></a>
### 12.3.1 标准MQ
1、生产者和消费者之间靠消息媒介传递信息内容<br />2、消息必须走特定的通道<br />3、消息通道（MessageChannel）的子接口SubscribableChannel，由MessageHandler消息处理器所订阅，订阅了才推送消息，不订阅不推送
<a name="oQw8W"></a>
### 12.3.2 引入Spring cloud stream
       一个系统用到了RabbitMQ和Kafka，由于这两个消息中间件的架构上的不同，像RabbitMQ有exchange，kafka有Topic和Partitions分区。<br />       这些中间件的差异性导致我们实际项目开发给我们造成了一定的困扰，我们如果用了两个消息队列的其中一种，后面的业务需求，我们想往另外一种消息队列进行迁移，这时候无疑就是一个灾难性的，一大堆东西都要重新推到重新做，因为它跟我们系统耦合了，这时候springcloudStream给我们提供了一种解耦合的方式。<br />       在没有绑定器这个概念的情况下，我们的SpringBoot应用要直接与消息中间件进行信息交互的时候，由于各消息中间件构建的初衷不同，他们的实现细节上会有较大的差异性<br />       通过定义绑定器作为中间层，完美地实现了应用程序与消息中间件细节之间的隔离<br />       通过向应用程序暴露统一的Channel通道，使得应用程序不需要再考虑各种不同的消息中间件实现<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1620879637007-9ab25e36-af24-4f3a-b731-7bbee49280b7.png#clientId=ufaf2f23b-4e4e-4&from=paste&height=649&id=u4f52c83c&margin=%5Bobject%20Object%5D&name=image.png&originHeight=649&originWidth=1116&originalType=binary&size=257877&status=done&style=none&taskId=u65cc36b4-bd49-4013-9625-5ed02865c1e&width=1116)<br />**Stream中消息通信方式遵循了发布-订阅模式，Topic主题进行广播，在RabbitMQ就是Exchange，在Kafka中就是Topic**
<a name="eZG6n"></a>
### 12.3.3 SpringCloud Stream标准流程套路
Binder（绑定器，屏蔽差异），INPUT对应消费者，OUTPUT对应生产者<br />Channel（通道），是队列Queue的一种抽象，在消息通讯系统中就是实现存储和转发的媒介，通过CHannel对队列进行配置<br />Source和Sink，参照对象是SpringCloudStream自身，从Stream发布消息就是输出，接收消息就是输入
<a name="tQkMv"></a>
### 12.3.4 编码和注解
| ![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1620880839845-8e523607-1d00-46c5-b102-19f222936a92.png#clientId=ufaf2f23b-4e4e-4&from=paste&height=391&id=ud5aecf25&margin=%5Bobject%20Object%5D&name=image.png&originHeight=391&originWidth=348&originalType=binary&size=35817&status=done&style=none&taskId=ufce3ebe5-b791-4a1a-ac6e-9733bce6615&width=348) | 组成​ | 说明 |
| --- | --- | --- |
|  | Middlerware | 中间件，目前只支持RabbitMQ和Kafka |
|  | Binder | Binder是应用与消息中间件之间的封装，目前实行了Kafka和RabbitMQ的Binder，通过Bind而可以很方便的连接中间件，可以动态的改变消息类型（对应于Kafka的topic，RabbitMQ的exchange），这些都可以通过配置文件来实现 |
|  | @Input | 注解标识输入通道，通过该输入通道接收到的消息进入应用程序 |
|  | @Output | 注解标识输出通道，发布的消息将通过钙通道离开应用程序 |
|  | @StreamListener | 监听队列，用于消费者的队列的消息接收 |
|  | @EnableBinding | 指通道channel和exchange绑定在一起 |

<a name="aEUXX"></a>
## 12.4 SpringCloud Stream生产者配置及使用
```xml
pom添加如下依赖
				<dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-stream-rabbit</artifactId>
        </dependency>
```
```yaml
配置文件加入
spring:
  application:
    name: cloud-stream-provider
  cloud:
    stream:
      binders: # 在此处配置要绑定的rabbitMQ的服务信息
        defaultRabbit: # 表示定义的名称，用于binding的整合
          type: rabbit # 消息中间件类型
          environment: # 设置rabbitMQ的相关环境配置
            spring:
              rabbitmq:
                host: localhost
                port: 5672
                username: guest
                password: guest
      bindings: # 服务的整合处理
        output: # 这个名字是一个通道的名称
          destination: studyExchange # 表示要使用的exchange名称定义
          content-type: application/json # 设置消息类型，本次为json，文本则设为text/plain
          binder: defaultRabbit # 设置要绑定的消息服务的具体设置
```
```java

public interface IMessageProvider {
    public String send();
}

import org.springframework.cloud.stream.messaging.Source;
import org.springframework.messaging.MessageChannel;
import org.springframework.messaging.support.MessageBuilder;

@EnableBinding(Source.class) //定义消息生成者的发送管道
public class MessageProviderImpl implements IMessageProvider {
    @Autowired
    private MessageChannel output;//发送消息管道
    @Override
    public String send() {
        String msg = "Stream测试";
        //使用消息绑定器把消息放进去然后构建
        output.send(MessageBuilder.withPayload(msg).build());
        return null;
    }
}

@RestController
public class SendMsgController {
    @Autowired
    private IMessageProvider iMessageProvider;

    @GetMapping("sendmsg")
    public String sendMsg(){
        return iMessageProvider.send();
    }
}
```
<a name="kl4mA"></a>
## 12.5 SpringCloud Stream消费者配置及使用
```xml
pom中加入依赖
				<dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-stream-rabbit</artifactId>
        </dependency>
```
```yaml
spring:
  application:
    name: cloud-stream-consumer
  cloud:
    stream:
      binders: # 在此处配置要绑定的rabbitMQ的服务信息
        defaultmq: # 表示定义的名称，用于binding的整合
          type: rabbit # 消息中间件类型
          environment: # 设置rabbitMQ的相关环境配置
            spring:
              rabbitmq:
                host: localhost
                port: 5672
                username: guest
                password: guest
      bindings: # 服务的整合处理
        input: # 这个名字是一个通道的名称
          destination: studyExchange # 表示要使用的exchange名称定义
          content-type: application/json # 设置消息类型，本次为json，文本则设为text/plain
          binder: defaultmq # 设置要绑定的消息服务的具体设置
```
```java
import org.springframework.messaging.Message;

public interface ReceiveMsg {
    public void receiveTime(Message<String> message);
}

import com.zq.cloud.service.ReceiveMsg;
import org.springframework.cloud.stream.annotation.EnableBinding;
import org.springframework.cloud.stream.annotation.StreamListener;
import org.springframework.cloud.stream.messaging.Sink;
import org.springframework.messaging.Message;
import org.springframework.stereotype.Component;

@Component
@EnableBinding(value= {Sink.class})
public class ReceiveMsgImpl implements ReceiveMsg {
    @Override
    @StreamListener(Sink.INPUT)
    public void receiveTime(Message<String> message) {
        System.out.println("接收消息" + message.getPayload().toString());
    }
}
```
<a name="tF1td"></a>
## 12.6 分组消费与持久化
<a name="ccuQn"></a>
### 12.6.1 解决重复消费问题
如在订单系统做集群部署，都会从RabbitMQ中获取订单信息，如果一个订单同时被两个服务获取到，那么就会造成数据错误，为避免这种情况，这时就可以使用Stream中的消息分组来解决<br />**注意**：在Stream中处于同一个分组中的多个消费者是竞争关系，就能够保证消息只会被其中一个应用消费一次。**不同组是可以重复消费的,同一组内会发生竞争关系，只有其中一个可以消费，消息中心轮询发送消息到一个组内不同的机器**
```yaml
配置文件中加入group项
bindings: # 服务的整合处理
        input: # 这个名字是一个通道的名称
          destination: studyExchange # 表示要使用的exchange名称定义
          content-type: application/json # 设置消息类型，本次为json，文本则设为text/plain
          binder: defaultmq # 设置要绑定的消息服务的具体设置
          group: atguiguA #分组
```
<a name="Tropl"></a>
### 12.6.2 消息持久化
如果消费端突然挂掉但是生产端没事，此时生产端发送了几个消息（**未被消费状态**），此时重启消费端，**配置了group属性的消费端会去消费未被消费的消息，而没有配置group的消费端则不会去消费**
<a name="tPT2V"></a>
# 13、Spring Cloud Sleuth 分布式请求链路跟踪
<a name="KpQf4"></a>
## 13.1 概述
       在微服务框架中，一个由客户端发起的请求在后端系统中会经过，多个不同的服务节点调用来协同产生最后的请求结果，每一个前端请求都会形成一条复杂的分布式服务调用链路，链路中的任何一环出现高延时或错误都会引起整个请求最后的失败。<br />       Spring Cloud Sleuth提供了一套完整的服务跟踪的解决方案，在分布式系统中提供追踪解决方案并且兼容支持了zipkin。
<a name="lAdJq"></a>
## 13.2 Sleuth之zipkin搭建安装
1、下载zipkin jar包<br />2、java -jar 运行zipkin jar<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1620908763818-ead59182-2e17-41b3-b94d-76e1c4219637.png#clientId=ufaf2f23b-4e4e-4&from=paste&height=442&id=ucd4f9572&margin=%5Bobject%20Object%5D&name=image.png&originHeight=442&originWidth=677&originalType=binary&size=36332&status=done&style=none&taskId=ue88e1a77-f58a-4db9-84b3-44dce75a00f&width=677)<br />3、运行控制台http://localhost:9411/zipkin<br />**专业术语：**<br />**Trace：**类似于树结构的span集合，表示一条调用链路，存在唯一标识<br />**span:**表示调用链路来源，通俗的理解span就是一次请求信息<br />完整的调用链路：表示请求链路，一条链路通过Trace Id唯一标识，Span标识发起的请求信息，各Span通过parent id关联起来<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1620909151795-30e43a5f-3dec-42a5-9072-fbf212881810.png#clientId=ufaf2f23b-4e4e-4&from=paste&height=326&id=u3c30af51&margin=%5Bobject%20Object%5D&name=image.png&originHeight=326&originWidth=968&originalType=binary&size=80791&status=done&style=none&taskId=uaea67319-dd68-42dd-84e2-dce99f05fbf&width=968)
<a name="Jjusi"></a>
## 13.3 项目加装Sleuth监控链路
<a name="OuTLZ"></a>
### 13.3.1 服务端
```xml
pom添加依赖
<!--包含了sleuth+zipkin-->
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-zipkin</artifactId>
        </dependency>
```
```yaml
zipkin:
    base-url: http://localhost:9411 #监控的数据去那看
  sleuth:
    sampler:
      probability: 0.5 #采样率值在0-1之间，1表示全部采集，一般用0.5即可
```
<a name="IPqVI"></a>
### 13.3.2 客户端
```xml
pom添加依赖
<!--包含了sleuth+zipkin-->
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-zipkin</artifactId>
        </dependency>
```
```yaml
zipkin:
    base-url: http://localhost:9411 #监控的数据去那看
  sleuth:
    sampler:
      probability: 0.5 #采样率值在0-1之间，1表示全部采集，一般用0.5即可
```
<a name="afCTQ"></a>
# 14、 SpringCloud Alibaba
<a name="Uk1Zt"></a>
## 14.1 概述
**服务限流降级**：默认支持Servlet、Feign、RestTemplate、Dubbo和RockerMQ限流降级功能的接入，可以再运行时通过控制台实时修改限流降级规则，还支持查看限流降级Metrics监控。<br />**服务注册与发现**：适配SpringCloud服务注册与发现标准，默认集成了Ribbon的支持。<br />**分布式配置管理**：支持分布式系统中的外部化配置，配置更改时自动刷新。<br />**消息驱动能力**：基于SpringCloudStream为微服务应用构建消息驱动能力。<br />**阿里云对象存储**：阿里云提供的海量、安全、低成本、高可靠的云存储服务。支持在任何应用、任何时间、任何地点存储和访问任意类型的数据。<br />**分布式任务调度**：提供秒级、精准、高可靠、高可用的定时（基于Cron表达式）任务调度服务。同时提供分布式的任务执行模型，如网格任务。网格任务支持海量子任务均匀分配到所有Worker（schedulerx-client）上执行
<a name="Fqujz"></a>
## 14.2 官方博客
https://github.com/alibaba/spring-cloud-alibaba/blob/master/README-zh.md
<a name="CKU0u"></a>
## 14.3 Nacos （注册中心+配置中心）
<a name="pNgzG"></a>
### 14.3.1 概述
Nacos：Dunamic Naming and Configuration Service<br />**名字解析：**前四个字母分别为Naming和Configuration的前两个字母，最后的s为Service。<br />一个更易于构建云原生应用的动态服务发现、配置管理和服务管理平台<br />Nacos就是注册中心+配置中心组合 **Nacos = Eureka + Config + Bus**<br />**官方网址:**[https://nacos.io/zh-cn/](https://nacos.io/zh-cn/)
<a name="iGwUN"></a>
### 14.3.2 下载使用
1、下载Nacos，解压运行bin目录下的startup.cmd<br />2、访问[http://localhost:8848/nacos](http://localhost:8848/nacos)，可以出现页面代表成功
<a name="x4eR5"></a>
### 14.3.3 Nacos服务提供者注册
```xml
父pom中依赖
<dependencyManagement>
	<dependency>
        <groupId>com.alibaba.cloud</groupId>
        <artifactId>spring-cloud-alibaba-dependencies</artifactId>
        <version>2.1.0.RELEASE</version>
        <type>pom</type>
        <scope>import</scope>
  </dependency>
</dependencyManagement>
子Module pom中引入
<!--springcloud alibaba nacos-->
        <dependency>
            <groupId>com.alibaba.cloud</groupId>
            <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
        </dependency>
```
```yaml
server:
  port: 9001

spring:
  application:
    name: nacos-payment-provider
  cloud:
    nacos:
      discovery:
        server-addr: localhost:8848 #配置Nacos地址

management:
  endpoints:
    web:
      exposure:
        include: '*'  #监控
```
```java
主启动类上加注解@EnableDiscoveryClient
@SpringBootApplication
@EnableDiscoveryClient
public class MainNacos9001 {
    public static void main(String[] args) {
        SpringApplication.run(MainNacos9001.class,args);
    }
}
```
**启动项目完成后可在nacos监控页面**[**http://localhost:8848/nacos**](http://localhost:8848/nacos)**看到如下显示即为集成成功**<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1620986720725-08270ad3-38a1-4d95-92ab-77fdba5b2144.png#clientId=u7bbab827-6a23-4&from=paste&height=566&id=u3aca67ba&margin=%5Bobject%20Object%5D&name=image.png&originHeight=566&originWidth=1854&originalType=binary&size=53036&status=done&style=none&taskId=u62aac1dc-df1e-4f39-bee4-fd018587139&width=1854)
<a name="Fz7xm"></a>
### 14.3.4 Nacos服务消费者注册
```xml
pom中加入依赖
				<dependency>
            <groupId>com.alibaba.cloud</groupId>
            <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
        </dependency>
```
```yaml
server:
  port: 83

spring:
  application:
    name: nacos-order-consumer
  cloud:
    nacos:
      discovery:
        server-addr: localhost:8848

#消费者将要去访问的微服务名称（成功注册进nacos的微服务提供者），在这配置了访问的服务，业务类就不用在定义常量了
service-url:
  nacos-user-service: http://nacos-payment-provider
```
```java
引入RestTemplate
@Configuration
public class ApplicationContextBean {
    @Bean
    @LoadBalanced
    public RestTemplate restTemplate(){
        return new RestTemplate();
    }
}
```
<a name="DtF6l"></a>
### 14.3.5 各种注册中心比较
**CAP模型：**<br />1、**一致性（Consistency）**：（等同于所有节点访问同一份最新的数据副本）<br />2、**可用性（Availability）**：（每次请求都能获取到非错的响应——但是不保证获取的数据为最新数据）<br />3、**分区容错性（Partition tolerance）**：（以实际效果而言，分区相当于对通信的时限要求。系统如果不能在时限内达成数据一致性，就意味着发生了分区的情况，必须就当前操作在C和A之间做出选择，保证分布式网络中部分网络不可用时, 系统依然正常对外提供服务。<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1620988738921-5ac33613-1651-4de4-9ccf-357ca28e15bd.png#clientId=u7bbab827-6a23-4&from=paste&height=247&id=u8ce7476c&margin=%5Bobject%20Object%5D&name=image.png&originHeight=247&originWidth=636&originalType=binary&size=63301&status=done&style=none&taskId=ud426fcbf-1ece-4bf1-92ef-eaf1b1ecfa9&width=636)<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1620988924364-a01f4d7c-cb41-4f98-b781-24035fb74aef.png#clientId=u7bbab827-6a23-4&from=paste&height=368&id=u93ab6f48&margin=%5Bobject%20Object%5D&name=image.png&originHeight=368&originWidth=750&originalType=binary&size=235789&status=done&style=none&taskId=ua5565e8a-c521-434d-a871-c8ee7234659&width=750)
<a name="MMPQG"></a>
### 14.3.6 Nacos AP和CP模式的切换
**AP模式：**<br />        如果不需要存储服务级别的信息且服务实例是通过nacos-client注册，并能够保持心跳上报，那么就可以选择AP模式。当前主流的服务如SpringCloud和Dubbo服务，都适用于AP模式，AP模式为了服务的可能性而减弱了一致性因此AP模式下只支持注册临时实例<br />**CP模式：**<br />        如果需要在服务级别编辑或者存储配置信息，那么CP是必须，K8S服务和DNS服务则适用于CP模式。<br />CP模式下则支持注册持久化实例，此时则是以Raft协议为集群运行模式，该模式下注册实例之前必须先注册服务，如果服务不存在，则返回错误。
<a name="YPNbX"></a>
### 14.3.7 Nacos作为配置中心之基础配置
```xml
pom中加入依赖
				<dependency>
            <groupId>com.alibaba.cloud</groupId>
            <artifactId>spring-cloud-starter-alibaba-nacos-config</artifactId>
        </dependency>
        <dependency>
            <groupId>com.alibaba.cloud</groupId>
            <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
        </dependency>
```
**Nacos配置中心需要两个配置文件，一个application.yml一个bootstrap.yml**<br />        Nacos同Springcloud-config一样，在项目初始化时，要保证先从配置中心进行配置拉取，拉取配置之后，才能保证项目的正常启动，bootstrap优先application加载
```yaml
bootstrap.yml配置
server:
  port: 3377

spring:
  application:
    name: nacos-config-client
  cloud:
    nacos:
      discovery:
        server-addr: localhost:8848 #Nacos服务注册中心地址
      config:
        server-addr: localhost:8848 #Nacos作为配置中心地址
        file-extension: yml  #指定yaml格式的配置
        group: DEV_GROUP
        #group: DEV_GROUP
        namespace: e69dbe0a-233d-4b73-a173-89e9e8a1d041

# ${spring.application.name}-${spring.profile.active}.${spring.cloud.nacos.config.file.extension}
# nacos-config-client-dev.yml

application.yml配置
spring:
  profiles:
    active: dev #开发环境
    #active: test #测试环境
    #active: info
```
```java
代码与config使用基本相同
@RestController
@RefreshScope//支持Nacos动态刷新
public class NacosConfigController {
    @Value("${name.name}")
    private String configPort;

    @GetMapping("/getConfig")
    public String getConfig(){
        return configPort;
    }
}
```
**Nacos中的匹配规则**<br />在 Nacos Spring Cloud 中，dataId 的完整格式如下：<br />${prefix}-${spring.profiles.active}.${file-extension}<br />prefix 默认为 spring.application.name 的值，也可以通过配置项 spring.cloud.nacos.config.prefix来配置。<br />spring.profiles.active 即为当前环境对应的 profile，详情可以参考 Spring Boot文档。 注意：当 spring.profiles.active 为空时，对应的连接符 - 也将不存在，dataId 的拼接格式变成 ${prefix}.${file-extension}<br />file-exetension 为配置内容的数据格式，可以通过配置项 spring.cloud.nacos.config.file-extension 来配置。目前只支持 properties 和 yaml 类型。<br />**根据Nacos匹配规则在nacos控制台建立对应名称的配置文件**<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1620993960362-1d0637ff-8e4d-4277-975b-6be3938613f9.png#clientId=u7bbab827-6a23-4&from=paste&height=330&id=u7ecbe292&margin=%5Bobject%20Object%5D&name=image.png&originHeight=330&originWidth=1919&originalType=binary&size=47204&status=done&style=none&taskId=u8c81fb16-e54d-40bd-8f49-95440de29f2&width=1919)<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1620993926561-ba833dbd-bd27-4a1f-8ca4-8b9a22f00ea9.png#clientId=u7bbab827-6a23-4&from=paste&height=726&id=ua57ecced&margin=%5Bobject%20Object%5D&name=image.png&originHeight=726&originWidth=1852&originalType=binary&size=57796&status=done&style=none&taskId=u4e87a9dd-0d05-4e87-8603-c41bf5c2c32&width=1852)
<a name="TMAv2"></a>
### 14.3.8 Nacos作为配置中心之分类配置
分类设计思想就类似Java里面的包名和类名<br />最外层的namespace是可以用于区分部署环境的，Group和DataID逻辑上区分两个目标对象。<br />**三者情况**<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1620996359489-43bfa767-c9e7-4fe5-b86b-338cec8012a8.png#clientId=u7bbab827-6a23-4&from=paste&height=297&id=uc93d9e94&margin=%5Bobject%20Object%5D&name=image.png&originHeight=297&originWidth=441&originalType=binary&size=55336&status=done&style=none&taskId=ua6e17839-67dd-4e85-acc2-890bf91b999&width=441)<br />默认情况：<br />Namespace=public，Group=DEFAULT_GROUP,默认Cluster是DEFAULT<br />​

Nacos默认的命名空间是public，**Namespace**主要用来实现隔离。<br />比方说我们现在有三个环境：开发、测试、生产环境，我们就可以创建三个Namespace，不同的Namespace之间是隔离的。<br />**Group**默认是DEFAULT_GROUP,Group可以吧不同的微服务划分到同一个分组里面去<br />**Service**就是微服务；一个Service微服务可以包含多个Cluster（集群），Nacos默认Cluster是DEFAULT，Cluster是对指定微服务的一个虚拟划分。比方说为了容灾，将Service微服务分别部署在了杭州机房和广州机房，这时就可以给杭州机房的Service微服务起一个集群名称（HZ），给广州机房的Service微服务起一个集群名称（GZ），还可以尽量让同一个机房的微服务互相调用，以提升性能。<br />最后是**Instance**，就是微服务实例。
<a name="asHrC"></a>
#### 14.3.8.1 根据dataId实现配置文件区分
nacos后台<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1620997376292-6febadbb-90f7-4b46-8b6d-702f16e020ed.png#clientId=u7bbab827-6a23-4&from=paste&height=106&id=u2434f41f&margin=%5Bobject%20Object%5D&name=image.png&originHeight=106&originWidth=471&originalType=binary&size=3891&status=done&style=none&taskId=u5479b127-9e13-408e-9c7d-52df9351ca9&width=471)<br />application配置文件<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1620997408288-f411f6bb-f7e0-46ab-a112-3207182b0a25.png#clientId=u7bbab827-6a23-4&from=paste&height=130&id=u608d52fb&margin=%5Bobject%20Object%5D&name=image.png&originHeight=130&originWidth=332&originalType=binary&size=15010&status=done&style=none&taskId=u0cc2e703-043b-42cb-88fc-48d75075bbe&width=332)
<a name="YdVs6"></a>
#### 14.3.8.2 根据group实现配置文件区分
nacos后台<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1620997492276-b1979d24-4c01-4987-b3e8-ab898f405114.png#clientId=u7bbab827-6a23-4&from=paste&height=577&id=u0dec8a6b&margin=%5Bobject%20Object%5D&name=image.png&originHeight=577&originWidth=1277&originalType=binary&size=31506&status=done&style=none&taskId=u072e68d1-56a7-40f7-b203-2ddaa639307&width=1277)<br />application配置文件<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1620997521706-fa17c28c-73c0-4de6-aed4-60fde9969640.png#clientId=u7bbab827-6a23-4&from=paste&height=455&id=u4c66e699&margin=%5Bobject%20Object%5D&name=image.png&originHeight=455&originWidth=622&originalType=binary&size=63740&status=done&style=none&taskId=uade43f38-13b2-42ad-be9c-be63f15f7aa&width=622)
<a name="s3V7I"></a>
#### 14.3.8.3 根据namespace实现配置文件区分
nacos后台<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1620997855967-859a7519-7aba-43c8-b172-bcd1e82c6227.png#clientId=u7bbab827-6a23-4&from=paste&height=537&id=u4ea0f5c2&margin=%5Bobject%20Object%5D&name=image.png&originHeight=537&originWidth=1920&originalType=binary&size=38401&status=done&style=none&taskId=uf2c1414b-0464-4d10-883c-84affb2a151&width=1920)<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1620997902223-f01b1f47-7000-4669-81fc-75741d763aaf.png#clientId=u7bbab827-6a23-4&from=paste&height=322&id=u22f83378&margin=%5Bobject%20Object%5D&name=image.png&originHeight=322&originWidth=961&originalType=binary&size=16074&status=done&style=none&taskId=u09503ae6-adbf-474f-906d-6651938d769&width=961)<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1620997928509-0f86ada5-f461-4ffa-89b2-33a1e5326573.png#clientId=u7bbab827-6a23-4&from=paste&height=188&id=ub75edad7&margin=%5Bobject%20Object%5D&name=image.png&originHeight=188&originWidth=1502&originalType=binary&size=16287&status=done&style=none&taskId=u168c9ebc-1781-4503-9ba2-1a687b2ab50&width=1502)<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1620998040953-17056240-30f9-4dda-b70f-ca9cef5fa27f.png#clientId=u7bbab827-6a23-4&from=paste&height=410&id=uf8c48f7e&margin=%5Bobject%20Object%5D&name=image.png&originHeight=410&originWidth=1902&originalType=binary&size=44966&status=done&style=none&taskId=u208f522a-bdf4-402c-8a0c-f15b52375c9&width=1902)<br />application配置<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1620998133720-b9d03e29-6d4f-4440-b595-c858ced53d83.png#clientId=u7bbab827-6a23-4&from=paste&height=449&id=u6f3f2a4b&margin=%5Bobject%20Object%5D&name=image.png&originHeight=449&originWidth=757&originalType=binary&size=67994&status=done&style=none&taskId=u5f657cd3-5f7f-4cab-ae10-7ccd1d1a70e&width=757)
<a name="rtgkv"></a>
### 14.3.9 Nacos配置MySQL数据库
1、找到Nacos安装目录下的xxx\nacos\conf的nacos-mysql.sql文件<br />2、按照文件描述创建数据库![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1621047641589-9e516b37-25d2-4d6d-aa38-855756b69b3a.png#clientId=u7b540796-65c9-4&from=paste&height=22&id=u23b82359&margin=%5Bobject%20Object%5D&name=image.png&originHeight=22&originWidth=249&originalType=binary&size=1721&status=done&style=none&taskId=u2dd1a808-ab3b-4402-ae6f-627fee72919&width=249)<br />3、连上数据库开始执行sql文件中的建表语句<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1621047680150-44ebee81-8701-40c0-bf0c-c0bf275bfb7d.png#clientId=u7b540796-65c9-4&from=paste&height=287&id=u69a70283&margin=%5Bobject%20Object%5D&name=image.png&originHeight=287&originWidth=239&originalType=binary&size=9962&status=done&style=none&taskId=ub9e63abd-f95a-47f9-b975-223d65b298d&width=239)<br />4、修改Nacos安装目录下的xxx\nacos\conf的application.properties文件<br />解开注释并修改数据库链接信息为自己的链接信息<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1621048962328-02aeb26b-e9a7-4b78-81b0-5a709c8304f5.png#clientId=u7b540796-65c9-4&from=paste&height=196&id=u6c844c92&margin=%5Bobject%20Object%5D&name=image.png&originHeight=196&originWidth=917&originalType=binary&size=15592&status=done&style=none&taskId=u82f2ff7e-16b2-4de8-9ec6-141d5da9580&width=917)<br />5、启动nacos看到之前的配置都消失了<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1621049019854-f70f1e27-36ec-4b2b-9d87-687fa433feaa.png#clientId=u7b540796-65c9-4&from=paste&height=352&id=u48043d11&margin=%5Bobject%20Object%5D&name=image.png&originHeight=352&originWidth=1894&originalType=binary&size=38055&status=done&style=none&taskId=ua7ebd2b2-67d1-4f21-aad2-3a87675b289&width=1894)<br />6、随便新增一个配置文件，在mysql库中可以看到这个配置文件的记录即为成功<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1621049236009-70ccca60-1452-4a04-b50a-19379de9f131.png#clientId=u7b540796-65c9-4&from=paste&height=129&id=uf1d77b15&margin=%5Bobject%20Object%5D&name=image.png&originHeight=129&originWidth=1574&originalType=binary&size=12179&status=done&style=none&taskId=u99aa60f0-8dca-4acd-b3a8-e26b7990c9b&width=1574)<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1621049301425-76642b9a-923d-4437-9458-ec80e9d510ec.png#clientId=u7b540796-65c9-4&from=paste&height=69&id=u957e73ef&margin=%5Bobject%20Object%5D&name=image.png&originHeight=69&originWidth=1010&originalType=binary&size=10870&status=done&style=none&taskId=u1c5d7257-1295-476e-9795-39d250feb19&width=1010)
<a name="Ukye8"></a>
### 14.3.10 Nacos集群
架构图<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1620999193510-b2477386-4c74-4e80-9161-d1517b7024a0.png#clientId=u7bbab827-6a23-4&from=paste&height=476&id=u48a2c9b5&margin=%5Bobject%20Object%5D&name=image.png&originHeight=476&originWidth=487&originalType=binary&size=81700&status=done&style=none&taskId=uf155e5d9-3aa0-4650-9100-1d8f46f443a&width=487)<br />
<br />默认nacos使用嵌入式数据库实现数据的存储。所以，如果启动多个默认配置下的nacos节点，数据存储是存在一致性问题的，为了解决这个问题，nacos采用了集中式存储的方式来支持集群化部署，目前只支持MySQL的存储<br />**nacos支持三种部署模式**<br />单机模式-用于测试和单机试用<br />集群模式-用于生产环境，确保高可用<br />多集群模式-用于多数据中心场景
<a name="Yld6D"></a>
#### 14.3.10.1 Linux下Nacos集群配置
1、拷贝Nacos安装目录下的xxx\nacos\conf的cluster.conf.example重命名为cluster.conf，修改文件内容配置该集群内其他服务器nacos的IP和端口号
<a name="P35NO"></a>
## 14.4 Sentinel （熔断与限流）
<a name="Qymrp"></a>
### 14.4.1 概述
官网地址：[https://github.com/alibaba/Sentinel/wiki/%E4%BB%8B%E7%BB%8D](https://github.com/alibaba/Sentinel/wiki/%E4%BB%8B%E7%BB%8D)<br />       随着微服务的流行，服务和服务之间的稳定性变得越来越重要。Sentinel 以流量为切入点，从流量控制、熔断降级、系统负载保护等多个维度保护服务的稳定性。<br />Sentinel 具有以下特征:

- **丰富的应用场景**：Sentinel 承接了阿里巴巴近 10 年的双十一大促流量的核心场景，例如秒杀（即突发流量控制在系统容量可以承受的范围）、消息削峰填谷、集群流量控制、实时熔断下游不可用应用等。
- **完备的实时监控**：Sentinel 同时提供实时的监控功能。您可以在控制台中看到接入应用的单台机器秒级数据，甚至 500 台以下规模的集群的汇总运行情况。
- **广泛的开源生态**：Sentinel 提供开箱即用的与其它开源框架/库的整合模块，例如与 Spring Cloud、Dubbo、gRPC 的整合。您只需要引入相应的依赖并进行简单的配置即可快速地接入 Sentinel。
- **完善的 SPI 扩展点**：Sentinel 提供简单易用、完善的 SPI 扩展接口。您可以通过实现扩展接口来快速地定制逻辑。例如定制规则管理、适配动态数据源等。

Sentinel 的主要特性：<br />![](https://cdn.nlark.com/yuque/0/2021/png/12668119/1621068003735-e1906397-bdb7-40ca-a855-6790427f3b6e.png#clientId=ua5beb810-3a70-4&from=paste&height=686&id=ufae4e29f&margin=%5Bobject%20Object%5D&originHeight=686&originWidth=1470&originalType=url&status=done&style=none&taskId=udca28a67-63f9-47d3-9e0e-0b40a19f74f&width=1470)<br />**Sentinel分为两个部分：**<br />**核心库（Java客户端）**不依赖任何框架/库，能够运行于所有Java运行时环境，同时对Dubbo/SpringCloud等框架也有较好的支持。<br />**控制台（Dashboard）**基于SpringBoot开发，打包后可以直接运行，不需要额外的Tomcat等应用容器
<a name="Ir6xD"></a>
### 14.4.2 下载和安装
官方下载地址:[https://github.com/alibaba/Sentinel](https://github.com/alibaba/Sentinel/wiki/%E4%BB%8B%E7%BB%8D)/releases<br />下载心仪版本的jar包 java -jar运行jar包，**前提JDK需8以上，8080端口不能被占用**<br />启动成功后访问localhost:8080，账号密码默认均为sentinel
<a name="fQHLI"></a>
### 14.4.3 初始化监控
```xml
pom引入依赖
<!--springcloud alibaba nacos-->
        <dependency>
            <groupId>com.alibaba.cloud</groupId>
            <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
        </dependency>
        <!--springcloud alibaba sentinel-datasource-nacos 后续做持久化用到-->
        <dependency>
            <groupId>com.alibaba.csp</groupId>
            <artifactId>sentinel-datasource-nacos</artifactId>
        </dependency>
        <!--springcloud alibaba sentinel-->
        <dependency>
            <groupId>com.alibaba.cloud</groupId>
            <artifactId>spring-cloud-starter-alibaba-sentinel</artifactId>
        </dependency>
```
```yaml
yaml中加入配置
server:
  port: 8401
spring:
  application:
    name: cloudalibaba-sentinel-service
  cloud:
    nacos:
      discovery:
        # Nacos服务注册中心地址
        server-addr: localhost:8848
    sentinel:
      transport:
        # sentinel dashboard 地址
        dashboard: localhost:8080
        # 默认为8719，如果被占用会自动+1，直到找到为止
        port: 8719
      # 流控规则持久化到nacos
      datasource:
        dsl:
          nacos:
            server-addr: localhost:8848
            data-id: ${spring.application.name}
            group-id: DEFAULT_GROUP
            data-type: json
            rule-type: flow
management:
  endpoints:
    web:
      exposure:
        include: "*"
```
**Sentinel采用懒加载机制，需要执行一次被监控程序接口的调用，Sentinel监控界面上就可以看到了**
<a name="vE2qr"></a>
### 14.4.4 Sentinel流量控制规则（流控规则）
**资源名**：唯一名称，默认请求路径<br />**针对来源**：Sentinel可以针对调用者进行限流，填写微服务名，默认default（不区分来源）<br />**阈值类型/单机阈值**：<br />QPS（每秒钟的请求数量）：当调用该api的QPS达到阈值的时候，进行限流<br />线程数：当调用该api的线程数达到阈值的时候，进行限流<br />**是否集群**：不需要集群<br />**流控模式**：<br />**直接**：api达到限流条件时，直接限流<br />**关联**：当关联的资源达到阈值时，就限流自己<br />**链路**：只记录指定链路上的流量（指定资源从入口资源进来的流量，如果达到阈值，就进行限流）【api级别针对来源】<br />**流控效果**：<br />**快速失败**：直接失败，抛异常<br />**Warm Up**：根据codeFactor（冷加载因子，默认3）的值，从阈值/codeFactor，经过预热时长，才达到设置的QPS阈值<br />**排队等待：**严格控制请求通过的间隔时间，也即是让请求以均匀的速度通过，对应的是漏桶算法
<a name="Ff0zH"></a>
#### 14.4.4.1 添加流控规则
**直接：**<br />对/test接口添加流控规则，一秒钟只能有一次请求，请求过多直接->快速失败<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1621073401444-a83e04c2-4c62-4f4e-a7fa-08d6586f9993.png#clientId=uf37caac0-99ae-4&from=paste&height=500&id=u333880f0&margin=%5Bobject%20Object%5D&name=image.png&originHeight=500&originWidth=673&originalType=binary&size=31348&status=done&style=none&taskId=ua59aa7b1-6142-40a1-98e4-848354264e2&width=673)<br />失败展示<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1621073412450-d61e7f74-1ef1-4d7e-8ff2-d7213d460745.png#clientId=uf37caac0-99ae-4&from=paste&height=106&id=u9e2fe416&margin=%5Bobject%20Object%5D&name=image.png&originHeight=106&originWidth=289&originalType=binary&size=8411&status=done&style=none&taskId=u114107ea-7b73-48e8-b6bc-dd585a9afd0&width=289)<br />**关联：**<br />当关联资源testB阈值超过1时，则限流test（一般用于testB为支付订单，test为下单）<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1621083273072-bdbe03fa-2928-4cf0-8c15-0000ff106e66.png#clientId=uf37caac0-99ae-4&from=paste&height=561&id=ub8f13bab&margin=%5Bobject%20Object%5D&name=image.png&originHeight=561&originWidth=683&originalType=binary&size=34900&status=done&style=none&taskId=u7c8fbfc7-bb34-4801-a202-d928c6a1340&width=683)<br />**链路：**<br />当存在一个接口test服务有testA、testB两个Controller调用时，同时对两个接口进行大批量访问，testB没事，testA会出现限流现象<br />参考帖子：[https://blog.csdn.net/qq_31155349/article/details/108478190](https://blog.csdn.net/qq_31155349/article/details/108478190)<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1621135325548-e413b043-97c6-43a4-8752-40ee25cc13c5.png#clientId=ud46ae29b-9998-4&from=paste&height=561&id=ue2631a2c&margin=%5Bobject%20Object%5D&name=image.png&originHeight=561&originWidth=686&originalType=binary&size=35469&status=done&style=none&taskId=u058b3a50-6e4d-4a61-96f0-5ee4df320dd&width=686)
<a name="t8hwi"></a>
#### 14.4.2 流控效果
**快速失败：**<br />当单机阈值达到设定限制时直接返回失败提示<br />**Warm Up（预热）：**<br />即预热/冷启动方式。当系统长期处于低水位的情况下，当流量突然增加时，直接把系统拉升到高水位可能瞬间把系统压垮。通过"冷启动"，让通过的流量缓慢增加，在一定时间内逐渐增加到阈值上限，给冷系统一个预热的时间，避免冷系统被压垮。<br />![](https://cdn.nlark.com/yuque/0/2021/png/12668119/1621136414718-ec6edf50-94b8-4bb8-87ce-f0074e8ae596.png#clientId=ud46ae29b-9998-4&from=paste&height=489&id=u1ed26b87&margin=%5Bobject%20Object%5D&originHeight=489&originWidth=567&originalType=url&status=done&style=none&taskId=u703c3ac9-25df-47fe-a937-89bb2f46b31&width=567)<br />设定单机阈值为10，开始coldFactor（冷加载因子）默认是3，经过5秒钟升至设定阈值10<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1621136671802-e14f140e-6da4-4ef4-805a-f48e44f4fc5d.png#clientId=ud46ae29b-9998-4&from=paste&height=589&id=ucbd3c6d7&margin=%5Bobject%20Object%5D&name=image.png&originHeight=589&originWidth=685&originalType=binary&size=37147&status=done&style=none&taskId=ucef4e523-67f1-408a-aa68-6d143d8e78e&width=685)<br />**排队等待：**<br />匀速排队，让请求以均匀的速度通过，阈值类型必须设成QPS，否则无效，方式会严格的控制请求通过的间隔时间，也即是让请求以均匀的速度通过，对应的是漏桶算法<br />设置含义：/test每秒1次请求，超过的话就排队等待，等待的超时时间为20000毫秒
<a name="rpDVa"></a>
### 14.4.5 Sentinel熔断熔断降级（降级规则）
**Sentinel熔断降级会在调用链路中某个资源出现不稳定状态时（例如调用超时或异常比例升高），对这个资源的调用进行限制，让请求快速失败，避免影响到其他的资源而导致级联错误。**<br />**当资源被降级后，在接下来的降级时间窗口内，对该资源的调用都自动熔断（默认行为时抛出DegradeException）**<br />**RT(平均响应时间，秒级)：**

- 慢调用比例 (SLOW_REQUEST_RATIO)：选择以慢调用比例作为阈值，需要设置允许的慢调用 RT（即最大的响应时间），请求的响应时间大于该值则统计为慢调用。当单位统计时长**默认1000ms**（statIntervalMs）内请求数目大于设置的最小请求数目（**默认5**），并且慢调用的比例大于阈值，则接下来的熔断时长内请求会自动被熔断。经过熔断时长后熔断器会进入探测恢复状态（HALF-OPEN 状态），若接下来的一个请求响应时间小于设置的慢调用 RT 则结束熔断，若大于设置的慢调用 RT 则会再次被熔断。

**异常比例（秒级）：**

- QPS>=5且异常比例（秒级统计）超过阈值时，触发降级；时间窗口结束后，关闭降级
- 异常比例 (ERROR_RATIO)：当单位统计时长**默认1000ms**（statIntervalMs）内请求数目大于设置的最小请求数目（**默认5**），并且异常的比例大于阈值，则接下来的熔断时长内请求会自动被熔断。经过熔断时长后熔断器会进入探测恢复状态（HALF-OPEN 状态），若接下来的一个请求成功完成（没有错误）则结束熔断，否则会再次被熔断。**异常比率的阈值范围是[0.0, 1.0]，代表 0% - 100%**。

**异常数（分钟级）：**

- 异常数（分钟统计）超过阈值时，触发降级；时间窗口结束后，关闭降级
- 异常数 (ERROR_COUNT)：当单位统计时长内的异常数目超过阈值之后会自动进行熔断。经过熔断时长后熔断器会进入探测恢复状态（HALF-OPEN 状态），若接下来的一个请求成功完成（没有错误）则结束熔断，否则会再次被熔断。
<a name="eYDAz"></a>
### 14.5.6 热点参数限流
何为热点？热点即经常访问的数据。很多时候我们希望统计某个热点数据中访问频次最高的 Top K 数据，并对其访问进行限制。比如：

- 商品 ID 为参数，统计一段时间内最常购买的商品 ID 并进行限制
- 用户 ID 为参数，针对一段时间内频繁访问的用户 ID 进行限制

热点参数限流会统计传入参数中的热点参数，并根据配置的限流阈值与模式，对包含热点参数的资源调用进行限流。热点参数限流可以看做是一种特殊的流量控制，仅对包含热点参数的资源调用生效。<br />Sentinel 利用 LRU 策略统计最近最常访问的热点参数，结合令牌桶算法来进行参数级别的流控。热点参数限流支持集群模式。<br />**如果使用热点参数限流则一定要设置兜底方法，不然异常返回页面用户看到不好**
```java
@GetMapping("/testHotKey")
    //SentinelResource的value值也可作为控制台的资源名使用
    @SentinelResource(value = "testHotKey",blockHandler = "deal_getHotKey")//blockHandler兜底方法
    public String getHotKey(@RequestParam(value = "p1",required = false)String p1,
                            @RequestParam(value = "p2",required = false)String p2){
        return "testHotKey";

    }
    //getHotKey的兜底方法
    public String deal_getHotKey(String p1, String p2, BlockException exception){
        return "deal_getHotKey - -";
    }
```
当参数索引0（对应资源方法的第一个参数）下标的值不为aa适用上面的热点规则方法，为aa则适用例外项<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1621257347690-4000cc69-7997-471b-9cdd-bc2e72ec4e88.png#clientId=u5818a23e-3674-4&from=paste&height=727&id=u9e498e02&margin=%5Bobject%20Object%5D&name=image.png&originHeight=727&originWidth=679&originalType=binary&size=43832&status=done&style=none&taskId=u5bfd3815-1f91-40e8-9dc4-26b7d3ede1e&width=679)
<a name="Dp9Cx"></a>
### 14.5.7 Sentinel系统自适应限流（系统规则）
系统保护规则是从应用级别的入口流量进行控制，从单台机器的 load、CPU 使用率、平均 RT、入口 QPS 和并发线程数等几个维度监控应用指标，让系统尽可能跑在最大吞吐量的同时保证系统整体的稳定性。<br />系统保护规则是应用整体维度的，而不是资源维度的，并且**仅对入口流量生效**。入口流量指的是进入应用的流量（EntryType.IN），比如 Web 服务或 Dubbo 服务端接收的请求，都属于入口流量。<br />系统规则支持以下的模式：

- **Load 自适应**（仅对 Linux/Unix-like 机器生效）：系统的 load1 作为启发指标，进行自适应系统保护。当系统 load1 超过设定的启发值，且系统当前的并发线程数超过估算的系统容量时才会触发系统保护（BBR 阶段）。系统容量由系统的maxQps * minRt估算得出。设定参考值一般是CPU cores * 2.5。
- **CPU usage**（1.5.0+ 版本）：当系统 CPU 使用率超过阈值即触发系统保护（取值范围 0.0-1.0），比较灵敏。
- **平均 RT**：当单台机器上所有入口流量的平均 RT 达到阈值即触发系统保护，单位是毫秒。
- **并发线程数**：当单台机器上所有入口流量的并发线程数达到阈值即触发系统保护。
- **入口 QPS**：当单台机器上所有入口流量的 QPS 达到阈值即触发系统保护。
<a name="OqsB5"></a>
### 14.5.8 @SentinelResource注解使用
```java
//value指定资源名，fallback程序异常指定的兜底方法，
blockHandler程序正常但不符合限流规则指定兜底方法，
当fallback和blockHandler都配置时程序出错fallback生效
不符合控制台规则blockHandler生效
访问出错的程序同时不符合控制台规则blockHandler生效
exceptionsToIgnore当方法报出该配置中已经配置的异常不走fallback方法
@SentinelResource(value = "testHotKey",fallback="fail",blockHandler = "deal_getHotKey",
                  exceptionsToIgnore= {NullPointerException.class})
```
**优化兜底方法避免代码膨胀，体现全局统一处理方法**
```java
@GetMapping("/testHotKey")
   /value指定资源名，blockHandlerClass兜底方法所在类，blockHandler指定兜底方法名
    @SentinelResource(value = "testHotKey",blockHandlerClass = MyBlockHandler.class,blockHandler = "aliHandler2")//blockHandler兜底方法
    public String getHotKey(@RequestParam(value = "p1",required = false)String p1,
                            @RequestParam(value = "p2",required = false)String p2){
        return "testHotKey";

    }


public class MyBlockHandler {
	//注意这里规定必须static方法
    public static String aliHandler(String p1, String p2, BlockException exception){
        return "aliHandler---------1";
    }

    public static String aliHandler2(String p1, String p2, BlockException exception){
        return "aliHandler---------2";
    }
}
```
<a name="jgqnc"></a>
### 14.5.9 Sentinel规则持久化
**将Sentinel配置规则持久化进Nacos保存**
```xml
pom中添加依赖
<!--springcloud alibaba sentinel-datasource-nacos 做持久化用到-->
        <dependency>
            <groupId>com.alibaba.csp</groupId>
            <artifactId>sentinel-datasource-nacos</artifactId>
        </dependency>
```
```yaml
spring:
  application:
    name: cloudalibaba-sentinel-service
  cloud:
    nacos:
      discovery:
        # Nacos服务注册中心地址
        server-addr: localhost:8848
    sentinel:
      transport:
        # sentinel dashboard 地址
        dashboard: localhost:8080
        # 默认为8719，如果被占用会自动+1，直到找到为止
        port: 8719
      # 流控规则持久化到nacos
      datasource:
        dsl:
          nacos:
            server-addr: localhost:8848
            data-id: ${spring.application.name} #在nacos的data id
            group-id: DEFAULT_GROUP #默认分组
            data-type: json #选择json类型
            rule-type: flow
```
启动nacos新增配置<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1621307423676-fe4b0450-419c-4845-aa79-5da7cdcec1bb.png#clientId=uaff3b15c-17da-4&from=paste&height=584&id=u0404deca&margin=%5Bobject%20Object%5D&name=image.png&originHeight=584&originWidth=724&originalType=binary&size=37765&status=done&style=none&taskId=u0b95f4ab-4fe8-45dd-8c01-83e4f152da5&width=724)
```json
[
    {
        "resource":"testHotKey", //资源名称
        "limitApp":"default",  //来源应用
        "grade":1, //阈值类型，0表示线程数，1表示QPS
        "count":1, //单机阈值
        "strategy":0, //流控模式，0表示直接，1表示关联，2表示链路
        "controlBehavior":0, //流控效果，0表示快速失败，1表示Warm Up，2表示排队等待
        "clusterMode":false //是否集群
    }
]
```
<a name="PrrRC"></a>
## 14.5 Seata （处理分布式事务）
<a name="aitYk"></a>
### 14.5.1 概述
Seata是一款开源的分布式事务解决方案，致力于在微服务架构下提供高性能和简单易用的分布式事务服务。Seata 将为用户提供了 AT、TCC、SAGA 和 XA 事务模式，为用户打造一站式的分布式解决方案。<br />Seata由一加三的套件组成，**一就是全局事务唯一ID，三见下方**<br />**Seata术语（三组件）**
<a name="y27En"></a>
#### TC (Transaction Coordinator) - 事务协调者
维护全局和分支事务的状态，驱动全局事务提交或回滚。
<a name="r9NyJ"></a>
#### TM (Transaction Manager) - 事务管理器
定义全局事务的范围：开始全局事务、提交或回滚全局事务。
<a name="Efb5W"></a>
#### RM (Resource Manager) - 资源管理器
管理分支事务处理的资源，与TC交谈以注册分支事务和报告分支事务的状态，并驱动分支事务提交或回滚。
<a name="pcy3p"></a>
#### 处理过程
1、TM向TC申请开启一个全局事务，全局事务创建成功并生成一个全局唯一的XID；<br />2、XID在微服务调用链路的上下文中传播；<br />3、RM向TC注册分支事务，将其纳入XID对应全局事务的管辖；<br />4、TM向TC发起针对XID的全局提交或回滚决议；<br />5、TC调度XID下管辖的全部分支事务完成提交或回滚请求。
<a name="S5jcb"></a>
### 14.5.2 官网地址
[http://seata.io/zh-cn/](http://seata.io/zh-cn/)
<a name="L2iZu"></a>
### 14.5.3 Seata安装及准备工作
1、下载好Seata修改目录下conf/file.conf文件（数据库配置相关）<br />2、Seata修改目录下conf/registry.conf（这里把seata注册到nacos中），registry下面type修改为nacos，修改nacos信息为自己的<br />3、启动nacos<br />4、修改好之后双击seata-server.bat启动服务，在nacos服务列表可以看到seata即为成功<br />5、创建config.txt并修改其中的数据库连接信息，其他不动，config.txt内容地址[https://github.com/seata/seata/blob/develop/script/config-center/config.txt](https://github.com/seata/seata/blob/develop/script/config-center/config.txt)创建好后放在seata的根目录<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1621404776533-98bf74c9-3c0a-4737-aeba-e68082d3a9f3.png#clientId=uab55f441-405f-4&from=paste&height=301&id=ue2f8fbfd&margin=%5Bobject%20Object%5D&name=image.png&originHeight=301&originWidth=470&originalType=binary&size=42355&status=done&style=none&taskId=ubac169df-bfb7-40de-917c-7d8e3a5a20b&width=470)<br />6、在conf目录创建nacos-config.sh，nacos-config.sh内容地址[https://github.com/seata/seata/blob/develop/script/config-center/nacos/nacos-config.sh](https://github.com/seata/seata/blob/develop/script/config-center/nacos/nacos-config.sh)<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1621404915585-aa4a8882-8278-4a15-a0cf-ac11071eb295.png#clientId=uab55f441-405f-4&from=paste&height=370&id=ud243325b&margin=%5Bobject%20Object%5D&name=image.png&originHeight=370&originWidth=682&originalType=binary&size=58677&status=done&style=none&taskId=u728b5628-1bb8-4a0b-a5a7-5e3a8026692&width=682)<br />在当前目录打开打开git bash here，执行命令sh nacos-config.sh -h 127.0.0.1将seata规则配置进nacos<br />如下二图即为成功（这里有个坑文件夹中间不能有空格，开始放在Program Files目录下一直报找不到config.txt的错）<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1621405013008-38b219ad-aa0f-4cc1-bb22-570bc71b1714.png#clientId=uab55f441-405f-4&from=paste&height=376&id=u4966add8&margin=%5Bobject%20Object%5D&name=image.png&originHeight=376&originWidth=595&originalType=binary&size=62784&status=done&style=none&taskId=u4cc87eda-6519-4afe-974c-3fe3d4af735&width=595)<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1621405019483-2ea46d4a-938e-4ffb-ada4-13a1211232ad.png#clientId=uab55f441-405f-4&from=paste&height=376&id=uc8233fc5&margin=%5Bobject%20Object%5D&name=image.png&originHeight=376&originWidth=595&originalType=binary&size=59577&status=done&style=none&taskId=uc5b9e242-d6de-42d5-af72-2899c03d328&width=595)<br />查看nacos规则已经成功配置<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1621405114176-3f415a25-afa4-4a82-bd8b-2405384c0e8a.png#clientId=uab55f441-405f-4&from=paste&height=602&id=ucb7a9b59&margin=%5Bobject%20Object%5D&name=image.png&originHeight=602&originWidth=1637&originalType=binary&size=81403&status=done&style=none&taskId=ube30343a-4c0b-49da-b92f-fdde50fe52d&width=1637)<br />到这Seata环境算是搭建好了，真坑啊
```sql
在每个微服务的库下面创建一张日志回滚表
CREATE TABLE `undo_log` (
  `id` bigint(20) NOT NULL AUTO_INCREMENT,
  `branch_id` bigint(20) NOT NULL,
  `xid` varchar(100) NOT NULL,
  `context` varchar(128) NOT NULL,
  `rollback_info` longblob NOT NULL,
  `log_status` int(11) NOT NULL,
  `log_created` datetime NOT NULL,
  `log_modified` datetime NOT NULL,
  `ext` varchar(100) DEFAULT NULL,
  PRIMARY KEY (`id`),
  UNIQUE KEY `ux_undo_log` (`xid`,`branch_id`)
) ENGINE=InnoDB AUTO_INCREMENT=1 DEFAULT CHARSET=utf8;
```
<a name="qHD2o"></a>
### 14.5.4 Seata下单->减库存->扣余额业务实现
```xml
pom依赖如下
 <!--nacos-->
        <dependency>
            <groupId>com.alibaba.cloud</groupId>
            <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
        </dependency>
        <!--seata-->
        <dependency>
            <groupId>com.alibaba.cloud</groupId>
            <artifactId>spring-cloud-starter-alibaba-seata</artifactId>
            <exclusions>
                <exclusion>
                    <groupId>io.seata</groupId>
                    <artifactId>seata-all</artifactId>
                </exclusion>
            </exclusions>
        </dependency>
        <dependency>
            <groupId>io.seata</groupId>
            <artifactId>seata-all</artifactId>
            <version>1.0.0</version>
        </dependency>
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-openfeign</artifactId>
        </dependency>
```
```yaml
配置文件如下
server:
  port: 2001

spring:
  application:
    name: seata-order-service
  cloud:
    alibaba:
      seata:
        # 自定义事务组名称需要与seata-server中的对应，1.4.0版本这项值在config.txt文件中
        #搜索service.vgroupMapping
        #完整配置项长这样service.vgroupMapping.my_test_tx_group=default
        #鬼知道为啥是这样，草
        tx-service-group: my_test_tx_group
    nacos:
      discovery:
        server-addr: 127.0.0.1:8848
  datasource:
    # 当前数据源操作类型
    type: com.alibaba.druid.pool.DruidDataSource
    # mysql驱动类
    driver-class-name: com.mysql.jdbc.Driver
    url: jdbc:mysql://localhost:3306/seata_order?useUnicode=true&characterEncoding=UTF-8&useSSL=false&serverTimezone=GMT%2B8
    username: root
    password: root
feign:
  hystrix:
    enabled: false
logging:
  level:
    io:
      seata: info

mybatis:
  mapper-locations: classpath*:mapper/*.xml
```
```java
在resource目录下建一个file.conf文件，内容如下，TMD此时我已懵逼
transport {
  # tcp udt unix-domain-socket
  type = "TCP"
  #NIO NATIVE
  server = "NIO"
  #enable heartbeat
  heartbeat = true
  #thread factory for netty
  thread-factory {
    boss-thread-prefix = "NettyBoss"
    worker-thread-prefix = "NettyServerNIOWorker"
    server-executor-thread-prefix = "NettyServerBizHandler"
    share-boss-worker = false
    client-selector-thread-prefix = "NettyClientSelector"
    client-selector-thread-size = 1
    client-worker-thread-prefix = "NettyClientWorkerThread"
    # netty boss thread size,will not be used for UDT
    boss-thread-size = 1
    #auto default pin or 8
    worker-thread-size = 8
  }
  shutdown {
    # when destroy server, wait seconds
    wait = 3
  }
  serialization = "seata"
  compressor = "none"
}
service {
  #vgroup->rgroup
  # 事务组名称
  vgroup_mapping.my_test_tx_group = "default"
  #only support single node
  default.grouplist = "127.0.0.1:8091"
  #degrade current not support
  enableDegrade = false
  #disable
  disable = false
  #unit ms,s,m,h,d represents milliseconds, seconds, minutes, hours, days, default permanent
  max.commit.retry.timeout = "-1"
  max.rollback.retry.timeout = "-1"
}

client {
  async.commit.buffer.limit = 10000
  lock {
    retry.internal = 10
    retry.times = 30
  }
  report.retry.count = 5
  tm.commit.retry.count = 1
  tm.rollback.retry.count = 1
}

## transaction log store
store {
  ## store mode: file、db
  #mode = "file"
  mode = "db"

  ## file store
  file {
    dir = "sessionStore"

    # branch session size , if exceeded first try compress lockkey, still exceeded throws exceptions
    max-branch-session-size = 16384
    # globe session size , if exceeded throws exceptions
    max-global-session-size = 512
    # file buffer size , if exceeded allocate new buffer
    file-write-buffer-cache-size = 16384
    # when recover batch read size
    session.reload.read_size = 100
    # async, sync
    flush-disk-mode = async
  }

  ## database store
  db {
    ## the implement of javax.sql.DataSource, such as DruidDataSource(druid)/BasicDataSource(dbcp) etc.
    datasource = "dbcp"
    ## mysql/oracle/h2/oceanbase etc.
    db-type = "mysql"
    driver-class-name = "com.mysql.jdbc.Driver"
    url = "jdbc:mysql://127.0.0.1:3306/seata?useUnicode=true&characterEncoding=utf-8&useSSL=false"
    user = "root"
    password = "123456"
    min-conn = 1
    max-conn = 3
    global.table = "global_table"
    branch.table = "branch_table"
    lock-table = "lock_table"
    query-limit = 100
  }
}
lock {
  ## the lock store mode: local、remote
  mode = "remote"

  local {
    ## store locks in user's database
  }

  remote {
    ## store locks in the seata's server
  }
}
recovery {
  #schedule committing retry period in milliseconds
  committing-retry-period = 1000
  #schedule asyn committing retry period in milliseconds
  asyn-committing-retry-period = 1000
  #schedule rollbacking retry period in milliseconds
  rollbacking-retry-period = 1000
  #schedule timeout retry period in milliseconds
  timeout-retry-period = 1000
}

transaction {
  undo.data.validation = true
  undo.log.serialization = "jackson"
  undo.log.save.days = 7
  #schedule delete expired undo_log in milliseconds
  undo.log.delete.period = 86400000
  undo.log.table = "undo_log"
}

## metrics settings
metrics {
  enabled = false
  registry-type = "compact"
  # multi exporters use comma divided
  exporter-list = "prometheus"
  exporter-prometheus-port = 9898
}

support {
  ## spring
  spring {
    # auto proxy the DataSource bean
    datasource.autoproxy = false
  }
}
```
拷贝修改好的registry.conf到resource目录下，后面就是业务逻辑实现了<br />
<br />​

