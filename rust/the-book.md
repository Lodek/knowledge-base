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

# 15
- Rust references are just like C pointers, except the compilerforbids two pointers to the same address.
- References never own the data they point to while most smart pointers do.
- `Deref` seems to derefence a reference as to operate with the data.
- `Drop` trait acts as hook which gets called once a Smart Pointer goes out of scope.
- Box stores a value in the Heap, as opposed to the stack. Use cases are: recursive data structures; large, static data sets or trait based generic ownership
