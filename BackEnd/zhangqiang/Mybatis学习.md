<a name="e63AE"></a>
# 1、简介
Hibernate：全自动全映射ORM（javaBean和数据库数据映射）框架<br />Mybatis：半自动ORM轻量级框架，SQL与编码分离，SQL由开发人员控制
<a name="vukoQ"></a>
## 1.1 原理：
mybatis运行原理：<br />1.通过加载mybatis全局配置文件以及mapper映射文件初始化configuration对象 <br />和Executor对象（通过全局配置文件中的defaultExecutorType初始化）；<br />2.创建一个defaultSqlSession对象，将configuration对象和Executor对象注入给 <br />defaulSqlSession对象中；<br />3.defaulSqlSession通过getMapper()获取mapper接口的代理对象mapperProxy <br />（mapperProxy中包含defaultSQLSession对象）<br />4.执行增删改查：<br />1）通过defaulSqlSession中的属性Executor创建statementHandler对象；<br />2）创建statementHandler对象的同时也创建parameterHandler和 <br />resultSetHandler；<br />3） 通过parameterHandler设置预编译参数及参数值；<br />4）调用statementHandler执行增删改查；<br />5）通过resultsetHandler封装查询结果
<a name="ielsK"></a>
# 2、使用
mapper.xml文件中namespace要指定为接口全类名（文件和接口绑定），文件中标签的id与接口中方法一致（标签与方法绑定）
<a name="lmA9p"></a>
## 2.1 resultMap标签使用
```xml
<resultMap id="test" type="com.zhangqiang.learn.bean.Zq">
        <!--id定义主键底层会有优化，
            column指定数据的一列
            property指定数据库的一列对应javaBean的哪一列-->
        <id column="id" property="id"></id>
        <!--result定义普通列的映射类型-->
        <result column="name" property="name"></result>
  		<!--假设Zq类中有其他类名叫Qq，使用如下赋值方式即可-->
  		<result column="nameqq" property="Qq.name"></result>
  <!--其他不指定的列都会自动封装，规范起见写了resultMap就把所有映射都写上，方便维护-->
    </resultMap>

    <select id="getAllZq" resultMap="test">
            select * from zq_test
    </select>
```
<a name="DKHQU"></a>
## 2.2 当给对象中包含的其他对象赋值时（使用association）
```xml
<resultMap id="test1" type="com.zhangqiang.learn.bean.Zq">
        <id column="id" property="id"></id>
        <!--result定义普通列的映射类型-->
        <!--Zq类中有其他类名叫user，property="user指定那个属性是级联查询对象
        javaType指定类路径-->
        <association property="user" javaType="com.zhangqiang.learn.bean.User">
            <result column="name" property="name"></result>
        </association>
    </resultMap>
```
<a name="njN9D"></a>
## 2.3 association分步查询
```xml
<resultMap id="test1" type="com.zhangqiang.learn.bean.Zq">
        <!--使用select指定的方法(传入column这列的参数)结果赋值给property指定的对象-->
  			<!--使用colum传多列值得写法column="{key1=column1,key2=column2}"
				key为select指定方法所需要的条件参数名，如getZq需要参数为deptId则key为deptId，column为
				当前查询结果集要传递给getZq当条件参数的列名-->
        <association property="user" select="com.zhangqiang.learn.mapper.TestMapper.getZq"
                     column="id">          
        </association>
    </resultMap>
```
<a name="aFexk"></a>
## 2.3 association分步查询配合延迟加载
```xml
在Mybatis主配置文件中加入配置
<setting name="lazyLoadingEnabled" value="true">开启懒加载
<setting name="aggressiveLazyLoading" value="false">true当你需要类中任何一个属性时，
  全部属性都会被加载，false，当你需要时只加载你需要的属性
```
<a name="Gam8z"></a>
## 2.4 嵌套结果集定义集合封装规则
```xml
<resultMap id="test1" type="com.zhangqiang.learn.bean.Zq">
        <id column="id" property="id"></id>
        <!--result定义普通列的映射类型-->
        <!--Zq类中有其他类名叫user，property="user指定那个属性是级联查询对象
        javaType指定类路径-->
        <association property="user" javaType="com.zhangqiang.learn.bean.User">
            <result column="name" property="name"></result>
        </association>
        <!--当查询结果返回有对象集合时使用下列方式关联
        property指定对象集合在类中的名字，ofType指定集合对象类型-->
        <collection property="pets" ofType="com.zhangqiang.learn.bean.Pet">
            <result column="name" property="name"></result>
        </collection>
    </resultMap>
```
<a name="JD9aO"></a>
## 2.5 collection开启延迟加载
```xml
<collection fetchType="lazy"延迟加载   fetchType="eager"立即加载
```
<a name="hFXlK"></a>
## 2.6 鉴别器（根据查询结果做不同处理）
```xml
<!-- =======================鉴别器============================ -->
	<!-- <discriminator javaType=""></discriminator>
		鉴别器：mybatis可以使用discriminator判断某列的值，然后根据某列的值改变封装行为
		封装Employee：
			如果查出的是女生：就把部门信息查询出来，否则不查询；
			如果是男生，把last_name这一列的值赋值给email;
	 -->
	 <resultMap type="com.atguigu.mybatis.bean.Employee" id="MyEmpDis">
	 	<id column="id" property="id"/>
	 	<result column="last_name" property="lastName"/>
	 	<result column="email" property="email"/>
	 	<result column="gender" property="gender"/>
	 	<!--
	 		column：指定判定的列名
	 		javaType：列值对应的java类型  -->
	 	<discriminator javaType="string" column="gender">
	 		<!--女生  resultType:指定封装的结果类型；不能缺少。/resultMap-->
	 		<case value="0" resultType="com.atguigu.mybatis.bean.Employee">
	 			<association property="dept" 
			 		select="com.atguigu.mybatis.dao.DepartmentMapper.getDeptById"
			 		column="d_id">
		 		</association>
	 		</case>
	 		<!--男生 ;如果是男生，把last_name这一列的值赋值给email; -->
	 		<case value="1" resultType="com.atguigu.mybatis.bean.Employee">
		 		<id column="id" property="id"/>
			 	<result column="last_name" property="lastName"/>
			 	<result column="last_name" property="email"/>
			 	<result column="gender" property="gender"/>
	 		</case>
	 	</discriminator>
	 </resultMap>
```
<a name="M8rlu"></a>
## 2.7 动态SQL 
动态 SQL是MyBatis强大特性之一。极大的简化我们拼装SQL的操作。<br />动态 SQL 元素和使用 JSTL 或其他类似基于 XML 的文本处理器相似。<br />MyBatis 采用功能强大的基于 OGNL 的表达式来简化操作。<br />– if<br />– choose (when, otherwise)<br />– trim (where, set)<br />– foreach
<a name="jcWxS"></a>
### 2.7.1 动态SQL if（根据条件动态拼接SQL）
```xml
<select id="getEmpsByConditionIf" resultType="com.atguigu.mybatis.bean.Employee">
	 	select * from tbl_employee
	 	<!-- where -->
		 	<!-- test：判断表达式（OGNL）
		 	OGNL参照PPT或者官方文档。
		 	  	 c:if  test
		 	从参数中取值进行判断
		 	
		 	遇见特殊符号应该去写转义字符：
		 	&&：
		 	-->
		 	<if test="id!=null">
		 		id=#{id}
		 	</if>
		 	<if test="lastName!=null &amp;&amp; lastName!=&quot;&quot;">
		 		and last_name like #{lastName}
		 	</if>
		 	<if test="email!=null and email.trim()!=&quot;&quot;">
		 		and email=#{email}
		 	</if> 
		 	<!-- ognl会进行字符串与数字的转换判断  "0"==0 -->
		 	<if test="gender==0 or gender==1">
		 	 	and gender=#{gender}
		 	</if>
	 </select>
```
<a name="UEWYc"></a>
### 2.7.2 OGNL表达式的使用
OGNL会进行字符串与数字的转换判断<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1622522436847-a3f856aa-6244-4cc5-85be-2429c667161f.png#clientId=u24966944-0da7-4&from=paste&height=567&id=u6081d4da&margin=%5Bobject%20Object%5D&name=image.png&originHeight=567&originWidth=906&originalType=binary&ratio=1&size=133864&status=done&style=none&taskId=ub2e9d816-a992-48b3-8787-bc2a7d887c0&width=906)
<a name="xkH1K"></a>
### 2.7.3 动态SQL where（去除where条件首个多余的and或or）
如2.7.1if，如果id为null则sql拼装就会存在问题，where条件后面直接拼装and就会有问题了,使用<where>标签去代替where条件则可以很好的解决SQL拼装错误问题（只会去掉多出来的第一个where或者or）
```xml
<select id="getEmpsByConditionIf" resultType="com.atguigu.mybatis.bean.Employee">
	 	select * from tbl_employee
	 	<!-- where -->
	 	<where>
		 	<!-- test：判断表达式（OGNL）
		 	OGNL参照PPT或者官方文档。
		 	  	 c:if  test
		 	从参数中取值进行判断
		 	
		 	遇见特殊符号应该去写转义字符：
		 	&&：
		 	-->
		 	<if test="id!=null">
		 		id=#{id}
		 	</if>
		 	<if test="lastName!=null &amp;&amp; lastName!=&quot;&quot;">
		 		and last_name like #{lastName}
		 	</if>
		 	<if test="email!=null and email.trim()!=&quot;&quot;">
		 		and email=#{email}
		 	</if> 
		 	<!-- ognl会进行字符串与数字的转换判断  "0"==0 -->
		 	<if test="gender==0 or gender==1">
		 	 	and gender=#{gender}
		 	</if>
	 	</where>
	 </select>
```
<a name="PquGE"></a>
### 2.7.4 动态SQL trim（自定义SQL截取规则）
由于<where>标签只能处理多出来的第一个and或or无法处理SQL末尾多出的and或or，可使用trim自定义截取规则
```xml
<select id="getEmpsByConditionTrim" resultType="com.atguigu.mybatis.bean.Employee">
	 	select * from tbl_employee
	 	<!-- 后面多出的and或者or where标签不能解决 
	 	prefix="":前缀：trim标签体中是整个字符串拼串 后的结果。
	 			prefix给拼串后的整个字符串加一个前缀 
	 	prefixOverrides="":
	 			前缀覆盖： 去掉整个字符串前面多余的字符，如下SQL and条件在前可以用这个条件
	 	suffix="":后缀
	 			suffix给拼串后的整个字符串加一个后缀 
	 	suffixOverrides=""
	 			后缀覆盖：去掉整个字符串后面多余的字符
	 			
	 	-->
	 	<!-- 自定义字符串的截取规则 -->
	 	<trim prefix="where" suffixOverrides="and">
	 		<if test="id!=null">
		 		id=#{id} and
		 	</if>
		 	<if test="lastName!=null &amp;&amp; lastName!=&quot;&quot;">
		 		last_name like #{lastName} and
		 	</if>
		 	<if test="email!=null and email.trim()!=&quot;&quot;">
		 		email=#{email} and
		 	</if> 
		 	<!-- ognl会进行字符串与数字的转换判断  "0"==0 -->
		 	<if test="gender==0 or gender==1">
		 	 	gender=#{gender}
		 	</if>
		 </trim>
	 </select>
```
<a name="zrWM7"></a>
### 2.7.5 动态SQL choose（多选一条件查询）
```xml
<select id="getEmpsByConditionChoose" resultType="com.atguigu.mybatis.bean.Employee">
	 	select * from tbl_employee 
	 	<where>
	 		<!-- 如果带了id就用id查，如果带了lastName就用lastName查;只会进入其中一个 -->
	 		<choose>
	 			<when test="id!=null">
	 				id=#{id}
	 			</when>
	 			<when test="lastName!=null">
	 				last_name like #{lastName}
	 			</when>
	 			<when test="email!=null">
	 				email = #{email}
	 			</when>
	 			<otherwise>
	 				gender = 0
	 			</otherwise>
	 		</choose>
	 	</where>
	 </select>
```
2.7.6 动态SQL set<br />​<br />
<a name="UjjkD"></a>
## 2.8 Mybatis缓存
<a name="E3WRy"></a>
### 2.8.1 一级缓存（本地缓存）
sqlSession级别的缓存，一直开启无法关闭，与数据库同一次会话期间查询到的数据会放在本地缓存中。以后如果需要获取相同数据，直接从缓存中拿，没必要再去查询数据库。
<a name="bCU3I"></a>
#### 一级缓存失效的四种情况：
1、查询使用的sqlSession不同<br />2、相同sqlSession但是查询条件不同<br />3、sqlSession相同，查询条件相同，但是两次查询中间有增删改操作<br />4、sqlSession相同，查询条件相同，手动调用清除缓存方法
<a name="uTHZH"></a>
### 2.8.2 二级缓存（全局缓存）
基于namespace级别的缓存，一个namespace对应一个二级缓存<br />一个会话，查询一条数据，这个数据就会被放在当前会话的一级缓存中；<br />如果会话关闭，一级缓存中的数据会被保存到二级缓存中，新的会话查询信息，就可以参照二级缓存里面的内容	。<br />不同namespace查出的数据会放在自己对应的缓存中（map）
<a name="R0TjL"></a>
#### 二级缓存配置项含义
eviction:缓存的回收策略：		<br />• LRU – 最近最少使用的：移除最长时间不被使用的对象。<br />		• FIFO – 先进先出：按对象进入缓存的顺序来移除它们。<br />		• SOFT – 软引用：移除基于垃圾回收器状态和软引用规则的对象。<br />		• WEAK – 弱引用：更积极地移除基于垃圾收集器状态和弱引用规则的对象。<br />		• 默认的是 LRU。<br />flushInterval：缓存刷新间隔<br />		缓存多长时间清空一次，默认不清空，设置一个毫秒值<br />readOnly:是否只读：<br />		true：只读；mybatis认为所有从缓存中获取数据的操作都是只读操作，不会修改数据。<br />				 mybatis为了加快获取速度，直接就会将数据在缓存中的引用交给用户。不安全，速度快<br />		false：非只读：mybatis觉得获取的数据可能会被修改。<br />				mybatis会利用序列化&反序列的技术克隆一份新的数据给你。安全，速度慢<br />size：缓存存放多少元素；<br />type=""：指定自定义缓存的全类名；<br />			实现Cache接口即可；<br />​<br />
<a name="KLzv4"></a>
# 1、什么是Mybatis？
（1）Mybatis是一个半ORM（对象关系映射）框架，它内部封装了JDBC，加载驱动、创建连接、创建statement等繁杂的过程，开发者开发时只需要关注如何编写SQL语句，可以严格控制sql执行性能，灵活度高。<br />​

