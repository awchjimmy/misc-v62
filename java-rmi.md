- [The Java Remote Method Invocation API (Java RMI)](https://docs.oracle.com/javase/8/docs/technotes/guides/rmi/hello/hello-world.html)
- [Getting Started Using Java RMI](https://docs.oracle.com/javase/8/docs/technotes/guides/rmi/hello/hello-world.html)

### Define the remote interface
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

### Implement the server
JDK 8 怎麼說：  
A "server" class, in this context, is the class which has a `main` method that creates an instance of the remote object implementation, exports the remote object, and then binds that instance to a name in a Java RMI `registry`. The class that contains this `main` method could be the implementation class itself, or another class entirely.

```java
public class ChannelWorldInterfaceImpl extends UnicastRemoteObject implements ChannelWorldInterface {}
public class LoginWorldInterfaceImpl extends UnicastRemoteObject implements LoginWorldInterface {}
public class WorldChannelInterfaceImpl extends UnicastRemoteObject implements WorldChannelInterface {}
public class WorldLoginInterfaceImpl extends UnicastRemoteObject implements WorldLoginInterface {}
public class WorldRegistryImpl extends UnicastRemoteObject implements WorldRegistry {}
```

### Implement the client
JDK 8 怎麼說：  
The client program obtains a stub for the registry on the server's host, looks up the remote object's stub by name in the registry, and then invokes the `sayHello` method on the remote object using the stub.

```java
// 1. get registry from host
Registry registry = LocateRegistry.getRegistry(initialProp.getProperty("net.sf.odinms.world.host"), Registry.REGISTRY_PORT, new SslRMIClientSocketFactory());

// 2. looks up the remote object's stub by name in the registry
worldRegistry = (WorldRegistry) registry.lookup("WorldRegistry");

// 3. invokes method
lwi = new LoginWorldInterfaceImpl();
wli = worldRegistry.registerLoginServer(initialProp.getProperty("net.sf.odinms.login.key"), lwi);
```
