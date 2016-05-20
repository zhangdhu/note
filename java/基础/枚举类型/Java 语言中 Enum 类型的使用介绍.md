#Java 语言中 Enum 类型的使用介绍

Enum 类型的介绍
枚举类型（Enumerated Type） 很早就出现在编程语言中，它被用来将一组类似的值包含到一种类型当中。而这种枚举类型的名称则会被定义成独一无二的类型描述符，在这一点上和常量的定义相似。不过相比较常量类型，枚举类型可以为申明的变量提供更大的取值范围。
举个例子来说明一下，如果希望为彩虹描绘出七种颜色，你可以在 Java 程序中通过常量定义方式来实现。
清单 1. 常量定义
 Public static class RainbowColor { 
    
    // 红橙黄绿青蓝紫七种颜色的常量定义
    public static final int RED = 0; 
    public static final int ORANGE = 1; 
    public static final int YELLOW = 2; 
    public static final int GREEN = 3; 
    public static final int CYAN = 4; 
    public static final int BLUE = 5; 
    public static final int PURPLE = 6; 
 }
使用的时候，你可以在程序中直接引用这些常量。但是，这种方式还是存在着一些问题。
类型不安全
由于颜色常量的对应值是整数形，所以程序执行过程中很有可能给颜色变量传入一个任意的整数值，导致出现错误。
没有命名空间
由于颜色常量只是类的属性，当你使用的时候不得不通过类来访问。
一致性差
因为整形枚举属于编译期常量，所以编译过程完成后，所有客户端和服务器端引用的地方，会直接将整数值写入。这样，当你修改旧的枚举整数值后或者增加新的枚举值后，所有引用地方代码都需要重新编译，否则运行时刻就会出现错误。
类型无指意性
由于颜色枚举值仅仅是一些无任何含义的整数值，如果在运行期调试时候，你就会发现日志中有很多魔术数字，但除了程序员本身，其他人很难明白其奥秘。
回页首
如何定义 Enum 类型
为了改进 Java 语言在这方面的不足弥补缺陷，5.0 版本 SDK 发布时候，在语言层面上增加了枚举类型。枚举类型的定义也非常的简单，用 enum 关键字加上名称和大括号包含起来的枚举值体即可，例如上面提到的彩虹颜色就可以用新的 enum 方式来重新定义：
 enum RainbowColor { RED, ORANGE, YELLOW, GREEN, CYAN, BLUE, PURPLE }
从上面的定义形式来看，似乎 Java 中的枚举类型很简单，但实际上 Java 语言规范赋予枚举类型的功能非常的强大，它不仅是简单地将整形数值转换成对象，而是将枚举类型定义转变成一个完整功能的类定义。这种类型定义的扩展允许开发者给枚举类型增加任何方法和属性，也可以实现任意的接口。另外，Java 平台也为 Enum 类型提供了高质量的实现，比如默认实现 Comparable 和 Serializable 接口，让开发者一般情况下不用关心这些细节。
回到本文的主题上来，引入枚举类型到底能够给我们开发带来什么样好处呢？一个最直接的益处就是扩大 switch 语句使用范围。5.0 之前，Java 中 switch 的值只能够是简单类型，比如 int、byte、short、char, 有了枚举类型之后，就可以使用对象了。这样一来，程序的控制选择就变得更加的方便，看下面的例子：
清单 2. 定义 Enum 类型
 // 定义一周七天的枚举类型         
 public enum WeekDayEnum { Mon, Tue, Wed, Thu, Fri, Sat, Sun } 

 // 读取当天的信息
 WeekDayEnum today = readToday(); 
 
 // 根据日期来选择进行活动
 switch(today) { 
  Mon: do something; break; 
  Tue: do something; break; 
  Wed: do something; break; 
  Thu: do something; break; 
  Fri: do something; break; 
  Sat: play sports game; break; 
  Sun: have a rest; break; 
 }

