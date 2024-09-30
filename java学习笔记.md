

# !1726058023617](assets/1726058023617.png)1.cmd中运行一个java程序

1.首先创建一个文件，后缀名改成.java，注意这里的文件名要和public claass后跟的类名保持一致，否则编译不通过

2.javac负责编译，java负责运行

3.cmd输出程序运行结果

![1712718456198](C:\Users\YWX132~1\AppData\Local\Temp\1712718456198.png)

![1726040853353](assets/1726040853353.png)

![1726109319770](assets/1726109319770.png)

SpringBoot整合myBatis

1.引入mybatis的起步依赖（操作的是mysql，就引入mysql的驱动依赖

![1726638430244](assets/1726638430244.png)

2.配置数据源信息

![1726638241163](assets/1726638241163.png)

3.编写Javabean类

![1726639396464](assets/1726639396464.png)

4.写controller

Bean扫描：

Springboot默认只能扫描启动类所在的包及其子包，因此需要@ComponentScan(basePackages = {"com.huawei.ssf.core", "com.tdtech.CMCenter"})

![1726640789919](assets/1726640789919.png)

1.成员变量和局部变量的区别：

成员变量：类中，方法外的变量

局部变量：类中，方法内的变量

![1727054637146](assets/1727054637146.png)

2.Java中一个Java文件可以定义多个class类，但只能有一个类是public修饰，而且public修饰的类名必须成为代码文件名

3.数据类型分为基本数据类型和引用数据类型：

基本数据类型：int long float boolean

引用数据类型：数组，接口，类，string

4.java访问权限问题：
![1727056859266](assets/1727056859266.png)





