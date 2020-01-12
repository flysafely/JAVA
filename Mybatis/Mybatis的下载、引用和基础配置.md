### Mybatis的下载
  + Mybatis非常的轻量级，只需要往项目中加入对相应的一个jar包即可
  + [Github下载](https://github.com/mybatis/mybatis-3/releases)<br>
    + **mybatis-3.5.3.zip:** <br>
      > 内含mybatis-3.5.3.jar和文档pdf，lib中包含的是如果需要使用mybatis中的其他功能需要添加的jar包
    + **Source code:** <br>
      > 内含mybatis-3.5.3.的源码，用于在编写代码时候查询相关内容具体信息
### Mybatis的引用
  + 导入jar包
    + mybatis-3.5.3.jar
    + mysql-connector-java.jar
    + log4j-1.2.17.jar //用于打印日志内容，同时需要配置一个[log4j.xml](https://blog.csdn.net/sndayYU/article/details/80722062)文件
### Mybatis的配置
  + 离线状态下mybatis配置文件(全局配置文件和SQL配置文件)中的代码提示功能(Alt+/)
    + 解压mybatis.jar包中的mybatis-3.5.3\org\apache\ibatis\builder\xml中的两个dtd约束文件
      + mybatis-3-config.dtd 全局配置约束文件
      + mybatis-3-mapper.dtd SQL映射配置约束文件
    + 在windows->preferences->XML->XML catalog->在User Specified Entries中Add
      + Location填入mybatis-3-mapper.dtd<br>
                    mybatis-3-config.dtd文件路径
      + key填http://mybatis.org/dtd/mybatis-3-mapper.dtd<br>
             http://mybatis.org/dtd/mybatis-3-config.dtd
  + 联线状态下
    + 只需要点击一下xml文件顶部的http://mybatis.org/dtd/mybatis-3-config.dtd就会自动下载，关闭xml后再打开就有提示了
    + 或者在Marketplace中搜索mybatis，安装即可