（2）作为一个半ORM框架，MyBatis 可以使用 XML 或注解来配置和映射原生信息，将 POJO映射成数据库中的记录，避免了几乎所有的 JDBC 代码和手动设置参数以及获取结果集。<br />​

称Mybatis是半自动ORM映射工具，是因为在查询关联对象或关联集合对象时，需要手动编写sql来完成。不像Hibernate这种全自动ORM映射工具，Hibernate查询关联对象或者关联集合对象时，可以根据对象关系模型直接获取。<br />​

（3）通过xml 文件或注解的方式将要执行的各种 statement 配置起来，并通过java对象和 statement中sql的动态参数进行映射生成最终执行的sql语句，最后由mybatis框架执行sql并将结果映射为java对象并返回。（从执行sql到返回result的过程）。<br />​

（4）由于MyBatis专注于SQL本身，灵活度高，所以比较适合对性能的要求很高，或者需求变化较多的项目，如互联网项目。<br />​

 <br />​<br />
<a name="lm8ep"></a>
# 2、Mybaits的优缺点：
​

（1）优点：<br />​

① 基于SQL语句编程，相当灵活，不会对应用程序或者数据库的现有设计造成任何影响，SQL写在XML里，解除sql与程序代码的耦合，便于统一管理；提供XML标签，支持编写动态SQL语句，并可重用。<br />​

