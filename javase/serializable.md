# Serializable 序列化和反序列化

1. 序列化就是一种用来处理对象流的机制,所谓对象流也就是将对象的内容进行流化。可以对流化后的对象进行读写操作,也可将流化后的对象传输于网络之间。
2. 序列化是为了解决在对对象流进行读写操作时所引发的问题。
3. `java.io.Serializable` `标识接口`
  - 类通过实现 `java.io.Serializable` 接口以启用其序列化功能
  - 未实现此接口的类将无法使其任何状态序列化或反序列化
  - 可序列化类的所有子类型本身都是可序列化的
  - 序列化接口没有方法或字段，仅用于标识可序列化的语义
  - `transient`
4. 一个模型类

  ```java
  public class User implements Serializable {
      private Integer id;
      private String name;
      private double height;
      private transient boolean isMarried;

      public User() {
      }

      public User(Integer id, String name, double height, boolean isMarried) {
          this.id = id;
          this.name = name;
          this.height = height;
          this.isMarried = isMarried;
      }

      @Override
      public String toString() {
          return "User{" +
                  "id=" + id +
                  ", name='" + name + '\'' +
                  ", height=" + height +
                  ", isMarried=" + isMarried +
                  '}';
      }
  }
  ```
    
5. `java.io.ObjectOutputStream` 类
  - 将 `Java` 对象写入 `OutputStream`
    
    ```java
    public class OutputTest {
        public static void main(String[] args) {
            User user = new User(1, "username", 1.8, true);
            try (ObjectOutputStream objectOutputStream = new ObjectOutputStream(new FileOutputStream("user.data"))) {
                objectOutputStream.writeObject(user);
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
    ```
  
6. `java.io.ObjectInputStream` 类
  - 从 `InputStream` 中重构 `Java` 对象
    
    ```java
    public class OutputTest {
        public static void main(String[] args) {
            try (ObjectInputStream objectInputStream = new ObjectInputStream(new FileInputStream("user.data"))) {
                User u = (User) objectInputStream.readObject();
                System.out.println(u);
            } catch (IOException | ClassNotFoundException e) {
                e.printStackTrace();
            }
        }
    }
    
    // output：
    // User{id=1, name='username', height=1.8, isMarried=false}
    ```