对于这些枚举的日期，JVM 都会在运行期构造成出一个简单的对象实例一一对应。这些对象都有唯一的 identity，类似整形数值一样，switch 语句就根据此来进行执行跳转。
回页首
如何定制 Enum 类型
除了以上这种最常见的枚举定义形式外，如果需要给枚举类型增加一些复杂功能，也可以通过类似 class 的定义来给枚举进行定制。比如要给 enum 类型增加属性，可以像下面这样定义：
清单 3. 定制枚举类型
 // 定义 RSS(Really Simple Syndication) 种子的枚举类型
 public enum NewsRSSFeedEnum { 
    // 雅虎头条新闻 RSS 种子
    YAHOO_TOP_STORIES("http://rss.news.yahoo.com/rss/topstories"), 
    
    //CBS 头条新闻 RSS 种子
    CBS_TOP_STORIES("http://feeds.cbsnews.com/CBSNewsMain?format=xml"), 
    
    // 洛杉矶时报头条新闻 RSS 种子
    LATIMES_TOP_STORIES("http://feeds.latimes.com/latimes/news?format=xml"); 
        
    // 枚举对象的 RSS 地址的属性
    private String rss_url; 
        
    // 枚举对象构造函数
    private NewsRSSFeedEnum(String rss) { 
        this.rss_url = rss; 
    } 
        
    // 枚举对象获取 RSS 地址的方法
    public String getRssURL() { 
        return this.rss_url; 
    } 
 }
上面头条新闻的枚举类型增加了一个 RSS 地址的属性 , 记录头条新闻的访问地址。同时，需要外部传入 RSS 访问地址的值，因而需要定义一个构造函数来初始化此属性。另外，还需要向外提供方法来读取 RSS 地址。
回页首
如何避免错误使用 Enum
不过在使用 Enum 时候有几个地方需要注意：
enum 类型不支持 public 和 protected 修饰符的构造方法，因此构造函数一定要是 private 或 friendly 的。也正因为如此，所以枚举对象是无法在程序中通过直接调用其构造方法来初始化的。
定义 enum 类型时候，如果是简单类型，那么最后一个枚举值后不用跟任何一个符号；但如果有定制方法，那么最后一个枚举值与后面代码要用分号';'隔开，不能用逗号或空格。
由于 enum 类型的值实际上是通过运行期构造出对象来表示的，所以在 cluster 环境下，每个虚拟机都会构造出一个同义的枚举对象。因而在做比较操作时候就需要注意，如果直接通过使用等号 ( ‘ == ’ ) 操作符，这些看似一样的枚举值一定不相等，因为这不是同一个对象实例。
看下面的这个例子：
清单 4. 避免错误使用 Enum 示例
 // 定义一个一周七天的枚举类型
 package example.enumeration.codes; 

 public enum WeekDayEnum { 
    Mon(1), Tue(2), Wed(3), Thu(4), Fri(5), Sat(6), Sun(7); 

    private int index; 

    WeekDayEnum(int idx) { 
        this.index = idx; 
    } 

    public int getIndex() { 
        return index; 
    } 
 } 

 // 客户端程序，将一个枚举值通过网络传递给服务器端
 package example.enumeration.codes; 

 import java.io.IOException; 
 import java.io.ObjectOutputStream; 
 import java.io.OutputStream; 
 import java.net.InetSocketAddress; 
 import java.net.Socket; 
 import java.net.UnknownHostException; 

 public class EnumerationClient { 

    public static void main(String... args) throws UnknownHostException, IOException { 
        Socket socket = new Socket(); 
  // 建立到服务器端的连接
        socket.connect(new InetSocketAddress("127.0.0.1", 8999)); 
    // 从连接中得到输出流
        OutputStream os = socket.getOutputStream(); 
        ObjectOutputStream oos = new ObjectOutputStream(os); 
  // 将星期五这个枚举值传递给服务器端
        oos.writeObject(WeekDayEnum.Fri); 
        oos.close(); 
        os.close(); 
        socket.close(); 
    } 
 } 

 // 服务器端程序，将从客户端收到的枚举值应用到逻辑处理中
 package example.enumeration.codes; 

 import java.io.*; 
 import java.net.ServerSocket; 
 import java.net.Socket; 

 public class EnumerationServer { 

    public static void main(String... args) throws IOException, ClassNotFoundException { 
        ServerSocket server = new ServerSocket(8999); 
  // 建立服务器端的网络连接侦听
        Socket socket = server.accept(); 
  // 从连接中获取输入流
        InputStream is = socket.getInputStream(); 
        ObjectInputStream ois = new ObjectInputStream(is); 
  // 读出客户端传递来的枚举值
        WeekDayEnum day = (WeekDayEnum) ois.readObject(); 
  // 用值比较方式来对比枚举对象
        if (day == WeekDayEnum.Fri) { 
            System.out.println("client Friday enum value is same as server's"); 
        } else if (day.equals(WeekDayEnum.Fri)) { 
            System.out.println("client Friday enum value is equal to server's"); 
        } else { 
            System.out.println("client Friday enum value is not same as server's"); 
        } 
        
  // 用 switch 方式来比较枚举对象
        switch (day) { 
            case Mon: 
                System.out.println("Do Monday work"); 
                break; 
            case Tue: 
                System.out.println("Do Tuesday work"); 
                break; 
            case Wed: 
                System.out.println("Do Wednesday work"); 
                break; 
            case Thu: 
                System.out.println("Do Thursday work"); 
                break; 
            case Fri: 
                System.out.println("Do Friday work"); 
                break; 
            case Sat: 
                System.out.println("Do Saturday work"); 
                break; 
            case Sun: 
                System.out.println("Do Sunday work"); 
                break; 
            default: 
                System.out.println("I don't know which is day"); 
                break; 
        } 
        
        ois.close(); 
        is.close(); 
        socket.close(); 
    } 
 }
