# Spring

### 1.1 ioc��Spring�е�ʵ��

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

#### ����һ��test��������һ�°ɣ�
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
### 1.2 ͨ��DI����ֵ
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
#### Ϊ�����͵����Ը�ֵ
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

### 1.3 factory bean
![img_9.png](img_9.png)
![img_10.png](img_10.png)
����Ҫ����User��ֱ����xml��������beanfactory��ͨ��beanfactory��get object����Ҳ���Եõ�User

### 1.4 �Զ�װ��
�����Զ�װ�䣬�Ͳ���Ҫ������һ���ҵ���Ӧ��bean��id��Ϊ�����͵����Ը�ֵ��
�����ʹ���Զ�װ��
```xml
<bean id="userService" class="offer.userService">
    <property name="userDao" ref="userDao"></property>
</bean>
<bean id="userDao" class="offer.userDao"></bean>
```
_ͨ��xmlʵ���Զ�װ��_
1. byType
```xml
<bean id="userService" class="offer.userService" autowire="byType">
    <property name="userDao" ref="userDao"></property>
</bean>
<bean id="userDao" class="offer.userDao" autowire="byType"></bean>
```
_����ע��������bean_

1.���ע��
```java
@Compontent
@Controller
@Service
@Repository
```
2.ɨ��
```xml
<context:component-scan base-package="offer"> 
</context:component-scan>
```

3.������xml������ʹ��@Autowired
```java
//ֱ�Ӱ����ӵ���Ա�����ϼ���
@Controller
public class UserController{ 
    @Autowired
    private UserService userService;
    public void saveUser(){
        userService.saveUser();
    }
}
```

### 2.1 aop�������
1.���й�ע�㣺���Ǻ���ҵ����룬��������������е���־����
2.���棺��װ���й�ע�����
3.֪ͨ���ͺ��й�ע����һ���Ķ�������������������ͽ�֪ͨ

���ӣ�
1.����Ŀ����������ಢ�ҽ���ioc����
```java
//Ŀ����
@Component
public class CalculatorImpl implements Calculator {
    @Override
    public int add(int i, int j) {
        int result = i + j;
        System.out.println("�����ڲ���result��"+result);
        return result;
    }

    @Override
    public int sub(int i, int j) {
        int result = i - j;
        System.out.println("�����ڲ���result��"+result);
        return result;
    }

    @Override
    public int mul(int i, int j) {
        int result = i * j;
        System.out.println("�����ڲ���result��"+result);
        return result;
    }

    @Override
    public int div(int i, int j) {
        int result = i / j;
        System.out.println("�����ڲ���result��"+result);
        return result;
    }
}

//������
@Component
@Aspect //����ǰ�����ʶΪ����
public class LoggerAspect {

   @Pointcut("execution(* com.atguigu.spring.aop.annotation.CalculatorImpl.*(..))")
   public void pointCut() {
   }

   //@Before("execution(public int com.atguigu.spring.aop.annotation.CalculatorImpl.add(int, int))")
   //@Before("execution(* com.atguigu.spring.aop.annotation.CalculatorImpl.*(..))")
   @Before("pointCut()")
   public void beforeAdviceMethod(JoinPoint joinPoint) {
      //��ȡ���ӵ�����Ӧ������ǩ����Ϣ
      Signature signature = joinPoint.getSignature();
      //��ȡ���ӵ�����Ӧ�����Ĳ���
      Object[] args = joinPoint.getArgs();
      System.out.println("LoggerAspect��������" + signature.getName() + "��������" + Arrays.toString(args));
   }

   @After("pointCut()")
   public void afterAdviceMethod(JoinPoint joinPoint) {
      //��ȡ���ӵ�����Ӧ������ǩ����Ϣ
      Signature signature = joinPoint.getSignature();
      System.out.println("LoggerAspect��������" + signature.getName() + "��ִ�����");
   }

   /**
    * �ڷ���֪ͨ����Ҫ��ȡĿ����󷽷��ķ���ֵ
    * ֻ��Ҫͨ��@AfterReturningע���returning����
    * �Ϳ��Խ�֪ͨ������ĳ������ָ��Ϊ����Ŀ����󷽷��ķ���ֵ�Ĳ���
    */
   @AfterReturning(value = "pointCut()", returning = "result")
   public void afterReturningAdviceMethod(JoinPoint joinPoint, Object result) {
      //��ȡ���ӵ�����Ӧ������ǩ����Ϣ
      Signature signature = joinPoint.getSignature();
      System.out.println("LoggerAspect��������" + signature.getName() + "�������" + result);
   }

   /**
    * ���쳣֪ͨ����Ҫ��ȡĿ����󷽷����쳣
    * ֻ��Ҫͨ��AfterThrowingע���throwing����
    * �Ϳ��Խ�֪ͨ������ĳ������ָ��Ϊ����Ŀ����󷽷����ֵ��쳣�Ĳ���
    */
   @AfterThrowing(value = "pointCut()", throwing = "ex")
   public void afterThrowingAdviceMethod(JoinPoint joinPoint, Throwable ex) {
      //��ȡ���ӵ�����Ӧ������ǩ����Ϣ
      Signature signature = joinPoint.getSignature();
      System.out.println("LoggerAspect��������" + signature.getName() + "���쳣��" + ex);
   }

   @Around("pointCut()")
   //����֪ͨ�ķ����ķ���ֵһ��Ҫ��Ŀ����󷽷��ķ���ֵһ��
   public Object aroundAdviceMethod(ProceedingJoinPoint joinPoint) {
      Object result = null;
      try {
         System.out.println("����֪ͨ-->ǰ��֪ͨ");
         //��ʾĿ����󷽷���ִ��
         result = joinPoint.proceed();
         System.out.println("����֪ͨ-->����֪ͨ");
      } catch (Throwable throwable) {
         throwable.printStackTrace();
         System.out.println("����֪ͨ-->�쳣֪ͨ");
      } finally {
         System.out.println("����֪ͨ-->����֪ͨ");
      }
      return result;
   }
}
```
