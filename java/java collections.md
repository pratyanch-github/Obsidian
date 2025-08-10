
interface vs classes in java, both uses inheritance i.e extends and implements

In Java, interfaces and classes are fundamental concepts used to define the structure and behavior of objects. Understanding the difference between them, as well as the use of `extends` and `implements`, is crucial for effective object-oriented programming.

### Classes

- **Definition**: A class is a blueprint for creating objects. It defines properties (fields) and behaviors (methods) that the objects created from the class can have.
- **Usage**: Classes are used to encapsulate data and functionality. They can have fields, methods, constructors, and can be instantiated to create objects.
- **Example**:
  ```java
  public class Animal {
      private String name;

      public Animal(String name) {
          this.name = name;
      }

      public void speak() {
          System.out.println(name + " makes a sound.");
      }
  }
  ```

### Interfaces

- **Definition**: An interface is a reference type in Java, similar to a class, that can contain only constants, method signatures, default methods, static methods, and nested types. Interfaces cannot contain instance fields.
- **Usage**: Interfaces are used to define a contract that other classes can implement. They specify what methods a class must have, without providing the implementation.
- **Example**:
  ```java
  public interface Speakable {
      void speak();
  }
  ```

### `extends` vs `implements`

- **`extends`**:
  - **Usage**: Used when a class inherits from another class or when an interface inherits from another interface.
  - **Functionality**: Allows a class to inherit fields and methods from a superclass, enabling code reuse and polymorphism.
  - **Example**:
    ```java
    public class Dog extends Animal {
        public Dog(String name) {
            super(name);
        }

        @Override
        public void speak() {
            System.out.println(getName() + " barks.");
        }
    }
    ```

- **`implements`**:
  - **Usage**: Used when a class implements an interface.
  - **Functionality**: A class that implements an interface must provide concrete implementations for all of the interface's methods.
  - **Example**:
    ```java
    public class Dog implements Speakable {
        private String name;

        public Dog(String name) {
            this.name = name;
        }

        @Override
        public void speak() {
            System.out.println(name + " barks.");
        }
    }
    ```

### Key Differences

- **Classes vs Interfaces**: Classes can have implementations of methods, while interfaces can only declare methods (unless they are default or static methods).
- **Inheritance**: A class can extend only one other class (single inheritance), but it can implement multiple interfaces (multiple inheritance of type).
- **Purpose**: Use classes to define objects with specific behaviors and states. Use interfaces to define a contract that multiple classes can adhere to, ensuring they provide specific behaviors.

By understanding these concepts, you can design flexible and reusable code in Java.

![[{3D516550-F374-4A60-B0EE-4E6082D4073E}.png]]

![[{2C328C17-A2E2-4705-85CF-0C0E4BE3901E}.png]]

collection interface extends the iterable interface means, if you are a collection you are an iterable because collection says i am iterable.

if you extend the iterable interface then you have to implement two necessary methods called hasnext() and next()

Fun fact - maps don't extend iterable so how do we iterate a map



![[{6803A750-F022-48F5-BD64-F40C8C9B3683}.png]]

![[{0E599FD6-33D5-4935-9737-CDF77BF58A95}.png]]

if you are a collection you have to implement below functions 
![[{1ED5DB5D-7562-46A3-AEBE-D34D969BDD88}.png]]

![[{03859BB0-11E8-4598-AF18-014BF9DA1F37}.png]]

![[{C93E70B3-ECC8-4736-BA64-E86AACBD28BF}.png]]

![[{00D34B64-C58E-47B8-902B-BF3778ABDD98}.png]]

![[{F5A02A72-89EB-46A4-A8C2-777183E7DF00}.png]]

![[{07AD4A0A-9C58-4FB8-8899-73F0BEE4EB51}.png]]

![[{D00E1D01-77F6-45C6-9B39-44DF52394935}.png]]

In Java, `List` is an interface, and `ArrayList` is a concrete class that implements the `List` interface. When you declare a variable of type `List<Integer>`, you are specifying that the variable will hold a list of integers, but you are not specifying how that list is implemented. By using `new ArrayList<>()`, you are creating an instance of `ArrayList`, which is a specific implementation of the `List` interface.

Here's a breakdown of what's happening:

1. **Interface vs. Implementation**:
   - `List<Integer> alist;` declares a variable `alist` of type `List<Integer>`. This means `alist` can hold any object that implements the `List` interface.
   - `new ArrayList<>()` creates an instance of `ArrayList`, which is a class that implements the `List` interface.

2. **Why Use Interfaces?**:
   - **Flexibility**: By programming to an interface (`List`), you can easily change the implementation without changing the rest of your code. For example, you could switch from `ArrayList` to `LinkedList` if needed.
   - **Abstraction**: It allows you to use the list without worrying about the underlying implementation details.

3. **Example**:
   ```java
   List<Integer> alist = new ArrayList<>();
   alist.add(1);
   alist.add(2);
   alist.add(3);
   ```

   In this example:
   - `alist` is declared as a `List<Integer>`, meaning it can hold a list of integers.
   - `new ArrayList<>()` creates an `ArrayList` object, which is assigned to `alist`.
   - You can use `alist` to add elements, remove elements, and perform other list operations, regardless of the specific list implementation.