② 与JDBC相比，减少了50%以上的代码量，消除了JDBC大量冗余的代码，不需要手动开关连接；<br />​

③ 很好的与各种数据库兼容（因为MyBatis使用JDBC来连接数据库，所以只要JDBC支持的数据库MyBatis都支持）。<br />​

④ 能够与Spring很好的集成；<br />​

⑤ 提供映射标签，支持对象与数据库的ORM字段关系映射；提供对象关系映射标签，支持对象关系组件维护。<br />​

（2）缺点：<br />​

① SQL语句的编写工作量较大，尤其当字段多、关联表多时，对开发人员编写SQL语句的功底有一定要求。<br />​

② SQL语句依赖于数据库，导致数据库移植性差，不能随意更换数据库。<br />​

 <br />​<br />
<a name="gpJGQ"></a>
# 3、#{}和${}的区别是什么？
​

${}是字符串替换，#{}是预处理；<br />​

Mybatis在处理${}时，就是把${}直接替换成变量的值。而Mybatis在处理#{}时，会对sql语句进行预处理，将sql中的#{}替换为?号，调用PreparedStatement的set方法来赋值；<br />​

使用#{}可以有效的防止SQL注入，提高系统安全性。<br />​

 <br />​<br />
<a name="Tu58H"></a>
# 4、通常一个mapper.xml文件，都会对应一个Dao接口，这个Dao接口的工作原理是什么？Dao接口里的方法，参数不同时，方法能重载吗？
​

