# coreJava笔记 7-25
## 一、JavaSE
* Java环境
    * 安装jdk
        * 包含了jre
          * 包含了jvm
* 环境变量
    * JAVA_HOME  安装jdk的目录
          * C:\Program Files\Java\jdk1.7.0_45
    * bin目录(java工具集)
        * 如javac、java
    * jstack,jps,jconsole等等可以帮助我们监控jvm的使用情况
    * src.zip
        * jdk提供给我们的源代码
    * jre/lib目录/rt.jar（java源代码编译之后的文件打包，运行的时候调用此文件而非src.zip压缩包里的源代码）
	     （保存是.java文件，编译之后是.class文件，打包之后就是.jar文件）
    * path（编译)
        * 命令行中  set path=JAVA_HOME目录\bin(只在该命令行有效)
        * 系统中设置
        * 进行编译
            * 进入.java文件所在的目录
            * javac  文件名.java
            * 产生.class文件(java字节码）
        * 文本编辑工具 EditPlus、UE
    * 运行
        * 进入目录
            * java  .class文件的文件名（包含主函数的)
    * 如果不在该目录下是否可以运行
        * classpath环境变量（用的时候设置，不会设置到系统中)
            * 寻找类的路径 默认值是. 代表当前目录，即在当前目录下找.class文件
            * set classpath=.;e:\aa（例，中间的分号表示可配置多个路径）
