#**Spring**

###**1.1 ioc在Spring中的实现**

![img_1.png](png/img_1.png)
使用的API是ApplicationContext

![img_2.png](png/img_2.png)
ClassPathXml是使用类路径下的xml文件来进行ioc容器的获取，上面的FileSystemXml是通过在磁盘的位置来访问的，但是我们的项目以后要供不同的人来使用，他们可能会把文件放在不同的位置，因此这种方法没有普遍性



1.引入dependencies
```xml
    <dependencies>
        <!-- 基于Maven依赖传递性，导入spring-context依赖即可导入当前所需所有jar包 -->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-context</artifactId>
            <version>5.3.1</version>
        </dependency>
        <!-- junit测试 -->
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
            <scope>test</scope>
        </dependency>
    </dependencies>
```

2.创建配置文件applicationContext![img_2.png](img_2.png)
现在就可以开始配置bean的属性了：
id是唯一标识，不能重复，想要管理一个特定的bean的时候，只需要告诉spring它的id就好了
class就是平时写java的时候的那个class，也叫类
```xml
<bean id="helloworld" class="com.atguigu.spring.pojo.HelloWorld"></bean>
```
这行就表示我把pojo包下面的Helloworld.class交给了spring管理，并且给这个文件起了个id叫Helloworld（注意：起什么id都可以，只不过这个比较适合）

####创建一个test类来测试一下吧！
```java
public class test{
    @Test
    public void test(){
        //获取ioc容器
        ApplicationContext ioc = new ClassPathXmlApplicationContext("applicationContext.xml");
        //获取bean对象，这个方法我用的是byname，也就是bean的id，也正是因为用的id，所以不知道bean的类型，因此需要强转
        HelloWorld HehlloWorld = (HelloWorld)ioc.getBean("helloworld");
        HehlloWorld.sayHello();
    }
}
```
###**1.2 通过DI来赋值**
为成员变量赋值有两种方法，一是set方法，另一个是有参构造，在spring里面也一样
```xml
<!--方法一-->
<bean id="student" class="pojo.student">
   <property name="name" value="Shiwen"></property>
</bean>
<!--方法二-->
<bean id="student" class="pojo.student">
    <constructuor-arg value="Shiwen"></constructuor-arg>
</bean>
```
####**为类类型的属性赋值**
因为class不可以像成员变量一样直接赋值（不可以用value了），两种解决办法
1. 外部bean先设置好value，再用ref来引用这个bean
```xml
<bean id="student" class="pojo.student">
   <property name="class" ref="'classone"></property>
</bean>

<bean id="class" class="pojo.class">
    <property name="amount" value="60"></property>
</bean>
```
2. 也可以通过内部bean来赋值，注意内部bean只能在bean的内部使用，无法通过ioc容器来获取
```xml
<bean id="student" class="pojo.student">
   <property name="class">
      <bean id="class" class="pojo.class">
         <property name="amount" value="60"></property>
      </bean>
   </property>
</bean>
```
这个是报的错误
![img_8.png](img_8.png)

###**1.3 factory bean**
![img_9.png](img_9.png)
![img_10.png](img_10.png)
不需要配置User，直接在xml里面配置beanfactory，通过beanfactory的get object方法也可以得到User

**自动装配**
有了自动装配，就不需要像上文一样找到对应的bean的id来为类类型的属性赋值了
如果不使用自动装配
![img_11.png](img_11.png)
_通过xml实现自动装配_
1. byType
![img_12.png](img_12.png)
_基于注解来管理bean_
![img_13.png](img_13.png)    
   ![img_14.png](img_14.png)
   配置注解并扫描

