# **Chapter 1: Clean Code**

## There Will Be Code:
- The world go fast, but always we will have code!
- The folks who think that code will one day disappear are like mathematicians who hope one day to discover a mathematicians who hope one day discover a mathematics that does not have to be formal.

## Bad Code:
> Story (to understand why bad code is dangerous)
> In the late 80s a company wrote a killer app. But then the release cycles began to stretch because
> - bugs were not repaired from one release to the next.
> - load times grew and crashes incresed
> In the end the product shut down and the company went out of the business (the reason => BAD CODE !!!)

**Why we write bad code ?**
- You felt tht you didn't have time to do a good job.
- Your boss would be angry with you if you took the time to clean up your code.
- You were just tired of working on this program and wanted it to be over.
- You looked at the backlog of other stuff that you had promised to get done and relized that you needed to slam this module together so you could move on the next.

> **WARNING**
> We have all looked at the mess we have just made and then chosen to leave it for another day.
> LATER == NEVER 

## The total cost of owning a mess:
Teams that were moving very fast at the beginning of a project can find themselves moving at a smail's pace (because fast => mess).
As the mess builds, the productivity of team continues to decrease asymptotcally approching zero.
<br>
<br>
<img width="831" alt="ProductivityTime" src="https://user-images.githubusercontent.com/59899627/156398449-b09c6ecd-fb01-4671-9876-d8bd025f3617.PNG">
<br>
<br>
### The grand redesign in the sky:
You should never redesign your project in the sky because it's took to bad code!
> Keeping your code clean is not just cost effective it's a matter of professional survival.

### Attitude:
It's unprofessional for programmers to bend to the will of managers who don't understand the risk of making mess (mess => time & bad code).

### The primal conundrum:
The only way to make deadline (go fast) is to keep your code as clean as possible at all times.

### The art of clean code:
- The question is how to write clean code ?
> It's not good trying to write clean code if you don't know what it means for code to be clean!
- Writing clean code is like painting a picture. 
> Most of us know when a picture is painted well or badly. So to being able to recognize clean code from dirty code, does not mean that we know how to write clean code!
- A programmer whitout **code-sense** can look at the messy module and recongnize the mess but will have no idea what to do about it.

### What is clean code ?
## **Bjarne Stroustrup, inventor of C++ and author of The C++ Programming Language**
<br>
<br>
<img width="368" alt="Bjarne Stroustrup" src="https://user-images.githubusercontent.com/59899627/156399033-0e7fd425-e7b5-447f-ac0a-5e7784c45df7.PNG">
<br>
<br>
I like my code to be elegant and efficient. The logic should be straightforward to make it hard for bugs to hide, the dependencies minimal to ease maintenance, error handling complete according to an articulated strategy, and performance close to optimal so as not to tempt people to make the code messy with unprincipled optimizations. Clean code does one thing well.

## **Grady Booch, author of Object Oriented Analysis and Design with Applications**
<br>
<br>
<img width="368" alt="Grady Booch" src="https://user-images.githubusercontent.com/59899627/156399356-ba37a12f-8e19-488c-9324-ef7706062d9b.PNG">
<br>
<br>
Clean code is simple and direct. Clean code reads like well-written prose. Clean code never obscures the designer’s intent but rather is full of crisp abstractions and straightforward lines of control.

## **“Big” Dave Thomas, founder of OTI, godfather of the Eclipse strategy**
<br>
<br>
<img width="368" alt="Dave Thomas" src="https://user-images.githubusercontent.com/59899627/156399607-a0cd017a-25d4-48df-928a-612d73ccacd8.PNG">
<br>
<br>
Clean code can be read, and enhanced by adeveloper other than its original author. It has unit and acceptance tests. It has meaningful names. It provides one way rather than many ways for doing one thing. It has minimal dependencies, which are explicitly defined, and provides a clear and minimal API. Code should be literate since depending on the language, not all necessary information can be expressed clearly in code alone.

## **Michael Feathers, author of Working Effectively with Legacy Code**
<br>
<br>
<img width="368" alt="Michael Feathers" src="https://user-images.githubusercontent.com/59899627/156399908-76d1e6e6-7f25-4f85-9cf7-30777b84c7a9.PNG">
<br>
<br>
I could list all of the qualities that I notice in clean code, but there is one overarching quality that leads to all of them. Clean code always looks like it was written by someone who cares. There is nothing obvious that you can do to make it better. All of those things were thought about by the code’s author, and if you try to imagine improvements, you’re led back to where you are, sitting in appreciation of the code someone left for you—code left by someone who cares deeply about the craft.

## **Ron Jeffries, author of Extreme Programming Installed and Extreme Programming Adventures in C#**
<br>
<br>
<img width="368" alt="Ron Jeffries" src="https://user-images.githubusercontent.com/59899627/156399969-df555a05-5450-47a7-970c-1764f9c29601.PNG">
<br>
<br>
In recent years I begin, and nearly end, with Beck’s rules of simple code. In priority order, simple code:
- Runs all the tests.
- Contains no duplication.
- Expresses all the design ideas that are in the system.
- Minimizes the number of entities such as classes, methods, functions, and the like.

## **Ward Cunningham, inventor of Wiki, inventor of Fit, coinventor of eXtreme Programming. Motive force behind Design Patterns. Smalltalk and OO thought leader. The godfather of all those who care about code.**
<br>
<br>
<img width="368" alt="Ward Cunningham" src="https://user-images.githubusercontent.com/59899627/156400010-ce745822-1cea-4b73-9e5c-017dd06ae573.PNG">
<br>
<br>
You know you are working on clean code when each routine you read turns out to be pretty much what you expected. You can call it beautiful code when the code also makes it look like the language was made for the problem.

### Schools of thought:
There are a lot of schools, student shoud choose one!

### The boy scout rule:
Leave the campground cleaner than you found it.
