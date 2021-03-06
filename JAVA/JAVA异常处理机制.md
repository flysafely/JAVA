### throw和throws的区别
>并且所有系统定义的编译和运行异常都可以由系统自动抛出，称为标准异常，但是一般情况下Java 强烈地要求应用程序进行完整的异常处理，给用户友好的提示，或者修正后使程序继续执行。
直接进入正题哈：
+ 1.用户程序自定义的异常和应用程序特定的异常,必须借助于 throws 和 throw 语句来定义抛出异常。

  + 1.1   throw是语句抛出一个异常。
    > 语法：throw (异常对象);
    ```java
             throw e;
    ```
  + 1.2   throws是方法可能抛出异常的声明。(用在声明方法时，表示该方法可能要抛出异常)
    > 语法：[(修饰符)](返回值类型)(方法名)([参数列表])[throws(异常类)]{......}
    ```java
             public void doA(int a) throws Exception1,Exception3{......}
    ```
+ 举例：

> throws E1,E2,E3只是告诉程序这个方法可能会抛出这些异常，方法的调用者可能要处理这些异常，而这些异常E1，E2，E3可能是该函数体产生的。
throw则是明确了这个地方要抛出这个异常。

```java
void doA(int a) throws IOException,{
           try{
                 ......

           }catch(Exception1 e){
              throw e;
           }catch(Exception2 e){
              System.out.println("出错了！");
           }
           if(a!=b)
              throw new  Exception3("自定义异常");
}
```
> 代码块中可能会产生3个异常，(Exception1,Exception2,Exception3)。<br>
  如果产生Exception1异常，则捕获之后再抛出，由该方法的调用者去处理。<br>
  如果产生Exception2异常，则该方法自己处理了（即System.out.println("出错了！");）。<br>
    所以该方法就不会再向外抛出Exception2异常了，void doA() throws Exception1,Exception3 里面的Exception2也就不用写了。<br>
  而Exception3异常是该方法的某段逻辑出错，程序员自己做了处理，在该段逻辑错误的情况下抛出异常Exception3，则该方法的调用者也要处理此异常。

+ 区别总结：

  > throw语句用在方法体内，表示抛出异常，由方法体内的语句处理。<br>
  throws语句用在方法声明后面，表示再抛出异常，由该方法的调用者来处理。

  > throws主要是声明这个方法会抛出这种类型的异常，使它的调用者知道要捕获这个异常。<br>
  throw是具体向外抛异常的动作，所以它是抛出一个异常实例。

  > throws说明你有那个可能，倾向。<br>
  throw的话，那就是你把那个倾向变成真实的了。
  
  > throws出现在方法函数头；<br>
  而throw出现在函数体。
  > throws表示出现异常的一种可能性，并不一定会发生这些异常；<br>
  throw则是抛出了异常，执行throw则一定抛出了某种异常。
  
  > 两者都是消极处理异常的方式（这里的消极并不是说这种方式不好），只是抛出或者可能抛出异常，但是不会由函数去处理异常，真正的处理异常由函数的上层调用处理。