打印结果如下：
 client Friday enum value is same as server's 
 Do Friday work
通过程序执行结果，我们能够发现在分布式条件下客户端和服务端的虚拟机上都生成了一个枚举对象，即使看起来一样的 Fri 枚举值，如果使用等号‘ == ’进行比较的话会出现不等的情况。而 switch 语句则是通过 equal 方法来比较枚举对象的值，因此当你的枚举对象较复杂时候，你就需要小心 override 与比较相关的方法，防止出现值比较方面的错误。
回页首
Enum 相关工具类
JDK5.0 中在增加 Enum 类的同时，也增加了两个工具类 EnumSet 和 EnumMap，这两个类都放在 java.util 包中。EnumSet 是一个针对枚举类型的高性能的 Set 接口实现。EnumSet 中装入的所有枚举对象都必须是同一种类型，在其内部，是通过 bit-vector 来实现，也就是通过一个 long 型数。EnumSet 支持在枚举类型的所有值的某个范围中进行迭代。回到上面日期枚举的例子上：
 enum WeekDayEnum { Mon, Tue, Wed, Thu, Fri, Sat, Sun }
你能够在每周七天日期中进行迭代，EnumSet 类提供一个静态方法 range 让迭代很容易完成：
 for(WeekDayEnum day : EnumSet.range(WeekDayEnum.Mon, WeekDayEnum.Fri)) { 
     System.out.println(day); 
 }
打印结果如下：
 Mon 
 Tue 
 Wed 
 Thu 
 Fri
EnumSet 还提供了很多个类型安全的获取子集的 of 方法，使你很容易取得子集：
 EnumSet<WeekDayEnum> subset = EnumSet.of(WeekDayEnum.Mon, WeekDayEnum.Wed); 
      for (WeekDayEnum day : subset) { 
          System.out.println(day);  
      }
打印结果如下：
 Mon 
 Wed
与 EnumSet 类似，EnumMap 也是一个高性能的 Map 接口实现，用来管理使用枚举类型作为 keys 的映射表，内部是通过数组方式来实现。EnumMap 将丰富的和安全的 Map 接口与数组快速访问结合到一起，如果你希望要将一个枚举类型映射到一个值，你应该使用 EnumMap。看下面的例子：
清单 5. EnumMap 示例
 // 定义一个 EnumMap 对象，映射表主键是日期枚举类型，值是颜色枚举类型
 private static Map<WeekDayEnum, RainbowColor> schema = 
            new EnumMap<WeekDayEnum, RainbowColor>(WeekDayEnum.class); 
    
 static{ 
    // 将一周的每一天与彩虹的某一种色彩映射起来
    for (int i = 0; i < WeekDayEnum.values().length; i++) { 
        schema.put(WeekDayEnum.values()[i], RainbowColor.values()[i]); 
    } 
 } 
 System.out.println("What is the lucky color today?"); 
 System.out.println("It's " + schema.get(WeekDayEnum.Sat));
当你询问周六的幸运色彩时候，会得到蓝色：
清单 6. 运行结果
 What is the lucky color today? 
 It's BLUE
回页首
结束语
Enum 类型提出给 JAVA 编程带了了极大的便利，让程序的控制更加的容易，也不容易出现错误。所以在遇到需要控制程序流程时候，可以多想想是否可以利用 enum 来实现。
