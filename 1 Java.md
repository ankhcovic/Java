# 基础知识

## 接口

接口引用指向一个实现类对象可以实现对象，这样不管哪个类都可以使用接口的方法

0x是16进制表示法

## 多态

对于多态，可以总结它为：

* 父类引用可以指向子类对象，子类引用不能指向父类对象。
* 把子类对象直接赋给父类引用叫upcasting向上转型，向上转型不用强制转型。
   　 如Father father = new Son();
* 把指向子类对象的父类引用赋给子类引用叫向下转型（downcasting），要强制转型。
   　 如father就是一个指向子类对象的父类引用，把father赋给子类引用son 即Son son =（Son）father；
      　 其中father前面的（Son）必须添加，进行强制转换。
* upcasting 会丢失子类特有的方法,但是子类overriding 父类的方法，子类方法有效
* 向上转型的作用，减少重复代码，父类为参数，调有时用子类作为参数，就是利用了向上转型。这样使代码变得简洁。体现了JAVA的抽象编程思想。
* 变量不能被重写（覆盖），”重写“的概念只针对方法，如果在子类中”重写“了父类中的变量，那么在编译时会报错。
* 多态的3个必要条件：
   1.继承   2.重写   3.父类引用指向子类对象。

## 链表初始化

```java
// "static void main" must be defined in a public class.
public class Main {
    public static void main(String[] args) {
        List<List<String>> strs = new ArrayList<List<String>>(){
            {
                add(new ArrayList<String>(){
                    {
                        add("a0");
                        add("a1");
                        add("a2");
                    }
                });
                add(new ArrayList<String>(){
                    {
                        add("b0");
                        add("b1");
                        add("b2");
                    }
                });
            }
        };
        // strs.add(new ArrayList<String>(){{add("a0");add("a1");add("a2");}});
        // strs.add(new ArrayList<String>(){{add("b0");add("b1");add("b2");}});
        System.out.println(strs.get(0).get(1));
    }
}
```

## 基本运算

- 位运算

  - 异或运算实现交换

    ```
    a^0 = a
    a^a = 0
    (a^b)^b = a
    ```

## [1. Java 基本功](https://snailclimb.gitee.io/javaguide/#/docs/java/basis/Java基础知识?id=_1-java-基本功)

### [1.1. Java 入门（基础概念与常识）](https://snailclimb.gitee.io/javaguide/#/docs/java/basis/Java基础知识?id=_11-java-入门（基础概念与常识）)

#### [1.1.1. Java 语言有哪些特点?](https://snailclimb.gitee.io/javaguide/#/docs/java/basis/Java基础知识?id=_111-java-语言有哪些特点)

1. 简单易学；
2. 面向对象（封装，继承，多态）；
3. 平台无关性（ Java 虚拟机实现平台无关性）；
4. 可靠性；
5. 安全性；
6. 支持多线程；
7. 支持网络编程并且很方便（ Java 语言诞生本身就是为简化网络编程设计的，因此 Java 语言不仅支持网络编程而且很方便）；
8. 编译与解释并存；

#### [1.1.2. 关于 JVM JDK 和 JRE 最详细通俗的解答](https://snailclimb.gitee.io/javaguide/#/docs/java/basis/Java基础知识?id=_112-关于-jvm-jdk-和-jre-最详细通俗的解答)

##### [1.1.2.1. JVM](https://snailclimb.gitee.io/javaguide/#/docs/java/basis/Java基础知识?id=_1121-jvm)

Java 虚拟机（JVM）是运行 Java 字节码的虚拟机。JVM 有针对不同系统的特定实现（Windows，Linux，macOS），目的是使用相同的字节码，它们都会给出相同的结果。

**什么是字节码?采用字节码的好处是什么?**

> 在 Java 中，JVM 可以理解的代码就叫做`字节码`（即扩展名为 `.class` 的文件），**它不面向任何特定的处理器，只面向虚拟机**。Java 语言通过字节码的方式，在一定程度上解决了传统解释型语言执行**效率**低的问题，同时又保留了解释型语言**可移植**的特点。所以 Java 程序运行时比较高效，而且，由于字节码并不针对一种特定的机器，因此，**Java 程序无须重新编译便可在多种不同操作系统的计算机上运行**。

**Java 程序从源代码到运行一般有下面 3 步：**

![Java程序运行过程](C:\Users\94307\OneDrive - zju.edu.cn\learnbm\JAVA\学习笔记\Java 程序运行过程.png)

我们需要格外注意的是 .class->机器码 这一步。在这一步 JVM 类加载器首先加载字节码文件，然后通过**解释器逐行解释执行**，这种方式的执行速度会相对比较慢。而且，有些方法和代码块是经常需要被调用的(也就是所谓的热点代码)，所以后面引进了 **JIT 编译器**，而 JIT 属于**运行时编译**。当 JIT 编译器完成第一次编译后，其会将字节码对应的机器码保存下来，下次可以直接使用。而我们知道，机器码的运行效率肯定是高于 Java 解释器的。这也解释了我们为什么经常会说 Java 是**编译与解释共存的语言**（半解释型语言）。

> HotSpot 采用了**惰性评估(Lazy Evaluation)**的做法，根据二八定律，消耗大部分系统资源的只有那一小部分的代码（热点代码），而这也就是 JIT 所需要编译的部分。JVM 会根据代码每次被执行的情况收集信息并相应地做出一些优化，因此**执行的次数越多，它的速度就越快**。JDK 9 引入了一种新的编译模式 AOT(Ahead of Time Compilation)，它是直接将字节码编译成机器码，这样就避免了 **JIT 预热**等各方面的开销。JDK 支持分层编译和 AOT 协作使用。但是 ，AOT 编译器的编译质量是肯定比不上 JIT 编译器的。

Java 虚拟机（JVM）是**运行 Java 字节码**的虚拟机，例如HotSpot。JVM 有针对不同系统的特定实现（Windows，Linux，macOS），目的是**使用相同的字节码**，它们都会给出相同的结果。字节码和不同系统的 JVM 实现是 Java 语言“一次编译，随处可以运行”的关键所在。

##### [1.1.2.2. JDK 和 JRE](https://snailclimb.gitee.io/javaguide/#/docs/java/basis/Java基础知识?id=_1122-jdk-和-jre)

JDK 是 Java Development Kit 缩写，它是功能齐全的 Java SDK。它拥有 JRE 所拥有的一切，还有编译器（javac）和工具（如 javadoc 和 jdb）。它能够创建和编译程序。

JRE 是 Java 运行时环境。它是运行已编译 Java 程序所需的所有内容的集合，包括 Java 虚拟机（JVM），Java 类库，java 命令和其他的一些基础构件。但是，它不能用于创建新程序。

如果你只是为了运行一下 Java 程序的话，那么你只需要安装 JRE 就可以了。如果你需要进行一些 Java 编程方面的工作，那么你就需要安装 JDK 了。但是，这不是绝对的。有时，即使您不打算在计算机上进行任何 Java 开发，仍然需要安装 JDK。例如，如果要使用 JSP 部署 Web 应用程序，那么从技术上讲，您只是在应用程序服务器中运行 Java 程序。那你为什么需要 JDK 呢？因为应用程序服务器会将 JSP 转换为 Java servlet，并且需要使用 JDK 来编译 servlet。

![img](C:\Users\94307\OneDrive - zju.edu.cn\learnbm\JAVA\学习笔记\v2-a46e2e80d024fe5bfb9e6b8ed9f3dea7_r.jpg)

#### [1.1.3. Oracle JDK 和 OpenJDK 的对比](https://snailclimb.gitee.io/javaguide/#/docs/java/basis/Java基础知识?id=_113-oracle-jdk-和-openjdk-的对比)

可能在看这个问题之前很多人和我一样并没有接触和使用过 OpenJDK 。那么 Oracle 和 OpenJDK 之间是否存在重大差异？下面我通过收集到的一些资料，为你解答这个被很多人忽视的问题。

对于 Java 7，没什么关键的地方。OpenJDK 项目主要基于 Sun 捐赠的 HotSpot 源代码。此外，OpenJDK 被选为 Java 7 的参考实现，由 Oracle 工程师维护。关于 JVM，JDK，JRE 和 OpenJDK 之间的区别，Oracle 博客帖子在 2012 年有一个更详细的答案：

> 问：OpenJDK 存储库中的源代码与用于构建 Oracle JDK 的代码之间有什么区别？
>
> 答：非常接近 - 我们的 Oracle JDK 版本构建过程基于 OpenJDK 7 构建，只添加了几个部分，例如部署代码，其中包括 Oracle 的 Java 插件和 Java WebStart 的实现，以及一些封闭的源代码派对组件，如图形光栅化器，一些开源的第三方组件，如 Rhino，以及一些零碎的东西，如附加文档或第三方字体。展望未来，我们的目的是开源 Oracle JDK 的所有部分，除了我们考虑商业功能的部分。

