#**Spring**

###**1.1 ioc��Spring�е�ʵ��**

![img_1.png](png/img_1.png)
ʹ�õ�API��ApplicationContext

![img_2.png](png/img_2.png)
ClassPathXml��ʹ����·���µ�xml�ļ�������ioc�����Ļ�ȡ�������FileSystemXml��ͨ���ڴ��̵�λ�������ʵģ��������ǵ���Ŀ�Ժ�Ҫ����ͬ������ʹ�ã����ǿ��ܻ���ļ����ڲ�ͬ��λ�ã�������ַ���û���ձ���



1.����dependencies
```xml
    <dependencies>
        <!-- ����Maven���������ԣ�����spring-context�������ɵ��뵱ǰ��������jar�� -->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-context</artifactId>
            <version>5.3.1</version>
        </dependency>
        <!-- junit���� -->
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
            <scope>test</scope>
        </dependency>
    </dependencies>
```

2.���������ļ�applicationContext![img_2.png](img_2.png)
���ھͿ��Կ�ʼ����bean�������ˣ�
id��Ψһ��ʶ�������ظ�����Ҫ����һ���ض���bean��ʱ��ֻ��Ҫ����spring����id�ͺ���
class����ƽʱдjava��ʱ����Ǹ�class��Ҳ����
```xml
<bean id="helloworld" class="com.atguigu.spring.pojo.HelloWorld"></bean>
```
���оͱ�ʾ�Ұ�pojo�������Helloworld.class������spring�������Ҹ�����ļ����˸�id��Helloworld��ע�⣺��ʲôid�����ԣ�ֻ��������Ƚ��ʺϣ�

####����һ��test��������һ�°ɣ�
```java
public class test{
    @Test
    public void test(){
        //��ȡioc����
        ApplicationContext ioc = new ClassPathXmlApplicationContext("applicationContext.xml");
        //��ȡbean��������������õ���byname��Ҳ����bean��id��Ҳ������Ϊ�õ�id�����Բ�֪��bean�����ͣ������Ҫǿת
        HelloWorld HehlloWorld = (HelloWorld)ioc.getBean("helloworld");
        HehlloWorld.sayHello();
    }
}
```
###**1.2 ͨ��DI����ֵ**
Ϊ��Ա������ֵ�����ַ�����һ��set��������һ�����вι��죬��spring����Ҳһ��
```xml
<!--����һ-->
<bean id="student" class="pojo.student">
   <property name="name" value="Shiwen"></property>
</bean>
<!--������-->
<bean id="student" class="pojo.student">
    <constructuor-arg value="Shiwen"></constructuor-arg>
</bean>
```
####**Ϊ�����͵����Ը�ֵ**
��Ϊclass���������Ա����һ��ֱ�Ӹ�ֵ����������value�ˣ������ֽ���취
1. �ⲿbean�����ú�value������ref���������bean
```xml
<bean id="student" class="pojo.student">
   <property name="class" ref="'classone"></property>
</bean>

<bean id="class" class="pojo.class">
    <property name="amount" value="60"></property>
</bean>
```
2. Ҳ����ͨ���ڲ�bean����ֵ��ע���ڲ�beanֻ����bean���ڲ�ʹ�ã��޷�ͨ��ioc��������ȡ
```xml
<bean id="student" class="pojo.student">
   <property name="class">
      <bean id="class" class="pojo.class">
         <property name="amount" value="60"></property>
      </bean>
   </property>
</bean>
```
����Ǳ��Ĵ���
![img_8.png](img_8.png)

###**1.3 factory bean**
![img_9.png](img_9.png)
![img_10.png](img_10.png)
����Ҫ����User��ֱ����xml��������beanfactory��ͨ��beanfactory��get object����Ҳ���Եõ�User

**�Զ�װ��**
�����Զ�װ�䣬�Ͳ���Ҫ������һ���ҵ���Ӧ��bean��id��Ϊ�����͵����Ը�ֵ��
�����ʹ���Զ�װ��
![img_11.png](img_11.png)
_ͨ��xmlʵ���Զ�װ��_
1. byType
![img_12.png](img_12.png)
_����ע��������bean_
![img_13.png](img_13.png)    
   ![img_14.png](img_14.png)
   ����ע�Ⲣɨ��

