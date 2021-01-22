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
