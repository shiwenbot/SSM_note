**IOC在Spring中的实现**

![img_1.png](img_1.png)
使用的API是ApplicationContext

![img_2.png](img_2.png)
使用类路径下的xml文件来进行ioc容器的获取，上面的filesystem是通过在磁盘的位置来访问的，但是我们的项目以后要供不同的人来使用，他们可能会把文件放在不同的位置，因此这种方法没有普遍性
