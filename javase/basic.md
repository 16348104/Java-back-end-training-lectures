# chapter 2 语言基础

1. 标识符和关键字
    - 标识符
        > 用来起名的字符

        - 包括字母/数字/下划线/美元符号 `$`
        - 首字符不能是数字
        - 区分大小写
        - 不能是关键字以及 `true`/`false`
        
    - Java 命名规范
        - 类名
                首字母大写，第二个单词起首字母大写
        - 方法名，变量名，参数名
                首字母小写，第二个单词起首字母大写
        - `switch`/`case` 中 `default` 后要写 `break`
        - `if` 后语句体只有一个，也要写`{}`
        
    - 关键字
        - 被 Java 语言占用的一些单词，不能作为标志符
        
        > Java  关键字表
        
        <table>
            <tr>
                <th width="30%" align="center">类别</th>
                <th width="30%" align="center">关键字</th>
                <th width="40%" align="center">说明</th>
            </tr>
            <tr>
                <td rowspan="3" align="center">访问控制</td>
                <td>private</td>
                <td>私有的</td>
            </tr>
            <tr>
                <td>protected</td>
                <td>受保护的</td>
            </tr>
            <tr>
                <td>public</td>
                <td>公共的</td>
            </tr>
            <tr>
                <td rowspan="13" align="center">类、方法和变量修饰符</td>
                <td>abstract</td>
                <td>声明抽象</td>
            </tr>
            <tr>
                <td>class</td>
                <td>类</td>
            </tr>
            <tr>
                <td>extends</td>
                <td>扩允，继承</td>
            </tr>
            <tr>
                <td>final</td>
                <td>终极，不可改变的</td>
            </tr>
            <tr>
                <td>implements</td>
                <td>实现</td>
            </tr>
            <tr>
                <td>interface</td>
                <td>接口</td>
            </tr>
            <tr>
                <td>native</td>
                <td>本地</td>
            </tr>
            <tr>
                <td>new</td>
                <td>新，创建</td>
            </tr>
            <tr>
                <td>static</td>
                <td>静态</td>
            </tr>
            <tr>
                <td>strictfp</td>
                <td>严格，精准</td>
            </tr>
            <tr>
                <td>synchronized</td>
                <td>线程，同步</td>
            </tr>
            <tr>
                <td>transient</td>
                <td>短暂</td>
            </tr>
            <tr>
                <td>volatile</td>
                <td>易失</td>
            </tr>
            <tr>
                <td rowspan="12" align="center">程序控制语句</td>
                <td>break</td>
                <td>跳出循环</td>
            </tr>
            <tr>
                <td>continue</td>
                <td>继续</td>
            </tr>
            <tr>
                <td>return</td>
                <td>返回</td>
            </tr>
            <tr>
                <td>do</td>
                <td>运行</td>
            </tr>
            <tr>
                <td>while</td>
                <td>循环</td>
            </tr>
            <tr>
                <td>if</td>
                <td>如果</td>
            </tr>
            <tr>
                <td>else</td>
                <td>否则</td>
            </tr>
            <tr>
                <td>for</td>
                <td>循环</td>
            </tr>
            <tr>
                <td>instanceof</td>
                <td>实例</td>
            </tr>
            <tr>
                <td>switch</td>
                <td>根据值选择执行</td>
            </tr>
            <tr>
                <td>case</td>
                <td>定义一个值以供 switch 选择</td>
            </tr>
            <tr>
                <td>default</td>
                <td>默认</td>
            </tr>
            <tr>
                <td rowspan="6" align="center">错误处理</td>
                <td>assert</td>
                <td>断言表达式是否为真</td>
            </tr>
            <tr>
                <td>catch</td>
                <td>捕捉异常</td>
            </tr>
            <tr>
                <td>finally</td>
                <td>有没有异常都执行</td>
            </tr>
            <tr>
                <td>throw</td>
                <td>抛出一个异常对象</td>
            </tr>
            <tr>
                <td>throws</td>
                <td>声明一个异常可能被抛出</td>
            </tr>
            <tr>
                <td>try</td>
                <td>捕获异常</td>
            </tr>
            <tr>
                <td rowspan="2" align="center">包相关</td>
                <td>import</td>
                <td>引入</td>
            </tr>
            <tr>
                <td>package</td>
                <td>包</td>
            </tr>
            <tr>
                <td rowspan="9" align="center">基本类型</td>
                <td>boolean</td>
                <td>布尔型</td>
            </tr>
            <tr>
                <td>byte</td>
                <td>字节型</td>
            </tr>
            <tr>
                <td>char</td>
                <td>字符型</td>
            </tr>
            <tr>
                <td>double</td>
                <td>双精度浮点</td>
            </tr>
            <tr>
                <td>float</td>
                <td>单精度浮点</td>
            </tr>
            <tr>
                <td>int</td>
                <td>整型</td>
            </tr>
            <tr>
                <td>long</td>
                <td>长整型</td>
            </tr>
            <tr>
                <td>short</td>
                <td>短整型</td>
            </tr>
            <tr>
                <td>null</td>
                <td>空</td>
            </tr>
            <tr>
                <td rowspan="3" align="center">变量引用</td>
                <td>super</td>
                <td>父类，超类</td>
            </tr>
            <tr>
                <td>this</td>
                <td>本类</td>
            </tr>
            <tr>
                <td>void</td>
                <td>无返回值</td>
            </tr>
            <tr>
                <td rowspan="1" align="center">保留关键字</td>
                <td>goto</td>
                <td>是关键字，但不能使用</td>
            </tr>
        </table>
    
