# **Chapter 7: Error Handling**

- All programmers should do error handling while coding.
- Error handling is important, but if it obscures logic it's wrong.

## Use Exceptions Rather than return code:
Sometimes we tend to handle errors in ```if else``` blocks. That is messy because it gets mixed with the logic. Using exceptions, throwing or handling them can be better.
**Exemple:**
```java
    public class DeviceController {
        //...
        public void sendShutDown() {
            DeviceHandle handle = getHandle(DEV1);
            // Check the state of the device
            if (handle != DeviceHandle.INVALID) {
                // Save the device status to the record field
                retrieveDeviceRecord(handle);
                // If not suspended, shut down
            if (record.getStatus() != DEVICE_SUSPENDED) {
                pauseDevice(handle);
                clearDeviceWorkQueue(handle);
                closeDevice(handle);
            } else {
                logger.log("Device suspended. Unable to shut down");
            }
            } else {
                logger.log("Invalid handle for: " + DEV1.toString());
            }
        }
        //...
    }
```
**With exception:**
```java
    public class DeviceController {
        // ...
        public void sendShutDown() {
            try {
                tryToShutDown();
            } catch (DeviceShutDownError e) {
                logger.log(e);
            }
        }

        private void tryToShutDown() throws DeviceShutDownError {
            DeviceHandle handle = getHandle(DEV1);
            DeviceRecord record = retrieveDeviceRecord(handle);
            pauseDevice(handle);
            clearDeviceWorkQueue(handle);
            closeDevice(handle);
        }
        private DeviceHandle getHandle(DeviceID id) {
            //...
            throw new DeviceShutDownError("Invalid handle for: " + id.toString());
            // ...
        }
        // ...
    }
```

## Write Your Try-Catch-Finally Statement first:
Exceptions are good because they define a scope for the error. And a try-catch-finally block leave the program in a consistent state. The author suggests that when we created our try-catch-finally structure our scope is defined and we can preceed with the rest of the logic.

## Use Unchecked Exceptions:(Issues with checked exception)
The author explains how checked exception are not actually worth its price. its price being the open/closed principle. If you throw exception from a method in your code and the catch is three levels above, you must declare that exception in the signature of each method between you and the catch. This breaks encapsulation because details about the code containing this exception should be known by all methods in the path.

## Provide Context With Exceptions:
Give a message of what the operation that failed and what type of failure it is.

## Define Exception Classes In Terms Of a Caller's Needs:
Define your own exception. Sometimes a piece of code maybe throwing many exception types. But in the application prespective it might be failure of one operation. So we can write new exception class to throw the custom exception whenever certain type of exceptions are thrown. This makes the code more readable understandable.

```java
public class LocalPort {
    private ACMEPort innerPort;

    public LocalPort(int portNumber) {
        innerPort = new ACMEPort(portNumber);
    }

    public void open() {
        try {
            innerPort.open();
        } catch (DeviceResponseException e) {
            throw new PortDeviceFailure(e);
        } catch (ATM1212UnlockedException e) {
            throw new PortDeviceFailure(e);
        } catch (GMXError e) {
            throw new PortDeviceFailure(e);
        }
    }
    // ...
}
```

## Define The Normal Flow:
For exemple in this case, the error handling and the logic are messed up!
```java
    try {
        MealExpenses expenses = expenseReportDAO.getMeals(employee.getID());
        m_total += expenses.getTotal();
    } catch(MealExpensesNotFound e) {
        m_total += getMealPerDiem();
    }
```

## Don't Return Null:
Returning null is an invitation to errors. Instead return an empty representation of that needed object.

## Don't Pass Null:
Passing null is worse than returning null. Prone to null pointer exceptions. Emptys objects be passed in this case as well, but it depends on the design.
