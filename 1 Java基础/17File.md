[TOC]



# File

File类

三个构造方法：

![image-20240621163923044](D:\md_image\image-20240621163923044.png)



```java
public class FileDemo {
    public static void main(String[] args) {

        //1 字符串路径变为File对象
        String path = "C:\\Users\\Administrator\\Desktop\\a.txt";
        File f1 = new File(path);
        System.out.println(f1);

        //2 父级路径 C:\Users\Administrator\Desktop
        // 子集路径 a.txt
        String parent = "C:\\Users\\Administrator\\Desktop";
        String child = "a.txt";
        File f2 = new File(parent, child);
        System.out.println(f2);

        //3 根据父路径文件对象和子路径名称 创建文件对象
        File f3 = new File(parent);
        File f4 = new File(f3 , child);
        System.out.println(f4);
    }
}
```



![image-20240622103612188](D:\md_image\image-20240622103612188.png)

## File中常用的成员方法

### 判断、获取

![image-20240622103810875](D:\md_image\image-20240622103810875.png)

代码示例：

```java
    public static void main(String[] args) {
        String path = "C:\\Users\\Administrator\\Desktop\\a.txt";
        File f1 = new File(path);
        System.out.println(f1.isDirectory());
        System.out.println(f1.isFile());
        System.out.println(f1.exists());
        System.out.println(f1.length());

        System.out.println(f1.getAbsolutePath());

        System.out.println(f1.getPath());

        System.out.println(f1.getName());
        System.out.println(new SimpleDateFormat().format(f1.lastModified()));

    }

结果：
false
true
true
1
C:\Users\Administrator\Desktop\a.txt
C:\Users\Administrator\Desktop\a.txt
a.txt
2024/6/22 上午10:28
```

 length 方法细节：

​		这个方法只能获取文件的大小，单位是字节

​		这个方法无法获取文件夹的大小，如果想获取文件夹的大小需要把文件夹下所有文件大小累加。

getPath 方法：

​		返回定义文件时的路径，就是在创建文件对象时，括号里的路径是什么，就返回什么。



### 创建、删除

![image-20240622105614447](D:\md_image\image-20240622105614447.png)





1. **createNewFile() 方法**

   细节1：如果当前路径表示的文件是不存在的，则创建成功，方法返回true；

   ​			  如果当前路径表示的文件存在，则创建失败，方法返回返回false。

   细节2：如果父级路径是不存在的，那么方法会有异常 IOException

   细节3：createNewFile 方法创建的一定是文件，如果路径中不包含后缀名，则创建一个没有后缀的文件。

2. **mkdir() 方法**

   只能创建单级文件夹（已存在文件夹下的一个新文件夹）

   创建失败返回false，创建成功返回true。

3. **mkdirs() 方法**

   既能创建单级文件夹也能创建多级文件夹。

4. **delete() 方法**

   delete方法默认只能删除文件和*空文件夹*，直接删除不走回收站。如果是有内容的文件夹则删除失败。





### 获取并遍历

![image-20240622142409131](D:\md_image\image-20240622142409131.png)

**重点：**

![image-20240622142345795](D:\md_image\image-20240622142345795.png)

![image-20240622143712279](D:\md_image\image-20240622143712279.png)





练习：

1. 找到磁盘中所有以mp4结尾的电影（考虑子文件夹）

```java
public class FileTest {
    public static void main(String[] args) {
        //找到电脑中所有以mp4结尾的电影 （考虑子文件夹）
        //递归
        findAVI(new File("G:\\"));

    }

    public static void findAVI(File src){
        File[] files = src.listFiles();
        if(files == null){
            return;
        }
        for(File file : files){
            if(file.isFile()){
                String fileName = file.getName();
                if(fileName.endsWith(".mp4")){
                    System.out.println(fileName);
                }

            }
            else{
                findAVI(file);
            }
        }
    }
}
```



2. 删除文件夹

```java
//删除文件夹，先删除文件夹中所有的内容再删除自己
public class FileTest2 {

    public static void main(String[] args) {

        File a = new File("G:\\aa");
        deleteFile(a);
    }

    public static void deleteFile(File src) {
        File[] files = src.listFiles();

        assert files != null;
        for (File file:files){
            if(file.isFile()) {
                file.delete();
            }
            else{
                deleteFile(file);
            }
        }
        //再删除自己
        src.delete();
    }
}
```



3. 统计文件夹大小

```java
public class FileTest3 {
    public static void main(String[] args) {
        //统计文件夹大小
        File files = new File("G:");
        System.out.println(getLen(files));
    }

    public static long getLen(File files) {
        long len = 0;
        File[] f = files.listFiles();
        if (f == null) {
            return len;
        }

        for(File file : f) {
            if(file.isFile()) {
                len += file.length();
            }
            else{
                len += getLen(file);
            }
        }
        return len;
    }
}
```



4. 统计各种文件数量

```java
public class FileTest4 {
    public static void main(String[] args) {

        File file = new File("D:\\md_image");
        HashMap<String,Integer> hm = getCount(file);

        hm.forEach((k,v)->{
            System.out.println(k+"\t"+v);
        });

    }

    public static HashMap<String,Integer> getCount(File src){

        HashMap<String,Integer> map = new HashMap<>();
        File[] files = src.listFiles();

        for(File file : files){
            if(file.isFile()){
                String name = file.getName();
                String[] arr = name.split("\\.");
                String endName = arr[arr.length-1];
                if(map.containsKey(endName)){
                    map.put(endName, map.get(endName)+1);
                }
                else{
                    map.put(endName, 1);
                }

            }
            else{
                HashMap<String,Integer> map1 = getCount(file);

                //map和map1合并
                Set<Map.Entry<String,Integer>> entry = map1.entrySet();
                for(Map.Entry<String,Integer> e: entry){
                    if(map.containsKey(e.getKey())){
                        Integer count = e.getValue();
                        count += map.get(e.getKey());
                        map.put(e.getKey(), count);
                    }
                    else{
                        map.put(e.getKey(), e.getValue());
                    }
                }
            }
        }
        return map;
    }
}
```

