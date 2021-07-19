# coreJava笔记7-26
* java中的数组
    * int[] a = {1,2,3}
    * int[] a = new int[10];
    * int[] a = new int[]{1,2,3};
    * `println`与`print`区别在于输出是否换行
    * 数组的扩容是新建一个容量更大的数组再把原数组内容copy过来
    * 多维数组
        * 二维数组
            * 一维数组中的每个元素又是一个一维数组
        * 三维数组
            * 一维数组中每个元素都是一个二维数组
    * 可变参数
        * int...a; String...a 底层当做数组处理
        ```java
        //public static int add(int...a){
        public static int add(int[] a){
            int sum = 0;
            for (int i:a){
                sum+=i;}
            return sum;
        }
        ```
        
        * 如果函数有多个参数，可变参数必须是最后一个。
   
* 抽象类（继承关系 is-a)
    * 抽象方法
        * 方法只有声明，没有实现，java中用abstract关键字来声明这样的方法
        
            ```java
            public abstract void draw(){}
            ```
        * 用abstract关键字声明的方法就是抽象方法，不能有实现
    * 只要包含一个抽象方法的类，就是抽象类，抽象类必须用abstract关键字声明
        ```java
        public abstract class Shape{}
        ```
    * 继承抽象类，就要重写抽象类中的抽象方法，否则该类就会变成抽象类，需要abstract关键字声明
    * 普通类有的元素抽象类都可以有
    * 抽象类不能直接创建对象
        * 看到抽象类的引用，引用的一定是其子类的实例对象
        * 如果看到函数的形式参数是抽象类
            * 调用的时候传递的是该抽象类子类的实例对象
        * 如果看到函数的返回值类型是抽象类
            * 返回的是该抽象类子类的实例对象
            
        ```java
        Shape s = new Rect(10,10,10,10);
        ```
    * 练习
        * 把Shape类写成抽象的
        * 创建Rect类继承Shape类
        * 创建Rect的对象并测试使用
   
* final 关键字
    * 修饰变量
        * 只能赋一次值
        * 如果修饰的是成员变量
            * **只能赋一次值**
            * **对象创建出来必须赋好了值**
                * 可以通过构造函数
                * 也可以通过定义初始化
       
    * final 修饰方法
        * 该方法不能被重写。
        * final能和abstract一起使用吗?不可以，abstract修饰的方法在子类中一定要重写
    * final修饰类该类不能被继承

* 接口
    * 体现的是一种标准
    * **隔离了变化，统一了标准**
    * 用interface关键字定义标准
        * 接口里的方法都是public abstract的
     
        ```java
        public interface Memory{
            public void store();
            }
        ```
    * 符合标准就是实现接口用implements关键字
        * 实现接口，就要重写接口里的抽象方法，否则该类就变成了抽象类
        
        ```java
        public class AMemory implements Memory{
            public void Store(){
                System.out.println("A store...")}
        ```
    * 接口是不能直接创建实例的
        * 看到接口类型的引用，引用的是实现了该接口的类的实例对象
        * 看到函数的参数是一个接口，调用的时候传递的是实现了该接口的类的实例对象
        * 看到函数的返回值类型是一个接口，返回的是实现了该接口的类的对象
        * 接口的引用一样可以理解为父类的引用引用了子类的实例
            * 不是子父类关系，体现的是can-do关系而不是is-a关系
    * 一个类可以实现多个接口
    
        ```java
        //可以继承也可以实现接口标准
        public class Hero extends Memory implements CanFly,CanFight{
            public void Store(){
                System.out.println("B store..")}}
            public void Fight(){
                System.out.println("B fight..")}}
            public void Fly(){
                System.out.println("B fly..")}}
        ```

