# Rust notes

- Pattern matching like Haskell (amazing)
- Tuple unpacking
- Tuples like Python (same synthax)
- Arrays are fixed like in C (json/python list syntax)
- Rust array indexing is wrapped in logic to verify the index is within the array's bounds
- for is unlike the C for. for in Rust iterates over a collection.
- Rust has range like python

## Types
- primitives: int, float, char (unicode), bool
- compounds: tuples (LIT), array

## Expressions and statements
Rust source code can be divided in either expressions and statements.
Expressions compute something, be it a value or evaluating a function.
Statements I'm not too sure of just yet, but it's something that mutates the code maybe?
`let` is a statement and any expression can be used to initialize a `let` statement.

Expressions can be used as a return in a function.
If the last line of a function is an expression (doesn't have a `;` at the end), it's an expression and it's considered to be the return value of the function.

## Break
The `break` keyword in rust has an interesting behavior.
On itself it can be used as a pseudo-return.
`break 3` will temrinate whatever loop it's under and yield the value 3.

As such, loops can be used as an expression to initialize values or as a computing procedure without declaring a function.

Yet another interesting little construct.

## Shadowing

## Ownership and memory considerations
What makes Rust Rust.
A different approach to memory allocation based on memory scopes.
Names are freed after closing `}`.
This concept of ownership comes from C++ and it's called *Resource Acquisition Is Initialization* (RAII).

The 3 pillars to ownership are:
- every value has a variable which is the owner
- each value can have at most one owner
- the value is free once the owner goes out of scope

Assigning a variable to another variable copies data.
Dynamic values are allocated in the heap alongside a stack value which contains metadata about the allocation (address, len and capacity).
Therefore, once a dynamic variable is assigned to another name, the metadata is copied with it and they both reference the same value, unsurprisngly.

The interesting thing Rust does to avoid double free errors is that it invalidates references.
Upon passing a value to another name, the original name is no longer valid and therefore there is no risk of a double free once a scope is finished.

So to respect safety, one must pass around the references to a value in the heap everywhere one wants to access it.
That works but is a bit tedious, therefore rust provides better syntax for that using & which gives another name permission to access a value but not modify it.

Note that in this approach there is an abstraction on top of memory addresses still, rust is dealing with the memory address associated with the value.
The job of the programmer is to specify which names access are allowed to see a value at a given time.
A variable of type `&String` has a copy of the allocation metadata but is not allowed to mutate that value or rust will yell at you.
A reference to the valued owned by a variable is made using the `&` operator.
```rust
let owner = String::from("foo");
let ref: &String = &owner;
```