**总结：**

1. Oracle JDK 大概每 6 个月发一次主要版本，而 OpenJDK 版本大概每三个月发布一次。但这不是固定的，我觉得了解这个没啥用处。详情参见：https://blogs.oracle.com/java-platform-group/update-and-faq-on-the-java-se-release-cadence 。
2. OpenJDK 是一个参考模型并且是完全开源的，而 Oracle JDK 是 OpenJDK 的一个实现，并不是完全开源的；
3. Oracle JDK 比 OpenJDK 更稳定。OpenJDK 和 Oracle JDK 的代码几乎相同，但 Oracle JDK 有更多的类和一些错误修复。因此，如果您想开发企业/商业软件，我建议您选择 Oracle JDK，因为它经过了彻底的测试和稳定。某些情况下，有些人提到在使用 OpenJDK 可能会遇到了许多应用程序崩溃的问题，但是，只需切换到 Oracle JDK 就可以解决问题；
4. 在响应性和 JVM 性能方面，Oracle JDK 与 OpenJDK 相比提供了更好的性能；
5. Oracle JDK 不会为即将发布的版本提供长期支持，用户每次都必须通过更新到最新版本获得支持来获取最新版本；
6. Oracle JDK 根据二进制代码许可协议获得许可，而 OpenJDK 根据 GPL v2 许可获得许可。

#### [1.1.4. Java 和 C++的区别?](https://snailclimb.gitee.io/javaguide/#/docs/java/basis/Java基础知识?id=_114-java-和-c的区别)

我知道很多人没学过 C++，但是面试官就是没事喜欢拿咱们 Java 和 C++ 比呀！没办法！！！就算没学过 C++，也要记下来！

- 都是面向对象的语言，都**支持封装、继承和多态**
- **Java 不提供指针**来直接访问内存，程序内存更加安全
- J**ava 的类是单继承的，C++ 支持多重继承**；虽然 Java 的类不可以多继承，但是**接口可以多继承**。
- **Java 有自动内存管理垃圾回收机制(GC)**，不需要程序员手动释放无用内存
- **在 C 语言中，字符串或字符数组最后都会有一个额外的字符`'\0'`来表示结束。但是，Java 语言中没有结束符这一概念。** 

#### [1.1.5. import java 和 javax 有什么区别？](https://snailclimb.gitee.io/javaguide/#/docs/java/basis/Java基础知识?id=_115-import-java-和-javax-有什么区别？)

刚开始的时候 JavaAPI 所必需的包是 java 开头的包，**javax 当时只是扩展 API 包来使用**。然而随着时间的推移，**javax 逐渐地扩展成为 Java API 的组成部分**。但是，将扩展从 javax 包移动到 java 包确实太麻烦了，最终会破坏一堆现有的代码。因此，最终决定 javax 包将成为标准 API 的一部分。

所以，实际上 java 和 javax 没有区别。这都是一个名字。

#### [1.1.6. 为什么说 Java 语言“编译与解释并存”？](https://snailclimb.gitee.io/javaguide/#/docs/java/basis/Java基础知识?id=_116-为什么说-java-语言编译与解释并存？)

高级编程语言按照程序的执行方式分为编译型和解释型两种。简单来说，编译型语言是指编译器针对特定的操作系统将源代码一次性翻译成可被该平台执行的机器码；解释型语言是指解释器对源程序逐行解释成特定平台的机器码并立即执行。比如，你想阅读一本英文名著，你可以找一个英文翻译人员帮助你阅读， 有两种选择方式，你可以先等翻译人员将全本的英文名著（也就是源码）都翻译成汉语，再去阅读，也可以让翻译人员翻译一段，你在旁边阅读一段，慢慢把书读完。

Java 语言既具有编译型语言的特征，也具有解释型语言的特征，因为 Java 程序要经过先编译，后解释两个步骤，由 Java 编写的程序需要先经过编译步骤，生成字节码（*.class 文件），这种字节码必须由 Java 解释器来解释执行。因此，我们可以认为 Java 语言编译与解释并存。

### [1.2. Java 语法](https://snailclimb.gitee.io/javaguide/#/docs/java/basis/Java基础知识?id=_12-java-语法)

![img](C:\Users\94307\OneDrive - zju.edu.cn\learnbm\JAVA\学习笔记\86735519.jpg)

#### [1.2.2. 关于注释？](https://snailclimb.gitee.io/javaguide/#/docs/java/basis/Java基础知识?id=_122-关于注释？)

> **代码的注释不是越详细越好。实际上好的代码本身就是注释，我们要尽量规范和美化自己的代码来减少不必要的注释。**
>
> **若编程语言足够有表达力，就不需要注释，尽量通过代码来阐述。**

#### [1.2.3. 标识符和关键字的区别是什么？](https://snailclimb.gitee.io/javaguide/#/docs/java/basis/Java基础知识?id=_123-标识符和关键字的区别是什么？)

在我们编写程序的时候，需要大量地为程序、类、变量、方法等取名字，于是就有了标识符，简单来说，标识符就是一个名字。但是有一些标识符，Java 语言已经赋予了其特殊的含义，只能用于特定的地方，这种特殊的标识符就是关键字。因此，关键字是被赋予特殊含义的标识符。

#### [1.2.4. Java 中有哪些常见的关键字？](https://snailclimb.gitee.io/javaguide/#/docs/java/basis/Java基础知识?id=_124-java-中有哪些常见的关键字？)

| 访问控制             | private  | protected  | public   |              |            |           |        |
| -------------------- | -------- | ---------- | -------- | ------------ | ---------- | --------- | ------ |
| 类，方法和变量修饰符 | abstract | class      | extends  | final        | implements | interface | native |
|                      | new      | static     | strictfp | synchronized | transient  | volatile  |        |
| 程序控制             | break    | continue   | return   | do           | while      | if        | else   |
|                      | for      | instanceof | switch   | case         | default    |           |        |
| 错误处理             | try      | catch      | throw    | throws       | finally    |           |        |
| 包相关               | import   | package    |          |              |            |           |        |
| 基本类型             | boolean  | byte       | char     | double       | float      | int       | long   |
|                      | short    | null       | true     | false        |            |           |        |
| 变量引用             | super    | this       | void     |              |            |           |        |
| 保留字               | goto     | const      |          |              |            |           |        |

##### static关键字

​		static 关键字，可以修饰变量、方法和代码块。在使用的过程中，其主要目的还是想**在不创建对象的情况 下，去调用方法**。

- 修饰类变量：

  ​		当 static 修饰成员变量时，该变量称为类变量。该类的**每个对象都共享同一个类变量的值**。任何对象都可以更改该类变量的值，但也可以**在不创建该类的对象的情况下对类变量进行操作**。

- 静态方法

  ​		当 static 修饰成员方法时，该方法称为类方法 。静态方法在声明中有 static ，**建议使用类名来调用**，而不需要创建类的对象。调用方式非常简单。 

  ​		类方法：使用 static关键字修饰的成员方法，习惯称为静态方法。

  静态方法调用的注意事项： 

  - 静态方法可以直接访问类变量和静态方法。 
  - 静态方法不能直接访问普通成员变量或成员方法。反之，成员方法可以直接访问类变量或静态方法。
  -  静态方法中，不能使用this关键字。

- static 修饰的内容：

  - 是随着类的加载而加载的，且只加载一次。 
  - 存储于一块固定的内存区域（静态区），所以，可以直接被类名调用。 
  - 它优先于对象存在，所以，可以被所有对象共享。

![image-20210311205928762](C:\Users\94307\OneDrive - zju.edu.cn\learnbm\JAVA\学习笔记\image-20210311205928762.png)

- 静态代码块
  - 静态代码块：定义在成员位置，使用static修饰的代码块{ }。 
    - 位置：类中方法外。 
    - 执行：随着类的加载而执行且执行一次，优先于main方法和构造方法的执行。
    - 作用：给类变量进行初始化赋值。

#### [1.2.5. 自增自减运算符](https://snailclimb.gitee.io/javaguide/#/docs/java/basis/Java基础知识?id=_125-自增自减运算符)

++和--运算符可以放在变量之前，也可以放在变量之后

当运算符放在变量之前时(前缀)，先自增/减，再赋值；

当运算符放在变量之后时(后缀)，先赋值，再自增/减。

