# springboot1
## Springboot学习（一） 自动配置特性
一、

在主程序中配置

@SpringBootApplication
相当于：

//@SpringBootConfiguration

@Configuration  //主要由他组成
 

//@EnableAutoConfiguration
@AutoConfigurationPackage
@Import(AutoConfigurationImportSelector.class)
getAutoConfigurationEntry(annotationMetadata); //批量导入组件
调用List<String> configurations = getCandidateConfigurations(annotationMetadata, attributes);  //获取到所有需要导入到容器中的配置类
List<String> configurations = SpringFactoriesLoader.loadFactoryNames(getSpringFactoriesLoaderFactoryClass(),  getBeanClassLoader());  //工厂加载器进行加载
private static Map<String, List<String>> loadSpringFactories(ClassLoader classLoader) {　　　　//进行加载,得到所有的组件

}




//@ComponentScan("spring.main.spring")，



//SpringBootApplication默认是在主程序所在的包下
复制代码
package spring.main.spring;


import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
//相当于
//@SpringBootConfiguration
//@EnableAutoConfiguration
//@ComponentScan("spring.main.spring")，
//SpringBootApplication默认是在主程序所在的包下
public class MainSpring {
    public static void main(String[] args) {

        SpringApplication.run(MainSpring.class,args);
    }
}
复制代码
若没有对

SpringBootApplication
进行配置则对应其的子程序需要放在主程序所在的同一文件夹下或者子文件夹下，默认扫描是在主程序所在文件夹，其对应的程序应该放在文件扫描的文件夹或者子文件夹

二、

其中springboot可以单独设置一个配置文件，在resources文件夹下创建一个配置文件application.propeties,想要改的任何配置在这个文件夹中修改即可

#可以在这里修改tomcat端口号等，或springmvc的一些设置
server.port=8888  #修改端口号
spring.servlet.multipart.max-file-size=10MB   #默认是1MB，只需在这里更改即可（文件上传大小）
各种配置均有默认值，

　　默认值配置最终都是映射到MultipartProperties中

　　配置文件的值最终会绑定到某个类上，这个类会在容器中创建对象

三、

在对应的pom.xml中需要编写基本信息，引入的parent中的包，包含了对应的自动装配的版本号，无需下载直接可以使用

复制代码
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.5.2</version>
        <relativePath/> <!-- lookup parent from repository -->
    </parent>
<!--    修改mysql版本不使用springboot给予的默认版本-->
<!--    <properties>-->
<!--        <mysql.version>5.1.47</mysql.version>-->
<!--    </properties>-->

    <groupId>com.example</groupId>
    <artifactId>spring-boot</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <name>spring-boot</name>
    <description>Demo project for Spring Boot</description>
    <properties>
        <java.version>1.8</java.version>
    </properties>
    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
　　　　　　　　　　　　这里对应的开发web项目

        </dependency>

        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>
    <packaging>jar</packaging>
    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
                <version>2.5.2</version>
            </plugin>
        </plugins>
    </build>

</project>
复制代码
web项目发开的jar包结构图（有自动装配tomcat、json、mvc、web） 查看方法（选中一个引入文件）右键点击Diagrams   ->    show   Diagrams   



 

 

pom.xml中引入了哪些场景，这个场景的自动配置才会开启,SpringBoot的所有自动配置功能都在

复制代码
<dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-autoconfigure</artifactId>
      <version>2.5.2</version>
      <scope>compile</scope>
    </dependency>
复制代码
 



 

 

 

 

 
