其他人的笔记：  
https://blog.csdn.net/qq_41157588/article/details/106737191



### RPC & Netty 原理

### Dubbo框架设计
https://dubbo.apache.org/zh/docs/v2.7/dev/design/#m-zhdocsv27devdesign

##### Service层
唯一的Business业务层，暴露接口和实现（implement与interface）。
也是Duboo以外，customer与provider需要实现的部分。

##### RPC层
1. Config
配置层。封装配置文件中解析出来的信息，如ReferenceConfig与ServiceConfig。
2. Proxy
服务代理层。生成客户端与服务端的代理对象。
3. Registry
注册中心层。完成服务的发现与注册。
4. Cluster
路由层。完成负载均衡。
5. monitor
监控层。
6. Protocol
远程调用层。封装RPC调用。Invoker/ Protocol/ Exporter

##### Remoting
远程通讯
1. Exchange
信息交换层。创建客户端、服务端，架起通讯管道。
2. Transport
传输层。传输数据，基于Netty
3. Serialize
序列化层。传输数据中的序列化与反序列化。



### 标签解析
如何解析Dubbo的xml配置？
是利用Spring的标签解析，Spring提供了一个总接口BeanDefinationParser。
DubboBeanDefinitionParser实现了该接口。

在初始化容器的时候，DubboNamespaceHandler注册了大量的BeanDefinitionParser。因此在扫描到对应标签的时候，如application、monitor等，就会有对用的Config，如ApplicationConfig.class等。

解析标签的目的，就是把标签的属性保存到对应的Config中。
其中ReferenceBean和ServiceBean是两个特殊的Config。

### 服务暴露流程
ServiceBean实现了InitializiongBean、ApplicationListener等接口

### 服务调用流程
https://dubbo.apache.org/zh/docs/v2.7/dev/design/#%E8%B0%83%E7%94%A8%E9%93%BE
