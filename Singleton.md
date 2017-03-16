# 单例的几种生成

### 懒汉式  

> 线程不安全，尽量不要用，虽说可以延迟初始化

```java
public class Singleton {

    private static Singleton instance = null;

    private Singleton() {}

    public static Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}

```

### 饿汉式

> 因为单例的实例被声明成 static 和 final 变量了，在第一次加载类到内存中时就会初始化，所以创建实例本身是线程安全的。


```java
 public class Singleton {
        //类加载时就初始化
        private static final Singleton instance = new Singleton();

        private Singleton() {}

        public static Singleton getInstance() {
            return instance;
        }
    }
```

### 静态内部类

> 这种写法仍然使用JVM本身机制保证了线程安全问题；由于 SingletonHolder 是私有的，除了 getInstance() 之外没有办法访问它，因此它是懒汉式的；同时读取实例的时候不会进行同步，没有性能缺陷；也不依赖 JDK 版本。

```java
public class Singleton {
    private static class SingletonHolder {
        private static final Singleton INSTANCE = new Singleton();
    }
    private Singleton() {}
    public static final Singleton getInstance() {
        return SingletonHolder.INSTANCE;
    }
}
```

### 枚举式

> 可以通过EasySingleton.INSTANCE来访问实例，比调用getInstance()方法简单。创建枚举默认就是线程安全的，不需要担心double checked locking。

```java
public enum Singleton {
    INSTANCE;
}
```
