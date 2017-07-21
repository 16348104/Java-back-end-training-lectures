# Lombok

> [Project Lombok](https://projectlombok.org/)

> [Lobmok Plugin on Github](https://github.com/mplushnikov/lombok-intellij-plugin)

1. bulid.gradle
```gradle
compile 'org.projectlombok:lombok:1.16.18'
```

2. IDEA
  - install Lombok plugin
    - [Lombok Plugin](http://plugins.jetbrains.com/plugin/6317?pr=idea)
  - File > Settings > Build, Execution, Deployment > Compiler > Annotation Processors
    - check "Enable annotation processing"

3. Model class

```java
import lombok.Data;
import lombok.EqualsAndHashCode;

@Data
@EqualsAndHashCode(callSuper = true)
public class Admin extends BaseModel {
    private Integer id;
    private String email;
    private String username;
    private String password;
}
```

```java
Warning: java: 
Generating equals/hashCode implementation but without a call to superclass, 
even though this class does not extend java.lang.Object. 
If this is intentional, add '@EqualsAndHashCode(callSuper=false)' to your type.
```