* 内部类
    * 成员内部类
        * 类在类内部的成员位置
        * 内部类也可以访问外部类的成员
        
        ```java
        Outer.Inner inner = Outer.new Inner(20,20)
        ```
    * 静态内部类
        * 相当于静态的成员内部类
        
        ```java
        Outer.Inner inner = new Outer.Inner(20,20)
        //静态的不属于对象而属于类，不需要Outer.new
        ```
        * 静态的内部类只能访问外部类的静态成员，不能访问非静态成员
    * 局部内部类
        * 类在函数中，只在函数中有效，出了函数就无效了
    
        ```java
        class Person{
    //看到返回值是一个接口|抽象类，返回的是实现了该接口|抽象类子类的实例对象
            public CanFly getOneCanFly(){
        //局部内部类，类在函数中有效，出了函数就无效了
                class implements CanFly{
                    public void Fly(){
                        System.out.println("xx...fly...");}
                        }
                    return new X();
            }
            public Shape getOneShape(){
            }
        }
//调用的时候
        Person p = new Person;
        p.getOneCanFly().fly();
        ```

    * 匿名内部类
        * 什么时候用
            * 已知父类，要获取其子类的实例对象
            * 已知接口，要获取接口的实现类的实例对象
        * 使用的是匿名类的实例对象
        * 如何用
            
            ```java
        new 父类(给父类构造函数传递参数){/*子类的实现部分*/}
        new 接口(){/*实现了该接口的类的实现部分*/}
            ```
            
            ```java
            class Person1{
                public CanFly getOneCanFly(){
        //看到函数的返回值是接口，返回的是实现了该接口的实例对象
        //智能提示可以自动生成
                    return new CanFly(){
                        public void fly(){
                            System.out.println("fly...");}
                    };
                public void playFly(CanFly canFly){
                    canFly.fly();}
                }
            }
            //已知接口，要获取实现了接口的实例对象
            Person1 p1 = new Person1();
            p1.playFly(new CanFly(){
            public void fly(){
                System.out.println("fly...")}});
```
    * 练习
        * 创建Person类添加两个方法
        ```java
     public Shape getOneShape(){
             /*请使用匿名类实现该方法*/
          }
     public void playShape(Shape shape){
              shape.draw();
          }
     //请在主函数中调用该方法，传递对象的时候使用匿名类实现
        ``` 
                       
* 比较抽象类和接口
    * 接口中所有的方法都是public abstract 即使没有这样声明
    * 抽象类里可以有普通方法，构造函数等，接口里没有
    * 接口里声明的变量都是public static final 的即使没有这样声明
    * 抽象类是is-a          extends
    * 接口体现的是can-do    implements
    * 一个类只能继承一个抽象类，但是可以实现多个接口
    * 接口的引用，可以看做是父类的引用引用了子类的实例
    * java中是单一继承,但是一个接口可以继承多个接口（一般不这么用）
                
    **思考:**
    * 如果构造函数私有如何获取对象
        * 不希望外部能够创建它的对象时，将构造函数私有
        
        ```java
        class X{
            private X(){}
            //普通方法必须要有对象才能调用，设为静态的即可不需要对象即可调用
            public static X getInstance(){
                return new X();}
            public void f(){
                System.out.println("hello");}
        }
        X.getInstance().f();
        //这么写的好处：1.使用者不需要关心对象是怎么创建的，拿到对象就可以用
        //（控制反转的设计思想）2.使用者和创建者分离的目的
        ```
    * 如果定义一个星期类，应该如何定义 
        * 将构造函数私有，不希望外部创建出“星期八”
        * 使用枚举类的情景：对象数目固定，且已知
        * 枚举类型      
            * 用enum声明(地位等价于一个类)
            * 构造函数默认就是private的
            
        ```java
public enum MyWeekDay{
    MON,TUE,WED,THU(5),FRI,SAT,SUN；//实际上都调用了private的默认的无参的构造函数
    private MyWeekDay(){}
    private MyWeekDay(int n){}
}
public enum MyWeekDay{
    MON{
        public MyWeekDay nextDay(){
        return TUE;}
    },TUE{},WED{},THU(5){},FRI{},SAT{},SUN{}；
    //其它同MON
    private MyWeekDay(){}
    private MyWeekDay(int n){}
    public abstract MyWeekDay nextDay();
}
        ```  
   
