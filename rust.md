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
