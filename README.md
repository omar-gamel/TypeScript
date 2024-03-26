 # What is TypeScript?

- TypeScript is a syntactic superset of JavaScript which adds <b>static typing.</b>
- This basically means that TypeScript adds syntax on top of JavaScript, allowing developers to add <b>types.</b>

# Why should I use TypeScript?

1. It can be difficult to understand what types of data are being passed around in JavaScript.
2. In JavaScript, function parameters and variables don't have any information! So developers need to look at documentation, or guess based on the implementation.
3. TypeScript allows specifying the types of data being passed around within the code, and has the ability to report errors when the types don't match.

<b>Example</b>
TypeScript will report an error when passing a string into a function that expects a number. JavaScript will not.

# What are “decorators” in typescript ?

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
