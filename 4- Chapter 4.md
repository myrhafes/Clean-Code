# **Chapter 4: Comments**

This chapter talks about rules should be followed when writing the comments, and some cases which writing a comment will be good and other cases will be bad.
- The proper use of comments is to compensate for our failure to express ourself in code.
- We must have to use them because we cannot always figure out how to express ourselves without them, but their use is not a cause for celebration.
- Inaccurate comments are worse than no comments at all.
- So, when you find yourself in a position where you need to write a comment, think it through and see whether there isn't some way to express yourself in the code without using comments.

## Comment Do Not Make Up For Bad Code:
The bad code is one of the more common motivations for comments. 
> So rather than spend your time writing the comments that explain the mess you have made, spend it cleaning that mess.

## Explain Your Self In Code:
```java
    // Check to see if the employee is eligible for full benefits
    if ((employee.flags & HOURLY_FLAG) && (employee.age > 65)) 
```

**Better :**
```java
    if (employee.isEligibleForFullBenefits())
```
It takes only a few seconds of thought to explain most of your intent in code. In many cases it’s simply a matter of creating a function that says the same thing as the comment you want to write.


## Good Comments:
Some comments are necessary or Benifical like the following:

### Legal comments:
For exemple copyright and authorship.
```java
    // Copyright (C) 2003,2004,2005 by Object Mentor, Inc. All rights reserved.
    // Released under the terms of the GNU General Public License version 2 or later.
```

### Informative comments:
```java
    // format matched kk:mm:ss EEE, MMM dd, yyyy
    Pattern timeMatcher = Pattern.compile("\\d*:\\d*:\\d* \\w*, \\w* \\d*, \\d*");
```
In this case the comment lets us know that the regular expression is intended to match a time and date that were formatted with the ```SimpleDateFormat.format```.

### Explanation of intent:
Sometimes a comment goes beyond just useful information about the implementation and provides the intent behind a decision. 
```java
    public int compareTo(Object o) {
        if(o instanceof WikiPagePath) {
            WikiPagePath p = (WikiPagePath) o;
            String compressedName = StringUtil.join(names, "");
            String compressedArgumentName = StringUtil.join(p.names, "");
            return compressedName.compareTo(compressedArgumentName);
        }
        return 1; // we are greater because we are the right type.
    }
```
### Clarification:
Sometimes it is just helpful to translate the meaning of some obscure argument or return value into something that’s readable.
For exemple:
```java
    public void testCompareTo() throws Exception {
        WikiPagePath a = PathParser.parse("PageA");
        WikiPagePath ab = PathParser.parse("PageA.PageB");
        WikiPagePath b = PathParser.parse("PageB");
        WikiPagePath aa = PathParser.parse("PageA.PageA");
        WikiPagePath bb = PathParser.parse("PageB.PageB");
        WikiPagePath ba = PathParser.parse("PageB.PageA");

        assertTrue(a.compareTo(a) == 0); // a == a
        assertTrue(a.compareTo(b) != 0); // a != b
        assertTrue(ab.compareTo(ab) == 0); // ab == ab
        assertTrue(a.compareTo(b) == -1); // a < b
        assertTrue(aa.compareTo(ab) == -1); // aa < ab
        assertTrue(ba.compareTo(bb) == -1); // ba < bb
        assertTrue(b.compareTo(a) == 1); // b > a
        assertTrue(ab.compareTo(aa) == 1); // ab > aa
        assertTrue(bb.compareTo(ba) == 1); // bb > ba
    }
```

### Warning of consequences:
Sometimes it is useful to warn other programmers about certain consequences.
```java
    public static SimpleDateFormat makeStandardHttpDateFormat() {
    //SimpleDateFormat is not thread safe, 
        //so we need to create each instance independently.
        SimpleDateFormat df = new SimpleDateFormat("EEE, dd MMM yyyy HH:mm:ss z");
        df.setTimeZone(TimeZone.getTimeZone("GMT"));
        return df;
    }
```
### To do comments:
TODOs are jobs that the programmer thinks should be done, but for some reason can’t do at the moment. It might be a reminder to delete a deprecated feature or a request for someone else to look at a problem. It might be a request for someone else to think of a better name or a reminder to make a change that is dependent on a
planned event. 