By using the `List` interface, your code becomes more flexible and easier to maintain, as you can change the list implementation without affecting the rest of your code.

# ArrayList in JAVA 

Certainly! Here's a table that includes the methods of `ArrayList`, their descriptions, return types, and typical time complexities. Note that the time complexities are average cases and can vary based on specific scenarios:

E is return type.

| Method          | Description                                                                 | Return Type | Time Complexity (Average) |
|-----------------|-----------------------------------------------------------------------------|-------------|---------------------------|
| `add(E e)`      | Add an item to the end of the list                                           | `boolean`   | O(1) amortized            |
| `add(int index, E element)` | Add an item at a specific position in the list                  | `void`      | O(n)                      |
| `addAll(Collection<? extends E> c)` | Add a collection of items to the list                   | `boolean`   | O(n)                      |
| `clear()`       | Remove all items from the list                                               | `void`      | O(n)                      |
| `clone()`       | Create a copy of the `ArrayList`                                             | `Object`    | O(n)                      |
| `contains(Object o)` | Checks whether an item exists in the list                               | `boolean`   | O(n)                      |
| `ensureCapacity(int minCapacity)` | Increase the capacity of the list to fit a specified number of items | `void` | O(n) (increases capacity) |
| `forEach(Consumer<? super E> action)` | Perform an action on every item in the list            | `void`      | O(n)                      |
| `get(int index)`| Return the item at a specific position in the list                           | `E`         | O(1)                      |
| `indexOf(Object o)` | Return the position of the first occurrence of an item in the list       | `int`       | O(n)                      |
| `isEmpty()`     | Checks whether the list is empty                                             | `boolean`   | O(1)                      |
| `iterator()`    | Return an `Iterator` object for the `ArrayList`                              | `Iterator`  | O(1)                      |
| `lastIndexOf(Object o)` | Return the position of the last occurrence of an item in the list    | `int`       | O(n)                      |
| `listIterator()`| Return a `ListIterator` object for the `ArrayList`                           | `ListIterator` | O(1)                   |
| `remove(Object o)` | Remove the first occurrence of an item from the list                      | `boolean`   | O(n)                      |
| `remove(int index)` | Remove an item at a specific position in the list                        | `E`         | O(n)                      |
| `removeAll(Collection<?> c)` | Remove a collection of items from the list                      | `boolean`   | O(n^2)                    |
| `removeIf(Predicate<? super E> filter)` | Remove all items from the list which meet a specified condition | `boolean` | O(n)                  |
| `replaceAll(UnaryOperator<E> operator)` | Replace each item in the list with the result of an operation on that item | `void` | O(n) |
| `retainAll(Collection<?> c)` | Remove all elements from the list which do not belong to a specified collection | `boolean` | O(n^2) |
| `set(int index, E element)` | Replace an item at a specified position in the list              | `E`         | O(1)                      |
| `size()`        | Return the number of items in the list                                       | `int`       | O(1)                      |
| `sort(Comparator<? super E> c)` | Sort the list                                               | `void`      | O(n log n)                |
| `spliterator()` | Return a `Spliterator` object for the `ArrayList`                            | `Spliterator` | O(1)                    |
| `subList(int fromIndex, int toIndex)` | Return a sublist which provides access to a range of this list's items | `List<E>` | O(1) (view)          |
| `toArray()`     | Return an array containing the list's items                                  | `Object[]`  | O(n)                      |
| `trimToSize()`  | Reduce the capacity of the list to match the number of items if necessary    | `void`      | O(n)                      |

### Notes:
- **Amortized Time Complexity**: The `add(E e)` method has an amortized time complexity of O(1) because, although resizing the array (when the capacity is exceeded) takes O(n) time, this operation happens infrequently.
- **O(n^2) Complexity**: Methods like `removeAll` and `retainAll` can have O(n^2) complexity because they may involve iterating over the list and checking membership in another collection, which can be costly if the other collection is not optimized for fast lookups.
- **Sublist**: The `subList` method returns a view of the list, not a new list, so it has O(1) complexity for creating the view. However, operations on the sublist can affect the original list.

### convert arrayList to Integer array - 
we can pass any size to toArray function, 
and we must use Integer type
![[{B546F38F-2DEB-4311-A290-33CF64A13356}.png]]

![[{7305895A-0D5B-4FF1-9EAD-700373A32789}.png]]

![[{1599A1B8-9BED-48D5-887A-ADDAC2C168A3}.png]]

![[{52E996E8-DAE1-4650-AE97-B2C569EF675A}.png]]

![[{781A8E4F-DE91-4AC2-BC49-AFC9845E66A0}.png]]


# LinkedList in java collection

as linkedList class implements list interface , arrayList and linkedList have same set of functions.
next() - first return the current element and then move to next
previous() - first moves to previous element and then return it.

![[{EF05E9A6-49A8-4FDB-9795-5D27A84448CE}.png]]