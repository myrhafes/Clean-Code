# **Chapter 3: Functions**

Functions are the first line of organisation in any program.
- So what is that makes a function easy to read and understand ?
- How can we make a function communicate its intent ?
- What attributes can we give our functions that will allow a casual reader to intuit the kind of program they live inside ? 

## Small:
- Should be at maximum 20 lines long.
- The blocks within if, else, while, should be one line long. Probably that line shoud be a function call.
- The nested structures (blocks) should be one or two at maximum.

## Do One Thing:
Functions should do one thing. They should do it well.
> Single Responsibility Principle (SRP).

## One Level Of Abstraction:
Make your code reads like a top to down story.
To do that, should every function written in a single level of abstraction and followed by the next function in the next level of abstraction, and the third one in the third level of abstraction, and so on ...

## Switch Statments:
The problem with switch is that there are an unlimeted number of functions that will have the same switch structure, and this repetition is an indication that your code well not design.

## Use Description Names:
- Don't be afraid to make a name long. A long description name is better than a short unclear name. And a long description name is is beter than a long descriptive comment.
- Don't be afraid to spend time choosing a name.
- Choosing descriptive name will clarify the design of the module in your mind and help you to improve it.
- Be consistent in your names. Use the same phrases, nouns and verbs in the function names that you choose for your modules.

## Function Arguments:
- The ideal number of arguments for a function is zero.
- Three arguments should be avoided as possible.
- More than three requires a special justification and souldn't be used anyway.

### Common Monadic Forms (One Arg Function):
There are three reasons (three forms) to pass a single argument into a function.
- Function that asking a question about that argument.
```java
    boolean fileExists("MyFile");
```
- Function that transforming the argument into something else and returning it.
```java
    InputStream fileOpen("MyFile"); //Transform a file
```
- Function is an event: in this form there is an input argument, and the function use the argument to alter the state of the system.
```java
    void passwordAttemptFailedNtimes(int attempts);
```

### Flag Arguments:
Flag arguments are ugly. It complicates the signature of the function. It make the function does more than one thing. One thing if the flag is true and another if the flag is false. They are confusing and should be eliminated if possible.
```java
    public Booking book (Consumer c, boolean isPremium) {
        if(isPremium){
            //...
        }else {
            //...
        }
        //...
    }
```
#### Better:
```java
    public Booking regularBook (Consumer c) {
        //...
    }

    public Booking premiumBook (Consumer c) {
        //...
    }
```
### Dyadic Functions (Two Arguments Function):
- A function with two argument is harder to understand than a monadic function. But of course, there are times where two arguments are appropriate like ``` Point p = new Point(0,0) ``` this is for sure because the point naturally take two arguments.

- It will be better if you find mechanism to convert the dyadic function to monadic (in some cases if possible). For exemple, ``` writeField(outputStrem, name) ``` can convert to monadic by any of these methods:
    - Make the ``` writeField ``` a membre function of ```outputStream``` class so that you say ``` outputStream.writeField(name) ``` .
    - Make the ```outputStream``` a member variable of the current class so that you don't have to pass it, like this ``` writeField(name) ``` .

### Triads Functions (Three Arguments Function):
Function that take three arguments are significantly harder to understand than dyadic. You should think very carefuly creating a triad.

### Argument Objects:
When a function seems to need more than two or three arguments then, it is likly that some of those arguments should be wrapped into a class of their own.

```java
    Circle makeCircle(double x, double y, double radius);
}
```

#### Better:

```java
    Circle makeCircle(Point center, double radius);
}
```

### Argument Lists:
- Sometimes we want to pass a variable of arguments into a function. For exemple ``` String.format("%s worked % .2f hours", name, hours); ```. Then the declaration for this function will be as below ``` public String format(String format, Object ...args) ```.

- So all the previous rules apply. Functions that take variable arguments can be monads, dyads or trias
```java
    void monad(Integer ...Args);
    void dyad(String name, Integer ...Args);
    void triad(String name, int count, Integer ...args);
```

### Verbs And Keywords:
choosing good names for a function can go a long ways toward explaining the intent of the function and the order and intent of the arguments.

```java
   assertEquals(expected, actual);
```

#### Better:

```java
   assertExpectedEqualsActual(expected, actual);
```

## Have No Side Effects:
No side effect mean that your function promises to do one thing. But it also does other hidden things. So try to avoid these things beacause they leads to a temporal couplings.
> For exemple the function ```checkedPassword()``` has a side effect is the call to ```Session.initialize()``` .
> In this case we might rename the function to ```checkPasswordAndInitializeSession()```, though that certainly violates **DO ONE THING**.

## Command Query Separation:
Functions should either do something or answer something, but not both. For exemple:
```java
   public boolean set(String attribute, String value);
```
- This function sets the value of a named attribute and returns true if it is successful and
false if no such attribute exists. This leads to odd statements like this:
```java
   if (set("username", "unclebob"))...
```
This function confused the reader. It is asking whether the **username** attribute was previously set to **unclebob**? Or is it asking whether the **username** attribute was successfully set to **unclebob**?
> The solution is to separate the command from the query so that the ambiguity cannot occur.
```java
   if (attributeExists("username")) {
        setAttribute("username", "unclebob");
        //...
    }
```
## Prefer Exceptions To Returning Error Codes:
Returning error codes from command functions is a subtle violation of command query separation. It promotes commands being used as expressions in the predicates of if statements.
```java
    if (deletePage(page) == E_OK)
```
This does not suffer from verb/adjective confusion but does lead to deeply nested structures. When you return an error code, you create the problem that the caller must deal with the error immediately.
```java
    if (deletePage(page) == E_OK) {
        if (registry.deleteReference(page.name) == E_OK) {
            if (configKeys.deleteKey(page.name.makeKey()) == E_OK){
                logger.log("page deleted");
            } else {
                logger.log("configKey not deleted");
            }
        } else {
            logger.log("deleteReference from registry failed");
        }
    } else {
        logger.log("delete failed");
        return E_ERROR;
    }
```
#### Better:
```java
    try {
        deletePage(page);
        registry.deleteReference(page.name);
        configKeys.deleteKey(page.name.makeKey());
    }
    catch (Exception e) {
        logger.log(e.getMessage());
    }
```
### Extact Try/Catch Blocks:
Try/catch blocks are ugly in their own right. They confuse the structure of the code and mix error processing with normal processing. So it is better to extract the bodies of the try and catch blocks out into functions of their own.
```java
    public void delete(Page page) {
        try {
            deletePageAndAllReferences(page);
        }catch (Exception e) {
            logError(e);
        }
    }

    private void deletePageAndAllReferences(Page page) throws Exception {
        deletePage(page);
        registry.deleteReference(page.name);
        configKeys.deleteKey(page.name.makeKey());
    }

    private void logError(Exception e) {
        logger.log(e.getMessage());
    }
```
### Error Handling Is One Thing:
Functions do one thing. Error handling is one thing!
So functions handles errors shoudn't do another thing.
> If the keyword ```try``` exist in a function, it should be first in the function and should be nothing after the ```catch/finally``` blocks.

### The Error.java Dependency Magnet:
> Never ever use enum for handling errors.

## Don't Repeat Your Self:
If an algorithm repeat you should create a function to eliminate the repetition.

## Structure programming:
Dijkstra’s rules of structured programming said that every function, and every block within a function, should have one entry and one exit. Following these rules means that there should only be one return statement in a function, no break or continue statements in a loop, and never, ever, any goto statements.
> So if you keep your function small, then the occasional multiple return, break, or continue statement does no harm and can sometimes even be more expensive than the single-entry, single-exit rule.
