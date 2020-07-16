# Fist Learnings in Rust 

[Learning Tutorial](https://tourofrust.com/TOC_en.html)

# Ch 1 : Basics 

## Variables 

Variables are declared using the let keyword. When assigning a value, Rust will be able to infer the type of your variable 99% of the time. If it cannot you may add the type to your variable declaration.

```
fn main() {
    // rust infers the type of x
    let x = 13;
    println!("{}", x);

    // rust can also be explicit about the type
    let x: f64 = 3.14159;
    println!("{}", x);

    // rust can also declare and initialize later, but this is rarely done
    let x;
    x = 0;
    println!("{}", x);
}
```

Rust cares a great deal about what variables are modifiable:
- mutable : the compiler will allow the variable to be written to and read from.
- immutable : the compiler will only allow the variable to be read from.

Mutable values are denoted with a mut keyword.

```
fn main() {
    let mut x = 42;
    println!("{}", x);
    x = 13;
    println!("{}", x);
}
```

### Basic Types 

- boolean, unsigned integers, signed integers, floating point, str
- pointer sized integers for representing indexes and sizes of things in memory
- tuple - (value, value, ...) for passing fixed sequences of values on the stack
- arrays - [value, value, ...] a collection of similar elements with fixed length known at compile time
- slices - a collection of similar elements with length known at runtime
- Constants: Unlike variables, constants must always have explicit types and are declared with the keyword `const`.
```
const PI: f32 = 3.14159;
```

Rust is a system programming language, it cares about memory issues you might not be used to. 

Numeric types can be explicitly specified by appending the type to the end of the number (e.g. 13u32, 2u8) for 32 bit unsigned integers etc.

#### Implicit Type Conversion 

Rust requires explicitness when it comes to numeric types. One cannot use a u8 for a u32 casually without error. Luckily Rust makes numeric type conversions very easy with the as keyword.
```
    let a = 13u8;
    let b = 7u32;
    let c = a as u32 + b;
```

#### Arrays

An array is a fixed length collection of data elements all of the same type. The data type for an array is [T;N] where T is the elements' type, and N is the fixed length known at compile-time.
Individual elements can be retrieved with the [x] operator where x is a usize index (starting at 0) of the element you want.

```
fn main() {
    let nums: [i32; 3] = [1, 2, 3];
    println!("{:?}", nums);
    println!("{}", nums[1]);
}
```

#### Function 
Example : the input and the return types are specified but do they have to be ? 
```
fn add(x: i32, y: i32) -> i32 {
    return x + y;
}

fn main() {
    println!("{}", add(42, 13));
}
```
- Functions can return multiple values by returning a tuple of values. 
```
fn swap(x: i32, y: i32) -> (i32, i32) {
    return (y, x);
}

fn main() {
    // return a tuple of return values
    let result = swap(123, 321);
    println!("{} {}", result.0, result.1);
```

- no return : If no return type is specified for a function, it returns an empty tuple, also known as a unit. An empty tuple is represented by `()`. This can be explicitly returned as well. 

## Chapter 2 - Basic Control Flow