#### [1.2.6. continue、break、和 return 的区别是什么？](https://snailclimb.gitee.io/javaguide/#/docs/java/basis/Java基础知识?id=_126-continue、break、和-return-的区别是什么？)

1. continue ：指跳出当前的这一次循环，继续下一次循环。
2. break ：指跳出整个循环体，继续执行循环下面的语句。
3. `return;` ：直接使用 return 结束方法执行，用于没有返回值函数的方法
4. `return value;` ：return 一个特定值，用于有返回值函数的方法

#### [1.2.7. Java 泛型了解么？什么是类型擦除？介绍一下常用的通配符？](https://snailclimb.gitee.io/javaguide/#/docs/java/basis/Java基础知识?id=_127-java-泛型了解么？什么是类型擦除？介绍一下常用的通配符？)

Java 泛型（generics）是 JDK 5 中引入的一个新特性, 泛型提供了编译时类型安全检测机制，该机制允许程序员在编译时检测到非法的类型。泛型的本质是参数化类型，也就是说所操作的数据类型被指定为一个参数。

**Java 的泛型是伪泛型，这是因为 Java 在编译期间，所有的泛型信息都会被擦掉，这也就是通常所说类型擦除 。**

泛型一般有三种使用方式:泛型类、泛型接口、泛型方法。

**常用的通配符为： T，E，K，V，？**

- ？ 表示不确定的 java 类型
- T (type) 表示具体的一个 java 类型
- K V (key value) 分别代表 java 键值中的 Key Value
- E (element) 代表 Element

#### [1.2.8. ==和 equals 的区别](https://snailclimb.gitee.io/javaguide/#/docs/java/basis/Java基础知识?id=_128-和-equals-的区别)

**`==`** : 它的作用是判断两个对象的地址是不是相等。即判断两个对象是不是同一个对象。(**基本数据类型==比较的是值，引用数据类型==比较的是内存地址**)

> 因为 Java 只有值传递，所以，对于 == 来说，不管是比较基本数据类型，还是引用数据类型的变量，其本质比较的都是值，只是引用类型变量存的值是对象的地址。

**`equals()`** : 它的作用也是判断两个对象是否相等，它不能用于比较基本数据类型的变量。`equals()`方法存在于`Object`类中，而`Object`类是所有类的直接或间接父类。

> 情况 1：类没有覆盖 `equals()`方法。则通过`equals()`比较该类的两个对象时，等价于通过“==”比较这两个对象。使用的默认是 `Object`类`equals()`方法。
>
> 情况 2：类覆盖了 `equals()`方法。一般，我们都覆盖 `equals()`方法来两个对象的内容相等；若它们的内容相等，则返回 true(即，认为这两个对象相等)。

#### [1.2.9. hashCode()与 equals()](https://snailclimb.gitee.io/javaguide/#/docs/java/basis/Java基础知识?id=_129-hashcode与-equals)

**1)hashCode()介绍:**

`hashCode()` 的作用是获取**哈希码**，也称为**散列码**；它实际上是返回一个 int 整数。这个哈希码的作用是确定该对象在哈希表中的索引位置。`hashCode()`定义在 JDK 的 `Object` 类中，这就意味着 Java 中的任何类都包含有 `hashCode()` 函数。另外需要注意的是： `Object` 的 hashcode 方法是**本地方法**，也就是用 c 语言或 c++ 实现的，该方法通常用来将对象的 内存地址 转换为整数之后返回。

```java
public native int hashCode();Copy to clipboardErrorCopied
```

散列表存储的是键值对(key-value)，它的特点是：能根据“键”快速的检索出对应的“值”。这其中就利用到了散列码！（可以快速找到所需要的对象）

**2)为什么要有 hashCode？**

我们以“`HashSet` 如何检查重复”为例子来说明为什么要有 hashCode？

当你把对象加入 `HashSet` 时，`HashSet` 会先计算对象的 hashcode 值来判断对象加入的位置，同时也会与其他已经加入的对象的 hashcode 值作比较，如果没有相符的 hashcode，`HashSet` 会假设对象没有重复出现。但是如果发现有相同 hashcode 值的对象，这时会调用 `equals()` 方法来检查 hashcode 相等的对象是否真的相同。如果两者相同，`HashSet` 就不会让其加入操作成功。如果不同的话，就会重新散列到其他位置。（摘自我的 Java 启蒙书《Head First Java》第二版）。这样我们就大大减少了 equals 的次数，相应就大大提高了执行速度。

**3)为什么重写 `equals` 时必须重写 `hashCode` 方法？**

如果两个对象相等，则 hashcode 一定也是相同的。两个对象相等,对两个对象分别调用 equals 方法都返回 true。但是，两个对象有相同的 hashcode 值，它们也不一定是相等的 。**因此，equals 方法被覆盖过，则 `hashCode` 方法也必须被覆盖。**

> `hashCode()`的默认行为是对堆上的对象产生独特值。如果没有重写 `hashCode()`，则该 class 的两个对象无论如何都不会相等（即使这两个对象指向相同的数据）

**4)为什么两个对象有相同的 hashcode 值，它们也不一定是相等的？**

在这里解释一位小伙伴的问题。以下内容摘自《Head Fisrt Java》。

因为 `hashCode()` 所使用的杂凑算法也许刚好会让多个对象传回相同的杂凑值。越糟糕的杂凑算法越容易碰撞，但这也与数据值域分布的特性有关（所谓碰撞也就是指的是不同的对象得到相同的 `hashCode`。

我们刚刚也提到了 `HashSet`,如果 `HashSet` 在对比的时候，同样的 hashcode 有多个对象，它会使用 `equals()` 来判断是否真的相同。也就是说 `hashcode` 只是用来缩小查找成本。

### [1.3. 基本数据类型](https://snailclimb.gitee.io/javaguide/#/docs/java/basis/Java基础知识?id=_13-基本数据类型)

#### [1.3.1. Java 中的几种基本数据类型是什么？对应的包装类型是什么？各自占用多少字节呢？](https://snailclimb.gitee.io/javaguide/#/docs/java/basis/Java基础知识?id=_131-java-中的几种基本数据类型是什么？对应的包装类型是什么？各自占用多少字节呢？)

Java**中**有 8 种基本数据类型，分别为：

1. 6 种数字类型 ：byte、short、int、long、float、double
2. 1 种字符类型：char
3. 1 种布尔型：boolean。

这八种基本类型都有对应的包装类分别为：Byte、Short、Integer、Long、Float、Double、Character、Boolean

| 基本类型 | 位数 | 字节 | 默认值  |
| -------- | ---- | ---- | ------- |
| int      | 32   | 4    | 0       |
| short    | 16   | 2    | 0       |
| long     | 64   | 8    | 0L      |
| byte     | 8    | 1    | 0       |
| char     | 16   | 2    | 'u0000' |
| float    | 32   | 4    | 0f      |
| double   | 64   | 8    | 0d      |
| boolean  | 1    |      | false   |

> 1. 对于 boolean，官方文档未明确定义，它依赖于 JVM 厂商的具体实现。逻辑上理解是占用 1 位，但是实际中会考虑计算机高效存储因素。
> 2. Java 里使用 long 类型的数据一定要在数值后面加上 **L**，否则将作为整型解析：
> 3. `char a = 'h'`char :单引号，`String a = "hello"` :双引号

#### [1.3.2. 自动装箱与拆箱](https://snailclimb.gitee.io/javaguide/#/docs/java/basis/Java基础知识?id=_132-自动装箱与拆箱)

- **装箱**：将基本类型用它们对应的引用类型包装起来；
- **拆箱**：将包装类型转换为基本数据类型；

### [1.4. 方法（函数）](https://snailclimb.gitee.io/javaguide/#/docs/java/basis/Java基础知识?id=_14-方法（函数）)

#### [1.4.1. 什么是方法的返回值?返回值在类的方法里的作用是什么?](https://snailclimb.gitee.io/javaguide/#/docs/java/basis/Java基础知识?id=_141-什么是方法的返回值返回值在类的方法里的作用是什么)

方法的返回值是指我们获取到的某个方法体中的代码执行后产生的结果！（前提是该方法可能产生结果）。返回值的作用是接收出结果，使得它可以用于其他的操作！

#### [1.4.2. 为什么 Java 中只有值传递？](https://snailclimb.gitee.io/javaguide/#/docs/java/basis/Java基础知识?id=_142-为什么-java-中只有值传递？)

首先回顾一下在程序设计语言中有关将参数传递给方法（或函数）的一些专业术语。**按值调用(call by value)表示方法接收的是调用者提供的值，而按引用调用（call by reference)表示方法接收的是调用者提供的变量地址。一个方法可以修改传递引用所对应的变量值，而不能修改传递值调用所对应的变量值。** 它用来描述各种程序设计语言（不只是 Java)中方法参数传递方式。