* 类的加载机制
    * java的类加载都要通过类加载器
    * 类加载的种类
        * 根类加载器
            * 负责加载jre/lib/rt.jar中的类  jdk提供的所有的类
        * 扩展类加载器
            * 负责加载jre/lib/ext/*.jar中的类
        * 应用类加载器
            * 负责加载classpath下能找到的类
    * 加载类的时候总是先从根类加载器找类，没有才去扩展类加载器，还没有才去classpath下找类
* 如果你写一个类java.lang.String，有用吗？没用

* 开发工具eclipse(下载对应版本    jee版)
    * 先安装jdk
    * 解压eclipse(找到可执行文件双击启动即可)
    * 新建项目
        * file---new-->project--javaproject
        * 在src目录下右击new--->class
    * 一些习惯 
        * 一个类就是一个单独的.java文件
        * 编译的时候javac 文件名，运行的时候java 类名，因此一般文件名就是类名.java
        * 如果类是public 的 ，那么文件必须是类名.java
        * 一个文件中只能有一个public的类对吗?对的
    * 了解包
        * 包是类名的一部分
        * 一般来说包命名的时候会包含 公司名.项目名.模块名.小组名.类名
        * 如果命名了包
            * 编译时刻
                * javac -d . 类名.java
            * 运行时刻
                * java 包名.类名.java
        * 包看起来就是一个文件夹（对于.class文件是类名的一部分)

    * 导入项目
        * file--import--general--Existing projects into...
        * 如果jdk版本和目录不一样项目会报错
            * 右击项目名称
                ->properties->JavaBuilderPath->Libraries->
            * 没有bind的jdk选中-->remove
            * add libaray -->jre system libaray
    * 如何在编译器中直接看java中某方法的源代码

##二、Javaoop
* 面向对象：**依赖于抽象而不依赖于具体**
* 类和对象
    * 类
        * 数据抽象（变量来表示）
            * boolean数据类型  true/false
            * 称为成员变量
            * 成员变量有初始值
        * 行为抽象(用函数表示)
            * 称为成员函数（方法）

    * 对象
        * 类的实例
        * 如何创建对象      
        `Clock c = new Clock()`  
        c指向了Clock的一个实例对象，这个指向称之为“引用”

    * 命名的基本规范
        * 类名首字母大写，如果由多个单词组成驼峰式
        * 变量名、函数名首字母小写，多个单词组成驼峰式

* 构造函数
    * 函数名和类名相同
    * 无任何返回类型，连void也没有
    * 主要是给成员变量赋初始值
    * 创建对象的时候会自动调用构造函数，创建一次对象就会调用一次
    * 如果一个类没有给构造函数jvm会给一个无参数的默认构造函数  
    `public 类名(){}`        
    一旦写了构造函数，这个默认的构造函数就不存在了。

* 函数重载
    * 同一个类中的一组函数
    * 这组函数函数名称相同，形式参数不同（类型、个数不同）
    * 与返回值类型无关
    * 调用的时候会根据参数类型和个数自动匹配
        * 这种匹配是不精确的，会找最精确的，找不到就找能匹配得上的。
 
* 构造函数的重载

* this
    * 当前对象(的引用)
    * 调用这个函数的那个对象(的引用)
    * 一个非静态的成员函数访问另外的非静态的成员前面都省略了this
    * 练习
        * 写一个点类Point
            * 数据抽象坐标x,y
            * 行为求到圆心的距离、到另外一个点的距离
                * Maht.sqrt(数据);
            * 构造函数、函数重载
            * 创建对象测试使用
        
        ```java
        public class Point{
        double x,y;
        Point(){}
        Point(double x, double y){
        this.x = x;
        this.y = y;
        }
        double distance(Point p){
        return Math.sqrt((x-p.x)*(x-p.x)+(y-p.y)*(y-p.y));
        }
        double distance(x,y){
        return this.distance(new Point(double x, double y))
        }
        }
        ```
    * this(参数)
        * 调用重载中的另外一个构造函数
        * 该语句只能放在构造函数，且必须是第一句
    * 练习
        * 写一个矩形类Rect
        * 矩形都是由左上角坐标，宽度和高度决定
        * 需要有构造函数、构造函数的重载
        * 判断一个点在不在矩形内
        * 创建对象并测试使用
        
        ```java
        public class Rect{
        Point leftTop;
        double h, w;
        public Rect(){}
        public Rect(Point leftTop, double h, double w){
        this.h = h;
        this.w = w;
        this.leftTop = leftTop;
        }
        public Rect(double x, double y, double h, double w){
        this(new Point(x,y),w,h)
        }
        boolean inRect(double x, double y){
        return this(new Point(x,y));
        }
        boolean inRect(Point p){
        return p.x<(leftTop.x+w) && p.y<(leftTop.y+h);
        }
        }
        ```
* 定义初始化
    * 给成员变量直接赋值
    * 定义初始化块 
        ```java
        public class Person{
        //double h=175;
        //等价于
        double h;
        {h = 175;}//顺序无所谓
        }
        ```
        
    * 创建对象的时候，先执行定义初始化后执行构造函数

* 静态成员
    * 静态成员变量
        * 属于类的，不属于某个对象
        * 只有一份，所有对象共享同一个
        * 可以直接通过类名.静态成员变量来访问
        * 也可以通过对象.静态成员变量来访问，不建议。
    * 静态定义初始化
        * 静态定义初始化块（静态块）
        ```java
        public class Demo{
            static{a = 10;}
        }
        ```
        
        * 用到类先加载其静态成员且只加载一次。
    * 静态成员函数
        * 可以直接通过类名.访问
        * 也可以对象.访问，不建议。
        * 静态的成员函数只能访问静态的成员，不可访问非静态
    * 用到一个类的时候，先静态定义初始化，创建对象的时候用到类就会先加载静态的且只加载一次，静态的只是成员，函数只有调用才会用，不调用函数没有意义，然后创建对象的时候才会定义初始化，构造函数。 
* 继承
    * 访问权限
        * 默认的
            * 修饰类和成员
            * 只能在同一个包中直接访问
                 * 使用其它包的类，需要先导入包（除了java.lang包下的)
            * import 包名.类名
            * import 包名.*;
        * private
            * 一般用来修饰成员变量
            * 只能在类的内部访问
            * 一般会对private的成员变量生成getter,setter方法，可以控制private成员变量的访问或赋值方法
        * protected
            * 同一包下可以直接访问
            * 不同包下的子类可以直接访问
        * public
            * 修饰类和成员
            * 能够在不同包下被访问

    * 继承
        * 从语法上是为了代码的复用
        * 将来主要用于设计方面
        * is-a关系
        * 用extends关键字实现继承体现代码的复用
         ```java
            public Circle extends Shape{}
         ```
         
            * java中除了构造函数全部继承
            * 继承中构造函数的问题
                * **子类的构造函数必须去调用父类的构造函数**
                * 如果子类没有写调用父类的构造函数，默认调用父类无参数的构造函数
                * 显式调用super(参数),也必须是第一句，在子类构造函数中
        * 练习
            * 写Point类加上访问权限
            * 写Shape类
            * 写矩形类继承Shape类
            
            ```java
            public class Rect extends Shape{
            private w, h;
            public Rect(){super();}
            //super()调用父类的构造函数，不写默认有
            public Rect(Point location, double w,,double h){
            super(location);
            //super(参数)显式调用父类构造函数，必须放在第一句
            this.w= w;
            this.h= h;
            }
            public Rect(double x,,double y, double w,,double h){
            //this(参数)调用上面的构造函数
            this(new Point(x, y),w,h);
            }
            }
            ```
        * 方法重写（函数覆盖）
            * 在父类中有个非private的方法
            * 方法的声明一样，实现不一样
            * 子类中有了重新实现,访问权限不能缩小
            * 注意方法重写（声明一致）与方法重载（形参不同）的区别
            * 重载是在编译时刻决定的，重写是在运行时刻决定的
        * 动态binding
            * 父类的引用引用了子类的实例，任何父类的引用都可以引用子类的实例。
            ```java
            Shape s = new Circle(5,3,20);
            ```
            
            * 调用方法的时候，如果方法构成重写就调用子类的方法          
            ```java
            public class Demo{
            public static void main(String[] args){
            B b = new B();}
            //1.B类没有给构造函数，jvm默认给一个无参的构造函数
            //2.子类的构造函数必须去调用父类的构造函数，如果没有写，默认调父类无参数的构造函数
            //3.非静态的成员函数调用非静态的成员都省略了this
            //4.this引用了谁->this是A类型的引用，调用这个函数的那个对象的引用
            //5.this引用了b引用的实例对象，构成了父类的引用引用了子类的实例对象
            //6.text方法构成方法重写
            //最后输出world
            }
            class A {
            public A(){this.test();}
            public void test(){
            System.out.println("hello");}
            }
            class B extends A{
            public void test(){
            System.out.println("world")}
            }
            ```
        * 整体的初始化顺序
            * 用到类先父类静态，再子类静态且只加载一次
            * 先父类定义初始化，然后父类构造函数
            * 最后子类定义初始化，子类构造函数

        * Java中的继承是单一继承
            * 一个类只能有一个直接父类
            * java中继承具有传递性
            * java中如果一个类没有父类，那么它的父类就是java.lang.Object类
                * Object类是一切类的父类
                * 常用的方法equals方法
                    * Java默认比较地址，可进行方法重载
                * 常用的方法toString()
                    * 直接打印一个对象就会打印对象的toString的返回值

**作业1：简答**
1.什么是方法重写（Overwirte）。
* 子类可以重写（覆盖）父类的方法，即方法名和参数列表与父类的方法相同但方法的实现不同。
* 当子类对象的重写方法被调用时（无论通过子类的引用调用还是父类的引用调用），运行的是子类重写后的版本。

2.重写和重载的区别
* 重载遵循“编译期绑定”，即在编译时根据参数变量的类型判断应该调用哪个方法。
* 重写遵循“运行期绑定”，即在运行时根据引用变量指向的实际类型调用方法。

3.对比访问控制修饰符public ，protected，默认，private。

**作业2：编程**
定义Question类，表示问题，该类有一个String类型的属性text表示题干,提供该类的两个构造方法。定义SingleChoice类，继承Question类，表示单选题，该类有两个属性，一个属于是String[]类型options，表示选项，另一个是String类型answerId，表示答案,提供该类的两个构造方法。定义MultiChoice类，继承Question类，表示多选题，该类有两个属性，一个属于是String[]类型options，表示选项，另一个是String[]类型answerIds，表示答案, 提供该类的两个构造方法。

```java
public class Question{
    private String text;
    public void Question(){}
    public void Question(String text){
        this.text = text;} 
}
public class SingleChoice extends Question{
    private String[] options;
    private String answerId;
    public void SingleChoice(){}
    public void SingleChoice(String text;String[] options;String answerId){
        super(text);
        this.options= options;
        this.answerId=answerId;}
}
public class MultiChoice extends Question{
    String[] options;
    String[] answerIds;
    public void MultiChoice(){}
    public void MultiChoice(String text;String[] options;String[] answerId){
        super(text);
        this.options= options;
        this.answerId=answerId;}
}
```
