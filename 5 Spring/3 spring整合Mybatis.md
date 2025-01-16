Spring提供了`SqlSessionFactoryBean，MapperScannerConfigure` 来整合Mybatis

1. Domain层

**Domain** 层，也称为 **Model** 层或 **实体层**，用于表示业务对象（实体），通常是 POJO（Plain Old Java Object），封装业务数据和领域逻辑。在面向对象设计中，Domain 对象是业务逻辑的核心和基础，通常映射到数据库中的表。



2. Dao层

**DAO** 层，即数据访问层，用于提供访问数据库的**接口**，将数据存储和读取的具体逻辑与业务逻辑分离。DAO 层封装了所有与数据库的交互操作，如增删改查操作，通过使用接口和实现类，使数据访问逻辑模块化。



3.Service层

**Service** 层，用于处理业务逻辑，它**与 DAO 层交互**，调用 DAO 方法来获取或保存数据，同时处理业务规则，确保数据的有效性、完整性和安全性。Service 层将复杂的业务逻辑集中在一处，使控制层无需直接操作数据库，保持代码的可维护性。

![image-20241029172712643](D:\md_image\image-20241029172712643.png)

![image-20241030103803632](D:\md_image\image-20241030103803632.png)

![image-20241121202446237](D:\md_image\image-20241121202446237.png)

> 在 MyBatis 的配置类 `MyBatisConfig` 中定义映射配置（mapping configuration）的主要作用是对 **数据库表与 Java 实体类之间的映射关系** 进行配置和管理。这些映射配置使得开发者可以通过 MyBatis 框架高效地完成数据库操作，而无需手写大量的 SQL 语句。



# spring整合Junit

 ![image-20241030105047030](D:\md_image\image-20241030105047030.png)

![image-20241030105109605](D:\md_image\image-20241030105109605.png)

1. 设定专用的类运行器
2. 指定spring上下文的配置类