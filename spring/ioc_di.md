# Chapter 2 IoC / DI

> [Inversion of Control Containers and the Dependency Injection pattern](http://martinfowler.com/articles/injection.html)

> by Martin Fowler

- `strong coupling` 强耦合：
    - 高层应用类 依赖于 底层模块类
    - 底层模块类 控制 高层应用类
    - 底层有改变，高层应用类有大量的代码级更改
- `loose coupling` 松散耦合
    - 高层应用类 不依赖于 底层模块类
    - 底层模块类 不能控制 高层应用类C
    - 底层有改变，高层应用类不需要做代码级更改 
- `Inversion of Control` 控制关系的反转

    > 从 强耦合 到 松散耦合 的 `decoupling` 解耦 过程中，实现了控制关系的反转
    
- Spring IoC
    1. `Constructor` Injection
    2. `Setter` Injection

- DI

  > Dependency Injection