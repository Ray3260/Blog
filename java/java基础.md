## java 和 c++ 区别
* java 和 c++ 都是面向对象的编程语言，都支持封装、多态、继承。
* java通过jvm支持多平台，c++需要特定平台
* java不支持指针直接访问内存，他的引用可以理解为安全指针。c++支持指针。
* java不支持多继承，可以通过实现多个接口来达到目的，c++支持多继承。
* java有自动内存管理垃圾回收机制，c++需要手动回收内存。
* java只支持方法重载（操作符重载增加了复杂性，不符合最初设计思想），c++同时支持方法重载和操作符重载

## JVM、JDK 和 JRE
* jdk = jre + java工具 + 编译器 + 调试器
* jre = jvm + java 核心类库

## 面向对象编程的六大原则
* 对象单一原则
  
  对象设计要求独立，不能设计万能对象
* 里式替换原则

  子类能够完全替代父类，反之则不行
* 迪米特法则

  高内聚，低耦合。尽量不要依赖细节。
* 开闭原则

  开放扩展，封闭修改
* 依赖倒置原则

  高层模块不应该直接依赖于底层模块的具体实现，而应该依赖于底层的抽象。面向抽象编程，基于接口编程。
* 接口隔离原则

  一个对象和另外一个对象交互的过程中，依赖的内容最小。接口大小设计要适中。
  
## 值传递和引用传递
* java中不存在引用传递，只存在值传递。
* 值传递是对基本型变量而言的，传递的是该变量的一个副本，改变副本不影响原变量。
* 引用传递一般是对于对象型变量而言的，传递的是该对象地址的一个副本，并不是原对象本身，两者指向同一片内存空间。所以对引用对象进行操作会同时改变原对象。

## 基本类型和包装类型
* 基本类型有默认值，包装类型不赋值就是null。
* 基本类型==比较的是值，包装类型==比较的是对象的内存地址，equals()方法用于比较值。
* 基本类型的存储位置取决于他们的作用域和声明方式，局部变量会放在栈中，成员变量会放在堆中。几乎所有对象实例都放在堆中。
* Byte、Short、Integer和Long 4种包装类型默认创建了【-128，127】相应类型的缓存数据。Character是【0，127】范围的缓存数据。
* 自动拆装箱，装箱(valueOf()), 拆箱(xxxValue(), e.g. intValue())

## String为什么不可变
* 线程安全：同一个字符串可以被多个线程共享，不可变保证了线程安全
* 支持hash映射和缓存：String的hash经常会被用到，比如map的key，不可变保证了hash不会变，减少了重新计算。
* 安全性问题：网络地址、文件路径、密码等通常使用String类型保存。不可变减少了被修改的安全隐患。
* 字符串常量池：String对象被创建后存储在常量池中，下次在创建相同的字符串时，可以直接返回缓存的引用。

## 静态方法为什么不能调用非静态类型
* 静态方法是属于类的，在类加载的时候就会分配内存，可以通过类名直接访问。非静态成员属于实例对象，只有在对象实例化之后才存在，需要通过类的实例对象去访问。
* 在类的非静态成员不存在的时候静态方法就已经存在了，此时调用在内存中还不存在的非静态成员，属于非法操作。

## 为什么重写 equals() 时必须重写 hashCode() 方法？
* 如果equals判断两个对象是相等的， 那么这两个对象的hashcode必须是相等的
* 如果重写 equals() 时没有重写 hashCode() 方法的话就可能会导致 equals 方法判断是相等的两个对象，而hashCode 值却不相等。

## Try-catch-finally
* Try 用于捕获异常，后面可接0-n个catch块，如果没有catch块，则必须跟一个finally块。
* catch块用于处理try捕获的异常。
* finally中语句始终被执行，即使try或catch块中有return语句，finally语句块将在return之前执行。
* 当jvm在finally之前终止，关闭cpu，或者所在线程死亡则不会被执行。
