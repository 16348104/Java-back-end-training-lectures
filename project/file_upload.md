# 文件上传

- 基于 `Servlet` 的文件上传实现

> [Apache Commons FileUpload](http://commons.apache.org/proper/commons-fileupload/)

> [quick use](http://commons.apache.org/proper/commons-fileupload/using.html)

1. Edit `build.gradle` file
```gradle
// build.gradle
compile 'commons-fileupload:commons-fileupload:1.3.2'
```
2. Edit `*.jsp` file

```html
<form action="your_action_url" method="post" enctype="multipart/form-data">
  <input type="file" name="upload">
</form>
```

3. Edit `Servlet` class

```java
DiskFileItemFactory diskFileItemFactory = new DiskFileItemFactory();
ServletContext servletContext = request.getServletContext();
String attribute= "javax.servlet.context.tempdir";
File repository = (File) servletContext.getAttribute(attribute);
diskFileItemFactory.setRepository(repository);

ServletFileUpload servletFileUpload = new ServletFileUpload(diskFileItemFactory);

try {
  List<FileItem> fileItems = servletFileUpload.parseRequest(request);
  for (FileItem fileItem : fileItems) {
      if (fileItem.isFormField()) {
          System.out.print(fileItem.getFieldName());
          System.out.print(" : ");
          System.out.println(fileItem.getString());
      } else {
          // FILE
          System.out.println(fileItem.getFieldName());
          System.out.println(fileItem.getName());
          System.out.println(fileItem.getContentType());
          System.out.println(fileItem.isInMemory());
          System.out.println(fileItem.getSize());

          File file = new File("d:/" + fileItem.getName());
          fileItem.write(file);
      }
  }
} catch (Exception e) {
  e.printStackTrace();
}
```
- 基于 `Spring` 的文件上传实现

1. Edit `build.gradle` file

```gradle
compile 'commons-fileupload:commons-fileupload:1.3.2'   
```
2. Edit `register.jsp` file

```html
<form action="${ctx}/student/register" method="post" enctype="multipart/form-data">
  <%-- change name from photo to photoFile --%> 
  <input type="file" name="photoFile" placeholder="PHOTO">
</form>
```

3. Edit `web-servlet.xml` file

```xml
<bean id="multipartResolver" class="org.springframework.web.multipart.commons.CommonsMultipartResolver">
  <property name="defaultEncoding" value="UTF-8"/>
</bean>
```

4. Create directory `/webapp/static/photo`      

5. Edit `StudentController` class

```java
public static final String PHOTO_PATH = "/static/photo";

@RequestMapping("register")
private String register(Student student, @RequestParam MultipartFile photoFile) throws IOException {
  String photoPath = application.getRealPath(PHOTO_PATH);
  photoFile.transferTo(new File(photoPath, photoFile.getOriginalFilename()));
  student.setPhoto(photoFile.getOriginalFilename());

  // register ...
}
```
