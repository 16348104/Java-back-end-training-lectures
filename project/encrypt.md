# 加密

> [Jasypt](http://www.jasypt.org/)

```gradle
// build.gradle
compile 'org.jasypt:jasypt:1.9.2'
```
- 密码

```java
// 加密
StrongPasswordEncryptor encryptor = new StrongPasswordEncryptor();
password = encryptor.encryptPassword(password);
// 验证
StrongPasswordEncryptor encryptor = new StrongPasswordEncryptor();
if (encryptor.checkPassword(password, encryptedPassword)) {
     // ...
} else {
     // ...
}
```
- 文本