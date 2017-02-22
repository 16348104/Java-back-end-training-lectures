# Chapter 7 Stream & File

1. `InputStream` / `OutputStream` / `Reader` / `Writer`

   > 都是抽象类，注意需要 `close()`
   >
   > 输入输出是对程序而言的

   * `InputStream`
     * 基于 字节 的输入流
   * `OutputStream`
     * 基于 字节 的输出流
   * `Reader`
     * 基于 字符 的输入流
   * `Writer`
     * 基于 字符 的输出流

2. `RandomAccessFile`

   > 基本取代 `DataInputStream` 和 `DataOutputStream`

   ```java
    public class DataInputStream
    extends FilterInputStream
    implements DataInput

    public class DataOutputStream
    extends FilterOutputStream
    implements DataOutput

    public class RandomAccessFile
    extends Object
    implements DataOutput, DataInput, Closeable
   ```

3. `BufferedInputStream` / `BufferedOutputStream` / `BufferedReader` / `BufferedWriter`

   > 提高输入输出效率

   * `bufferedReader.readLine()`

4. `File`

   * `File` 指代文件 `file` 或目录 `directory`
   * `File` 不处理文件内容，只处理文件或目录的周边信息
   * `File` 常用方法
     * `canRead`
     * `canWrite`
     * `createNewFile`
     * `delete`
     * `deleteOnExit`
     * `getAbsoluteFile`
     * `getAbsolutePath`
     * `getName`
     * `getParent`
     * `getParentFile`
     * `getPath`
     * `getTotalSpace`
     * `getUsableSpace`
     * `isAbsolute`
     * `isDirectory`
     * `isFile`
     * `isHidden`
     * `lastModified`
     * `length`
     * `list`
     * `listFiles`
     * `listRoots`
     * `mkdir`
     * `mkdirs`
     * `renameTo`
     * `setLastModified`
     * `setReadable`
     * `setReadOnly`
     * `setWritable`



