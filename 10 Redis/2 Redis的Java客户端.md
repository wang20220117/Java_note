 ![image-20241126214830252](D:\md_image\image-20241126214830252.png)

![image-20241126214950402](D:\md_image\image-20241126214950402.png)

​																																																				

# Jedis

![image-20241127103617272](D:\md_image\image-20241127103617272.png)

 ![image-20241127103631290](D:\md_image\image-20241127103631290.png)

# Jedis的连接池

![image-20241127103745962](D:\md_image\image-20241127103745962.png)



# SpringDataRedis

![image-20241127105803425](D:\md_image\image-20241127105803425.png)

把不同数据类型封装到了对象中：

![image-20241127110130557](D:\md_image\image-20241127110130557.png)



![image-20241127111924276](D:\md_image\image-20241127111924276.png)

```yaml
# yml文件中配置Redis信息
spring:
  data:
    redis:
      host: 192.168.169.129
      port: 6379
      password: 123456
      lettuce:
        pool:
          max-active: 8
          max-idle: 8
          min-idle: 0
          max-wait: 1000ms
```



```java
@SpringBootTest
class SpringdataredisDemoApplicationTests {
	
    //注入RedisTemplate
    @Autowired
    private RedisTemplate redisTemplate;

    @Test
    void testString() {
        //传object也可以接受，因为底层有个自动的序列化机制，将object序列化为字符串
        redisTemplate.opsForValue().set("name", "wck");
        //获取
        Object name = redisTemplate.opsForValue().get("name");
        System.out.println(name);
    }

}
```

![image-20241127112419319](D:\md_image\image-20241127112419319.png)

打印：![image-20241127112440688](D:\md_image\image-20241127112440688.png)



## 序列化问题

![image-20241127141331730](D:\md_image\image-20241127141331730.png)

![image-20241127142053179](D:\md_image\image-20241127142053179.png)

写一个配置类：

```java
@Configuration
public class RedisConfig {

    @Bean
    public RedisTemplate<String, Object> redisTemplate(RedisConnectionFactory factory) {
        //创建redisTemplate对象
        RedisTemplate<String, Object> template = new RedisTemplate<>();

        //设置连接工厂
        template.setConnectionFactory(factory);

        //创建Json序列化工具
        GenericJackson2JsonRedisSerializer jsonRedisSerializer = new GenericJackson2JsonRedisSerializer();

        //设置Key的序列化
        template.setKeySerializer(RedisSerializer.string());
        template.setHashKeySerializer(RedisSerializer.string());

        //设置Value的序列化
        template.setValueSerializer(jsonRedisSerializer);
        template.setHashValueSerializer(jsonRedisSerializer);

        //返回
        return template;
    }
}
```



## StringRedisTemplate

![image-20241127145648638](D:\md_image\image-20241127145648638.png)

![image-20241127145822780](D:\md_image\image-20241127145822780.png)



![image-20241127150205206](D:\md_image\image-20241127150205206.png)

![image-20241127151826605](D:\md_image\image-20241127151826605.png)