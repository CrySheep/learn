jvm

虚拟机内存：
    运行时数据区域
        方法区
        堆
        ----
        虚拟机栈
        本地方法栈
        程序计数器
    其他
        执行引擎
        本地库接口
        本地方法库

    
    程序计数器  
        当前程序执行字节码的行号指示器。通过改变值来选取下一条执行的字节码指令
        （分支、循环、跳转、一场处理、线程恢复）
        线程私有
        执行本地方法时为undefined 
    
    Java 虚拟机栈 
        描述java 方法执行的线程内存模型
        方法执行时创建栈帧，用于存储局部表量表、操作数栈、动态链接、方法出口等
        方法调用对应栈帧的入栈到出栈

        StackOverFlowerror
        outofMemoryError


    局部变量表

        编译器可知的基本数据类型：
            boolean、byte、char、short、int、float、long、double 
        对象引用
        returnAdress 类型（指向一条字节码指令地址）

    本地方法栈
        本地方法 
        StackOverFlowerror OutOfMeomoryError
    java 堆 
        对象实例
        经典分代：
            新生代
                Eden 
                Survivor 
                    From
                    To

            老年代
        
        -Xmx 
        -Xms
    方法区
        虚拟机加载的类信息
        常量
        静态变量
        即时编译器编译后的代码缓存数据


        永久代：
            HotSpot JDK8 
                用永久代来实现方法去，不用重新设计内存管理
                缺点：更容易内存溢出。-XX：MaxPermSize 
            演变：
                JDK6  计划
                JDK7 字符串常量池、静态变量移出
                JDK8 元空间（类型信息）
        OutOfMeomoryError、

        运行时常量池
            类文件中常量池（用于存放编译期生成的各种字面量与符号引用），类加载后存入运行时常量池 (一般来说也存储直接引用)
            动态性：
                String.intern()

    直接内存
        NIO ，基于Channel 和缓冲区Buffer，使用Native函数库直接分配对堆外内存l通过DirectByteBuffer作为内存引用进行操作。

        OutOfMeomoryError


    分配缓冲区 Thread Local Allocation Buffer 



对象创建
    new 指令
    检查new 指令参数是否在常量池中存在类的符号引用。
    如果存在，检查类是否加载，解析、初始化（如果没有，进行加载、解析、初始化）
    在新生代中分配内存。
        分配方式：（指针碰撞、空闲列表）(垃圾收集器决定分配方式)
        问题解决：内存冲突
            CAS失败重试
            本地线程分配缓冲  -XX:+/-UseTLAB
    初始化内存
    设置对象
        哪个类的实例、类的元数据信息、队形的哈希码、GC分代年龄

    java程序对象创建
        class <init>
        new <init>
对象布局
    Header、实例数据、对其填充

    Header 
        两类信息
            自身运行时数据、类型指针

            自身运行时数据 
                哈希码、GC粉黛年龄、锁状态标志、线程持有的锁、偏向线程ID、偏向时间戳 （32位、64位Bitmap Mark Word） (25\4\2\0\)
            类型指针
                指向它的类型元数据的指针（数组存数组长度）
    实例数据
        代码定义的各种类型的字段内容（虚拟机分配策略影响（-XX：FieldsAllocationStyle）和定义顺序的影响）（分配顺序 longs/doubles \ ints/shorts/chars \ bytes/booleans \oops）
    对齐填充 
        对象大小必须8字节的整数倍
对象访问
    通过堆上的reference数据来操作对上的具体对象（reference 实现方式由虚拟机实现）

     对象访问方式
        句柄和直接指针
        句柄
            堆中划出句柄池，reference 存句柄地址，句柄包含对象实例数据与类型数据各自的具体地址

            优势：
                reference 存储内容稳定，对象变动只需改变句柄的实例数据指针

        直接指针 
            reference存储对象地址
            又是：速度快
        hotspot 采用直接指针    

内存溢出实例：




            






    



