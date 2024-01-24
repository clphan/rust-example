[wip]
## enums and pattern matching
features:
- allow to define type by enumerating its possible variants.
- Option
- pattern matching
- `if let` 

draft:
- rectangle is one of a set of possible shapes that also includes Circle and Triangle.
- enum gives you a way of saying a value is one of a possible set of values.
- enumerate all possible variants.

human {
  male,
  female
}

enum IpAddrKind {
  V4,
  V6,
}

- can put any kind of data insid an enum: strings, numberic types, or structs for example. 
- 