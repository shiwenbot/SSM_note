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
`@Test
public void test(){
    //��ȡioc����
    ApplicationContext ioc = new ClassPathXmlApplicationContext("applicationContext.xml");
    //��ȡbean��������������õ���byname��Ҳ����bean��id��Ҳ������Ϊ�õ�id�����Բ�֪��bean�����ͣ������Ҫǿת
    HelloWorld HehlloWorld = (HelloWorld)ioc.getBean("helloworld");
    HehlloWorld.sayHello();
}`