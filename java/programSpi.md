*Java编码规范*

**功能要求**

1. 所有用到临时目录的类都应该通过工具类申请自己的临时目录。同时，需要清理临时目录时只能清理自己申请的临时目录
2. 对于所有的的下载功能，都要限制下载目录
3. 所有需要查看功能运行情况的地方都要调用log处理，不能使用 ``` System.out.println()```方法
4. 对于so/dll文件的调用，要将so/dll文件放到自己的路径，同时指定so/dll文件优先搜索路径

**工具类方法**

1. ```java
   /**
   *@param file 要下载的文件
   *@param limitDir 限制下载的目录
   *下载文件，该方法在下载前会校验file是否在limitDir的目录中，如果不在则要抛出异
   */
   public static void download(File file,File limitDir)
   ```

2. ```java
   /**
   *获取临时目录
   *@param classe 要获取临时目录的类
   */
   public static File getTempDir(Class classe)
   ```

