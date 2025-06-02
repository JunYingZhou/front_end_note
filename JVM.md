# JVM

1. ## 初始JVM

1. 1. ### 解释与运行

![img](https://cdn.nlark.com/yuque/0/2024/png/40432188/1715064046948-d05e8bcb-5535-4b7d-8e10-d3b25ca3659b.png)

1. 1. ### 内存管理

![img](https://cdn.nlark.com/yuque/0/2024/png/40432188/1715064197095-9a383654-db16-425d-a6ec-6188328a85ce.png)

1. 1. ### 即时编辑

![img](https://cdn.nlark.com/yuque/0/2024/png/40432188/1715064224180-6d1a0fcd-9777-4d2e-ae4b-162c3a20440f.png)

不做性能优化的话，不如c,c++

***为什么呢，主要是为了跨平台特性***

![img](https://cdn.nlark.com/yuque/0/2024/png/40432188/1715064293466-21651e45-d6f2-4159-8db2-c541e992e6c6.png)

*将第一次编译的内容**存储到内存当中，当**第二次执行的时候，**就直接调用**，(JIT)就可以提高java的性能*

![image-20240507144819138](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240507144819138.png)



## 2、字节码文件详解

### 2.1 JVM的组成

类加载器--》运行时数据区（JVM管理的内存）--》**执行引擎 --》 本地接口**（执行、本地无法修改）

![image-20240507145700537](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240507145700537.png)

