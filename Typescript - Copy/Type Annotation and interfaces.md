In TypeScript, a type interface and a type annotation are two ways to define the shape of an object or the type of a variable. They help TypeScript understand the structure of your data and provide type checking.

1. **Type Annotation:** Type annotation is a way to explicitly specify the type of a variable, parameter, or return value. It is written after the variable name, separated by a colon. For example:
   ```typescript
   let count: number = 5;
   function greet(name: string): string {
       return "Hello, " + name;
   }
   ```

2. **Type Interface:** Type interface is a way to define the structure of an object without explicitly specifying its type. TypeScript infers the type based on the shape of the object. For example:
   ```typescript
   interface Person {
       name: string;
       age: number;
   }
   let person: Person = { name: "John", age: 30 };
   ```

In the above example, `Person` is a type interface that defines an object with `name` and `age` properties. When you declare a variable `person` and assign an object with `name` and `age` properties, TypeScript infers that `person` should be of type `Person`.

Type annotations are useful when you want to be explicit about the types in your code, while type interfaces are useful when you want TypeScript to infer the types based on the structure of your objects. Both type annotations and type interfaces help in making your code more readable and maintainable by providing type safety.