# **Chapter 9: Unit Tests**

## The Three Lows Of TDD:
By now everyone knows that TDD asks us to write unit tests first, before we write production code. But that rule is just the tip of iceberg.
- **First law:** You may not write production code unitil you have written a failing unit test.
- **Second law:** You may not write more of unit test than is sufficient to fail and not compiling is failing.
- **Third law:** You may not write more production code than is sufficient to pass the curently failing test.

## Keeping tests clean:
- Having dirty test is equivalent to having no tests.
- Test code is just as important as production code. It must be kept as clean as production code.
- If you don't keep your tests clean, you will lose them. And without them, you lose the very thing that keeps your production code flexible. It is unit tests that keep our code flexible. Maintainable, and reusable. 
- If you have tests, you do not fear making changes to the code. Whitout test every change is a possible bug ! So if your test are dirty, then your ability to change your code is hampered, and begin to lose the ability to improve the structure of that code. 
> The dirtier your tests, the dirtier your code becomes. Eventually you lose the tests and your code rots.

## One Assert Per Test:
Each test should assert one aspect of behavior.

## Single Concept Per Test:
Each test focuses on a single concept.

## FIRST:
- Fast: Tests should run quickly.
- Independent: Tests should not depend on one another or the order that they run in to be successful.
- Repeatable: Tests should be repeatable in any environment.
- Self-Validating: Test should be either pass or fail. Test results should only be validated through one means.
- Timely: Tests should be written in a timely fashion