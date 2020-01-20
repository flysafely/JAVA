### [@注释的原理](https://www.cnblogs.com/zsty/p/10058185.html)
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
    + **@Target()**
      > @Target – 表示该注解用于什么地方。如果不明确指出，该注解可以放在任何地方。
        需要说明的是：属性的注解是兼容的，如果你想给7个属性都添加注解，仅仅排除一个属性，那么你需要在定义target包含所有的属性。
        以下是一些可用的参数：
        * ElementType.TYPE:用于描述类、接口或enum声明
        * ElementType.FIELD:用于描述实例变量
        * ElementType.METHOD
        * ElementType.PARAMETER
        * ElementType.CONSTRUCTOR
        * ElementType.LOCAL_VARIABLE
        * ElementType.ANNOTATION_TYPE 另一个注释
        * ElementType.PACKAGE 用于记录java文件的package信息
    + **@Retention()**
      > 定义该注解的生命周期
        * RetentionPolicy.SOURCE
          > 在编译阶段丢弃。这些注解在编译结束之后就不再有任何意义，所以它们不会写入字节码。@Override, @SuppressWarnings都属于这类注解。
        * RetentionPolicy.CLASS
          > 在类加载的时候丢弃。在字节码文件的处理中有用。注解默认使用这种方式。
        * RetentionPolicy.RUNTIME
          > 始终不会丢弃，运行期也保留该注解，因此可以使用反射机制读取该注解的信息。我们自定义的注解通常使用这种方式。
    + Tips:
      > 如果注解中只有一个属性，可以直接命名为“value”，使用时无需再标明属性名。
      ```java
      @interface Author{
        String value();
      }
      //使用Author注解
      @Author("flysafely")
      public void someMethod {
      
      }
      ```
    + 注解使用范例
      + BusinessLogic.java
      ```java
         public class BusinessLogic {
            public BusinessLogic() {
                super();
            }

            public void compltedMethod() {
                System.out.println("This method is complete");
            }    

            @Todo(priority = Todo.Priority.HIGH)
            public void notYetStartedMethod() {
                // No Code Written yet
            }

            @Todo(priority = Todo.Priority.MEDIUM, author = "Uday", status = Todo.Status.STARTED)
            public void incompleteMethod1() {
                //Some business logic is written
                //But its not complete yet
            }

            @Todo(priority = Todo.Priority.LOW, status = Todo.Status.STARTED )
            public void incompleteMethod2() {
                //Some business logic is written
                //But its not complete yet
            }
        }
      ```
      + Todo.java
      ```java
      import java.lang.annotation.ElementType;
      import java.lang.annotation.Retention;
      import java.lang.annotation.RetentionPolicy;
      import java.lang.annotation.Target;

      @Target(ElementType.METHOD)
      @Retention(RetentionPolicy.RUNTIME)
      @interface Todo {
          public enum Priority {LOW, MEDIUM, HIGH}
          public enum Status {STARTED, NOT_STARTED}    
          String author() default "Yash";
          Priority priority() default Priority.LOW;
          Status status() default Status.NOT_STARTED;
      }
      ```
      + TodoTest
      ```java
      import java.lang.reflect.Method;

      public class TodoReport {
          public TodoReport() {
              super();
          }

          public static void main(String[] args) {
              getTodoReportForBusinessLogic();
          }

          /**
           * This method iterates through all messages of BusinessLogic class and fetches annotations defined on each of them.
           * After that it displays the information from annotation accordingly.
           */
          private static void getTodoReportForBusinessLogic() {

              Class businessLogicClass = BusinessLogic.class;
              for(Method method : businessLogicClass.getMethods()) {
                  Todo todoAnnotation = (Todo)method.getAnnotation(Todo.class);
                  if(todoAnnotation != null) {
                      System.out.println(" Method Name : " + method.getName());
                      System.out.println(" Author : " + todoAnnotation.author());
                      System.out.println(" Priority : " + todoAnnotation.priority());
                      System.out.println(" Status : " + todoAnnotation.status());
                      System.out.println(" --------------------------- ");
                  }
              }
          }
      }
      ```
