 ![image-20241024192411752](.assets/image-20241024192411752.png)

 ![image-20241025150247754](.assets/image-20241025150247754.png)

使用Mapper代理开发：

1. 定义与SQL映射文件同名的Mapper接口，并将该接口和SQL映射文件放置在同一目录下
2. 更改SQL映射文件的namespace属性为 Mapper接口的全限定名
3. 在Mapper接口中定义方法，方法名就是SQL映射文件中sql语句的id，返回值类型就是resultType
4. 获取Mapper接口的代理方法并调用对应方法。

```java
UserMapper userMapper = sqlSession.getMapper(UserMapper.class);
List<User> users = userMapper.selectAll();
```



![image-20241025152657032](.assets/image-20241025152657032.png)



# 实体类属性名和数据库列名不一致，mybatis不能自动封装数据

  ![image-20241028111351198](.assets/image-20241028111351198.png)

主要使用resultMap方法：

 ![image-20241028111305355](.assets/image-20241028111305355.png)

 ![image-20241028111515812](.assets/image-20241028111515812.png)



 ![image-20241028160911027](.assets/image-20241028160911027.png)

 ![image-20241028161239619](D:\md_image\image-20241028161239619.png)

 ![image-20241028161326465](.assets/image-20241028161326465.png)

# 多条件查询

 ![image-20241028172557469](.assets/image-20241028172557469.png)

# 多条件-动态条件查询

* 恒等式

 ![image-20241028200444532](.assets/image-20241028200444532.png)

* where标签

 ![image-20241028200653453](.assets/image-20241028200653453.png)



 ![image-20241028200751819](.assets/image-20241028200751819.png)

# 单条件-动态条件查询