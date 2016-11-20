# Chapter 5 泛型 `Generic Types`

> since Java JDK 5

> generic 泛化的，通用的，一般的

1. 类型参数 `type parameters`
    ```java
    class(interface) 类名（接口名）<类型参数列表 extends / super 类型 & 类型 & ...> {...}
    ```
    
    > 类型参数的命名

        E - Element (used extensively by the Java Collections Framework)
        K - Key
        V - Value
        N - Number
        T - Type
        S,U,V etc. - 2nd, 3rd, 4th types
        
    > 有界类型

    > PECS `Producer Extends, Consumer Super`
      
        extends
        super
   
2. 泛型的类
3. 泛型的接口

## 泛型的作用
- 类型安全，附加了类型检查。避免强制类型转换时出现 `ClassCastException`
- 简化代码