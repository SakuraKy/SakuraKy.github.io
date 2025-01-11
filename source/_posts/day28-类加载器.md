---
title: day25-类加载器
date: 2025-01-06 10:44:00
tags:
  - 基础加强
categories: java
photos: /tupian/j25.jpg
---

# 写在前面的话：

> 基础加强包含了：
>
> 反射，动态代理，类加载器，xml，注解，日志，单元测试等知识点
>
> 其中最难的是反射和动态代理，其他知识点都非常简单
>
> 由于 B 站 P 数限制，xml，注解等知识点，阿玮写了详细文档供大家学习

## 1.类加载器

### 1.1 类加载器

- 作用

  负责将.class 文件（存储的物理文件）加载在到内存中

  ![01_类加载器](/tupian/01_类加载器.png)

### 1.2 类加载的完整过程

- 类加载时机

  简单理解：字节码文件什么时候会被加载到内存中？

  有以下的几种情况：

  - 创建类的实例（对象）
  - 调用类的类方法
  - 访问类或者接口的类变量，或者为该类变量赋值
  - 使用反射方式来强制创建某个类或接口对应的 java.lang.Class 对象
  - 初始化某个类的子类
  - 直接使用 java.exe 命令来运行某个主类

  总结而言：用到了就加载，不用不加载

- 类加载过程

  1. 加载

     - 通过包名 + 类名，获取这个类，准备用流进行传输
     - 在这个类加载到内存中
     - 加载完毕创建一个 class 对象

     ![02_类加载过程加载](/tupian/02_类加载过程加载.png)

  2. 链接

     - 验证

       确保 Class 文件字节流中包含的信息符合当前虚拟机的要求，并且不会危害虚拟机自身安全

       (文件中的信息是否符合虚拟机规范有没有安全隐患)

     ![03_类加载过程验证](/tupian/03_类加载过程验证.png)

     - 准备

       负责为类的类变量（被 static 修饰的变量）分配内存，并设置默认初始化值

       (初始化静态变量)

     ![04_类加载过程准备](/tupian/04_类加载过程准备.png)

     - 解析

       将类的二进制数据流中的符号引用替换为直接引用

       (本类中如果用到了其他类，此时就需要找到对应的类)

     ![05_类加载过程解析](/tupian/05_类加载过程解析.png)

  3. 初始化

     根据程序员通过程序制定的主观计划去初始化类变量和其他资源

     (静态变量赋值以及初始化其他资源)

     ![06_类加载过程初始化](/tupian/06_类加载过程初始化.png)

- 小结

  - 当一个类被使用的时候，才会加载到内存
  - 类加载的过程: 加载、验证、准备、解析、初始化

### 1.3 类加载的分类【理解】

- 分类

  - Bootstrap class loader：虚拟机的内置类加载器，通常表示为 null ，并且没有父 null
  - Platform class loader：平台类加载器,负责加载 JDK 中一些特殊的模块
  - System class loader：系统类加载器,负责加载用户类路径上所指定的类库

- 类加载器的继承关系

  - System 的父加载器为 Platform
  - Platform 的父加载器为 Bootstrap

- 代码演示

  ```java
  public class ClassLoaderDemo1 {
      public static void main(String[] args) {
          //获取系统类加载器
          ClassLoader systemClassLoader = ClassLoader.getSystemClassLoader();

          //获取系统类加载器的父加载器 --- 平台类加载器
          ClassLoader classLoader1 = systemClassLoader.getParent();

          //获取平台类加载器的父加载器 --- 启动类加载器
          ClassLoader classLoader2 = classLoader1.getParent();

          System.out.println("系统类加载器" + systemClassLoader);
          System.out.println("平台类加载器" + classLoader1);
          System.out.println("启动类加载器" + classLoader2);

      }
  }
  ```

### 1.4 双亲委派模型【理解】

- 介绍

  如果一个类加载器收到了类加载请求，它并不会自己先去加载，而是把这个请求委托给父类的加载器去执行，如果父类加载器还存在其父类加载器，则进一步向上委托，依次递归，请求最终将到达顶层的启动类加载器，如果父类加载器可以完成类加载任务，就成功返回，倘若父类加载器无法完成此加载任务，子加载器才会尝试自己去加载，这就是双亲委派模式

  ![07_双亲委派模型](/tupian/07_双亲委派模型.png)

### 1.5ClassLoader 中的两个方法【应用】

- 方法介绍

  | 方法名                                              | 说明               |
  | --------------------------------------------------- | ------------------ |
  | public static ClassLoader getSystemClassLoader()    | 获取系统类加载器   |
  | public InputStream getResourceAsStream(String name) | 加载某一个资源文件 |

- 示例代码

  ```java
  public class ClassLoaderDemo2 {
      public static void main(String[] args) throws IOException {
          //static ClassLoader getSystemClassLoader() 获取系统类加载器
          //InputStream getResourceAsStream(String name)  加载某一个资源文件

          //获取系统类加载器
          ClassLoader systemClassLoader = ClassLoader.getSystemClassLoader();

          //利用加载器去加载一个指定的文件
          //参数：文件的路径（放在src的根目录下，默认去那里加载）
          //返回值：字节流。
          InputStream is = systemClassLoader.getResourceAsStream("prop.properties");

          Properties prop = new Properties();
          prop.load(is);

          System.out.println(prop);

          is.close();
      }
  }
  ```

## 本篇文章代码由[黑马程序员](https://space.bilibili.com/37974444?spm_id_from=333.337.search-card.all.click)提供
