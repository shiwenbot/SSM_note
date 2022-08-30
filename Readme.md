**IOC��Spring�е�ʵ��**

![img_1.png](png/img_1.png)
ʹ�õ�API��ApplicationContext

![img_2.png](png/img_2.png)
ʹ����·���µ�xml�ļ�������ioc�����Ļ�ȡ�������filesystem��ͨ���ڴ��̵�λ�������ʵģ��������ǵ���Ŀ�Ժ�Ҫ����ͬ������ʹ�ã����ǿ��ܻ���ļ����ڲ�ͬ��λ�ã�������ַ���û���ձ���



1.����dependencies
![img.png](img.png)

2.���������ļ�applicationContext![img_2.png](img_2.png)
���ھͿ��Կ�ʼ����bean�������ˣ�
id��Ψһ��ʶ�������ظ�����Ҫ����һ���ض���bean��ʱ��ֻ��Ҫ����spring����id�ͺ���
class����ƽʱдjava��ʱ����Ǹ�class��Ҳ����
![img_3.png](img_3.png)
���оͱ�ʾ�Ұ�pojo�������Helloworld.class������spring�������Ҹ�����ļ����˸�id��Helloworld��ע�⣺��ʲôid�����ԣ�ֻ��������Ƚ��ʺϣ�



**IOC��Spring�е�ʵ�ֵĲ���**
����һ��test��������һ�°ɣ�
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
**ͨ��DI����ֵ**

Ϊ��Ա������ֵ�����ַ�����һ��set��������һ�����вι��죬��spring����Ҳһ��
![img_4.png](img_4.png)

**Ϊ�����͵����Ը�ֵ**
1. ![img_5.png](img_5.png)
��Ϊclass��һ�����ͣ�û�취���ϸ���������ֱ����value����ֵ�����������ⲿ��bean����ֵ��Ȼ������ref������bean
2. ![img_6.png](img_6.png)
Ҳ����ͨ���ڲ�bean����ֵ��ע���ڲ�beanֻ����bean���ڲ�ʹ�ã��޷�ͨ��ioc��������ȡ
   ![img_7.png](img_7.png)
   ![img_8.png](img_8.png)

**factory bean**
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

