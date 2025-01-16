![image-20241126131932589](.assets/image-20241126131932589.png)

 ![image-20241126132100309](.assets/image-20241126132100309.png)

上面五种类型是基本类型，下面三种是特殊类型。

这些数据类型怎么用？什么时候用？

官网上的命令按数据结构做了分组：[Commands | Docs](https://redis.io/docs/latest/commands/)



# 通用命令

* KEYS ： 查看符合模板的所有key，这种模糊匹配速度慢，会产生阻塞，**不建议在生产环境设备上使用**。
* DEL key [key ...]：删除一个key或多个key
* EXISTS key： 判断key是否存在。
* EXPIRE key seconds： 给key设置一个有效期，有效期到期时该key会被自动删除。
* TTL ：查看一个key的剩余有效期。

通过help [command]可以查看一个命令的具体用法。



# String类型

 ![image-20241126134901390](.assets/image-20241126134901390.png)

 ![image-20250116222245298](.assets/image-20250116222245298.png)

 ![image-20241126135716511](.assets/image-20241126135716511.png)



# key的层级结构

 ![image-20241126172227908](.assets/image-20241126172227908.png)

![image-20241126173001370](.assets/image-20241126173001370.png)



# Hash类型

![image-20241126205205738](.assets/image-20241126205205738.png)

 Hash类型相比json字符串，可以对单个值进行修改。



![image-20241126210616825](.assets/image-20241126210616825.png)

* HSET  

 ![image-20241126205708084](.assets/image-20241126205708084.png)

 ![image-20241126205725932](.assets/image-20241126205725932.png)

 允许对单个键值进行修改：![image-20241126205944652](.assets/image-20241126205944652.png)



* HGETALL ：获取一个键中的所有field和value。

   ![image-20241126210244837](.assets/image-20241126210244837.png)

* HKEYS和HVALS

​	 ![image-20241126210442159](.assets/image-20241126210442159.png)

 ![image-20241126210559388](D:\md_image\image-20241126210559388.png)



# List类型

 ![image-20241126210807303](1%20Redis%E5%B8%B8%E8%A7%81%E5%91%BD%E4%BB%A4.assets/image-20241126210807303.png)

 ![image-20241126210821164](1%20Redis%E5%B8%B8%E8%A7%81%E5%91%BD%E4%BB%A4.assets/image-20241126210821164.png)

 ![image-20241126211359415](.assets/image-20241126211359415.png)

BLPOP和BRPOP阻塞式获取value。

 ![image-20241126211606997](.assets/image-20241126211606997.png)



# Set类型

 ![image-20241126211742056](.assets/image-20241126211742056.png)

 ![image-20241126212326082](.assets/image-20241126212326082.png)

 单个集合的运算：

 ![image-20241126212123229](.assets/image-20241126212123229.png)

两个集合的运算：

 ![image-20241126212640572](.assets/image-20241126212640572.png)



# SortedSet类型

 ![image-20241126213035776](.assets/image-20241126213035776.png)

 ![image-20241126213050470](.assets/image-20241126213050470.png)

注意，所有的排名均是升序，如果要降序则在命令的Z后面添加REV即可。

 ![image-20241126213917873](.assets/image-20241126213917873.png)



已学习的五种数据类型：

* String
* Hash
* List
* Set
* SortedSet