```python
# Python Classes, Objects, and Inheritance Tutorial

# Define a class named Person
class Person:
    # Class variable to keep track of the number of Person instances
    person_count = 0 

    def __init__(self, name, age, height):
        # Initialize instance variables
        self.name = name
        self.age = age
        self.height = height
        # Increment the class variable when a new instance is created
        Person.person_count += 1
        
    def helloWorld(self):
        # A simple method that prints a message
        print('helloWorld')
        
    def __del__(self):
        # Destructor method called when an object is deleted
        print("Object deleted")
        # Decrement the class variable when an instance is deleted
        Person.person_count -= 1
        
    def __str__(self):
        # String representation of the object
        return "Name: {}, Age: {}, Height: {}".format(self.name, self.age, self.height)

# Creating an instance of the Person class
person1 = Person('Ram', 88, 32)
# Accessing instance variables
# print(person1.name, person1.age, person1.height)  # Output: Ram 88 32
# Using the __str__ method to get a string representation of the object
# print(person1)  # Output: Name: Ram, Age: 88, Height: 32
# Deleting the instance
# del person1

# Define a subclass named Worker that inherits from Person
class Worker(Person):
    
    def __init__(self, name, age, height, salary):
        # Initialize instance variables of the parent class using super()
        super(Worker, self).__init__(name, age, height)
        # Initialize instance variables specific to the Worker class
        self.salary = salary
    
    # Method overriding: redefining the __str__ method for Worker
    def __str__(self):  
        # Get the string representation from the parent class
        text = super(Worker, self).__str__()
        # Add additional information specific to Worker
        text += " , Salary: {}".format(self.salary)
        return text
        
    def calYearlySalary(self):
        # Calculate the yearly salary
        return self.salary * 12

# Creating an instance of the Worker class
worker1 = Worker('Ram', 40, 132, 50000)
# Using the overridden __str__ method to get a string representation of the object
print(worker1)  # Output: Name: Ram, Age: 40, Height: 132 , Salary: 50000
# Calling a method specific to the Worker class
# print(worker1.calYearlySalary())  # Output: 600000

```

### Summary of Python Classes, Objects, and Inheritance

1. **Class Definition and Variables**
   - **Class Definition**: Defined with the `class` keyword followed by the class name.
   - **Class Variable**: A variable shared by all instances of the class. Example: `person_count`.

2. **Constructor**
   - **Constructor Method (`__init__`)**: Initializes instance variables when an object is created.

3. **Instance Variables**
   - Unique to each instance of the class. Example: `name`, `age`, `height`.

4. **Methods**
   - Functions defined within a class that operate on instance variables.
   - Example Method: `helloWorld()` prints a message.

5. **Special Methods**
   - **Destructor (`__del__`)**: Called when an object is deleted.
   - **String Representation (`__str__`)**: Returns a string representation of the object.

6. **Creating an Instance**
   - Instantiate an object by calling the class with the required arguments. Example: `person1 = Person('Ram', 88, 32)`.

7. **Accessing Instance Variables and Methods**
   - Access instance variables using the dot notation. Example: `person1.name`.
   - Call methods using the dot notation. Example: `person1.helloWorld()`.

8. **Class Variable Access**
   - Access class variables using the class name. Example: `Person.person_count`.

9. **Deleting an Instance**
   - Use the `del` keyword to delete an instance. Example: `del person1`.

10. **Inheritance**
    - Define a subclass that inherits methods and properties from a parent class. Example: `class Worker(Person):`.
    - Use the `super()` function to call the constructor of the parent class.
    - Method overriding allows a subclass to provide a specific implementation of a method already defined in the parent class.

11. **Creating an Instance of Subclass**
    - Instantiate an object of a subclass by calling the subclass with the required arguments. Example: `worker1 = Worker('Ram', 40, 132, 50000)`.

12. **Using Overridden Methods**
    - Use methods from the parent class and overridden methods in the subclass. Example: `print(worker1)` calls the overridden `__str__` method.

This tutorial covers the basics of defining and using classes, objects, and inheritance in Python, including constructors, methods, special methods, and class variables.

==================================================================

# Python Operator Overloading Tutorial with Vector Class
```python


# Define a class named vector
class vector:
    def __init__(self, x, y):
        # Initialize instance variables
        self.x = x
        self.y = y

    # Overload the addition operator
    def __add__(self, other):
        # Return a new vector instance with summed coordinates
        return vector(self.x + other.x, self.y + other.y)

    # Overload the subtraction operator
    def __sub__(self, other):
        # Return a new vector instance with subtracted coordinates
        return vector(self.x - other.x, self.y - other.y)

    # String representation of the vector object
    def __str__(self):
        return 'x: {}, y: {}'.format(self.x, self.y)

# Creating instances of the vector class
v1 = vector(5, 6)
v2 = vector(1, 1)

# Using the overloaded addition operator
v3 = v1 + v2
# Using the overloaded subtraction operator
v4 = v1 - v2

# Printing the results
print(v3)  # Output: x: 6, y: 7
print(v4)  # Output: x: 4, y: 5
```

### Summary of Python Operator Overloading with the Vector Class

1. **Class Definition and Constructor**
   - **Class Definition**: Defined with the `class` keyword followed by the class name.
   - **Constructor Method (`__init__`)**: Initializes instance variables when an object is created. In this example, `x` and `y` are the coordinates of the vector.

2. **Operator Overloading**
   - **Addition Operator (`__add__`)**: Overloaded to allow adding two vector instances. It returns a new vector instance with the summed coordinates.
   - **Subtraction Operator (`__sub__`)**: Overloaded to allow subtracting one vector instance from another. It returns a new vector instance with the subtracted coordinates.

3. **String Representation**
   - **String Representation (`__str__`)**: Returns a string representation of the vector object, showing its coordinates.

4. **Creating Instances**
   - Instantiate objects by calling the class with the required arguments. Example: `v1 = vector(5, 6)`.

5. **Using Overloaded Operators**
   - Use the overloaded operators to perform operations on instances. Example: `v3 = v1 + v2` and `v4 = v1 - v2`.

6. **Printing Results**
   - Print the results using the string representation method. Example: `print(v3)`.

This tutorial covers the basics of operator overloading in Python, including how to define and use overloaded operators in a class.