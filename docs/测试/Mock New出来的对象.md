https://blog.csdn.net/u012760435/article/details/90703954

主要是两点：  
1. 要将New出来的对象的类，和所在的类，放入PrepareForTest注解中  
2. MockNew  
```java
PowerMockito.whenNew(MyThread.class).withAnyArguments().thenReturn(myThread);
```
