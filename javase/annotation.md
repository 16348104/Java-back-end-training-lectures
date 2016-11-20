# Annotation

## 元注解
1. `@Target`
  
  > 用来说明注解所修饰的对象

  - `ElementType` enum
    - `CONSTRUCTOR` 用于描述构造器
    - `FIELD` 用于描述域
    - `LOCAL_VARIABLE` 用于描述局部变量
    - `METHOD` 用于描述方法
    - `PACKAGE` 用于描述包
    - `PARAMETER` 用于描述参数
    - `TYPE` 用于描述类、接口、注解类型、enum 声明

2. `@Retention`

  > 在什么级别保存该注释信息，用于描述注解的生命周期
  
  - `RetentionPoicy` enum
    - `SOURCE` 在源文件中有效，即源文件保留
    - `CLASS` 在class文件中有效，即 class 保留
    - `RUNTIME` 在运行时有效，即运行时保留

3. `@Documented`

  > 一个标记注解，，没有成员。工具文档化

4. `@Inherited`

  > 一个标记注解，，没有成员。阐述了某个被标注的类型是被继承的

## 自定义注解

```java
public @interface 注解名 {
  // 注解体
}
```