Java 程序设计语言总是采用**按值调用**。也就是说，**方法得到的是所有参数值的一个拷贝**，也就是说，方法**不能修改传递给它的任何参数变量的内容**。

**一个方法不能修改一个基本数据类型的参数，而对象引用作为参数就不一样**

Java 程序设计语言对对象采用的不是引用调用，实际上，对象引用是按值传递的。

下面再总结一下 Java 中方法参数的使用情况：

- 一个方法不能修改一个基本数据类型的参数（即数值型或布尔型）。
- 一个方法可以改变一个对象参数的状态。
- 一个方法不能让对象参数引用一个新的对象。

#### [1.4.3. 重载和重写的区别](https://snailclimb.gitee.io/javaguide/#/docs/java/basis/Java基础知识?id=_143-重载和重写的区别)

> 重载就是同样的一个方法能够根据输入数据的不同，做出不同的处理
>
> 重写就是当子类继承自父类的相同方法，输入数据一样，但要做出有别于父类的响应时，你就要覆盖父类方法

- **重载：**发生在编译期

```
发生在同一个类中（或者父类和子类之间），方法名必须相同，参数类型不同、个数不同、顺序不同，方法返回值和访问修饰符可以不同
重载就是同一个类中多个同名方法根据不同的传参来执行不同的逻辑处理。
可以重载任何方法，不只是构造器方法。
```

- **重写：**发生在运行期

```
重写发生在运行期，是子类对父类的允许访问的方法的实现过程进行重新编写。
1. 返回值类型、方法名、参数列表必须相同，抛出的异常范围小于等于父类，访问修饰符范围大于等于父类。
2. 如果父类方法访问修饰符为 `private/final/static` 则子类就不能重写该方法，但是被 static 修饰的方法能够被再次声明。
3. 构造方法无法被重写
重写就是子类对父类方法的重新改造，外部样子不能改变，内部逻辑可以改变
```

| 区别点     | 重载方法 | 重写方法                                                     |
| ---------- | -------- | ------------------------------------------------------------ |
| 发生范围   | 同一个类 | 子类                                                         |
| 参数列表   | 必须修改 | 一定不能修改                                                 |
| 返回类型   | 可修改   | 子类方法返回值类型应比父类方法返回值类型更小或相等           |
| 异常       | 可修改   | 子类方法声明抛出的异常类应比父类方法声明抛出的异常类更小或相等； |
| 访问修饰符 | 可修改   | 一定不能做更严格的限制（可以降低限制）                       |
| 发生阶段   | 编译期   | 运行期                                                       |

重写遵循两同两小一大：

同：方法名、参数名相同

小：子类方法返回值类型比父类方法返回值类型更小或相等；子类方法声明抛出的异常类比父类方法声明抛出的异常类更小或相等

大：子类方法的访问权限比父类方法的访问权限更大或相等

> 如果方法的返回类型是void和基本数据类型，则返回值重写时不可修改。
>
> 但是如果方法的返回值是引用类型，重写时是可以返回该引用类型的子类的。

#### [1.4.4. 深拷贝 vs 浅拷贝](https://snailclimb.gitee.io/javaguide/#/docs/java/basis/Java基础知识?id=_144-深拷贝-vs-浅拷贝)

1. **浅拷贝**：对基本数据类型进行值传递，对引用数据类型进行引用传递般的拷贝，此为浅拷贝。
2. **深拷贝**：对基本数据类型进行值传递，对引用数据类型，创建一个新的对象，并复制其内容，此为深拷贝。

![deep and shallow copy](C:\Users\94307\OneDrive - zju.edu.cn\learnbm\JAVA\学习笔记\java-deep-and-shallow-copy.jpg)

### [2.1. 类和对象](https://snailclimb.gitee.io/javaguide/#/docs/java/basis/Java基础知识?id=_21-类和对象)

#### [2.1.1. 面向对象和面向过程的区别](https://snailclimb.gitee.io/javaguide/#/docs/java/basis/Java基础知识?id=_211-面向对象和面向过程的区别)

- **面向过程** ：**面向过程性能比面向对象高。** 因为类调用时需要实例化，开销比较大，比较消耗资源，所以当性能是最重要的考量因素的时候，比如单片机、嵌入式开发、Linux/Unix 等一般采用面向过程开发。但是，**面向过程没有面向对象易维护、易复用、易扩展。**
- **面向对象** ：**面向对象易维护、易复用、易扩展。** 因为面向对象有封装、继承、多态性的特性，所以可以设计出低耦合的系统，使系统更加灵活、更加易于维护。但是，**面向对象性能比面向过程低**。

> 这个并不是根本原因，面向过程也需要分配内存，计算内存偏移量，Java 性能差的主要原因并不是因为它是面向对象语言，而是 Java 是半编译语言，最终的执行代码并不是可以直接被 CPU 执行的二进制机械码。
>
> 而面向过程语言大多都是直接编译成机器码在电脑上执行，并且其它一些面向过程的脚本语言性能也并不一定比 Java 好。

#### [2.1.2. 构造器 Constructor 是否可被 override?](https://snailclimb.gitee.io/javaguide/#/docs/java/basis/Java基础知识?id=_212-构造器-constructor-是否可被-override)

Constructor 不能被 override（重写）,但是可以 overload（重载）,所以你可以看到一个类中有多个构造函数的情况。

#### [2.1.3. 在 Java 中定义一个不做事且没有参数的构造方法的作用/在调用子列构造方法之前会先调用父类没有参数的构造方法目的](https://snailclimb.gitee.io/javaguide/#/docs/java/basis/Java基础知识?id=_213-在-java-中定义一个不做事且没有参数的构造方法的作用)

Java 程序在初始化子类的时候执行子类的构造方法之前，如果没有用 `super()`来调用父类特定的构造方法，则会调用父类中“没有参数的构造方法”。因此，如果父类中只定义了有参数的构造方法，而在子类的构造方法中又没有用 `super()`来调用父类中特定的构造方法，则编译时将发生错误，因为 Java 程序在父类中找不到没有参数的构造方法可供执行。解决办法是在父类里加上一个不做事且没有参数的构造方法。

#### [2.1.4. 成员变量与局部变量的区别有哪些？](https://snailclimb.gitee.io/javaguide/#/docs/java/basis/Java基础知识?id=_214-成员变量与局部变量的区别有哪些？)

1. 从语法形式上看:成员变量是属于类的，而局部变量是在代码块或方法中定义的变量或是方法的参数；成员变量可以被 public,private,static 等修饰符所修饰，而局部变量不能被访问控制修饰符及 static 所修饰；但是，成员变量和局部变量都能被 final 所修饰。
2. 从变量在内存中的存储方式来看:如果成员变量是使用`static`修饰的，那么这个成员变量是属于类的，如果没有使用`static`修饰，这个成员变量是属于实例的。而对象存在于堆内存，局部变量则存在于栈内存。
3. 从变量在内存中的生存时间上看:成员变量是对象的一部分，它随着对象的创建而存在，而局部变量随着方法的调用而自动消失。
4. 成员变量如果没有被赋初值:则会自动以类型的默认值而赋值（一种情况例外:被 final 修饰的成员变量也必须显式地赋值），而局部变量则不会自动赋值。

#### [2.1.5. 创建一个对象用什么运算符?对象实体与对象引用有何不同?](https://snailclimb.gitee.io/javaguide/#/docs/java/basis/Java基础知识?id=_215-创建一个对象用什么运算符对象实体与对象引用有何不同)

new 运算符，new 创建对象实例（对象实例在堆内存中），对象引用指向对象实例（对象引用存放在栈内存中）。一个对象引用可以指向 0 个或 1 个对象（一根绳子可以不系气球，也可以系一个气球）;一个对象可以有 n 个引用指向它（可以用 n 条绳子系住一个气球）。

#### [2.1.6. 一个类的构造方法的作用是什么? 若一个类没有声明构造方法，该程序能正确执行吗? 为什么?](https://snailclimb.gitee.io/javaguide/#/docs/java/basis/Java基础知识?id=_216-一个类的构造方法的作用是什么-若一个类没有声明构造方法，该程序能正确执行吗-为什么)

