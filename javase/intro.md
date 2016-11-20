# chapter 1 引言


1. 参考
2. 学习方法
    * 项目导向
3. About Java
    - 自然语言
    - 计算机语言发展
        - 1GL
                二进制机器语言
        - 2GL LLL Low Level Language
                低级计算机语言
                eg. 汇编语言
        - 3GL HLL High Level Language
                高级计算机语言
                eg. Java C C++ Delphi Basic Python VC C# VB GO
        - 4GL
                第四代计算机语言 
                SQL
    - Java历史
        - 1991 SUN Green Project
        - 1995 Java published
        - Java 语言的版本
            - Java Standard Edition
            - Java Enterprise Edition
            - ~~Java Micro Edition~~
                    Android
                    iOS
    - Java特性
        - Write once, Run anywhere
                跨平台
    - 程序分类
        - Application 应用程序
        - ~~Applet 小应用程序~~
                pig-let
                lake-let
4. 开发环境
    - JDK `Java Development Kit`
      - 安装 JDK JRE
    - 环境变量
      - 开始 - 计算机（右键） - 属性 - 高级系统设置 - 高级 - 环境变量 - 系统变量 - 新建
      
      ```
      1.
      JAVA_HOME 新建
      your_jdk_path
      
      2.
      Path 加在最前
      %JAVA_HOME%\bin;%JAVA_HOME%\jre\bin;
      
      3.
      CLASSPATH 新建
      .;%JAVA_HOME%\lib;%JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\lib\tools.jar
      ```
      
      - 验证 CMD

      ```
      java
      javac
      java -version
      ```
    
    - Java Documentation
5. Hello,world!
    ```java
    // Hello.java
    public class Test {
    //    psvm + Tab
    //    sout + Enter
        public static void main(String[] args) {
            System.out.println("Hello,world!");
        }
    }
    ```
    - Java 程序
        - 编辑
        - 编译
        - 运行
    - java 源文件
    - class 字节码文件 `byte code`

6. Java VM
    - Write once,run anywhere.