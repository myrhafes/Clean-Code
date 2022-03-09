# **Chapter 7: Error Handling**

The goal of this chapter is to keep the bondaties of our code clean, when dealing with code that are out of our control.

## Using Third Party Code:
Third party interfaces are made to fit in to any environment so that the usability of it. the user actually wants the interface only to do what it to do. This results in bad code and code misure. Book suggest to use the third party components in way whish is easier to understand and harder to misure.

## Exploring And Learning Boundaries:
Learning test (unit test to understand the third party component) can be used to get familiarized with the unknown code. Additionally, when there has been a change in the third partty component, we cab use these tests to check whether it provides the same functionality as before.

## Using Code That Does Not Exist Yet:
Sometimes we have to use thing like third party APIs we don't know the interface of the API. So we should create a module of our expectation and adapter to connect when the real implementation is available.

## Clean Boundaries:
This part looks very important when dealing with third party libraries. The book suggests to have tests to verify the it serves your purpose, have very few places in the code that refer to them, dont depend too much on third party code, use wrappers or adapters.