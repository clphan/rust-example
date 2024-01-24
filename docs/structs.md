# structs or structure
- structs is similar to tulpes or like a object's data attributes in object-oriented language.
- peace of code can be in different type.
- fileds is name and types of the pieces of data.
```
struct User {
  avtive: bool,
  username: String,
  email: String,
  sign_in_count: u64,
}
```
- using struct by creating an instance (specify concrete value for each of the fields),
```
fn main() {
  let user1 = User {
    active: true,
    username: String::from("someuser123"),
    email: String::from("someemail@gmail.com),
    sign_in_count: 1
  }
}
```
- to change value of a field in struct
```
user1.email = String::from("newemail@gmail.com");
```
- use field init shorthand to avoid repeat name
```
fn build_user(email: String, username: String) -> User {
  User {
    active: true,
    username,
    email,
    sign_in_count: 1,
  }
}
```
- use update syntax to reduce code still achieve same purpose
```
// before
fn main() {
  let user2 = User {
    active: user1.active,
    username: user1.username,
    email: String::from("another@example.com"),
    sign_in_count: user1.sign_in_count,
  };
}

// after
fn main() {
  let user2 = User{
    email: String::from("another@example.com"),
    ..user1
  };
}
```

## tuple structs
- useful when we want to give the whole tuple a name
- useful when we want to make the tuple a different type from other tuples
```
struct Color(i32, i32, i32);
struct Point(i32, i32, i32);

fn main() {
  let black = Color(0,0,0);
  let origin = Point(0,0,0);
}
```
- each struct above has its own type

## unit-like structs [WIP]
- usefull when implementing a trait on some type but dont have any data
```
struct AlwaysEqual;

fn main() {
  let subject = AlwaysEqual;
}
```

## ownership of struct data
```
struct User {
  active: bool,
  username: &str, // expected named lifetime parameter
  email: &str, // expected named lifetime parameter
  sign_in_count: u64,
}

fn main() {
  let user1 = User {
    active: true,
    username: "someusername123",
    email: "someone@example.com",
    sign_in_count: 1,
  }
}
```
- using String not &str mean that instance in struct own its data. As long as entire struct is valid the data also valid.
- using &str might require defining lifetime.

## example
```
fn main() {
  let width1 = 30;
  let height1 = 50;

  println!("the area of the rectangle  is {} square pixels.",
  area(width1, height1));
}

fn area(width: u32, height: u32) -> u32 {
  width * height
}
```
- area function has two params which are related.
- the two params should be groupped for more readable and manageble.

option 1: using tuple
- pros: code is abit more structure
- cons: we have to remember .0 is width and .1 is height
```
fn main() {
  let rect1 = (30, 50);

  println!("the area of the rectangle is {} square pixels.", area(rect1));
}

fn area(dimensions: (u32, u32)) -> u32 {
  dimensions.0 * dimensions.1
}
```
option2: using structs
```
struct Rectangle {
  width: u32,
  height: u32,
}

fn main() {
  let rect1 = Rectangle {
    width: 30,
    height: 50,
  }

  println!("the area of the rectangle is {} square pixels.", area(&rect1));
}

fn area(rectangle: &Rectangle) -> u32 {
  rectangle.width * rectangle.height
}
```

## debug mode
[wip]

## method syntax
- method is similar to function but useful when want more organization in stead of making code in various places.
- methods are defined within the context of a struct or enum or trait object.
- first param is always `self` (instance of the struct method)
- everything inside `impl` block will be assiciated with the `Rectangle` type.
- `&self` in the method is short for `self: &Self`, need to use `&` to indicate method borrows the `Self`.
- method name similar to struct field is allowed in rust, sometime called getters.
```
#[derive(Debug)]
struct Rectangle {
  width: u32,
  height: u32,
}

impl Rectangle {
  fn area(&self) -> u32 {
    slef.width * self.height
  }
}

fn main() {
  let rect1 = Rectangle {
    width: 30,
    height: 50,
  }

  println!("the area of the rectangle is {} square pixels.", rect1.area())
}
```

## associated functions
- often called new, but new isn't special name and isn't build into the language.
- functions inside impl are called associated functions.
- function dont associated to self does not a method.
```
impl Rectangle {
  fn square(size: u32) -> Self {
    Self {
      width: size,
      height: size,
    }
  }
}
```

## multiple impl blocks
- multiple impl blocks for one struct are allow

```
impl Rectangle {
  fn area(&self) -> u32 {
    self.width * self.height
  }
}

impl Rectangle {
  fn can_hold(&self, other: &Rectangle) -> {
    self.width > other.width && self.height > other.height
  }
}
```