主要作用是**完成对类对象的初始化工作**。可以执行。因为一个类即使没有声明构造方法也会有默认的不带参数的构造方法。如果我们自己添加了类的构造方法（无论是否有参），Java 就不会再添加默认的无参数的构造方法了，这时候，就不能直接 new 一个对象而不传递参数了，所以我们一直在不知不觉地使用构造方法，这也是为什么我们在创建对象的时候后面要加一个括号（因为要调用无参的构造方法）。如果我们**重载了有参的构造方法，记得都要把无参的构造方法也写出来**（无论是否用到），因为这可以帮助我们在创建对象的时候少踩坑。

#### [2.1.7. 构造方法有哪些特性？](https://snailclimb.gitee.io/javaguide/#/docs/java/basis/Java基础知识?id=_217-构造方法有哪些特性？)

1. 名字与类名相同。
2. 没有返回值，但不能用 void 声明构造函数。
3. 生成类的对象时自动执行，无需调用。

#### [2.1.8. 对象的相等与指向他们的引用相等,两者有什么不同?](https://snailclimb.gitee.io/javaguide/#/docs/java/basis/Java基础知识?id=_219-对象的相等与指向他们的引用相等两者有什么不同)

对象的相等，比的是内存中存放的内容是否相等。而引用相等，比较的是他们指向的内存地址是否相等。

### [2.2. 面向对象三大特征](https://snailclimb.gitee.io/javaguide/#/docs/java/basis/Java基础知识?id=_22-面向对象三大特征)

#### [2.2.1. 封装](https://snailclimb.gitee.io/javaguide/#/docs/java/basis/Java基础知识?id=_221-封装)

封装是指把一个对象的**状态信息（也就是属性）隐藏在对象内部，不允许外部对象直接访问对象的内部信息**。但是可以**提供一些可以被外界访问的方法来操作属性**。就好像我们看不到挂在墙上的空调的内部的零件信息（也就是属性），但是可以通过遥控器（方法）来控制空调。如果属性不想被外界访问，我们大可不必提供方法给外界访问。但是如果一个类没有提供给外界访问的方法，那么这个类也没有什么意义了。就好像如果没有空调遥控器，那么我们就无法操控空凋制冷，空调本身就没有意义了。

#### [2.2.2. 继承](https://snailclimb.gitee.io/javaguide/#/docs/java/basis/Java基础知识?id=_222-继承)

不同类型的对象，相互之间经常有一定数量的共同点。例如，小明同学、小红同学、小李同学，都共享学生的特性（班级、学号等）。同时，每一个对象还定义了额外的特性使得他们与众不同。例如小明的数学比较好，小红的性格惹人喜爱；小李的力气比较大。继承是**使用已存在的类的定义作为基础建立新类**的技术，新类的定义可以增加新的数据或新的功能，也可以用父类的功能，但不能选择性地继承父类也就是拥有父类全部的属性和方法。通过使用继承，可以快速地创建新的类，可以提高代码的重用，程序的可维护性，节省大量创建新类的时间 ，提高我们的开发效率。

> 1. 子类拥有父类对象所有的属性和方法（包括私有属性和私有方法），但是父类中的私有属性和方法子类是无法访问，**只是拥有**。
> 2. 子类可以拥有自己属性和方法，即子类可以对父类进行扩展。
> 3. 子类可以用自己的方式实现父类的方法。(重写，不能重写构造方法)

#### [2.2.3. 多态](https://snailclimb.gitee.io/javaguide/#/docs/java/basis/Java基础知识?id=_223-多态)

多态，顾名思义，表示一个对象具有多种的状态。

具体表现为父类的引用指向子类的实例。

**多态的特点:**

- 对象类型和引用类型之间具有继承（类）/实现（接口）的关系；
- 引用类型变量发出的方法调用的到底是哪个类中的方法，必须在程序运行期间才能确定；
- 多态不能调用“只在子类存在但在父类不存在”的方法；
- 如果子类重写了父类的方法，真正执行的是子类覆盖的方法，如果子类没有覆盖父类的方法，执行的是父类的方法。

也就是说父类的引用执行的全是父类的方法，如果子类有重写方法，那么执行子类的方法

### [2.3. 修饰符](https://snailclimb.gitee.io/javaguide/#/docs/java/basis/Java基础知识?id=_23-修饰符)

#### [2.3.1. 在一个静态方法内调用一个非静态成员为什么是非法的?](https://snailclimb.gitee.io/javaguide/#/docs/java/basis/Java基础知识?id=_231-在一个静态方法内调用一个非静态成员为什么是非法的)

静态方法可以不通过对象进行调用，类名/对象名.方法名。

new一个对象，先将类中的静态方法的代码加载到方法去，然后再堆中创建对象，所以静态方法会随着类的加载而加载，当new一个对象时，对象存在于堆内存中，this关键字一般指该对象，如果没有new对象，直接通过类名访问类的静态方法也可以。

静态方法是属于类的，而动态方法或其他是属于实例对象的，在类加载时会分配内存，可以通过类名直接访问，**非静态成员(变量方法)属于类的对象**，所以**只有对象实例化之后才能存在**，需要通过类的对象去访问。

在一个类的静态成员去访问非静态成员之所以会出错是因为在类的非成员变量不存在的时候静态成员变量就存在了，访问一个内存不存在的东西当然会出错，而类在需要调用的时候才会被加载。

如果静态方法调用动态方法，那别人通过类名调用静态方法时实例对象可能并不存在，但是方法内又调用了对象的方法，由于对象不存在，所以动态方法肯定也不存在，程序会报错，所以java在编译期检查这种错误，避免运行时异常。

因此在静态方法里，不能调用其他非静态变量，也不可以访问非静态成员。

#### [2.3.2. 静态方法和实例方法有何不同](https://snailclimb.gitee.io/javaguide/#/docs/java/basis/Java基础知识?id=_232-静态方法和实例方法有何不同)

1. 在外部调用静态方法时，可以使用"类名.方法名"的方式，也可以使用"对象名.方法名"的方式。而实例方法只有后面这种方式。也就是说，调用静态方法可以无需创建对象。
2. 静态方法在访问本类的成员时，只允许访问静态成员（即静态成员变量和静态方法），而不允许访问实例成员变量和实例方法；实例方法则无此限制。

#### [2.4. 其它重要知识点](https://snailclimb.gitee.io/javaguide/#/docs/java/basis/Java基础知识?id=_24-其它重要知识点)

#### [2.4.1. String StringBuffer 和 StringBuilder 的区别是什么? String 为什么是不可变的?](https://snailclimb.gitee.io/javaguide/#/docs/java/basis/Java基础知识?id=_241-string-stringbuffer-和-stringbuilder-的区别是什么-string-为什么是不可变的)

**可变性**

简单的来说：`String` 类中使用 final 关键字修饰字符数组来保存字符串，`private final char[] value`，所以`String` 对象是不可变的。

> 在 Java 9 之后，String 、`StringBuilder` 与 `StringBuffer` 的实现改用 byte 数组存储字符串 `private final byte[] value`

而 `StringBuilder` 与 `StringBuffer` 都继承自 `AbstractStringBuilder` 类，在 `AbstractStringBuilder` 中也是使用字符数组保存字符串`char[] value` 但是没有用 `final` 关键字修饰，所以这两种对象都是可变的。

`StringBuilder` 与 `StringBuffer` 的构造方法都是调用父类构造方法也就是`AbstractStringBuilder` 实现的

**线程安全性**

`String` 中的对象是不可变的，也就可以理解为**常量，线程安全**。`AbstractStringBuilder` 是 `StringBuilder` 与 `StringBuffer` 的公共父类，定义了一些字符串的基本操作，如 `expandCapacity`、`append`、`insert`、`indexOf` 等公共方法。`StringBuffer` 对方法加了同步锁或者对调用的方法加了同步锁，所以是线程安全的。`StringBuilder` 并没有对方法进行加同步锁，所以是非线程安全的。

**性能**

每次对 `String` 类型进行改变的时候，都会生成一个新的 `String` 对象，然后将指针指向新的 `String` 对象。`StringBuffer` 每次都会对 `StringBuffer` 对象本身进行操作，而不是生成新的对象并改变对象引用。相同情况下使用 `StringBuilder` 相比使用 `StringBuffer` 仅能获得 10%~15% 左右的性能提升，但却要冒多线程不安全的风险。

**对于三者使用的总结：**

1. 操作少量的数据: 适用 `String`
2. 单线程操作字符串缓冲区下操作大量数据: 适用 `StringBuilder`
3. 多线程操作字符串缓冲区下操作大量数据: 适用 `StringBuffer`

#### [2.4.2. Object 类的常见方法总结](https://snailclimb.gitee.io/javaguide/#/docs/java/basis/Java基础知识?id=_242-object-类的常见方法总结)

Object 类是一个特殊的类，是所有类的父类。它主要提供了以下 11 个方法：

