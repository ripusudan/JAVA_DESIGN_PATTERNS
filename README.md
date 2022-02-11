# JAVA_DESIGN_PATTERNS

##### A design pattern is a common, well-described solution to a common software problem
---

Three category 

## Creational , Structural , Behavioral 

`REMEMBER TIP ==>   Create Structure to Bahave or (BSC)`

--- 
# Creational Design Patterns

> ANGRY BOSS :angry: TO LAZY WORKERS :speech_balloon: 
 
"single factory :factory: you can not build using prototype"

1. Singleton Pattern
2. Factory Pattern
3. Abstract Factory Pattern
4. Builder Pattern
5. Prototype Pattern

## Singleton Pattern

`Single class object does tons of work with only one instance`

* As only one object is restriction hence singleton is a class is instantiated only once.
* Put that single object refrence in class itself  by creating a static field in the class.
* A static method exists on the class to obtain the instance of the class and is typically named something such as getInstance(). 
* The singleton class typically has a private constructor to prevent the singleton class from being instantiated via a constructor.
* Rather, the instance of the singleton is obtained via the static getInstance() method.

> Create a class with private constructor and have a refrence of class object in static refrence of same class.
> How we get that static object when we have private construtor,obviusly by a static method getInstance()

### Singleton Pattern (Eager initialization)
> do it fast !! :beer:

```java
public class SingletonExample {

	private static SingletonExample singletonExample = new SingletonExample();

	private SingletonExample() {
	}

	public static SingletonExample getInstance() {		
		return singletonExample;
	}

	public void sayHello() {
		System.out.println("Hello");
	}
}

public class Demo {

	public static void main(String[] args) {
		SingletonExample singletonExample = SingletonExample.getInstance();

		singletonExample.sayHello();
	}

}
```

### Singleton Pattern (Static block initialization)
> Eager initialization you are doing ,have you think about exception? :angry:

> Static block initialization implementation is similar to eager initialization, except that instance of class is created in the static block that provides option for exception handling.

```java
public class StaticBlockSingleton {

    private static StaticBlockSingleton instance;
    
    private StaticBlockSingleton(){}
    
    //static block initialization for exception handling
    static{
        try{
            instance = new StaticBlockSingleton();
        }catch(Exception e){
            throw new RuntimeException("Exception occured in creating singleton instance");
        }
    }
    
    public static StaticBlockSingleton getInstance(){
        return instance;
    }
}

```

### Singleton Pattern (Lazy Initialization)
> do it lazy :tired_face:

```java
public class LazyInitializedSingleton {

    private static LazyInitializedSingleton instance;
    
    private LazyInitializedSingleton(){}
    
    public static LazyInitializedSingleton getInstance(){
        if(instance == null){
            instance = new LazyInitializedSingleton();
        }
        return instance;
    }
}

```

### Singleton Pattern (Thread Safe Singleton)
> How about multithreading above all break ,do it in thread safe manner :lock:

```java
public class ThreadSafeSingleton {

    private static ThreadSafeSingleton instance;
    
    private ThreadSafeSingleton(){}
    
    public static synchronized ThreadSafeSingleton getInstance(){
        if(instance == null){
            instance = new ThreadSafeSingleton();
        }
        return instance;
    }
    
}

```

> Singleton pattern is used for logging, drivers objects, caching and thread pool.
> Singleton design pattern is also used in other design patterns like Abstract Factory, Builder, Prototype, Facade etc.
> Singleton design pattern is used in core java classes also, for example java.lang.Runtime, java.awt.Desktop.

## Prototype Pattern

* In the prototype pattern, a new object is created by cloning an existing object.
* In JavaSW, the clone() method is an implementation of this design pattern.
* The prototype pattern can be a useful way of creating copies of objects.
* if an original object is created with a resource such as a data stream that may not be available at the time that a clone of the object is needed.
* if the original object creation involves a significant time commitment, such as reading data from a databaseW or over a network.
* you can utilize the clone() method and the Cloneable interface. By default, clone() performs a shallow copy.

> Create an interface of type Prototype which return Prototype and implement with various class like Person & Dog .
> in doClone method return new Object of same type


```java
public interface Prototype {

	public Prototype doClone();

}

public class Person implements Prototype {

	String name;

	public Person(String name) {
		this.name = name;
	}

	@Override
	public Prototype doClone() {
		return new Person(name);
	}

	public String toString() {
		return "This person is named " + name;
	}
}

public class Dog implements Prototype {

	String sound;

	public Dog(String sound) {
		this.sound = sound;
	}

	@Override
	public Prototype doClone() {
		return new Dog(sound);
	}

	public String toString() {
		return "This dog says " + sound;
	}
}

public class Demo {

	public static void main(String[] args) {

		Person person1 = new Person("Fred");
		System.out.println("person 1:" + person1);
		Person person2 = (Person) person1.doClone();
		System.out.println("person 2:" + person2);

		Dog dog1 = new Dog("Wooof!");
		System.out.println("dog 1:" + dog1);
		Dog dog2 = (Dog) dog1.doClone();
		System.out.println("dog 2:" + dog2);

	}

}
```


