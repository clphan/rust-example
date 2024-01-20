# Variable and Mutability 
- By default, variables are immutable. Once a value is bound to a name, you can't change the value.
Options to set it mutable or change value:
  - adding `mut` in front of variable
  - using `shadowing` to change value but keep immutable.

# Constants
- Bound to a name and are not allowed to change.
- Constants can't use `mut` (always immutable).
- Naming convention: use all uppercase with underscores between words.
- Constants are valid in scope in which they were declared.
```
Example: const THREE_HOURS_IN_SECONDS: u32 = 120;
```

# Shadowing
```
let x = 3;
let x = x + 1;
```
- Use same variable's name and repeat use `let` keyword.
- First variable is shadowed by the second. The second variable overshadows the first.
- Allow reuse variable name but different type:
```
let mut spaces = "  ";
spaces = spaces.len();
```
# Data types
Rust is statically typed language -> it must be know the types of all variables at compile time.

Two data type subsets:
- scalar: represnet single value (integers, floating-point, numbers, Booleans, and characters).
- compound: group of mutiple value in one type (tuples and arrays).

## Scalar

- Integer types in Rust (default: i32): 

| Length  | Signed | Unsigned |
|---------|--------|----------|
| 8-bit   | i8     | u8       |
| 16-bit  | i16    | u16      |
| 32-bit  | i32    | u32      |
| 64-bit  | i64    | u64      |
| 128-bit | i128   | u128     |
| arch    | isize  | usize    |

To easier for read we can use  visual separator _, for example: `1_000` same as `1000`.

Integer literal in Rust:

| Number literals | Example    |
|-----------------|------------|
| Decimal         | 98_222     |
| Hex             | 0xff       |
| Octal           | 0o77       |
| Binary          | 0b111_0000 |
| Byte (u8 only)  | b'A'       |

- Floating-point types:
Allows: f32 (single-precision float) or f64(double precision).

- Numeric Operations: addition (+), subtraction (-), multiplication (*), division (/), and remainder (%).

- Boolean type:
  - type: bool
  - values: true/false

- Character type:
  - char literals using single quotes: '', by contrast string literals using "".
  - char type is four bytes in size

## Compound types
### tulple type: fixed length (once declared -> cant grow or shrink in size)
- each position in tuple has a type:

```
fn main() {
  let tup: (i32, f64, u8) = (500, 6.4, 1);
}
```

- using pattern matching to destructive a tuple value
- using dot (.) to access a tuple element

```
let tup = (1, 1.1, 0);
let (x, y, z) = tup; // called destructing
let first_element = tup.0; // access a tuple element
```
### array type
- every element of an array must have same type.
- array in Rust have a fixed length.
- data is allocated in stack.
- using array to ensure always have a fixed number of elements.
```
let a: [i32; 5] = [1,2,3,4,5]; // type: i32 and num element: 5
let a = [3;5] // similar to: a = [3,3,3,3,3]
```
- using index to access array: `a[0]`
- access array with invalid index will cause a Rust panic

## Function
- main is entry point
- using `snake_case` as conventional style for function and variable names. (lowercase and underscores).
- Rust dont care where you define functions. (eg. function another_function can be defined before or after main).

## Parameters
```
fn another_function(param1: i32, param2: &str) {
  // TODO: 
}
```
- using comma to separate parammeter declarations

## Statements and Expressions
- Statelements are instructions that perform some actions and do not return a value.
- Expressions evaluate to a resultant value.

```
fn main() {
  let x = 3; // statement
  let x = (let y = 3); // throw error becuase statement do not return a value.
}
```
- expression can be:
  - function
  - macro
  - curly brackets 

- expression do not include ending semicolons.
- if expression contain ending semicolons it will become a statelemt.

## Control flow
Control flow: if,  for, loop, whote, rev

- if: 
  - it's expression `let number = if condition { 5 } else { 6 }`
  - result of if else must be same type `Throw error X: let number = if condition { 5 } else { "six" }`

- loop: 
  - using `break` to exit loop or exit manually
  - loop return value:
  ```
  let result = loop {
    counter += 1;

    if(counter == 10){
      break counter * 2;
    }
  }
  ```
  - loop label for case control break, exit, continue:

  ```
  fn main() {
    let mut count = 0;
    'counting_up: loop { // outer loop
      println!("count = {count}");
      let mut remaining = 10;

      loop { // inner loop
        println!("remaining = {remaining}");
        if remaining == 9 {
          break; // exit inner loop only
        }
        if count =  2 {
          break 'counting_up; // exit outer loop
        }
        remaining -= 1;
      }
      count += 1;
    }
    println!("End count = {count}");
  }
  ```

- while:
  - call break to stop loop
  - condition is true -> code run

- for:
  - more safety and conciseness when compare to while in some cases.
  - example:
  ```
  // Less performance & error prone:
  let a = [10, 20, 30, 40, 50];
  let mut index = 0;

  while index < 5 {
    println!("the value is: {}", a[index]);

    index +=1;
  }
  ```
  ```
  // more concise
  let a = [10, 20, 30, 40, 50];

  for element in a {
    println!("the value is: {element}");
  }
  ```
