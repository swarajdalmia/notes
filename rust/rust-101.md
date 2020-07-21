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

This is not very different from the flow control in C, except a few differences. 

### if-else
Conditions don't have parentheses!
```
if x < 42 {
        println!("less than 42");
    } else if x == 42 {
        println!("is 42");
    } else {
        println!("greater than 42");
    }
```

Loop has a secret we'll talk about soon.


```
let mut x = 0;
    loop {
        x += 1;
        if x == 42 {
            break;
        }
    }
    println!("{}", x);
```

### While loops
```
    let mut x = 0;
    while x != 42 {
        x += 1;
    }
```

### For loops
Rust's for loop is a powerful upgrade. It iterates over values from any expression that evaluates into an iterator. What's an iterator? An iterator is an object that you can ask the question "What's the next item you have?" until there are no more items.

The .. operator creates an iterator that generates numbers from a start number up to but not including an end number.

The ..= operator creates an iterator that generates numbers from a start number up to and including an end number.

```
for x in 0..=5 {
        println!("{}", x);
    }
```

### Match
Miss your switch statement? Rust has an incredibly useful keyword for matching all possible conditions of a value and executing a code path if the match is true. match is exhaustive so all cases must be handled.
```
fn main() {
    let x = 42;

    match x {
        0 => {
            println!("found zero");
        }
        // we can match against multiple values
        1 | 2 => {
            println!("found 1 or 2!");
        }
        // we can match against ranges
        3..=9 => {
            println!("found a number 3 to 9 inclusively");
        }
        // we can bind the matched number to a variable
        matched_num @ 10..=100 => {
            println!("found {} number between 10 to 100!", matched_num);
        }
        // this is the default match that must exist if not all cases are handled
        _ => {
            println!("found something else!");
        }
    }
}
```
### return values from a loop
loop can break to return a value.
```
let mut x = 0;
    let v = loop {
        x += 1;
        if x == 13 {
            break "found the 13";
        }
    };
    println!("from loop: {}", v);
```

### Returning Values From Block Expressions
if, match, functions, and scope blocks all have a unique way of returning values in Rust.

If the last statement in an if, match, function, or scope block is an expression without a ;, Rust will return it as a value from the block. This is a great way to create concise logic that returns a value that can be put into a new variable.

Notice that it also allows an if statement to operate like a concise ternary expression.
```
fn example() -> i32 {
    let x = 42;
    // Rust's ternary expression
    let v = if x < 42 { -1 } else { 1 };
    println!("from if: {}", v);

    let food = "hamburger";
    let result = match food {
        "hotdog" => "is hotdog",
        // notice the braces are optional when its just a single return expression
        _ => "is not hotdog",
    };
    println!("identifying food: {}", result);

    let v = {
        // This scope block lets us get a result without polluting function scope
        let a = 1;
        let b = 2;
        a + b
    };
    println!("from block: {}", v);

    // The idiomatic way to return a value in rust from a function at the end
    v + 4
}
```

## Chapter - 3 : Basic Data Structure Types

In this chapter we will look at the most primitive data structures in Rust, paying close attention to their representations in memory. I think you will enjoy how little Rust hides from you how things work.

### Structure 
A struct is a collection of fields.

A field is simply a data value associated with a data structure. Its value can be of a primitive type or a data structure.

Its definition is like a blueprint for a compiler on how to layout the fields in memory nearby each other.

```
struct SeaCreature {
    name: String,
    legs: i32,
    weapon: String,
}
```
- for conciseness, you can create structs that are used like a tuple.
```
struct Location(i32, i32);

fn main() {
    // This is still a struct on a stack
    let loc = Location(42, 32);
    println!("{}, {}", loc.0, loc.1);
}
```
- Unit-like Structs : Structs do not have to have any fields at all. This type of struct is rarely used.

```
struct Marker;

fn main() {
    let _m = Marker;
}
```

### Calling Methods
Unlike functions, methods are functions associated with a specific data type.

static methods — methods that belong to a type itself are called using the :: operator.

instance methods — methods that belong to an instance of a type are called using the . operator.

```
// Using a static method to create an instance of String
let s = String::from("Hello world!");
// Using a method on the instance
println!("{} is {} characters long.", s, s.len());
```
### Memory
- data memory - For data that is fixed in size and **static** (i.e. always available through life of program). Consider the text in your program (e.g. "Hello World!"): This text's bytes are only ever read from one place and therefore can be stored in this region. Compilers make lots of optimizations with this kind of data, and they are generally considered very fast to use since locations are known and fixed.
- stack memory - For data that is declared as variables within a function. The location of this memory never changes for the duration of a function call; because of this compilers can optimize code so stack data is very fast to access.
- heap memory - For data that is created while the application is running. Data in this region may be added, moved, removed, resized, etc. Because of its dynamic nature it's generally considered slower to use, but it allows for much more creative usages of memory. When data is added to this region we call it an allocation. When data is removed from this section we call it a deallocation.

### Creating Data In Memory
There is some confusion here, in terms of what is stores on the stack, heap vs data memory so i'll just skip this for now. 

### Enumerations
Enumerations allow you to create a new type that can have a value of several tagged elements using the enum keyword.

match helps ensure exhaustive handling of all possible enum values making it a powerful tool in ensuring quality code.

```
enum Species {
    Crab,
    Octopus,
}

struct SeaCreature {
    species: Species,
    name: String,
}

fn main() {
    let ferris = SeaCreature {
        species: Species::Crab,
        name: String::from("Ferris"),
    };

    match ferris.species {
        Species::Crab => println!("{} is a crab",ferris.name),
        Species::Octopus => println!("{} is a octopus",ferris.name),
    }
}
```

### Enumerations With Data

