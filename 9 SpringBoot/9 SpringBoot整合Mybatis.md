 ![image-20241121202135872](D:\md_image\image-20241121202135872.png)

![image-20241121202635489](D:\md_image\image-20241121202635489.png)



跟spring整合mybatis有两点变化：

* jdbc.properties 配置文件换成 application.yml，配置数据源信息写在yml文件中。
* 定义映射配置改为只写注解 @Mapper，记得在dao接口中加上@Mapper