```java
public final native Class<?> getClass()//native方法，用于返回当前运行时对象的Class对象，使用了final关键字修饰，故不允许子类重写。

public native int hashCode() //native方法，用于返回对象的哈希码，主要使用在哈希表中，比如JDK中的HashMap。
public boolean equals(Object obj)//用于比较2个对象的内存地址是否相等，String类对该方法进行了重写用户比较字符串的值是否相等。

protected native Object clone() throws CloneNotSupportedException//naitive方法，用于创建并返回当前对象的一份拷贝。一般情况下，对于任何对象 x，表达式 x.clone() != x 为true，x.clone().getClass() == x.getClass() 为true。Object本身没有实现Cloneable接口，所以不重写clone方法并且进行调用的话会发生CloneNotSupportedException异常。

public String toString()//返回类的名字@实例的哈希码的16进制的字符串。建议Object所有的子类都重写这个方法。

public final native void notify()//native方法，并且不能重写。唤醒一个在此对象监视器上等待的线程(监视器相当于就是锁的概念)。如果有多个线程在等待只会任意唤醒一个。

public final native void notifyAll()//native方法，并且不能重写。跟notify一样，唯一的区别就是会唤醒在此对象监视器上等待的所有线程，而不是一个线程。

public final native void wait(long timeout) throws InterruptedException//native方法，并且不能重写。暂停线程的执行。注意：sleep方法没有释放锁，而wait方法释放了锁 。timeout是等待时间。

public final void wait(long timeout, int nanos) throws InterruptedException//多了nanos参数，这个参数表示额外时间（以毫微秒为单位，范围是 0-999999）。 所以超时的时间还需要加上nanos毫秒。

public final void wait() throws InterruptedException//跟之前的2个wait方法一样，只不过该方法一直等待，没有超时时间这个概念

protected void finalize() throws Throwable { }//实例被垃圾回收器回收的时候触发的操作
```

#### [2.4.3. == 与 equals(重要)](https://snailclimb.gitee.io/javaguide/#/docs/java/basis/Java基础知识?id=_243-与-equals重要)

**==** : 它的作用是判断两个对象的地址是不是相等。即，判断两个对象是不是同一个对象(基本数据类型==比较的是值，引用数据类型==比较的是内存地址)。

**equals()** : 它的作用也是判断两个对象是否相等。但它一般有两种使用情况：

- 情况 1：类没有覆盖 equals() 方法。则通过 equals() 比较该类的两个对象时，等价于通过“==”比较这两个对象。
- 情况 2：类覆盖了 equals() 方法。一般，我们都覆盖 equals() 方法来比较两个对象的内容是否相等；若它们的内容相等，则返回 true (即，认为这两个对象相等)。

#### [2.4.4. hashCode 与 equals (重要)](https://snailclimb.gitee.io/javaguide/#/docs/java/basis/Java基础知识?id=_244-hashcode-与-equals-重要)

面试官可能会问你：“你重写过 hashcode 和 equals 么，为什么重写 equals 时必须重写 hashCode 方法？”

##### [2.4.4.1. hashCode（）介绍](https://snailclimb.gitee.io/javaguide/#/docs/java/basis/Java基础知识?id=_2441-hashcode（）介绍)

hashCode() 的作用是获取哈希码，也称为散列码；它实际上是返回一个 int 整数。这个哈希码的作用是确定该对象在哈希表中的索引位置。hashCode() 定义在 JDK 的 Object.java 中，这就意味着 Java 中的任何类都包含有 hashCode() 函数。

散列表存储的是键值对(key-value)，它的特点是：能根据“键”快速的检索出对应的“值”。这其中就利用到了散列码！（可以快速找到所需要的对象）

##### [2.4.4.2. 为什么要有 hashCode](https://snailclimb.gitee.io/javaguide/#/docs/java/basis/Java基础知识?id=_2442-为什么要有-hashcode)

**我们先以“HashSet 如何检查重复”为例子来说明为什么要有 hashCode：** 当你把对象加入 HashSet 时，HashSet 会先计算对象的 hashcode 值来判断对象加入的位置，同时也会与该位置其他已经加入的对象的 hashcode 值作比较，如果没有相符的 hashcode，HashSet 会假设对象没有重复出现。但是如果发现有相同 hashcode 值的对象，这时会调用 `equals()`方法来检查 hashcode 相等的对象是否真的相同。如果两者相同，HashSet 就不会让其加入操作成功。如果不同的话，就会重新散列到其他位置。这样我们就大大减少了 equals 的次数，相应就大大提高了执行速度。

通过我们可以看出：`hashCode()` 的作用就是**获取哈希码**，也称为散列码；它实际上是返回一个 int 整数。这个**哈希码的作用**是**确定该对象在哈希表中的索引位置**。**`hashCode()`在散列表中才有用，在其它情况下没用**。在散列表中 hashCode() 的作用是获取对象的散列码，进而确定该对象在散列表中的位置。

> 上面的散列表，指的是：Java集合中本质是散列表的类，如HashMap，Hashtable，HashSet。

##### [2.4.4.3. hashCode（）与 equals（）的相关规定](https://snailclimb.gitee.io/javaguide/#/docs/java/basis/Java基础知识?id=_2443-hashcode（）与-equals（）的相关规定)

1. 如果两个对象相等，则 hashcode 一定也是相同的
2. 两个对象相等,对两个对象分别调用 equals 方法都返回 true
3. 两个对象有相同的 hashcode 值，它们也不一定是相等的
4. **因此，equals 方法被覆盖过，则 hashCode 方法也必须被覆盖**
5. hashCode() 的默认行为是对堆上的对象产生独特值。如果没有重写 hashCode()，则调用equals方法时会调用object类的hashcode方法，返回的时对象的地址是否相同，答案一定是否定的，则该 class 的两个对象无论如何都不会相等（即使这两个对象指向相同的数据）。

#### [2.4.5. Java 序列化中如果有些字段不想进行序列化，怎么办？](https://snailclimb.gitee.io/javaguide/#/docs/java/basis/Java基础知识?id=_245-java-序列化中如果有些字段不想进行序列化，怎么办？)

对于**不想进行序列化的变量，使用 transient 关键字修饰**。

transient 关键字的作用是：阻止实例中那些用此关键字修饰的的变量序列化；当对象被反序列化时，被 transient 修饰的变量值不会被持久化和恢复。transient 只能修饰变量，不能修饰类和方法。



## [3. Java 核心技术](https://snailclimb.gitee.io/javaguide/#/docs/java/basis/Java基础知识?id=_3-java-核心技术)

### [3.1. 反射机制](https://snailclimb.gitee.io/javaguide/#/docs/java/basis/Java基础知识?id=_31-反射机制)

![image-20210320234130824](C:\Users\94307\OneDrive - zju.edu.cn\learnbm\JAVA\学习笔记\image-20210320234130824.png)

JAVA 反射机制是**在运行状态中**，对于任意一个类，都能够知道这个类的所有属性和方法；对于任意一个对象，都能够调用它的任意一个方法和属性；这种**动态获取的信息以及动态调用对象的方法的功能称为 java 语言的反射机制**。

用反射的方式新建一个类：字节码文件名.newInstance()

**好处：**

- 反射可以在程序运行过程中，获取一个类的属性、方法、构造方法、和全类名

- 可以在程序的运行过程中，操作这些对象，动态加载类
- 可以解耦，降低程序的耦合，提高程序的可扩展性
- 用于框架，在不改变当前类的代码，可以创建任意类的对象调用任意类的方法
  - 将需要创建的对象的全类名和需要执行的方法定义在配置文件中
  - 在程序中加载读取配置文件（类加载器不仅可以找到类也可以找到配置文件）
  - 使用反射技术来加载文件进内存
  - 创建对象
  - 执行方法

**坏处：**

- 性能瓶颈，反射相当于一些列解释操作，通知JVM要做的事情，性能比直接的java代码要慢很多
- 安全问题，动态操作改变类的属性同时也增加了类的安全隐患

**使用场景：**

- 模块化的开发，通过反射去调用对应的字节码；
- 我们在使用 JDBC 连接数据库时使用 `Class.forName()`通过反射加载数据库的驱动程序；

- 动态代理设计模式也采用了反射机制；
- 动态配置实例的属性；

-  Spring／Hibernate 等框架也大量使用到了反射机制
- Spring 框架的 IOC（动态加载管理 Bean）创建对象以及 AOP（动态代理）功能都和反射有联系；

#### [获取 Class 对象的四种方式](https://snailclimb.gitee.io/javaguide/#/docs/java/basis/反射机制?id=获取-class-对象的四种方式)

