# Chapter 3 常用库

- Java Library
    1. `org.json`

      ```
      // build.gradle
      compile 'org.json:json:20151123'
      ```

      ```java
      // Java object to JSON object 
      JSONObject jsonObject = new JSONObject(model);
      String json = jsonObject.toString(4);

      // Java collection to JSON array
      JSONArray jsonArray = new JSONArray(collection);
      String json = jsonArray.toString(4);

      // JSON object to Java object

      ```
        
    2. `Jackson JSON Processor`
    
      ```
      // build.gradle
      compile 'com.fasterxml.jackson.core:jackson-databind:2.5.3'
      ```

      ```java

      ObjectMapper objectMapper = new ObjectMapper();
      objectMapper.configure(SerializationFeature.INDENT_OUTPUT, true);

      // Java object to JSON Object
      String json = objectMapper.writeValueAsString(model);

      // Java collection to JSON Array
      String json = objectMapper.writeValueAsString(collection);

      // JSON Object to Java object
      Model model = objectMapper.readValue(json, Model.class);

      ```
        
    3. `Google-gson`

      ```
      // build.gradle
      compile 'com.google.code.gson:gson:2.5'
      ```

      ```java
      Gson gson = new GsonBuilder().setPrettyPrinting().create();

      //  Java object to JSON object
      String json = gson.toJson(model); 

      // JSON object to JAVA object
      Model model = gson.fromJson(json, Model.class);
      ```
        
    4. `fastjson`
    
      ```
      // build.gradle
      compile 'com.alibaba:fastjson:1.2.7'
      ```

      ```java
      // Java Object to JSON object
      String json = JSON.toJSONString(model, true);

      // JSON object to Java object
      Model model = JSON.parseObject(json, Model.class);
      ```
        
- 一个完整的例子

    ```java
    package test;

    import com.alibaba.fastjson.JSON;
    import com.fasterxml.jackson.core.type.TypeReference;
    import com.fasterxml.jackson.databind.ObjectMapper;
    import com.fasterxml.jackson.databind.SerializationFeature;
    import com.fasterxml.jackson.databind.type.TypeFactory;
    import com.google.gson.Gson;
    import com.google.gson.GsonBuilder;
    import com.google.gson.reflect.TypeToken;
    import model.User;
    import org.json.JSONArray;
    import org.json.JSONObject;

    import java.io.IOException;
    import java.util.ArrayList;
    import java.util.Arrays;
    import java.util.List;

    /**
     * @author mingfei.net@Gmail.com
     *         21:17, 6/25/16.
     */
    public class JSONTest {
          public static void main(String[] args) {

              User user = new User(1, "user@gmail.com", "123");

              List<User> users = new ArrayList<>();
              for (int i = 0; i < 2; i++) {
                  users.add(new User(i, "user" + i + "@gmail.com", "123"));
              }

              String jsonObjectString, jsonArrayString;

              System.out.println("\n--- json.org ---\n");

              JSONObject jsonObject = new JSONObject(user);
              // java object to json object
              System.out.println(jsonObject.toString(4));

              JSONArray jsonArray = new JSONArray(users);
              // java collection to json array
              System.out.println(jsonArray.toString(4));

              System.out.println("\n--- jackson ---\n");

              ObjectMapper objectMapper = new ObjectMapper();
              objectMapper.configure(SerializationFeature.INDENT_OUTPUT, true);

              try {
                  // java object to json object
                  jsonObjectString = objectMapper.writeValueAsString(user);
                  System.out.println(jsonObjectString);
                  // java collection to json array
                  jsonArrayString = objectMapper.writeValueAsString(users);
                  System.out.println(jsonArrayString);
                  // json object to java object
                  System.out.println(objectMapper.readValue(jsonObjectString, User.class));
                  // json array to java collection
                  System.out.println(objectMapper.readValue(jsonArrayString, TypeFactory.defaultInstance().constructCollectionType(List.class, User.class))); // method 1
                  System.out.println(objectMapper.readValue(jsonArrayString, new TypeReference<List<User>>() {
                  })); // method 2
                  System.out.println(objectMapper.readValue(jsonArrayString, objectMapper.getTypeFactory().constructCollectionType(List.class, User.class))); // method 3
                  System.out.println(Arrays.asList(objectMapper.readValue(jsonArrayString, User[].class))); // method4
              } catch (IOException e) {
                  e.printStackTrace();
              }

              System.out.println("\n--- gson ---\n");

              Gson gson = new GsonBuilder().setPrettyPrinting().create();
              // java object to json object
              jsonObjectString = gson.toJson(user);
              System.out.println(jsonObjectString);
              // java collection to json array
              jsonArrayString = gson.toJson(users);
              System.out.println(jsonArrayString);
              // json object to java object
              System.out.println(gson.fromJson(jsonObjectString, User.class));
              // json array to java collection
              System.out.println(gson.fromJson(jsonArrayString, new TypeToken<List<User>>() {
              }.getType())); // method 1
              System.out.println(gson.fromJson(jsonArrayString, ArrayList.class)); // method 2

              System.out.println("\n--- fastjson ---\n");

              // java object to json object
              jsonObjectString = JSON.toJSONString(user, true);
              System.out.println(jsonObjectString);
              // java collection to json array
              jsonArrayString = JSON.toJSONString(users, true);
              System.out.println(jsonArrayString);
              // json object to java object
              System.out.println(JSON.parseObject(jsonObjectString, User.class));
              // json array to java collection
              System.out.println(JSON.parseArray(jsonArrayString, User.class));
          }
    }
    
    // model class
    class User implements Serializable {
          private Integer id;
          private String email;
          private String password;

          public User() {
          }

          public User(Integer id, String email, String password) {
              this.id = id;
              this.email = email;
              this.password = password;
          }
          
          // getters and setters
    }

    ```
    