2. 数据类型、直接量和变量

    - **数据类型**
        - 基本数据类型 `primitive data type`
            - **布尔类型** `boolean`
            - 基本数值类型
                - 定点类型
                    - 字节 `byte`
                    - 字符 `char`
                    - 短整型 `short`
                    - **整形** `int`
                    - 长整型 `long`
                - 浮点类型
                    - 单精度浮点数 `float`
                    - **双精度浮点数** `double`
        - 引用数据类型 `reference data type`
            - 类 `class`
            - 接口 `interface`
            - 枚举 `enum`
            - 数组 `array`
    - 基本数据类型的封装类 `wrapper class`
      - `Boolean` - `boolean`
      - `Byte` - `byte`
      - `Character` - `char`
      - `Short` - `short`
      - `Integer` - `int`
      - `Long` - `long`
      - `Float` - `float`
      - `Double` - `double`
      - 自动装箱 `Autoboxing`
      - 自动拆箱 `Unboxing`
    - 浮点数的精度损失
      - java.math.BigDecimal
    - 变量
        - 类型
        - 名字
        - 值
        - 存储单元
    - 直接量
        - 基本数据类型直接量
            - 整形默认为 `int`

            ```java
            long l = 2147483648L;
            ```
                    
            - 浮点型默认为 `double` 

            ```java
            float f = 1.23f;
            ```

            - `char` 的直接量
                - 1 整数 `[0,65535]`
                - 'a' 单个字符
                - '\123' 3位八进制字符 `\000 ~ \377`
                - '\u4E00' 4位十六进制字符，unicode 字符
                - '\t' 转义字符串 `escape sequence`
                
                ```
                \t    tab
                \b	backspace
                \n	newline
                \r	carriage return
                \f	form feed
                \'	single quote character
                \"	a double quote character
                \\	a backslash character
                ```

            - 字符串直接量
            - `null` 一切引用数据类型的直接量

3. 运算符
    - 算术运算符
        - +
        > &plus; 在数值与字符串中的运算规则
        
                + 的运算顺序是从左至右，其他类型与字符串的 + 为字符串拼接
        - &minus;
        - *
        - / 整数除法，截去余数
        - ++ 自增运算，注意先后的区别
        - &minus;&minus; 自减运算，注意先后的区别
        - % 模运算，求余，符号只与被除数有关
    - 关系运算符
        - &gt;
        - &lt;
        - &gt;=
        - &lt;=
        - == 可用于任意类型比较
        - != 可用于任意类型比较
    - 布尔逻辑运算符
        - & 逻辑与
        - | 逻辑或
        - ^ 异或
        - ! 非
        - && 条件与
        - || 条件或
        > 短路规则

                &&
                ||
                第一个表达式即可确定运算结果时，不再判断第二个表达式
                使用短路规则与否，可能副作用不同
    - ~~位运算符~~
    - 赋值类运算符
        - =
        - +=
        - -=
        - *=
        - /=
        - %=
        - &= 针对布尔值
        - |= 针对布尔值
        - ^= 针对布尔值
    - 条件运算符
        - (condition)?(ture value):(false value) 三目运算符
    - 其他运算符
        - `(`类型`)` 强制类型转换
        - `.` 引用
        - `[]` 数组
        - `()` 改变运算优先级，推荐使用
        > Java 的运算优先级
        
                非 > 算术 > 关系 > 与 > 或 > 赋值
        - `instanceof`
        - `new`
4. 控制结构
    - 程序运行的控制结构
        - 顺序结构
        - 选择结构
            - `if`
            - `if`/`else`(`if`)
            
            > 注意 `else` 有无的区别
                  
            - `switch`/`case`
            > 可用于 `switch` 的变量类型
            
                    byte char int short enum String(JDK 1.7+) 
        - 循环结构
            - `for`
            - `for-each` - `enhanced fpr loop`
            - `while`
            - `do`/`while`
        - `break` 跳出当前这一个循环
        - `continue` 跳出当前这一次循环