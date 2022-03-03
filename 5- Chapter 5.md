# **Chapter 5: Formatting**
Code formatting is important. Code formatting is about communication, and communication is the professional developer's first order of business.

## Vertical Formatting:
### Vertical openness between concepts:
You should separate the package declaration, the import(s), and each of the functions.
```java
    package fitnesse.wikitext.widgets;

    import java.util.regex.*;

    public class BoldWidget extends ParentWidget {
        public static final String REGEXP = "'''.+?'''";
        private static final Pattern pattern = Pattern.compile("'''(.+?)'''", Pattern.MULTILINE + Pattern.DOTALL );

        public BoldWidget(ParentWidget parent, String text) throws Exception {
            super(parent);
            Matcher match = pattern.matcher(text);
            match.find();
            addChildWidgets(match.group(1));
        }

        public String render() throws Exception {
            StringBuffer html = new StringBuffer("<b>");
            html.append(childHtml()).append("</b>");
            return html.toString();
        }
    }
```

### Vertical density:
The lines of code that are more related to each other should appear close to each other.
For exemple:
```java
    public class ReporterConfig {
        /**
        * The class name of the reporter listener
        */
        private String m_className;
        /**
        * The properties of the reporter listener
        */
        private List<Property> m_properties = new ArrayList<Property>();
        public void addProperty(Property property) {
            m_properties.add(property);
        }
    }
```

### Vertical distance:
#### Variable declarations:
Variables should be declared as close to their usage as possible because our functions are very short, local variables should appear at the top to each function. like the following:
```java
    private static void readPreferences() {
        InputStream is= null;
        try {
            is= new FileInputStream(getPreferencesFile());
            setPreferences(new Properties(getPreferences()));
            getPreferences().load(is);
        } catch (IOException e) {
            try {
                if (is != null)
                is.close();
            } catch (IOException e1) {
                
            }
        }
    }
```
For loops control variable should usually be declared within the loop statement.
```java
    public int countTestCases() {
        int count= 0;
        for (Test each : tests) count += each.countTestCases();
        return count;
    }
```

#### Instance variables:
Variables should be declared in one well-known place(at the top of the class). Because they are used by many methods within the class. And because every body should know where to go to see the declarations.

#### Dependent functions:
If one function calls another, they should be vertically close, and the caller should be above the call.

#### Conceptual affinity:
This mean certain parts of code want to be near other parts, sometimes because a group of functions perform a similar operation or one function calling another.
```java
    public class Assert {

        static public void assertTrue(String message, boolean condition) {
            if (!condition)
            fail(message);
        }

        static public void assertTrue(boolean condition) {
            assertTrue(null, condition);
        }

        static public void assertFalse(String message, boolean condition) {
            assertTrue(message, !condition);
        }

        static public void assertFalse(boolean condition) {
            assertFalse(null, condition);
        } 
        // ...
    }
```
#### Vertical ordering:
This mean a function that is called should be below a function that does calling. We want this because it creates nice flow down the source code module from high level to low level.

## Horizental Formatting:
> How wide should a line be ?
The answer for that is : **You should never have to scroll to the right.**

### Horizental opennes and density:
We use horizental white space to associate things that are strongly related and disassociate things that are more weakly related.
```java
    private void measureLine(String line) {
        lineCount++;
        int lineSize = line.length();
        totalChars += lineSize;
        lineWidthHistogram.addLine(lineSize, lineCount);
        recordWidestLine(lineSize);
    }
```
- The writer didn't put horizental spaces between the function name and the opening parenthesis. This is because the function and its arguments are closely related.

### Horizental alignment:
The hrizental alignment is not useful and it leads my eye away from true prupose.
> Wrong :
```java
public class FitNesseExpediter implements ResponseSender {
    private Socket socket;
    private InputStream input;
    private OutputStream output;
    private Request request;
    private Response response;
    private FitNesseContext context;
    protected long requestParsingTimeLimit;
    private long requestProgress;
    private long requestParsingDeadline;
    private boolean hasError;

    //...
}
```
> Correct :
```java
public class FitNesseExpediter implements ResponseSender {
    private Socket socket;
    private InputStream input;
    private OutputStream output;
    private Request request;
    
    // ...
}
```

### Identation:
never use this :
```java
    public class FitNesseServer implements SocketServer { private FitNesseContext 
    context; public FitNesseServer(FitNesseContext context) { this.context = 
    context; } public void serve(Socket s) { serve(s, 10000); } public void 
    serve(Socket s, long requestTimeout) { try { FitNesseExpediter sender = new 
    FitNesseExpediter(s, context); 
    sender.setRequestParsingTimeLimit(requestTimeout); sender.start(); } 
    catch(Exception e) { e.printStackTrace(); } } }
```

## Team rules:
A team of devlopers should agtee upon a single formatting style, and then every member of that team should use that style. We want the software to have a consistent style.