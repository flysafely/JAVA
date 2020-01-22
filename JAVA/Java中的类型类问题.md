### 类名.class和getClass()的区别
  + 区别：
    * **getClass()**：在程序运行时期动态获得对象类型信息的操作
      > 一般所使用的对象都直接或间接继承自Object类,getClass()是Object类的方法，它可以获得一个实例的类型类(Class类的实例)<br>
        有多态能力，运行时可以返回子类的类型信息
    * **.class**：在编译阶段决定使用的类型
      > .class是没有多态的，是静态解析的，编译时可以确定类型信息
    * **反射：动态获得类型**
      > 每个类都会产生一个对应的Class对象，也就是保存在.class文件。所有类都是在对其第一次使用时，动态加载到JVM的，当程序创建一个对类的静态成员的引用时，就会加载这个类。Class对象仅在需要的时候才会加载。
      类加载器首先会检查这个类的Class对象是否已被加载过，如果尚未加载，默认的类加载器就会根据类名查找对应的.class文件。
      获得Class对象的三种方式
      Object的getClass()
    * **静态加载.class**
      > 通过Class的静态方法forName（String className），最为常用
      反射通俗理解是把类中各个组成部分映射成一个对象。加载过程：
      反射加载类，JVM会检测是否有.class类文件
      如果没有，则会把.class文件加载从磁盘中加载进内存
      自动创建一个Class对象，通过这个对象可以得到要创建的对象实例
    * 举例：
      ```java
      public static void main(String[] args) {
      ClassA a=new ClassA();
      System.out.println(a.getClass());
      System.out.println(ClassA.class);
      }
      ```
      > 对象a是A的一个实例，ClassA是某一个类，在Java中表示一个特定类型的类型类可以用“类型.class”的方式获得，因为a.getClass()获得是ClassA的类型类，
      也就是ClassA.class。所以ClassA.class和a.getClass()是一样的。类型类是一一对应的，父类的类型类和子类的类型类是不同的，
      因此，假设ClassA是ClassB的子类，那么ClassB.class和a.getClass是不一样的。