如果我们动态获取到这些信息，我们需要依靠 Class 对象。Class 类对象将一个类的方法、变量等信息告诉运行的程序。Java 提供了四种方式获取 Class 对象:

**1.知道具体类的情况下可以使用：**

```java
Class alunbarClass = TargetObject.class;
```

但是我们一般是不知道具体类的，基本都是通过遍历包下面的类来获取 Class 对象，通过此方式获取**Class对象不会进行初始化**

**2.通过 `Class.forName()`传入类的路径获取：**

```java
Class alunbarClass1 = Class.forName("cn.javaguide.TargetObject");
```

Class.forName(className)方法，内部实际调用的是一个native方法 forName0(className, true, ClassLoader.getClassLoader(caller), caller);

第2个boolean参数表示类是否需要初始化，**Class.forName(className)默认是需要初始化。**

一旦初始化，就会触发目标对象的 static块代码执行，**static参数也会被再次初始化**。

**3.通过对象实例`instance.getClass()`获取：**

```java
Employee e = new Employee();
Class alunbarClass2 = e.getClass();Copy to clipboardErrorCopied
```

**4.通过类加载器`xxxClassLoader.loadClass()`传入类路径获取**

```java
class clazz = ClassLoader.LoadClass("cn.javaguide.TargetObject");
```

通过类加载器获取**Class对象不会进行初始化**，意味着不进行包括初始化等一些列步骤，**静态块和静态对象不会得到执行**



#### [静态编译和动态编译](https://snailclimb.gitee.io/javaguide/#/docs/java/basis/反射机制?id=静态编译和动态编译)

- **静态编译：** 在编译时确定类型，绑定对象
- **动态编译：** 运行时确定类型，绑定对象

### [3.2. 异常](https://snailclimb.gitee.io/javaguide/#/docs/java/basis/Java基础知识?id=_32-异常)

异常，就是不正常的意思。在生活中:医生说,你的身体某个部位有异常,该部位和正常相比有点不同,该部位的功能将 受影响.在程序中的意思就是：

> 异常 ：指的是程序在执行过程中，出现的非正常的情况，最终会导致JVM的非正常停止。

在Java等面向对象的编程语言中，异常本身是一个类，**产生异常就是创建异常对象并抛出了一个异常对象**。

> Java处理异常的方式是**中断处理**。异常指的并不是语法错误,语法错了,编译不通过,不会产生字节码文件,根本不能运行.

#### [3.2.1. Java 异常类层次结构图](https://snailclimb.gitee.io/javaguide/#/docs/java/basis/Java基础知识?id=_321-java-异常类层次结构图)


