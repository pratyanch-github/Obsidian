# Python Operator Overloading Tutorial with Vector Class

```python
# Python Operator Overloading Tutorial with Vector Class

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