* jdk提供的常用基础类
    * java.lang.String（类用final修饰不可被继承）
        * 查询帮助文档，看看如何创建对象、有哪些方法。
        * 正则表达式
            * 原子（代表一个字符)

                ```java
          [a-zA-Z]
          [0-9] or  \d
          [abc]
          [a-zA-Z0-9_] or \w
          [^a-zA-Z0-9_] or \W
          [^a-z] //^代表相反，此为非a-z
          [^0-9] or \D
            ```
            * 特殊字符
            
                ```java
           *  代表出现零次或者多次
           +  代表出现1次或者多次
           ?  代表出现0次或者1次
           {n} 代表出现n次
           {n,m}
           ^代表开始
           $代表结束
                ```
            * 从键盘输入字符：`Scanner s = new Scanner(System.in)`
            * 判断是否符合正则表达式用`s.matches(reg)`
    * java.lang.StringBuffer,java.lang.StringBuilder
        * 两者区别只是使用线程是否安全，用法完全一样
        * 线程安全：资源的访问同时之后一个线程可以进来(synchronize)，
    * 不建议用‘+’做字符串拼接
        
        ```java
String s2 = s + "world";
//使用‘+’拼接是内部执行以下代码
//new StringBuilder(s).append("world").toString();
//使用‘+’拼接循环字符串时，每次拼接得到的新字符串都会一直占用内存
        ```
    * java.lang.Math
 
-------
   
