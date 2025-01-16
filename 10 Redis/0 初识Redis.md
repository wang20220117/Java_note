![image-20241125170701818](D:\md_image\image-20241125170701818.png)

NoSQL：非关系型数据库

![image-20241126105543205](D:\md_image\image-20241126105543205.png)

![image-20241126105716413](D:\md_image\image-20241126105716413.png)

![image-20241126110130761](D:\md_image\image-20241126110130761.png)

 ![image-20241126110647150](D:\md_image\image-20241126110647150.png)



# 命令行客户端

Redis安装完成后就自带了命令行客户端：redis-cli，使用方式如下：

```sh
redis-cli [options] [commonds]

redis-cli -h 192.168.169.129  //本机ip
```

其中常见的options有：

- `-h 127.0.0.1`：指定aut要连接的redis节点的IP地址，默认是127.0.0.1
- `-p 6379`：指定要连接的redis节点的端口，默认是6379
- `-a 123321`：指定redis的访问密码 

其中的commonds就是Redis的操作命令，例如：

- `ping`：与redis服务端做心跳测试，服务端正常会返回`pong`

![image-20241207181309320](D:\md_image\image-20241207181309320.png)