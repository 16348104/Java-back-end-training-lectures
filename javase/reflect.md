# 补2. 反射 `Reflect`

> Reflection: This is a relatively advanced feature and should be used only by developers who have a strong grasp of the fundamentals of the language.

1. java.lang.reflect
    - `AccessibleObject` 
    - `Array`
    - `Constructor` 
    - `Field` 
    - `Method`
    - `Modifier` 
    - `Proxy`
    - `ReflectPermission`

2. Java 类的加载机制
    - 加载 `loading`
        1. 加载器分类
            - 启动类加载器 `bootstrap class loader` 
            - 自定义加载器 `user-defined class loader`
            - 系统类加载器 `system class loader`
        2. 过程
            - 通过一个类的全限定名来获取其定义的二进制字节流
            - 将这个字节流所代表的静态存储结构转化为方法区的运行时数据结构
            - 在 `Java` 堆中生成一个代表这个类的 `java.lang.Class` 对象
        3. 结果：`byte code` ---> `java.lang.Class` 对象
            
    - 链接 `linking`
        - 验证 `verification`
        - 准备 `preparapent`
        - 解析 `resuolutation`
        
    - 初始化 `initialization`

3. java.lang.Class
    - ClassName.class;
    - instance.getClass();
    - Class.forName(String className);
    
4. A demo `Human` class

    ```java
    // super class Animals
    class Animals {
        public int age; // It's public
        private double weight;
    
        public Animals() {
        }
    
        public Animals(int age, double weight) {
            this.age = age;
            this.weight = weight;
        }
    
        public int sleep(int hours) {
            return hours;
        }
    
        public void eat(String food) {
            System.out.println("eating " + food);
        }
        
        // This's a private method!
        private void killHuman() {
            System.out.println("killed a poor guy...");
        }
        
        // getters and setters
    }
    ```
    
    ```java
    // sub class Human
    public final class Human extends Animals {
        public String name; // It's public!
        private boolean married;
    
        Human() { // It's package-private!
        }
    
        public Human(int age, double weight, String name, boolean married) {
            super(age, weight);
            this.name = name;
            this.married = married;
        }
    
        @Override
        public void eat(String food) {
            System.out.println(name + " is now eating " + food);
        }
    
        public void study(String course) {
            System.out.println(name + " is now studying " + course);
        }
    
        // This's a private method!
        private void killAnimals(String animal) {
            System.out.println(name + " is now killing " + animal);
        }
        
        // getters and setters
    }
    ```

5. Fields
    - `getFields()`

        > All the public fields up the entire class hierarchy.

    - `getDeclaredFields()`

        > All the fields, regardless of their accessibility but only for the current class 

    ```java
    class HumanTest {
        public static void main(String[] args) {
            Human human = new Human();
            Field[] fields = human.getClass().getFields();
            System.out.println("--- getFields() ---");
            for (Field field : fields) {
                System.out.println(field.getName());
            }
            Field[] declaredFields = human.getClass().getDeclaredFields();
            System.out.println("--- getDeclaredFields() ---");
            for (Field declaredField : declaredFields) {
                System.out.println(declaredField.getName());
            }
        }
    }
    
    /*
    --- getFields() ---
    name
    age
    --- getDeclaredFields() ---
    name
    married
     */
    ```
    
    ```java
    // 通过反射获取 ArrayList 的容量
    List<Integer> list = new ArrayList<>();
    Field array = ArrayList.class.getDeclaredField("elementData");
    array.setAccessible(true);
    System.out.println("list capacity: " + ((Object[]) array.get(list)).length); // 10
    ```

6. Constructors

    - getConstructors

        > only public constructors

    - getDeclaredConstructors

        >  all the constructors

    ```java
    class HumanTest {
        public static void main(String[] args) {
            Human human = new Human();
            Constructor[] constructors = human.getClass().getConstructors();
            System.out.println("--- getConstructors ---");
            for (Constructor constructor : constructors) {
                System.out.println(constructor.getName());
                for (Parameter parameter : constructor.getParameters()) {
                    System.out.println("\t" + parameter);
                }
            }
    
            Constructor[] declaredConstructors = human.getClass().getDeclaredConstructors();
            System.out.println("--- getDeclaredConstructors ---");
            for (Constructor declaredConstructor : declaredConstructors) {
                System.out.println(declaredConstructor.getName());
                for (Parameter parameter : declaredConstructor.getParameters()) {
                    System.out.println("\t" + parameter);
                }
            }
        }
    }
    
    /*
    --- getConstructors ---
    Human
        int arg0
        double arg1
        java.lang.String arg2
        boolean arg3
    --- getDeclaredConstructors ---
    Human
    Human
        int arg0
        double arg1
        java.lang.String arg2
        boolean arg3
     */
    ```
    
    ```java
    // constructor - object
    Human human = null;
    try {
        human = (Human) constructor.newInstance(20, 60, "Tom", false);
        System.out.println(human.getAge());
    } catch (InstantiationException | IllegalAccessException | InvocationTargetException e) {
        e.printStackTrace();
    }
 
    /*
    20
   */
    ```

7. Methods

    - getMethods

        > All the public methods up the entire class hierarchy.

    - `getDelcaredMethods()`

        > All the methods, regardless of their accessibility but only for the current class 

    ```java
    class HumanTest {
        public static void main(String[] args) {
            Human human = new Human();
            Method[] methods = human.getClass().getMethods();
            System.out.println("--- getMethods ---");
            for (Method method : methods) {
                System.out.println(method);
            }
            Method[] declaredMethods = human.getClass().getDeclaredMethods();
            System.out.println("--- getDeclaredMethods ---");
            for (Method declaredMethod : declaredMethods) {
                System.out.println(declaredMethod);
            }
        }
    }
    
    /*
    --- getMethods ---
    public int java1702.javase.regex.Human.sleep(int)
    public void java1702.javase.regex.Human.study(java.lang.String)
    public void java1702.javase.regex.Human.eat(java.lang.String)
    public final void java.lang.Object.wait(long,int) throws java.lang.InterruptedException
    public final native void java.lang.Object.wait(long) throws java.lang.InterruptedException
    public final void java.lang.Object.wait() throws java.lang.InterruptedException
    public boolean java.lang.Object.equals(java.lang.Object)
    public java.lang.String java.lang.Object.toString()
    public native int java.lang.Object.hashCode()
    public final native java.lang.Class java.lang.Object.getClass()
    public final native void java.lang.Object.notify()
    public final native void java.lang.Object.notifyAll()
    --- getDeclaredMethods ---
    public int java1702.javase.regex.Human.sleep(int)
    public void java1702.javase.regex.Human.study(java.lang.String)
    private void java1702.javase.regex.Human.killAnimals(java.lang.String)
    public void java1702.javase.regex.Human.eat(java.lang.String)
     */
    ```

8. Modifiers

    ```java
    class HumanTest {
        public static void main(String[] args) throws NoSuchFieldException {
            Human human = new Human();
            System.out.println(Modifier.toString(human.getClass().getModifiers()));
            Field field = human.getClass().getField("name");
            System.out.println(Modifier.toString(field.getModifiers()));
        }
    }
    
    /*
    public final
    public
     */
    ```
