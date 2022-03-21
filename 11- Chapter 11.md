# **Chapter 11: Systems**

## Introduction:
Program is like city. Could you manage all details yourself ? Probably not.
In the city you find a lot of teams who manage particular parts of the city (The water systems, power systems, traffic ...).
Although software teams are often organized like that too.

## Separate Constructing A System From Using It:
> First of all, construction a system is different process than use !
- The startup process is a concern that any application must address.
- The separation of concerns is one of the oldest and most important design techniques in our craft.
> Unfortunately, most applications don’t separate this concern. 
```java
    public Service getService() {
        if (service == null)
            service = new MyServiceImpl(...); // Good enough default for most cases?
        return service;
    }
```

### Separation of main:
One way to separate construction from use is simply to move all aspects of construction to
main, or modules called by main, and to design the rest of the system assuming that all
objects have been constructed and wired up appropriately.
<br>
<img  width="831" alt="Separating Main"  src="https://user-images.githubusercontent.com/59899627/159249180-bb8205f8-a51a-4d9b-8911-91490e152e7e.PNG">
<br>

### Dependece Injection:
- A powerful mechanism for separating construction from use.
- In the context of dependency management, an object should not take responsibility for instantiating dependencies itself.
**Exemple:**
```java
    MyService myService = (MyService)(jndiContext.lookup(“NameOfMyService”));
```
- The invoking object doesn’t control what kind of object is actually returned (as long it implements the appropriate interface, of course), but the invoking object still actively resolves the dependency.
- The Spring Framework provides the best known DI container for Java. You define which objects to wire together in an XML or annotation configuration file, then you ask for particular objects by name in Java code.

## Java Proxies:
- Why Java Proxies ?
> Proxy is a structural design pattern that provides an object that acts as a substitute for a real service object used by a client. A proxy receives client requests, does some work (access control, caching, etc.) and then passes the request to a service object.

**Exemple:**
<br>
<img  width="831" alt="java proxy" src="https://user-images.githubusercontent.com/59899627/159249227-eaf2b7ec-971a-46a8-becd-131617e1c53f.PNG">
<br>
- Step 1: Create an interface, Image.java:
```java
    public interface Image {
        void display();
    }
```
- Step 2: RealImage.java & ProxyImage.java
```java
    public class RealImage implements Image {

        private String fileName;

        public RealImage(String fileName){
            this.fileName = fileName;
            loadFromDisk(fileName);
        }

        @Override
        public void display() {
            System.out.println("Displaying " + fileName);
        }

        private void loadFromDisk(String fileName){
            System.out.println("Loading " + fileName);
        }
    }
```

```java
    public class ProxyImage implements Image{

        private RealImage realImage;
        private String fileName;

        public ProxyImage(String fileName){
            this.fileName = fileName;
        }

        @Override
        public void display() {
            if(realImage == null){
                realImage = new RealImage(fileName);
            }
            realImage.display();
        }
    }
```
- Step 3: ProxyPatternDemo.java
```java
    public class ProxyPatternDemo {
        
        public static void main(String[] args) {
            Image image = new ProxyImage("test_10mb.jpg");

            //image will be loaded from disk
            image.display(); 
            System.out.println("");
            
            //image will not be loaded from disk
            image.display(); 	
        }
    }   
```
- Step 4: Verify the output.
```Loading test_10mb.jpg```
```Displaying test_10mb.jpg```
```Displaying test_10mb.jpg```

## Pure Java AOP Frameworks:
- AOP is a programming paradigm that aims to increase modularity by allowing the separation of cross-cutting concerns. It does this by adding additional behavior to existing code without modifying the code itself.
- Instead, we can declare the new code and the new behaviors separately.
- Spring's AOP framework helps us implement these cross-cutting concerns.

## AspectJ Aspects:
It's an AOP Framework.



