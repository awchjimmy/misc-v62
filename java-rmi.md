- [The Java Remote Method Invocation API (Java RMI)](https://docs.oracle.com/javase/8/docs/technotes/guides/rmi/hello/hello-world.html)
- [Getting Started Using Java RMI](https://docs.oracle.com/javase/8/docs/technotes/guides/rmi/hello/hello-world.html)

### interface
JDK 8 怎麼說：  
A remote object is an instance of a class that implements a `remote interface`. A remote interface extends the interface `java.rmi.Remote` and declares a set of `remote methods`. Each `remote method` must declare `java.rmi.RemoteException` (or a superclass of `RemoteException`) in its `throws` clause, in addition to any application-specific exceptions.

```java
public interface ChannelWorldInterface extends Remote, WorldChannelCommonOperations {}
public interface LoginWorldInterface extends Remote {}
public interface WorldChannelCommonOperations extends Remote {}
public interface WorldChannelInterface extends Remote, WorldChannelCommonOperations {}
public interface WorldLoginInterface extends Remote {}
public interface WorldRegistry extends Remote {}
```
