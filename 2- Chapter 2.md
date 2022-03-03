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

## Make Meaningful Distinctions:

## Use Prounounceable Names:

## Use Searchable Names:

## Avoid Encoding:

## Avoid Mental Mapping:

## Class Names:

## Method Names:

## Don't Be Cute:

## Pick One Word Per Concept:

## Don't Pun:

## Use Solution Domain Names:

## Use Problem Domain Name:

## Add Meaningful Context/