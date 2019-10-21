#### 1.定义服务类(类的成员变量不要定义接口类型，不需要对外暴露的方法定义成private)
```java
package com.webservice.test;
public static class Test{
	public int add(int a,int b){
		return a+b;
	}
}
```

#### 2.添加sun-jaxws.xml
<?xml version="1.0" encoding="UTF-8"?>
```xml
<endpoints xmlns="http://java.sun.com/xml/ns/jax-ws/ri/runtime" version="2.0">
	<endpoint name="test" implementation="com.webservice.test.Test" url-pattern="/services/test" />
	<!--implementation 写服务类类名，url-pattern 写访问路径-->
</endpoints>
```

#### 3.如果需要注入Spring容器管理的bean，调用ContextLoader.getCurrentWebApplicationContext() 方法获取Context，再调用getBean方法获取需要的Bean即可