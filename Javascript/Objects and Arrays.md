Certainly! Here are some more tricks and tips for working with objects and arrays in JavaScript:

**Objects:**

1. **Object Destructuring:**
   ```javascript
   const person = { name: 'John', age: 30 };
   const { name, age } = person;
   console.log(name, age); // Output: John 30
   ```

2. **Object Spread Operator:**
   ```javascript
   const person = { name: 'John', age: 30 };
   const newPerson = { ...person, city: 'New York' };
   console.log(newPerson); // Output: { name: 'John', age: 30, city: 'New York' }
   ```

3. **Computed Property Names:**
   ```javascript
   const key = 'name';
   const person = { [key]: 'John' };
   console.log(person); // Output: { name: 'John' }
   ```

4. **Object.keys, Object.values, Object.entries:**
   ```javascript
   const person = { name: 'John', age: 30 };
   console.log(Object.keys(person)); // Output: ['name', 'age']
   console.log(Object.values(person)); // Output: ['John', 30]
   console.log(Object.entries(person)); // Output: [['name', 'John'], ['age', 30]]
   ```

5. **Checking if an Object has a Property:**
   ```javascript
   const person = { name: 'John', age: 30 };
   console.log('name' in person); // Output: true
   ```

**Arrays:**

1. **Array Destructuring:**
   ```javascript
   const numbers = [1, 2, 3, 4, 5];
   const [first, second, ...rest] = numbers;
   console.log(first, second, rest); // Output: 1 2 [3, 4, 5]
   ```

2. **Array Spread Operator:**
   ```javascript
   const numbers = [1, 2, 3];
   const newNumbers = [...numbers, 4, 5];
   console.log(newNumbers); // Output: [1, 2, 3, 4, 5]
   ```

3. **Array.map:**
   ```javascript
   const numbers = [1, 2, 3];
   const doubled = numbers.map(num => num * 2);
   console.log(doubled); // Output: [2, 4, 6]
   ```

4. **Array.filter:**
   ```javascript
   const numbers = [1, 2, 3, 4, 5];
   const evens = numbers.filter(num => num % 2 === 0);
   console.log(evens); // Output: [2, 4]
   ```

5. **Array.reduce:**
   ```javascript
   const numbers = [1, 2, 3, 4, 5];
   const sum = numbers.reduce((acc, cur) => acc + cur, 0);
   console.log(sum); // Output: 15
   ```

6. **Array.includes:**
   ```javascript
   const numbers = [1, 2, 3];
   console.log(numbers.includes(2)); // Output: true
   ```

These are just a few examples of the many ways you can work with objects and arrays in JavaScript. Experimenting with these features can help you become more proficient in working with complex data structures in your code.