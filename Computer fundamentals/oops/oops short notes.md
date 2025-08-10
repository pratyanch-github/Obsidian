
static keyword- https://www.geeksforgeeks.org/static-keyword-cpp/
polymorphism - https://www.geeksforgeeks.org/cpp-polymorphism/
final keyword - https://www.geeksforgeeks.org/c-final-specifier/


1. class constructor don't have datatype , not even void , they are not meant to return a value.
2. this is a pointer to the current obj , so we use arrow operator to access data members.
3. if we create pointer of base class , we can use it to point the base class object or object of any descendant of base class. 
    1. when we create a base class pointer and assign a child class object to it , and if both classes have a function with common name , then in current case base class function will be called . And if we want the base class function to be overridden , we have to make base class function virtual.
    2. if we create child class pointer then it will always call child class function even if we don't make that function virtual in base class.
4. virtual inheritance is different from virtual function
5. diamond problem is solved with virtual inheritance or scope resolution operator.
6. A [virtual function](https://www.geeksforgeeks.org/virtual-function-cpp/) is a member function which us used to achieve late binding(dynamic binding), that is declared in the base class using the keyword virtual and is re-defined (Overridden) in the derived class.
7. pure virtual function === do nothing function 
   class Shape { public: virtual void draw() = 0; virtual void area() = 0; };
8. if any class has at least one pure virtual function , it is called abstract class.
   - we should not be able to call pure virtual function 
   - so we cannot create obj of abstract class
   - if we inherit from abstract class then we must override pure virtual function
   - also we have to make the do nothing function virtual, for late binding
   - https://www.youtube.com/watch?v=0IR_D1qZy2g&list=PLLYz8uHU480j37APNXBdPz7YzAi4XlQUF&index=46



1. When a class inherits from multiple classes, constructors of base classes are called in the same order as they are specified in inheritance.