（详细的工作原理请参考这篇文章：[https://blog.csdn.net/a745233700/article/details/89308762](https://blog.csdn.net/a745233700/article/details/89308762)）<br />​

Mapper 接口的工作原理是JDK动态代理，Mybatis运行时会使用JDK动态代理为Mapper接口生成代理对象proxy，代理对象会拦截接口方法，根据类的全限定名+方法名，唯一定位到一个MapperStatement并调用执行器执行所代表的sql，然后将sql执行结果返回。<br />​

Mapper接口里的方法，是不能重载的，因为是使用 全限名+方法名 的保存和寻找策略。<br />​

Dao接口即Mapper接口。接口的全限名，就是映射文件中的namespace的值；接口的方法名，就是映射文件中Mapper的Statement的id值；接口方法内的参数，就是传递给sql的参数。<br />​

当调用接口方法时，接口全限名+方法名拼接字符串作为key值，可唯一定位一个MapperStatement。在Mybatis中，每一个SQL标签，比如<select>、<insert>、<update>、<delete>标签，都会被解析为一个MapperStatement对象。<br />​

举例：com.mybatis3.mappers.StudentDao.findStudentById，可以唯一找到namespace为com.mybatis3.mappers.StudentDao下面 id 为 findStudentById 的 MapperStatement。<br />​

 <br />​<br />
<a name="FQ3MN"></a>
# 5、Mybatis的Xml映射文件中，不同的Xml映射文件，id是否可以重复？
​

不同的Xml映射文件，如果配置了namespace，那么id可以重复；如果没有配置namespace，那么id不能重复；<br />​

原因就是namespace+id是作为Map<String, MapperStatement>的key使用的，如果没有namespace，就剩下id，那么，id重复会导致数据互相覆盖。有了namespace，自然id就可以重复，namespace不同，namespace+id自然也就不同。<br />​

备注：在旧版本的Mybatis中，namespace是可选的，不过新版本的namespace已经是必须的了。<br />​

 <br />​<br />
<a name="cgUN2"></a>
# 6、Mybatis是如何进行分页的？分页插件的原理是什么？
​

        Mybatis使用RowBounds对象进行分页，它是针对ResultSet结果集执行的内存分页，而非物理分页。可以在sql内直接书写带有物理分页的参数来完成物理分页功能，也可以使用分页插件来完成物理分页。<br />​

       分页插件的基本原理是使用Mybatis提供的插件接口，实现自定义插件，在插件的拦截方法内拦截待执行的sql，然后重写sql，根据dialect方言，添加对应的物理分页语句和物理分页参数。<br />​

 <br />​<br />
<a name="Tk4HV"></a>
# 7、简述Mybatis的插件运行原理，以及如何编写一个插件。
​

答：Mybatis仅可以编写针对ParameterHandler、ResultSetHandler、StatementHandler、Executor这4种接口的插件，Mybatis使用JDK的动态代理，为需要拦截的接口生成代理对象以实现接口方法拦截功能，每当执行这4种接口对象的方法时，就会进入拦截方法，具体就是InvocationHandler的invoke()方法，当然，只会拦截那些你指定需要拦截的方法。<br />​

编写插件：实现Mybatis的Interceptor接口并复写intercept()方法，然后再给插件编写注解，指定要拦截哪一个接口的哪些方法即可，最后在配置文件中配置你编写的插件。<br />​

 <br />​<br />
<a name="NRQTF"></a>
# 8、Mybatis是否支持延迟加载？如果支持，它的实现原理是什么？
​

Mybatis仅支持association关联对象和collection关联集合对象的延迟加载，association指的就是一对一，collection指的就是一对多查询。在Mybatis配置文件中，可以配置是否启用延迟加载lazyLoadingEnabled=true|false。<br />​

延迟加载的基本原理是，使用CGLIB创建目标对象的代理对象，当调用目标方法时，进入拦截器方法，比如调用a.getB().getName()，拦截器invoke()方法发现a.getB()是null值，那么就会单独发送事先保存好的查询关联B对象的sql，把B查询上来，然后调用a.setB(b)，于是a的对象b属性就有值了，接着完成a.getB().getName()方法的调用。<br />​

当然了，不光是Mybatis，几乎所有的包括Hibernate，支持延迟加载的原理都是一样的。<br />​

 <br />​<br />
<a name="K7I6A"></a>
#  9、Mybatis的一级、二级缓存:
​

（1）一级缓存: 基于 PerpetualCache 的 HashMap 本地缓存，其存储作用域为 Session，当 Session flush 或 close 之后，该 Session 中的所有 Cache 就将清空，默认打开一级缓存。<br />​

（2）二级缓存与一级缓存其机制相同，默认也是采用 PerpetualCache，HashMap 存储，不同在于其存储作用域为 Mapper(Namespace)，并且可自定义存储源，如 Ehcache。默认不打开二级缓存，要开启二级缓存，使用二级缓存属性类需要实现Serializable序列化接口(可用来保存对象的状态),可在它的映射文件中配置<cache/> ；<br />​

（3）对于缓存数据更新机制，当某一个作用域(一级缓存 Session/二级缓存Namespaces)的进行了C/U/D 操作后，默认该作用域下所有 select 中的缓存将被 clear 掉并重新更新，如果开启了二级缓存，则只根据配置判断是否刷新。<br />​

 <br />​<br />
<a name="d1x5p"></a>
# 10、Mybatis是如何将sql执行结果封装为目标对象并返回的？都有哪些映射形式？
​

第一种是使用<resultMap>标签，逐一定义数据库列名和对象属性名之间的映射关系。<br />​

第二种是使用sql列的别名功能，将列的别名书写为对象属性名。<br />​

有了列名与属性名的映射关系后，Mybatis通过反射创建对象，同时使用反射给对象的属性逐一赋值并返回，那些找不到映射关系的属性，是无法完成赋值的。<br />​

 <br />​<br />
<a name="cw24o"></a>
# 11、Mybatis动态sql有什么用？执行原理？有哪些动态sql？
​

Mybatis动态sql可以在Xml映射文件内，以标签的形式编写动态sql，执行原理是根据表达式的值 完成逻辑判断 并动态拼接sql的功能。<br />​

Mybatis提供了9种动态sql标签：trim | where | set | foreach | if | choose | when | otherwise | bind。<br />​

 <br />​<br />
<a name="oYuZZ"></a>
# 12、Xml映射文件中，除了常见的select|insert|updae|delete标签之外，还有哪些标签？
​

<resultMap>、<parameterMap>、<sql>、<include>、<selectKey>，加上动态sql的9个标签，其中<sql>为sql片段标签，通过<include>标签引入sql片段，<selectKey>为不支持自增的主键生成策略标签。<br />​

 <br />​<br />
<a name="Bn8m4"></a>
# 13、使用MyBatis的mapper接口调用时有哪些要求？
​

 Mapper接口方法名和mapper.xml中定义的每个sql的id相同；<br /> Mapper接口方法的输入参数类型和mapper.xml中定义的每个sql 的parameterType的类型相同；<br /> Mapper接口方法的输出参数类型和mapper.xml中定义的每个sql的resultType的类型相同；<br /> Mapper.xml文件中的namespace即是mapper接口的类路径。<br /> <br />​<br />
<a name="nWddi"></a>
# 14、 模糊查询like语句该怎么写?
​

第1种：在Java代码中添加sql通配符。<br />​

    string wildcardname = “%smi%”;<br />    list<name> names = mapper.selectlike(wildcardname);<br /> <br />    <select id=”selectlike”><br />     select * from foo where bar like #{value}<br />    </select><br />第2种：在sql语句中拼接通配符，会引起sql注入<br />​

    string wildcardname = “smi”;<br />    list<name> names = mapper.selectlike(wildcardname);<br /> <br />    <select id=”selectlike”><br />         select * from foo where bar like "%"${value}"%"<br />    </select><br /> <br />​<br />
<a name="KxfBe"></a>
# 15、当实体类中的属性名和表中的字段名不一样 ，怎么办 ？
​

第1种： 通过在查询的sql语句中定义字段名的别名，让字段名的别名和实体类的属性名一致。<br />​

    <select id=”selectorder” parametertype=”int” resultetype=”me.gacl.domain.order”><br />       select order_id id, order_no orderno ,order_price price form orders where order_id=#{id};<br />    </select><br />第2种： 通过<resultMap>来映射字段名和实体类属性名的一一对应的关系。<br />​

 <select id="getOrder" parameterType="int" resultMap="orderresultmap"><br />        select * from orders where order_id=#{id}<br />    </select><br /> <br />   <resultMap type=”me.gacl.domain.order” id=”orderresultmap”><br />        <!–用id属性来映射主键字段–><br />        <id property=”id” column=”order_id”><br /> <br />        <!–用result属性来映射非主键字段，property为实体类属性名，column为数据表中的属性–><br />        <result property = “orderno” column =”order_no”/><br />        <result property=”price” column=”order_price” /><br />    </reslutMap><br /> <br />​<br />
<a name="CrMDj"></a>
# 16、如何获取自动生成的(主)键值?
​

insert 方法总是返回一个int值 ，这个值代表的是插入的行数。<br />​

如果采用自增长策略，自动生成的键值在 insert 方法执行完后可以被设置到传入的参数对象中。<br />​

<insert id=”insertname” usegeneratedkeys=”true” keyproperty=”id”><br />     insert into names (name) values (#{name})<br /></insert><br />    name name = new name();<br />    name.setname(“fred”);<br /> <br />    int rows = mapper.insertname(name);<br />    // 完成后,id已经被设置到对象中<br />    system.out.println(“rows inserted = ” + rows);<br />    system.out.println(“generated key value = ” + name.getid());<br /> <br />​<br />
<a name="iUDjc"></a>
# 17、在mapper中如何传递多个参数?
​

（1）第一种：<br />//DAO层的函数<br />Public UserselectUser(String name,String area);  <br />//对应的xml,#{0}代表接收的是dao层中的第一个参数，#{1}代表dao层中第二参数，更多参数一致往后加即可。<br /><select id="selectUser"resultMap="BaseResultMap">  <br />    select *  fromuser_user_t   whereuser_name = #{0} anduser_area=#{1}  <br /></select>  <br /> <br />（2）第二种： 使用 @param 注解:<br />public interface usermapper {<br />   user selectuser(@param(“username”) string username,@param(“hashedpassword”) string hashedpassword);<br />}<br />然后,就可以在xml像下面这样使用(推荐封装为一个map,作为单个参数传递给mapper):<br /><select id=”selectuser” resulttype=”user”><br />         select id, username, hashedpassword<br />         from some_table<br />         where username = #{username}<br />         and hashedpassword = #{hashedpassword}<br /></select><br /> <br />（3）第三种：多个参数封装成map<br />try{<br />//映射文件的命名空间.SQL片段的ID，就可以调用对应的映射文件中的SQL<br />//由于我们的参数超过了两个，而方法中只有一个Object参数收集，因此我们使用Map集合来装载我们的参数<br />Map<String, Object> map = new HashMap();<br />     map.put("start", start);<br />     map.put("end", end);<br />     return sqlSession.selectList("StudentID.pagination", map);<br /> }catch(Exception e){<br />     e.printStackTrace();<br />     sqlSession.rollback();<br />    throw e; }<br />finally{<br /> MybatisUtil.closeSqlSession();<br /> }<br /> <br />​<br />
<a name="S9t72"></a>
# 18、 一对一、一对多的关联查询 ？ 
​

<mapper namespace="com.lcb.mapping.userMapper">  <br />    <!--association  一对一关联查询 -->  <br />    <select id="getClass" parameterType="int" resultMap="ClassesResultMap">  <br />        select * from class c,teacher t where c.teacher_id=t.t_id and c.c_id=#{id}  <br />    </select>  <br /> <br />    <resultMap type="com.lcb.user.Classes" id="ClassesResultMap">  <br />        <!-- 实体类的字段名和数据表的字段名映射 -->  <br />        <id property="id" column="c_id"/>  <br />        <result property="name" column="c_name"/>  <br />        <association property="teacher" javaType="com.lcb.user.Teacher">  <br />            <id property="id" column="t_id"/>  <br />            <result property="name" column="t_name"/>  <br />        </association>  <br />    </resultMap>  <br /> <br /> <br />    <!--collection  一对多关联查询 -->  <br />    <select id="getClass2" parameterType="int" resultMap="ClassesResultMap2">  <br />        select * from class c,teacher t,student s where c.teacher_id=t.t_id and c.c_id=s.class_id and c.c_id=#{id}  <br />    </select>  <br /> <br />    <resultMap type="com.lcb.user.Classes" id="ClassesResultMap2">  <br />        <id property="id" column="c_id"/>  <br />        <result property="name" column="c_name"/>  <br />        <association property="teacher" javaType="com.lcb.user.Teacher">  <br />            <id property="id" column="t_id"/>  <br />            <result property="name" column="t_name"/>  <br />        </association>  <br /> <br />        <collection property="student" ofType="com.lcb.user.Student">  <br />            <id property="id" column="s_id"/>  <br />            <result property="name" column="s_name"/>  <br />        </collection>  <br />    </resultMap>  <br /></mapper> <br /> <br />​<br />
<a name="EXj64"></a>
# 19、MyBatis实现一对一有几种方式?具体怎么操作的？
​

有联合查询和嵌套查询,联合查询是几个表联合查询,只查询一次, 通过在resultMap里面配置association节点配置一对一的类就可以完成；<br />​

嵌套查询是先查一个表，根据这个表里面的结果的 外键id，去再另外一个表里面查询数据,也是通过association配置，但另外一个表的查询通过select属性配置。<br />​

 <br />​<br />
<a name="TZliI"></a>
# 20、MyBatis实现一对多有几种方式,怎么操作的？
​

        有联合查询和嵌套查询。联合查询是几个表联合查询,只查询一次,通过在resultMap里面的collection节点配置一对多的类就可以完成；嵌套查询是先查一个表,根据这个表里面的 结果的外键id,去再另外一个表里面查询数据,也是通过配置collection,但另外一个表的查询通过select节点配置。<br />​

 <br />​<br />
<a name="NE3dT"></a>
# 21、Mapper编写有哪几种方式？
​

第一种：接口实现类继承SqlSessionDaoSupport：使用此种方法需要编写mapper接口，mapper接口实现类、mapper.xml文件。<br />​

（1）在sqlMapConfig.xml中配置mapper.xml的位置<br /><mappers><br />    <mapper resource="mapper.xml文件的地址" /><br />    <mapper resource="mapper.xml文件的地址" /><br /></mappers><br />（2）定义mapper接口<br />（3）实现类集成SqlSessionDaoSupport<br />mapper方法中可以this.getSqlSession()进行数据增删改查。<br />（4）spring 配置<br /><bean id=" " class="mapper接口的实现"><br />    <property name="sqlSessionFactory" ref="sqlSessionFactory"></property><br /></bean> <br />​

 第二种：使用org.mybatis.spring.mapper.MapperFactoryBean：<br />​

（1）在sqlMapConfig.xml中配置mapper.xml的位置，如果mapper.xml和mappre接口的名称相同且在同一个目录，这里可以不用配置<br /><mappers><br />    <mapper resource="mapper.xml文件的地址" /><br />    <mapper resource="mapper.xml文件的地址" /><br /></mappers><br />（2）定义mapper接口：<br />①mapper.xml中的namespace为mapper接口的地址<br />②mapper接口中的方法名和mapper.xml中的定义的statement的id保持一致<br />③Spring中定义<br /><bean id="" class="org.mybatis.spring.mapper.MapperFactoryBean"><br />    <property name="mapperInterface"   value="mapper接口地址" /> <br />    <property name="sqlSessionFactory" ref="sqlSessionFactory" /> <br /></bean><br />​

第三种：使用mapper扫描器：<br />​

（1）mapper.xml文件编写：<br />mapper.xml中的namespace为mapper接口的地址；<br />mapper接口中的方法名和mapper.xml中的定义的statement的id保持一致；<br />如果将mapper.xml和mapper接口的名称保持一致则不用在sqlMapConfig.xml中进行配置。 <br />（2）定义mapper接口：<br />注意mapper.xml的文件名和mapper的接口名称保持一致，且放在同一个目录<br />（3）配置mapper扫描器：<br /><bean class="org.mybatis.spring.mapper.MapperScannerConfigurer"><br />    <property name="basePackage" value="mapper接口包地址"></property><br />    <property name="sqlSessionFactoryBeanName" value="sqlSessionFactory"/> <br /></bean><br />（4）使用扫描器后从spring容器中获取mapper的实现对象。<br />​

 <br />​<br />
<a name="dgLmo"></a>
# 22、什么是MyBatis的接口绑定？有哪些实现方式？
​

接口绑定，就是在MyBatis中任意定义接口,然后把接口里面的方法和SQL语句绑定, 我们直接调用接口方法就可以,这样比起原来了SqlSession提供的方法我们可以有更加灵活的选择和设置。<br />​

接口绑定有两种实现方式,一种是通过注解绑定，就是在接口的方法上面加上 @Select、@Update等注解，里面包含Sql语句来绑定；另外一种就是通过xml里面写SQL来绑定, 在这种情况下,要指定xml映射文件里面的namespace必须为接口的全路径名。当Sql语句比较简单时候,用注解绑定, 当SQL语句比较复杂时候,用xml绑定,一般用xml绑定的比较多。<br />​

 <br />​<br />
<a name="xVtcF"></a>
# 23、MyBatis与Hibernate有哪些不同？
​

（1）Mybatis和hibernate不同，它不完全是一个ORM框架，因为MyBatis需要程序员自己编写Sql语句。<br />​

（2）Mybatis直接编写原生态sql，可以严格控制sql执行性能，灵活度高，非常适合对关系数据模型要求不高的软件开发，因为这类软件需求变化频繁，一但需求变化要求迅速输出成果。但是灵活的前提是mybatis无法做到数据库无关性，如果需要实现支持多种数据库的软件，则需要自定义多套sql映射文件，工作量大。 <br />​

（3）Hibernate对象/关系映射能力强，数据库无关性好，对于关系模型要求高的软件，如果用hibernate开发可以节省很多代码，提高效率。
