# Generic types, traits, and lifetimes
There are two types:
- concrete such as i32 or String
- generic type, using generic allow run the same code on multiple concrete values.

Traits: constrain a generic type to accept only those types that have a particular behavior.

Lifetime: provide information to compiler about borrowed values -> ensure references will be valid.

## Generic type
Benefits:
- create definition for items: function or structs -> use with many different concrete data types.
- improve code performance.