![img](https://guide-blog-images.oss-cn-shenzhen.aliyuncs.com/2020-12/Java%E5%BC%82%E5%B8%B8%E7%B1%BB%E5%B1%82%E6%AC%A1%E7%BB%93%E6%9E%84%E5%9B%BE.png)

图片来自：https://simplesnippets.tech/exception-handling-in-java-part-1/

![img](https://guide-blog-images.oss-cn-shenzhen.aliyuncs.com/2020-12/Java%E5%BC%82%E5%B8%B8%E7%B1%BB%E5%B1%82%E6%AC%A1%E7%BB%93%E6%9E%84%E5%9B%BE2.png)

图片来自：https://chercher.tech/java-programming/exceptions-java

在 Java 中，所有的异常都有一个共同的祖先 `java.lang` 包中的 `Throwable` 类。`Throwable` 类有两个重要的子类 `Exception`（异常）和 `Error`（错误）。`Exception` 能被程序本身处理(`try-catch`)， `Error` 是无法处理的(只能尽量避免)。

`Exception` 和 `Error` 二者都是 Java 异常处理的重要子类，各自都包含大量子类。

- **`Exception`** :**程序本身可以处理的异常**，可以通过 `catch` 来进行捕获。`Exception` 又可以分为 受检查异常(必须处理) 和 不受检查异常(可以不处理)。
- **`Error`** ：**`Error` 属于程序无法处理的错误** ，我们没办法通过 `catch` 来进行捕获 。例如，Java 虚拟机运行错误（`Virtual MachineError`）、虚拟机内存不够错误(`OutOfMemoryError`)、类定义错误（`NoClassDefFoundError`）等 。这些异常发生时，Java 虚拟机（JVM）一般会选择线程终止。

**受检查异常**checked异常

Java 代码在编译过程中，如果受检查异常没有被 `catch`/`throw` 处理的话，就没办法通过编译 。比如下面这段 IO 操作的代码。

![check-exception](https://guide-blog-images.oss-cn-shenzhen.aliyuncs.com/2020-12/check-exception.png)

除了`RuntimeException`及其子类以外，其他的`Exception`类及其子类都属于受检查异常 。常见的受检查异常有： IO 相关的异常、`ClassNotFoundException` 、`SQLException`...。

**不受检查异常**runtime异常

Java 代码在编译过程中 ，我们即使不处理不受检查异常也可以正常通过编译。

`RuntimeException` 及其子类都统称为非受检查异常，例如：`NullPointerException`、`NumberFormatException`（字符串转换为数字）、`ArrayIndexOutOfBoundsException`（数组越界）、`ClassCastException`（类型转换错误）、`ArithmeticException`（算术错误）等。



**受检查异常例如IOException如果受检查没有try/catch的话是通过不了编译的，不受检查异常例如RuntimeException几十不处理不受检查也可以通过编译**



#### [3.2.2. Throwable 类常用方法](https://snailclimb.gitee.io/javaguide/#/docs/java/basis/Java基础知识?id=_322-throwable-类常用方法)

- **`public void printStackTrace()`** :打印异常的详细信息。
  包含了异常的类型,异常的原因,还包括异常出现的位置,在开发和调试阶段,都得使用printStackTrace。 
- **`public String getMessage()`** :获取发生异常的原因。
  提示给用户的时候,就提示错误原因。 
- **`public String toString()`** :获取异常的类型和异常描述信息(不用)
- **`public string getLocalizedMessage()`**:返回异常对象的本地化信息。使用 `Throwable` 的子类覆盖这个方法，可以生成本地化信息。如果子类没有覆盖该方法，则该方法返回的信息与 `getMessage（）`返回的结果相同

#### [3.2.3. try-catch-finally](https://snailclimb.gitee.io/javaguide/#/docs/java/basis/Java基础知识?id=_323-try-catch-finally)

- **`try`块：** 用于捕获异常。其后可接零个或多个 `catch` 块，如果没有 `catch` 块，则必须跟一个 `finally` 块。
- **`catch`块：** 用于处理 try 捕获到的异常。
- **`finally` 块：** 无论是否捕获或处理异常，`finally` 块里的语句都会被执行。当在 `try` 块或 `catch` 块中遇到 `return` 语句时，`finally` 语句块将在方法返回之前被执行。

**在以下 3 种特殊情况下，`finally` 块不会被执行：**

1. 在 `try` 或 `finally `块中用了 `System.exit(int)`退出程序。但是，如果 `System.exit(int)` 在异常语句之后，`finally` 还是会被执行
2. 程序所在的线程死亡。
3. 关闭 CPU。

下面这部分内容来自 issue:https://github.com/Snailclimb/JavaGuide/issues/190。

**注意：** 当 try 语句和 finally 语句中都有 return 语句时，在方法返回之前，finally 语句的内容将被执行，并且 finally 语句的返回值将会覆盖原始的返回值。如下：

```java
public class Test {
    public static int f(int value) {
        try {
            return value * value;
        } finally {
            if (value == 2) {
                return 0;
            }
        }
    }
}Copy to clipboardErrorCopied
```

如果调用 `f(2)`，返回值将是 0，因为 finally 语句的返回值覆盖了 try 语句块的返回值。

#### [3.2.4. 使用 `try-with-resources` 来代替`try-catch-finally`](https://snailclimb.gitee.io/javaguide/#/docs/java/basis/Java基础知识?id=_324-使用-try-with-resources-来代替try-catch-finally)

1. **适用范围（资源的定义）：** 任何实现 `java.lang.AutoCloseable`或者 `java.io.Closeable` 的对象
2. **关闭资源和 final 的执行顺序：** 在 `try-with-resources` 语句中，任何 catch 或 finally 块在声明的资源关闭后运行

《Effecitve Java》中明确指出：

> 面对必须要关闭的资源，我们总是应该优先使用 `try-with-resources` 而不是`try-finally`。随之产生的代码更简短，更清晰，产生的异常对我们也更有用。`try-with-resources`语句让我们更容易编写必须要关闭的资源的代码，若采用`try-finally`则几乎做不到这点。

Java 中类似于`InputStream`、`OutputStream` 、`Scanner` 、`PrintWriter`等的资源都需要我们调用`close()`方法来手动关闭，一般情况下我们都是通过`try-catch-finally`语句来实现这个需求，如下：

```java
        //读取文本文件的内容
        Scanner scanner = null;
        try {
            scanner = new Scanner(new File("D://read.txt"));
            while (scanner.hasNext()) {
                System.out.println(scanner.nextLine());
            }
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } finally {
            if (scanner != null) {
                scanner.close();
            }
        }Copy to clipboardErrorCopied
```

使用 Java 7 之后的 `try-with-resources` 语句改造上面的代码:

```java
try (Scanner scanner = new Scanner(new File("test.txt"))) {
    while (scanner.hasNext()) {
        System.out.println(scanner.nextLine());
    }
} catch (FileNotFoundException fnfe) {
    fnfe.printStackTrace();
}Copy to clipboardErrorCopied
```

当然多个资源需要关闭的时候，使用 `try-with-resources` 实现起来也非常简单，如果你还是用`try-catch-finally`可能会带来很多问题。

通过使用分号分隔，可以在`try-with-resources`块中声明多个资源。

```java
try (BufferedInputStream bin = new BufferedInputStream(new FileInputStream(new File("test.txt")));
             BufferedOutputStream bout = new BufferedOutputStream(new FileOutputStream(new File("out.txt")))) {
            int b;
            while ((b = bin.read()) != -1) {
                bout.write(b);
            }
        }
        catch (IOException e) {
            e.printStackTrace();
        }
```

**finally**：有一些特定的代码无论异常是否发生，都需要执行。另外，因为异常会引发程序跳转，导致有些语句执行 不到。而finally就是解决这个问题的，在finally代码块中存放的代码都是一定会被执行的。

### [3.3. 多线程](https://snailclimb.gitee.io/javaguide/#/docs/java/basis/Java基础知识?id=_33-多线程)

#### [3.3.1. 简述线程、程序、进程的基本概念。以及他们之间关系是什么?](https://snailclimb.gitee.io/javaguide/#/docs/java/basis/Java基础知识?id=_331-简述线程、程序、进程的基本概念。以及他们之间关系是什么)

**线程**(thread)：与进程相似，但线程是一个比进程更小的执行单位。一个进程在其执行的过程中可以产生多个线程。与进程不同的是同类的**多个线程共享同一块内存空间和一组系统资源**，所以系统在产生一个线程，或是在各个线程之间作切换工作时，负担要比进程小得多，也正因为如此，**线程也被称为轻量级进程**。

**程序**(programme)：是含有指令和数据的文件，被存储在磁盘或其他的数据存储设备中，也就是说**程序是静态的代码**。

**进程**(process)：是程序的一次执行过程，是系统运行程序的基本单位，因此进程是动态的。**系统运行一个程序即是一个进程从创建**，运行到消亡的过程。简单来说，**一个进程就是一个执行中的程序**，它在计算机中一个指令接着一个指令地执行着，同时，每个进程还占有某些系统资源如 CPU 时间，内存空间，文件，输入输出设备的使用权等等。换句话说，当程序在执行时，将会被操作系统载入内存中。 线程是进程划分成的更小的运行单位。线程和进程最大的不同在于基本上**各进程是独立的，而各线程则不一定，因为同一进程中的线程极有可能会相互影响**。从另一角度来说，进程属于操作系统的范畴，主要是同一段时间内，可以同时执行一个以上的程序，而线程则是在同一程序内几乎同时执行一个以上的程序段。

#### [3.3.2. 线程有哪些基本状态?](https://snailclimb.gitee.io/javaguide/#/docs/java/basis/Java基础知识?id=_332-线程有哪些基本状态)

Java 线程在运行的生命周期中的指定时刻只可能处于下面 6 种不同状态的其中一个状态（图源《Java 并发编程艺术》4.1.4 节）。

| 状态名称     | 说明                                                         |
| ------------ | ------------------------------------------------------------ |
| NEW          | 初始状态，线程被构建，但是还没有调用 start方法               |
| RUNNABLE     | 运行状态，Java线程将操作系统中的就绪和运行两种状态笼统地称作“运行中” |
| BLOCKED      | 阻塞状态，表示线程阻塞于锁                                   |
| WAITING      | 等待状态，表示线程进入等待状态，进入该状态表示当前线程需要等待其他线程做出一些特定动作（通知或中断） |
| TIME WAITING | 超时等待状态，该状态不同于 WAITING,它是可以在指定的时间自行返回的 |
| TERMINATED   | 终止状态，表示当前线程已经执行完毕                           |

线程在生命周期中并不是固定处于某一个状态而是随着代码的执行在不同状态之间切换。Java 线程状态变迁如下图所示（图源《Java 并发编程艺术》4.1.4 节）：

![Java线程状态变迁](https://my-blog-to-use.oss-cn-beijing.aliyuncs.com/19-1-29/Java%20%E7%BA%BF%E7%A8%8B%E7%8A%B6%E6%80%81%E5%8F%98%E8%BF%81.png)

由上图可以看出：

线程创建之后它将处于 **NEW（新建）** 状态，调用 `start()` 方法后开始运行，线程这时候处于 **READY（可运行）** 状态。可运行状态的线程获得了 cpu 时间片（timeslice）后就处于 **RUNNING（运行）** 状态。

> 操作系统隐藏 Java 虚拟机（JVM）中的 READY 和 RUNNING 状态，它只能看到 RUNNABLE 状态（图源：[HowToDoInJava](https://howtodoinjava.com/)：[Java Thread Life Cycle and Thread States](https://howtodoinjava.com/java/multi-threading/java-thread-life-cycle-and-thread-states/)），所以 Java 系统一般将这两个状态统称为 **RUNNABLE（运行中）** 状态 。

![RUNNABLE-VS-RUNNING](C:\Users\94307\OneDrive - zju.edu.cn\learnbm\JAVA\学习笔记\RUNNABLE-VS-RUNNING.png)

当线程执行 `wait()`方法之后，线程进入 **WAITING（等待）** 状态。进入等待状态的线程需要依靠其他线程的通知才能够返回到运行状态，而 **TIME_WAITING(超时等待)** 状态相当于在等待状态的基础上增加了超时限制，比如通过 `sleep（long millis）`方法或 `wait（long millis）`方法可以将 Java 线程置于 TIMED WAITING 状态。当超时时间到达后 Java 线程将会返回到 RUNNABLE 状态。当线程调用同步方法时，在没有获取到锁的情况下，线程将会进入到 **BLOCKED（阻塞）** 状态。线程在执行 Runnable 的`run()`方法之后将会进入到 **TERMINATED（终止）** 状态。

#### 3.3.3 线程安全

如果有多个线程在同时运行，而这些线程可能会同时运行一个线程类。程序每次运行结果和单线程运行的结果是一样的，而且其他的变量的值也和预期的是一样的，就是线程安全的。

线程安全问题都是由**全局变量及静态变量**引起的。若每个线程中对全局变量、静态变量**只有读操作，而无写操作**，一般来说，这个全局变量是线程安全的；若有多个线程同时执行写操作，一般都需要**考虑线程同步**， 否则的话就可能影响线程安全。

#### 3.3.4 线程同步

#####3.3.4.1 同步代码块 

synchronized 关键字可以用于方法中的某个区块中，表示只对这个区块的资源实行互斥访问。

```
synchronized(同步锁){	
	需要同步操作的代码
}
```

同步锁: 对象的同步锁只是一个概念,可以想象为在对象上标记了一个锁.
- 锁对象 可以是任意类型。 

- 多个线程对象 要使用同一把锁。

注意:在任何时候,**最多允许一个线程拥有同步锁**,谁拿到锁就进入代码块,其他的线程只能在外等着 (BLOCKED)。

#####3.3.4.2 同步方法

同步方法:使用synchronized修饰的方法,就叫做同步方法,保证A线程执行该方法的时候,其他线程只能在方法外 等着。

```
public synchronized void method(){ 
	可能会产生线程安全问题的代码
}
```

同步锁是谁? 

- 对于非static方法,同步锁就是this。 

- 对于static方法,我们使用当前方法所在类的字节码对象(类名.class)。

#####3.3.4.3 锁机制 Lock锁

java.util.concurrent.locks.Lock 机制提供了比synchronized代码块和synchronized方法更广泛的锁定操作,

同步代码块/同步方法具有的功能Lock都有,除此之外更强大,更体现面向对象。 

Lock锁也称同步锁，加锁与释放锁方法化了，如下：

- public void lock() :加同步锁。 

- public void unlock() :释放同步锁。
