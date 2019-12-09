URLClassLoader可以加载class而不依赖于已经设定的classpath，使用方法：
 ```java
	URL url=null;
        try {
            url=new URL("file:/E:classes/");
        } catch (MalformedURLException e) {
            e.printStackTrace();
        }
        URL urls[]=new URL[]{url};
        URLClassLoader cl=new URLClassLoader(urls);//构造classLoader使用url形式的指定的classpath
        try {
            Class c=cl.loadClass("com.tcmkb.controller.TestController");
            Method ms[]=c.getMethods();
            for (Method m:ms){
                System.out.println(m.getName());
            }
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        }
```