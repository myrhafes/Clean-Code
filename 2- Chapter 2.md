# **Chapter 2: Meaningful Names**

## Introduction:
- Names are everywhere in software.
- Because we do so much of it, we'd better do it well.

**So what follows are some simple rules for creating good names ?**

## Use intention-revealing names:
The name of variable, function or class should answer the big questions :
- It should tell you why it exists.
- what it does.
- How it used
> If the name requires a comment then the name does not reveal its intent.

**Exemple 1:**
```java
	int d; //elapsed time in days
```

### Better:
```java
	int elapsedTimeInDays;
    // or:
    int daysSinceCreation;
    // or :
    int fileAgeInDays;
```

**Exemple 2:**
```java
    public List<int[]> getThem() {
        List<int[]> list1 = new ArrayList<int[]>();
        for (int[] x : theList)
            if (x[0] == 4) list1.add(x);
        return list1;
    }
```
### Better:

```java
    public List<int[]> getFlaggedCells() {
        List<int[]> flaggedCells = new ArrayList<int[]>();
        for (int[] cell : gameBoard)
            if (cell[STATUS_VALUE] == FLAGGED) flaggedCells.add(cell);
        return flaggedCells;
    }
```

## Avoid Disinformation:
- Do not refer to a grouping of accounts as an ```accountList``` unless it’s actually a ```List```. The word list means something specific to programmers. If the container holding the accounts is not actually a ```List```, it may lead to false conclusions. So ```accountGroup``` or ```bunchOfAccounts``` or just plain accounts would be better.
- A truly awful example of disinformative names would be the use of lower-case L or uppercase O as variable names, especially in combination. The problem, of course, is that they look almost entirely like the constants one and zero, respectively.
```java
    int a = l;
    if ( O == l )
        a = O1;
    else
        l = 01;
```

## Make Meaningful Distinctions:
Programmers create problems for themselves when they write code solely to satisfy a compiler or interpreter. For example:
- ```moneyAmount``` is indistinguishable from ```money```.
- ```consumerInfo``` is indistinguishable from ```consumer```.

## Use Prounounceable Names:
Humans are good at words. So make your names pronounceable.
**Bad name:**
```java
    private Date genymdhms;
```
**Good name:**
```java
    private Date generationTimeStamp;
```

## Use Searchable Names:
Single-letter names and numeric constants have a particular problem in that they are not easy to locate across a body of text.
Exemple(whitout searchable names):
```java
    for (int j=0; j<34; j++) {
        s += (t[j]*4)/5;
    }
```
**Better:**
```java
    int realDaysPerIdealDay = 4;
    const int WORK_DAYS_PER_WEEK = 5;
    int sum = 0;
    for (int j=0; j < NUMBER_OF_TASKS; j++) {
        int realTaskDays = taskEstimate[j] * realDaysPerIdealDay;
        int realTaskWeeks = (realdays / WORK_DAYS_PER_WEEK);
        sum += realTaskWeeks;
    }
```

## Avoid Encoding:
We have enough encodings to deal with without adding more to our burden. Encoding type or scope information into names simply adds an extra burden of deciphering. It hardly seems reasonable to require each new employee to learn yet another encoding “language” in addition to learning the (usually considerable) body of code that they’ll be working in. It is an unnecessary mental burden when trying to solve a problem. Encoded names are seldom pronounceable and are easy to mis-type.

## Avoid Mental Mapping:
One difference between a smart programmer and a professional programmer is that the professional understands that clarity is king. Professionals use their powers for good and write code that others can understand.

## Class Names:
- Classes and objects should have noun or noun phrase names like ```Customer```, ```WikiPage```,```Account```, and ```AddressParser```. Avoid words like ```Manager```, ```Processor```, ```Data```, or ```Info``` in the name of a class. 
- A class name should not be a verb.

## Method Names:
- Methods should have verb or verb phrase names like ```postPayment```, ```deletePage```, or ```save```.
- Accessors, mutators, and predicates should be named for their value and prefixed with ```get```, ```set```, and is according to the javabean standard.

## Don't Be Cute:
Always remember:
> **Say what you mean. Mean what you say**
If names are too clever, they will be memorable only to people who share the author’s sense of humor, and only as long as these people remember the joke. Will they know what the function named HolyHandGrenade is supposed to do? Sure, it’s cute, but maybe in this case DeleteItems might be a better name.

## Pick One Word Per Concept:
If you have two components with similar role. However, the first component is named ```userController``` while the other one is ```transactionManager```. If you are the new member of the team, you're confused. Now you faced the dilemma and you start ask your self:
- What is the difference between ```controller``` and ```manager``` ?
- Why do they have diffrent kinds of concept names whrn they have the same role in codebase ?

> So don't confuse yourself and others. Just pick one word per concept and stick to them all the time.

## Don't Pun:
Avoid using the same word for two purposes. Using the same term for two different ideas is essentially a pun.
If you follow the “one word per concept” rule, you could end up with many classes that have, for example, an add method. As long as the parameter lists and return values of the various add methods are semantically equivalent, all is well.

## Use Solution Domain Names:
Remember that the people who read your code will be programmers. So go ahead and use computer science (CS) terms, algorithm names, pattern names, math terms, and so forth.

## Use Problem Domain Name:
When there is no “programmer-eese” for what you’re doing, use the name from the problem domain. At least the programmer who maintains your code can ask a domain expert what it means.

## Add Meaningful Context:
The context of the solution is important then the solution them self.