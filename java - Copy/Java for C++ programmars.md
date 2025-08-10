
![](file:///C:/Users/praty/AppData/Local/Temp/msohtmlclip1/01/clip_image002.png)

![](file:///C:/Users/praty/AppData/Local/Temp/msohtmlclip1/01/clip_image004.jpg)

![](file:///C:/Users/praty/AppData/Local/Temp/msohtmlclip1/01/clip_image006.jpg)

![](file:///C:/Users/praty/AppData/Local/Temp/msohtmlclip1/01/clip_image008.png)

![](file:///C:/Users/praty/AppData/Local/Temp/msohtmlclip1/01/clip_image010.png)

![](file:///C:/Users/praty/AppData/Local/Temp/msohtmlclip1/01/clip_image012.jpg)

Static means its not associated with the obj , but it is associated with the class.

Final means it cannot change

![](file:///C:/Users/praty/AppData/Local/Temp/msohtmlclip1/01/clip_image014.png)

In java everything is new’ed except  primitive types. No delete is needed ever.

In c++ some things are newed and they need to be deleted.

![](file:///C:/Users/praty/AppData/Local/Temp/msohtmlclip1/01/clip_image016.png)

![](file:///C:/Users/praty/AppData/Local/Temp/msohtmlclip1/01/clip_image018.png)

![](file:///C:/Users/praty/AppData/Local/Temp/msohtmlclip1/01/clip_image020.png)

![](file:///C:/Users/praty/AppData/Local/Temp/msohtmlclip1/01/clip_image022.png)

![](file:///C:/Users/praty/AppData/Local/Temp/msohtmlclip1/01/clip_image024.png)

### Understanding Static and Non-Static Methods in Java



| Feature                  | Static Methods                         | Non-Static Methods                            |
| ------------------------ | -------------------------------------- | --------------------------------------------- |
| **Belong to**            | Class itself                           | Instance of the class                         |
| **Access**               | Can be called without an instance      | Requires an instance to be called             |
| **Usage**                | Utility or helper methods              | Operate on instance variables                 |
| **Access to Static**     | Can access other static methods/fields | Can access both static and non-static         |
| **Access to Non-Static** | Cannot directly access non-static      | Can directly access non-static methods/fields |
| **Example Call**         | `ClassName.methodName()`               | `instanceName.methodName()`                   |
| **Typical Use Case**     | Math operations, utility functions     | Business logic, instance-specific operations  |


In Java, methods can be either static or non-static. Understanding the difference is crucial for effective programming.

#### Static Methods

- **Definition**: Belong to the class, not to any specific instance.
- **Access**: Can be called without creating an instance of the class.
- **Usage**: Commonly used for utility or helper methods.

#### Non-Static Methods

- **Definition**: Belong to an instance of the class.
- **Access**: Require an instance of the class to be called.
- **Usage**: Operate on instance variables and can access static members.

#### Key Rule

- **Static methods cannot directly call non-static methods or access non-static fields.**

#### How to Call Non-Static Methods from Static Methods

1. **Create an Instance**: Instantiate the class within the static method.
2. **Call the Method**: Use the instance to call the non-static method.

#### Example

```java
public class Example {

    // Non-static method
    public void nonStaticMethod() {
        System.out.println("This is a non-static method.");
    }

    // Static method
    public static void main(String[] args) {
        // Step 1: Create an instance of the class
        Example example = new Example();

        // Step 2: Call the non-static method using the instance
        example.nonStaticMethod();
    }
}
```

#### Summary

- **Static methods**: Use for class-level operations.
- **Non-static methods**: Use for instance-level operations.
- **To call non-static from static**: Create an instance of the class.

![[{B8209AAF-897B-485C-A100-DE63A90605C9}.png]]


![[{65DC8666-408F-4543-8B4A-14971F845835}.png]]

![[{F272BAF4-DED8-423A-99C4-99870CA0FCF4}.png]]

### Java: `import`

- **Purpose**: The `import` statement in Java is used to bring other classes or entire packages into visibility, allowing you to use them without needing to specify their full package name each time.
- **Usage**: It is used to import classes from Java's built-in libraries or from user-defined packages.
- **Syntax**: 
  ```java
  import java.util.List; // Imports the List class from the java.util package
  import java.util.*;    // Imports all classes from the java.util package
  ```
- **Functionality**: The `import` statement does not physically include code; it simply makes the classes available to the current file. Java's compiler handles the actual linking of classes.

### C++: `#include`

- **Purpose**: The `#include` directive in C++ is used to include the contents of a file or library into the current file. This is a preprocessor directive.
- **Usage**: It is used to include standard library headers or user-defined header files.
- **Syntax**:
  ```cpp
  #include <iostream>  // Includes the standard input-output stream library
  #include "MyClass.h" // Includes a user-defined header file
  ```
- **Functionality**: The `#include` directive literally copies the contents of the specified file into the location of the `#include` statement. This happens before the actual compilation process, during the preprocessing phase.

### Key Differences

- **Nature**: `import` is a language feature in Java, while `#include` is a preprocessor directive in C++.
- **Scope**: `import` deals with namespaces and class visibility, whereas `#include` deals with file inclusion.
- **Compilation**: Java's `import` does not duplicate code; it simply makes classes available. C++'s `#include` physically inserts the file's contents, which can lead to larger compiled files if not managed properly (e.g., using include guards).

Understanding these differences is crucial for effectively managing dependencies and code organization in Java and C++ projects.

# hash symbol is called octothorpe(#)

![[{72A12F53-7731-4D09-8353-E06C5369C4EE}.png]]


![[{FFF38A98-4981-4F3C-8004-33C833AB8FFE}.png]]


![[Pasted image 20250216014332.png]]


![[Pasted image 20250216014354.png]]

![[{66AE454A-D3BE-4F59-841A-BCFA378958CC}.png]]

![[{92DC0C4E-B737-4667-B409-067D3DD7A4A2}.png]]