- fastjson 数据绑定

    > [Samples DataBind](https://github.com/alibaba/fastjson/wiki/Samples-DataBind)
    
    > Fastjson full support databind, it's simple to use.
    
    - Encode
    
        ```java
        import com.alibaba.fastjson.JSON;
        
        Group group = new Group();
        group.setId(0L);
        group.setName("admin");
        
        User guestUser = new User();
        guestUser.setId(2L);
        guestUser.setName("guest");
        
        User rootUser = new User();
        rootUser.setId(3L);
        rootUser.setName("root");
        
        group.addUser(guestUser);
        group.addUser(rootUser);
        
        String jsonString = JSON.toJSONString(group);
        
        System.out.println(jsonString);
        ```
    
    - Output
        
        ```
        {"id":0,"name":"admin","users":[{"id":2,"name":"guest"},{"id":3,"name":"root"}]}
        ```
    
    - **Decode**
    
        > Group group = JSON.parseObject(jsonString, Group.class);
        
        ```
        String jsonString = ...;
        Group group = JSON.parseObject(jsonString, Group.class);
        ```
    
    - Group.java
        
        ```java
        public class Group {
        
            private Long       id;
            private String     name;
            private List<User> users = new ArrayList<User>();
        
            public Long getId() {
                return id;
            }
        
            public void setId(Long id) {
                this.id = id;
            }
        
            public String getName() {
                return name;
            }
        
            public void setName(String name) {
                this.name = name;
            }
        
            public List<User> getUsers() {
                return users;
            }
        
            public void setUsers(List<User> users) {
                this.users = users;
            }
    
                public void addUser(User user) {
                    users.add(user);
                }
        }
        ```
    
    - User.java
    
        ```java
        public class User {
        
            private Long   id;
            private String name;
        
            public Long getId() {
                return id;
            }
        
            public void setId(Long id) {
                this.id = id;
            }
        
            public String getName() {
                return name;
            }
        
            public void setName(String name) {
                this.name = name;
            }
        }
        ```
    
- JavaScript
  1. Parse JSON in jQuery AJAX

    ```javascript
    $(function () {
        $.ajax({
            url: 'request_url',
            type: 'POST',
            data: {'key': value},
            dataType: 'json',
            success: function (result) {
                // parse JSON object
                alert(result.property);
                // iterate JSON array
                $.each(result, function (index, item) {
                    alert(item.property);
                });
            }
        });
    });
    ```

  