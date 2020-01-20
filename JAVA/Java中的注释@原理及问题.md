### @注释的原理
  + 注解的结构
    ```java
      @Target(ElementType.METHOD)
      @Retention(RetentionPolicy.RUNTIME)
      @interface Todo {
          public enum Priority {LOW, MEDIUM, HIGH}
          public enum Status {STARTED, NOT_STARTED}
          //一下是该注释的成员
          String author() default "Yash";//这里的方法定义是注解Annotation类型的特殊形式
          Priority priority() default Priority.LOW;//注释使用的时候给成员赋值直接使用=
          Status status() default Status.NOT_STARTED;//default后定义的是该成员属性的默认值
      }
    ```
    > 注意：<br>
      1.注解Annotation的类型使用关键字@interface而不是声明接口用的interface,它继承了java.lang.annotition.Annotition接口,不是一个普通类<br>
      2.注解Annotation类型、方法定义是独特的、受限制的<br>
      3.注解Annotation类型的**方法**必须申明为无参数、无异常抛出的<br>
      4.注解Annotation的成员：方法名称为了成员名，而方法返回值称为了成员的类型
