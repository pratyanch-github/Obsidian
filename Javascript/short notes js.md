global execution context - 
  1. as js program runs gec is pushed into call stack
  2. separate execution context is created in thread of execution for each function and function pushed in call stack 
  3. when return encounter it's corresponding execution gets deleted 

hoisting-
  1. works because of memory creating phase of execution context
  2. variables - undefined , functions - entire definition

shortest js program - GEC, global object(window), this  are created
   1. empty file is shortest js program because js engine does lot of things even then.
   2. it created gec 
   3. it created window object in global space , which is accessible by anywhere in the program
   4. it also create this keyword which points to window object

scope chain and scope lexical environment -
 1. lexical environment - local memory + lexical environment of its parent
 2. the process of one by one into parent hierarchy is called scope chain

let and const - 
 1. they are also hoisted but not in global space , their space is allocated in script space
 2. they are only accessible after proving value to them

temporal dead zone -
 1. the time since the let variable was hoisted , until it is initialized some value, If you try to access it before unlike var(gives undefined) it throws reference error(i.e in that time let variable was dead)

**variable is always present in global space 

closure 
 1. Function bundled with its lexical environment is called closure.
 2. when we return a function (like a variable ) 





