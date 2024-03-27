 # What is TypeScript?

- TypeScript is a syntactic superset of JavaScript which adds <b>static typing.</b>
- This basically means that TypeScript adds syntax on top of JavaScript, allowing developers to add <b>types.</b>

# Why should I use TypeScript?

1. It can be difficult to understand what types of data are being passed around in JavaScript.
2. In JavaScript, function parameters and variables don't have any information! So developers need to look at documentation, or guess based on the implementation.
3. TypeScript allows specifying the types of data being passed around within the code, and has the ability to report errors when the types don't match.

<b>Example:</b></br>
TypeScript will report an error when passing a string into a function that expects a number. JavaScript will not.

# 1- What are decorators in Typescript ?

A Decorator is a special kind of declaration that can be attached to a <b>class</b> declaration, <b>method</b>, <b>accessor</b>, <b>property</b>, or <b>parameter</b>. Decorators use the form <b>@expression</b>, where <b>expression</b> must evaluate to a function that will be called at runtime with information about the decorated declaration.

<h3>How to use decorators:</h3>

To enable experimental support for decorators, you must enable the <b>experimentalDecorators</b> compiler option either on the command line or in your tsconfig.json:

<h3>Command Line:</h3>

``` 
tsc --target ES5 --experimentalDecorators
```

<h3>tsconfig.json:</h3>

``` json
{
  "compilerOptions": {
    "target": "ES5",
    "experimentalDecorators": true
  }
}
```

There are several built-in decorators provided by TypeScript, such as <b>@deprecated</b>, <b>@experimental</b>, and <b>@abstract</b>, among others. Additionally, you can create custom decorators to suit your specific needs.

Here's a basic example of how to define and use a decorator in TypeScript:

``` typescript
// Custom decorator function
function log(target: any, key: string, descriptor: PropertyDescriptor) {
    const originalMethod = descriptor.value;

    // Redefine the method
    descriptor.value = function (...args: any[]) {
        console.log(`Calling method ${key} with arguments ${args}`);
        return originalMethod.apply(this, args);
    };

    return descriptor;
}

// Using the decorator
class MyClass {
    @log
    myMethod(x: number, y: number) {
        return x + y;
    }
}

const instance = new MyClass();
instance.myMethod(3, 5); // Output: Calling method myMethod with arguments 3,5
```

# 2- What are generics in TypeScript?

- Generics are a TypeScript feature that allows us to pass in various types of data and create reusable code to handle different inputs. They allow us to define placeholder types which are then replaced when the code is executed with the actual types passed in.
  
- Generics are like a template that can be reused across the same piece of code multiple times but with the value being independent of each invocation of the function. Let’s look at an example to get a better understanding of this.

``` typescript
// 👇 We define a generic value called T with <T>
function getFirstElement<T>(arr: T[]): T {
  return arr[0];
}

const numberArray: number[] = [1, 2, 3, 4, 5];
const stringArray: string[] = ['apple', 'banana', 'orange'];

// 👇 Note the generic values being passed in <number> & <string>
const firstNumber = getFirstElement<number>(numberArray);
const firstString = getFirstElement<string>(stringArray);
```
<h3>Generics offer us multiple benefits as developers, but some of the biggest ones are:</h3>

1. <b>Type Safety and Error Detection:</b> Generics allow us to write code that operates on various types of data without losing the type safety of TypeScript.

2. <b>Code Reusability & Flexibility:</b>b In a similar sense to the above point, generics help us make our code more reusable and flexible. This is because, with generics, we can abstract a piece of code to be more generic and work with multiple data types instead of just one, cutting down on the amount of duplicate code required to work with different data types.

3. <b>Better Maintainability:</b> Because generics allow us to write more reusable code, we now have fewer instances of code to maintain and update with bug fixes when required.

<h3>How to Use Generics:</h3>

Generics are declared using angle brackets <b>(<>)</b> and can be used in functions, classes, interfaces, and type aliases.

<b>1. Function Generics:</b>

``` typescript
function identity<T>(arg: T): T {
    return arg;
}

// Usage
let result = identity<number>(10); // result will be of type number
let value = identity<string>("Hello"); // value will be of type string
```

<b>2. Class Generics:</b>

``` typescript
class Box<T> {
    private item: T;

    constructor(item: T) {
        this.item = item;
    }

    getItem(): T {
        return this.item;
    }
}

// Usage
let box = new Box<number>(10); // box will hold a number
console.log(box.getItem()); // Output: 10
```


<b>3. Interface Generics:</b>

``` typescript
interface Pair<T, U> {
    first: T;
    second: U;
}

// Usage
let pair: Pair<number, string> = { first: 1, second: "two" };
console.log(pair); // Output: { first: 1, second: "two" }
```
<h3>When to Use Generics</h3>

You should consider using generics when:

- You want to create reusable components or functions that can work with different types.
- You need to maintain type safety while writing flexible code.
- You want to write abstract algorithms that are independent of specific data types.
  
Generics are particularly useful in scenarios such as creating data structures (like arrays, lists, or trees), implementing algorithms (sorting, searching), and designing libraries or frameworks.

# 3- Interface vs Type in TypeScript ?

In TypeScript, both <b>interface</b> and <b>type</b> are constructs you can use to define shapes of data or objects. They have similarities and differences, and understanding these can help you decide when to use each.

<h3>Interface</h3>

1. <b>Extension:</b> An interface can be extended using the extends keyword. This allows you to create new interfaces that inherit properties from an existing interface.

2. <b>Declaration Merging:</b> Interfaces support declaration merging. If you define an interface twice with the same name, TypeScript will merge the two declarations into one. This feature is handy when augmenting existing interfaces or declaring additional properties for existing libraries.

3. <b>Implementation:</b> An interface can be implemented by a class. This enforces that the class conforms to the structure defined by the interface.

<b>Example:</b>

``` typescript
interface Animal {
    name: string;
}

interface Dog extends Animal {
    bark(): void;
}
```

<h3>Type</h3>

1. <b>Unions and Intersections:</b> Type aliases can define unions or intersections of other types, which interfaces cannot.
   
2. <b>Non-object Types:</b> Type aliases can be used to alias not just object shapes but also other types such as primitives, unions, and tuples. Here's how you can use type aliases with these types of data:

    1. <b>Primitives:</b> You can create a type alias for a primitive type, though this is less common and usually not as useful as the other uses of type aliases.
  
      ``` typescript
         type MyString = string;
         type MyNumber = number;
      ```

    2. <b>Unions:</b> This is particularly powerful. You can define a type that can be one of several types. For instance, if you want a variable to accept either a string or a number, you can define a type alias like this:

       ``` typescript
         type StringOrNumber = string | number;
       ```

    3. <b>Tuples:</b> Tuples are like arrays with fixed types and lengths. You can define a tuple using a type alias, specifying the type of each element in the tuple.

       ``` typescript
         type NameAndAge = [string, number];
       ```
   
4. <b>Cannot be Reopened/Extended:</b> Once you've defined a type, you cannot redefine or extend it with new properties (unlike interfaces).

<b>Example:</b>

``` typescript
type Animal = {
    name: string;
};

type Bear = Animal & {
    honey: boolean;
};

type StringOrNumber = string | number;

```

<h3>Choosing Between interface and type</h3>

- <b>Use interface when:</b> you need to define a contract for an object or you want to take advantage of features like extension or implementation by classes.
- <b>Use type when:</b> you need to define a type that might not be an object, or you need to use unions, intersections, or tuples.
  
In many TypeScript style guides, <b>interface</b> is preferred for defining object shapes due to its more extensible and readable nature.   
