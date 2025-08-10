In TypeScript, basic types refer to the fundamental data types that are used to define the types of variables. Here are some of the basic types in TypeScript:

1. **Number:** Represents both integer and floating-point numbers. Example: `let count: number = 5;`

2. **String:** Represents textual data. Example: `let name: string = "John";`

3. **Boolean:** Represents a logical value, `true` or `false`. Example: `let isDone: boolean = false;`

4. **Array:** Represents a list of elements of a specific type. Example: `let numbers: number[] = [1, 2, 3, 4, 5];` or `let names: Array<string> = ["John", "Doe"];`

5. **Tuple:** Represents an array with a fixed number of elements where each element may be of a different type. Example: `let tuple: [string, number] = ["John", 25];`

6. **Enum:** Represents a set of named constants. Example:
   ```typescript
   enum Color {
       Red,
       Green,
       Blue
   }
   let c: Color = Color.Green;
   ```

7. **Any:** Represents any type. Use it when you are not sure about the type of the value or when working with dynamic content. Example: `let value: any = 5; value = "hello";`

8. **Void:** Represents the absence of a value. Typically used as the return type of functions that do not return a value. Example:
   ```typescript
   function logMessage(message: string): void {
       console.log(message);
   }
   ```

9. **Null and Undefined:** Represents `null` and `undefined` values respectively. Example:
   ```typescript
   let nullValue: null = null;
   let undefinedValue: undefined = undefined;
   ```

These are the basic types in TypeScript. They provide a way to define the types of variables, parameters, and function return types, making your code more robust and less error-prone.