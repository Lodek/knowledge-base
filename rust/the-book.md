```yml
book: 
  title: The rust programming Language
  date: 2021-01-22
```

# 9
- panic is a good option when the application gets to a bad/invalid state, such as when an invariant or contract is violated.
- another valid panic scenario would be a point in the code where the code needs to be in a valid state. 
- inability to cleanly signal the failure.
- panic when the library code relies on code from a library which in turn returns an error. this means ther eis no possibility for my library code to recover.
- panic on caller side errors, as in, error made by the programmer, not input or invalid data.
- panic when there's a potential security threat

# 10
- Due to the borrow checker, the only case a function can return a reference is if it receives a reference. there is no other case where returning a reference would have a permissible lifetime.
- When a function receives more than one references and returns a reference, we got a problem because the compiler isn't able to correctly compute for how long the return reference has to live for  because it doesn't know from which input  reference the return reference is associated to.
- When a function with lifetimes is called, the compilers substitue the generic lifetimes for the smallest lifetime of the calling arguments and the enforces it.

# 13
- Rust Iterators remind me of higher kinded data type as in haskell. I don't remember the specifics about kindess of a type, but it's a type that returns a type. A type constructor. Then traits like Monads are a function that takes a higher order type and returns a constraint. The iterator trait seems to follow that pattern
- Iterator adaptor vs consuming adapators. Erm, one seems to be map-like iterators that operator over an iterator and return a new one. The other is a fold-lke function that produces a result from an interator
- consumer adaptors: collect (fold with a type constructor), sum (fold that uses the addition operator).

# 15
- Rust references are just like C pointers, except the compilerforbids two pointers to the same address.
- References never own the data they point to while most smart pointers do.
- `Deref` seems to derefence a reference as to operate with the data.
- `Drop` trait acts as hook which gets called once a Smart Pointer goes out of scope.
- Box stores a value in the Heap, as opposed to the stack. Use cases are: recursive data structures; large, static data sets or trait based generic ownership
- `Deref` trait is used to derefence a value. `let box = Box::new(3);` `assert_eq!(3, *box)'` works because when the compiler applied the derefence operator to a type that implements `Deref` the code is expanded to `*(box.deref());`.
