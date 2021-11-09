### 验证方法被正确调用  
Mockito.verify()  
```java
@Test
void verifyTest(){
  Person mockPerson = Mockito.mock(Person.class);
  mockPerson.setId(1);
  mockPerson.setName("TestOps");

  Mockito.verify(mockPerson).setId(1);
  Mockito.verify(mockPerson).setName("TestOps");
}
```

### 使用桩代码模拟方法返回
```java
Mockito.when(objectA.functionA(...)).thenReturn(resultA);
Mockito.verify(objectA).functionA(...);
Mockito.verify(objectA, times(n)).functionA(...);
```
times(n) 表示验证方法被调用了n次

### 验证调用顺序
```java
@Test
void orderTest(){
  Person singleMock = Mockito.mock(Person.class);
  singleMock.setName("1");
  singleMock.setName("2");

  InOrder inOrder = Mockito.inOrder(singleMock);
  inOrder.verify(singleMock).setName("1");
  inOrder.verify(singleMock).setName("2");


  Person first = Mockito.mock(Person.class);
  Person second = Mockito.mock(Person.class);
  first.setName("1");
  second.setName("2");

  InOrder inOrder = Mockito.inOrder(first, second);
  inOrder.verify(first).setName("1");
  inOrder.verify(second).setName("2");
}
```

### 连续调用
```java
Mockito.when(objectA.functionA(...)).thenReturn(resultA).thenReturn(resultB);
```
当objectA.functionA(...)被调用两次时，第一次返回resultA，第二次返回resultB

### Spy
spy是以真实对象创建的一个监控对象，当使用spy对象时，真实对象也会被调用。
```java
@Test
void spyTest(){
  Person person = new Person(1, "name");
  Person spy = Mockito.spy(person);
  Mockito.when(spy.getName()).thenReturn("other");
  
  System.out.println(spy.getName());
  System.out.println(spy.getId());
}
```
注意返回的是  
other  
1  
