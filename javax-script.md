花時間了解以下 class 用途，並且找出在專案中如何應用
```
javax.script.Compilable;
javax.script.CompiledScript;
javax.script.Invocable;
javax.script.ScriptEngine;
javax.script.ScriptEngineFactory;
javax.script.ScriptEngineManager;
javax.script.ScriptException;
```

### ScriptEngineManager

JDK 8 怎麼說：
> The ScriptEngineManager implements a discovery and instantiation mechanism for ScriptEngine classes and also maintains a collection of key/value pairs storing state shared by all engines created by the Manager. This class uses the service provider mechanism to enumerate all the implementations of ScriptEngineFactory.


```java
ScriptEngineManager manager = new ScriptEngineManager();

ScriptEngine engine = manager.getEngineByName("javascript");
```

要怎麼知道 `getEngineByName` 有什麼選項呢？
> shortName - The short name of the ScriptEngine implementation. returned by the getNames method of its ScriptEngineFactory.

```java
ScriptEngineManager manager = new ScriptEngineManager();
List<ScriptEngineFactory> factories = manager.getEngineFactories();

for (ScriptEngineFactory factory : factories) {
    List<String> names = factory.getNames();
}
```

### ScriptEngineFactory

JDK 8 怎麼說：
> ScriptEngineFactory is used to describe and instantiate ScriptEngines.

### ScriptEngine

JDK 8 怎麼說：
> ScriptEngine is the fundamental interface whose methods must be fully functional in every implementation of this specification.

### Invocable

JDK 8 怎麼說：
> The optional interface implemented by ScriptEngines whose methods allow the invocation of procedures in scripts that have previously been executed.

讓 java 可以呼叫 js 寫的 function

----

### Upgrade Journey
* [Rhino Migration Guide](https://wiki.openjdk.org/display/Nashorn/Rhino+Migration+Guide) (JDK 7 to JDK 8)
* [The Nashorn Java API](https://docs.oracle.com/javase//9/nashorn/nashorn-java-api.htm)

### 升級痛點
從 Rhino 的 package 到 Nashorn 的 class。  
從一個 script 的觀點來看，必須先找到使用哪些 class，再找到它屬於哪個 package 才能引用，沒辦法單純搜尋取代完成。

細節討論參考：[issue #1](https://github.com/awchjimmy/misc-v62/issues/1)