```java
    /* TO DO:
        * ...
        * ...
    */
```

### Amplification:
A comment may be used to amplify the importance of something.
```java
    String listItemContent = match.group(3).trim();
    // the trim is real important. It removes the starting 
    // spaces that could cause the item to be recognized
    // as another list.
    new ListItemWidget(this, listItemContent, this.level + 1);
    return buildList(text.substring(match.end()));
```

### Javadocs in public APIs:
If you are writing a public APIs. Then you should certainly write good javadocs for it. And krrp in mind all the advice in this chapter.

## Bad Comments:
Most comments fall into this category. Usually they are crutches or excuses for poor code or justifications for insufficient decisions.

### Mumbling:
For exemple, the following is a comment might indeed have been useful. But the author was in a hurry or just not paying much attetion while writing.
```java
    public void loadProperties() {
        try {
            String propertiesPath = propertiesLocation + "/" + PROPERTIES_FILE;
            FileInputStream propertiesStream = new FileInputStream(propertiesPath);
            loadedProperties.load(propertiesStream);
        }catch(IOException e) {
        // No properties files means all defaults are loaded
        }
    }
```

### Redundant comments:
In the following function there is a header comment that is completley redundant. The comment probably takes longer to read than the code itself. also it's not more informative than the code.
```java
// Utility method that returns when this.closed is true. Throws an exception
// if the timeout is reached.
    public synchronized void waitForClose(final long timeoutMillis) throws Exception {
        if(!closed) {
            wait(timeoutMillis);
            if(!closed) throw new Exception("MockResponseSender could not be closed");
        }
    }
```

### Misleading comments:
Take your times to write comment, because if you do a small mistake maybe other programmers read your comment and think othrway about your function.

### Mandated comments:
For exemple, required javadocs for every function lead to ugly code such as:
```java
    /**
    * 
    * @param title The title of the CD
    * @param author The author of the CD
    * @param tracks The number of tracks on the CD
    * @param durationInMinutes The duration of the CD in minutes
    */
    public void addCD(String title, String author, int tracks, int durationInMinutes) {
        CD cd = new CD();
        cd.title = title;
        cd.author = author;
        cd.tracks = tracks;
        cd.duration = duration;
        cdList.add(cd);
    }
```

### Journal comments:
```java
/*
* Changes (from 11-Oct-2001)
 * --------------------------
 * 11-Oct-2001 : Re-organised the class and moved it to new package 
 * com.jrefinery.date (DG);
 * 05-Nov-2001 : Added a getDescription() method, and eliminated NotableDate 
 * class (DG);
 * 12-Nov-2001 : IBD requires setDescription() method, now that NotableDate 
 * class is gone (DG); Changed getPreviousDayOfWeek(), 
 * getFollowingDayOfWeek() and getNearestDayOfWeek() to correct 
 * bugs (DG);
 * 05-Dec-2001 : Fixed bug in SpreadsheetDate class (DG);
 * 29-May-2002 : Moved the month constants into a separate interface 
 * (MonthConstants) (DG);
 * 27-Aug-2002 : Fixed bug in addMonths() method, thanks to N???levka Petr (DG);
 * 03-Oct-2002 : Fixed errors reported by Checkstyle (DG);
 * 13-Mar-2003 : Implemented Serializable (DG);
 * 29-May-2003 : Fixed bug in addMonths method (DG);
 * 04-Sep-2003 : Implemented Comparable. Updated the isInRange javadocs (DG);
 * 05-Jan-2005 : Fixed bug in addYears() method (1096282) (DG);
*/
```
We no longer need the journal comment, because we have source code control system (Git).

### Noise comments:
Sometimes you see comments that are nothing but noise. They restate the obvious and provide no new information.
```java
    /** The day of the month. */
    private int dayOfMonth;

    /**
    * Default constructor.
    */
    protected AnnualDateRule() {
    }

    /**
    * Returns the day of the month.
    *
    * @return the day of the month.
    */
    public int getDayOfMonth() {
        return dayOfMonth;
    }
```