##三、java核心专题之集合操作   java.util.*;
* 这个包里封装的都是数据结构
* java.util.Collection接口
    * java.util.List接口
        * 数组和链表实现统一接口
        * java.util.ArrayList
            * 数组结构
            * 导包快捷键  ctrl+shift+o 
            * 既然封装的是数组结构
                * 包装的无非是数组的插入元素、移除元素、扩容等操作。插入操作存放数据必须是连续的，否则报错数组下标越界
            * 常用的API
                * size(),remove()等，查帮助手册用法
            * 遍历的几种方式
                
            ```java
//for
for(int i = 0; i< list.size();i++){
    Stu xx = (Stu)list.get(i);
    System.out.printn(xx);}
//迭代
Iterator itor = list.iterator
while(itor.hasNext()){
    Stu xx = (Stu)itor.next();
    System.out.printn(xx);}
//foreach
for(Object obj:list){
    Stu xx = (Stu)obj;
    System.out.printn(xx);}
            ```
            * 集合中可以容纳任何对象，但是大部分应用，我们一个集合实例往往都容纳相同类型的对象
            * **泛型**——为了防止错误类型输入
                
            ```java
public class Demo{
    public static void main(String[] args){
        ArrayList<Stu> stus = new ArrayList<Stu>();
        //说明这个表里只能加Stu类型的对象
        //再进行遍历时不需要强制类型转换了
        for(int i = 0; i< list.size();i++){
            Stu xx = list.get(i);
            System.out.printn(xx);}}
        //迭代器—也有泛型
        Iterator<Stu> itor = list.iterator
        while(itor.hasNext()){
            Stu xx = itor.next();
            System.out.printn(xx);}
        }
            ```
            * 练习
                * 创建ArrayList的实例，只能存放字符串
                * 添加几个字符串
                * 用三种方式遍历
            * 使用注意：
                * 尽量预估大小避免扩容，自动扩容时一次扩容1.5倍 
        * java.util.LinkedList
            * 链表结构（java内是双向链表）
            * 基本操作和ArrayList类似，但是数据结构不一样
            * 链表提供了丰富的头尾操作
                * getFirst(),getLast(),addFirst(),addLast(),removeFirst(),removeLast()
                
    * java.util.Set(不容纳重复元素)
        * java.util.HashSet
            * 不能容纳重复对象
            * 重复对象如何定义呢？
                * java默认只根据地址来区分。
                * 实际应用时应该根据业务来决定如何才是重复对象
                * java提供了重写equals、和hashCode方法来决定是否为重复对象（编译器中直接右键generate选取对象生成equals和hashcode方法即可）
            * 遍历方式只有迭代器和foreach的方式，没有数组循环的方式了
            * 练习:
            练习题目1：
                * 创建一个课程类Course,有课程名称（是唯一标识），学分属性。
                * 创建一个学生类Student,有学生姓名（是唯一标识），年龄属性，有一个集合类(HashSet)，存放学生所选的课程，有添加课程和移除课程的方法
                * 创建一个班级类Team,有班级编号（唯一标识），班级描述属性，有一个集合类(HashSet)，存放班级中学生，有添加学生和移除学生的方法
                
            ```java
            public class Course{
                private String courseName;
                private int score;
                public Course(){};
                public Course(String courseName, int score) {
                    this.courseName = courseName;
                    this.score = score;}
                public boolean equals(Object o) {
                    if (this == o) return true;
                    if (o == null || getClass() != o.getClass()) return false;
                    Course course = (Course) o;
                    return Objects.equals(courseName, course.courseName);}
                public int hashCode() {
                    return Objects.hash(courseName);}
            }
            public class Student{
                String stuName;
                int stuAge;
                HashSet<Course> coursesSet = new HashSet<Course>();
                public Student() {}
                public Student(String stuName, int stuAge) {
                    this.stuName = stuName;
                    this.stuAge = stuAge;}
                public void removeCourse(Course cor){
                    coursesSet.remove(cor);}
                public void addCourse(Course cor){
                    coursesSet.add(cor);}
                public String getStuName() {
                    return stuName;}
                public void setStuName(String stuName) {
                    this.stuName = stuName;}
                public int getStuAge() {
                    return stuAge;}
                public void setStuAge(int stuAge) {
                    this.stuAge = stuAge;}
                public String toString() {
                    return stuName + '_' + stuAge;}
                public boolean equals(Object o) {
                    if (this == o) return true;
                    if (o == null || getClass() != o.getClass()) return false;
                    Student student = (Student) o;
                    return Objects.equals(stuName, student.stuName);}
                public int hashCode() {
                    return Objects.hash(stuName);}
            }
            public class Team {
                int teanNum;
                String classdis;
                public Team() { }
                public Team(int teanNum, String classdis) {
                    this.teanNum = teanNum;
                    this.classdis = classdis;}
                HashSet<Student> stuSet = new HashSet<Student>();
                public void addStu(Student stu){
                    stuSet.add(stu);}
                public void removeStu(Student stu){
                    stuSet.remove(stu);}
                public boolean equals(Object o) {
                    if (this == o) return true;
                    if (o == null || getClass() != o.getClass()) return false;
                    Team team = (Team) o;
                    return teanNum == team.teanNum;}
                public int hashCode() {
                    return Objects.hash(teanNum);}
                public String toString() {
                    return teanNum +'_' +classdis +'_'+ stuSet ;}
            }
            ```
            * 问题1：主函数中创建一些课程对象，创建一些学生对象，创建一个班级对象，给学生添加一些课程，给班级添加学生
            
            ```java
            public class Test1 {
                public static void main(String[] args) {
                    Course cor1 = new Course("math",2);
                    Course cor2 = new Course("english",3);
                    Course cor3 = new Course("chinese",2);
                    Student stu1 = new Student("zhangsan",18);
                    Student stu2 = new Student("lisi",19);
                    Student stu3 = new Student("wangwu",20);
                    Team team1 = new Team(123,"s");
                    stu1.addCourse(cor1);
                    stu2.addCourse(cor2);
                    stu3.addCourse(cor3);
                    team1.addStu(stu1);
                    System.out.println(team1);
                }
            }
            ```
        * java.util.TreeSet
            * 加入到TreeSet中的类型必须是实现Comparable接口的
            * 容纳的对象可以根据自定义的规则进行排序
            * 比较返回0认为是同一个对象
            ```java
            public int compareTo(User o){
              return this.username.compareTo(o.username);
                //按照放进TreeSet的元素等字母顺序进行排序}
            ```

            * 比较器
                * 1.放入TreeSet中的类要实现java.lang.Comparable接口
                
                ```java
                public class User implements Comparable<User>{}
                ```
            
      
作业1：完成练习
作业2：在练习的基础上要求输出课程及其被选的次数（预习HashMap)，并按照次数降序输出，如果次数相同按照课程名称字母顺序输出
         
     
         
                
