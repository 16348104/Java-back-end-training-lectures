# 反射

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

2. java.lang.Class
    - ClassName.class;
    - instance.getClass();
    
3. A demo `Human` class

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
    
    // getters and setters
}
```

```java
// sub class Human
public class Human extends Animals {
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

    // getters and setters
}
```

4. Fields
- `getFields()`

> All the public fields up the entire class hierarchy.

- `getDelcaredFields()`

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

5. Constructors

- getConstructors

> all the constructors

- getDeclaredConstructors

>  only public constructors

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