### Don't use comment when you can use a function or variable:
```java
    // does the module from the global list <mod> depend on the
    // subsystem we are part of?
    if (smodule.getDependSubsystems().contains(subSysMod.getSubSystem()))
```
**Better:**
```java
    ArrayList moduleDependees = smodule.getDependSubsystems();
    String ourSubSystem = subSysMod.getSubSystem();
    if (moduleDependees.contains(ourSubSystem))
```

### Position markers:
Sometimes programmers like to mark a particular position in a source file. For example:
```java
    // Actions //////////////////////////////////
```

### Closing brace comments:
Sometimes programmers will put special comments on closing braces.
```java
    public class wc {
        public static void main(String[] args) {
            BufferedReader in = new BufferedReader(new InputStreamReader(System.in));
            String line;
            int lineCount = 0;
            int charCount = 0;
            int wordCount = 0;
            try {
                while ((line = in.readLine()) != null) {
                    lineCount++;
                    charCount += line.length();
                    String words[] = line.split("\\W");
                    wordCount += words.length;
                } //while
                System.out.println("wordCount = " + wordCount);
                System.out.println("lineCount = " + lineCount);
                System.out.println("charCount = " + charCount);
            } // try
            catch (IOException e) {
                System.err.println("Error:" + e.getMessage());
            } //catch
        } //main
    }
```

### Attributions and bylines:
```java
/* Added by Rick */
```
Source code control systems (Git) are very good at remembring who added what.

### Commented-out code:
```java
    InputStreamResponse response = new InputStreamResponse();
    response.setBody(formatter.getResultStream(), formatter.getByteCount());
    // InputStream resultsStream = formatter.getResultStream();
    // StreamReader reader = new StreamReader(resultsStream);
    // response.setContent(reader.read(formatter.getByteCount()));
```
We have good source control systems for a very long time now. Those systems will remember the code for us. We don't have to comment it any more. Just delete the code we won't lose it.

### HTML comments:
Don't use HTML comments in our source code.
```java
    /**
    * Task to run fit tests. 
    * This task runs fitnesse tests and publishes the results.
    * <p/>
    * <pre>
    * Usage:
    * &lt;taskdef name=&quot;execute-fitnesse-tests&quot; 
    * classname=&quot;fitnesse.ant.ExecuteFitnesseTestsTask&quot; 
    * classpathref=&quot;classpath&quot; /&gt;
    * OR
    * &lt;taskdef classpathref=&quot;classpath&quot; 
    * resource=&quot;tasks.properties&quot; /&gt;
    * <p/>
    * &lt;execute-fitnesse-tests 
    * suitepage=&quot;FitNesse.SuiteAcceptanceTests&quot; 
    * fitnesseport=&quot;8082&quot; 
    * resultsdir=&quot;${results.dir}&quot; 
    * resultshtmlpage=&quot;fit-results.html&quot; 
    * classpathref=&quot;classpath&quot; /&gt;
    * </pre>
    */
```

### Nonlocal information:
All comment should describe our code!
This comment don't describe the code:
```java
    /**
    * Port on which fitnesse would run. Defaults to <b>8082</b>.
    *
    * @param fitnessePort
    */
    public void setFitnessePort(int fitnessePort) {
        this.fitnessePort = fitnessePort;
    }
```
### Too much information:
Don't put historical discussion in your code!
For exemple:
```java
    /*
    RFC 2045 - Multipurpose Internet Mail Extensions (MIME) 
    Part One: Format of Internet Message Bodies
    section 6.8. Base64 Content-Transfer-Encoding
    The encoding process represents 24-bit groups of input bits as output 
    strings of 4 encoded characters. Proceeding from left to right, a 
    24-bit input group is formed by concatenating 3 8-bit input groups. 
    These 24 bits are then treated as 4 concatenated 6-bit groups, each 
    of which is translated into a single digit in the base64 alphabet. 
    When encoding a bit stream via the base64 encoding, the bit stream 
    must be presumed to be ordered with the most-significant-bit first. 
    That is, the first bit in the stream will be the high-order bit in 
    the first 8-bit byte, and the eighth bit will be the low-order bit in 
    the first 8-bit byte, and so on.
    */
```

### Inobvious connection:
The goal of comment is explain the code. So don't make comments difficults to understand.

### Function header:
Short fubctions don't need much description. A well-chosen name for a samall function that does one thing is usually better than a comment header.
