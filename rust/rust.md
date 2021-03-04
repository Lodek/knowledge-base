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
# On traits vs interfaces
Althought I've studied Haskell before and it has the concept of typeclasses, the difference between a typeclass/trait vs interface has always been blurry to me.
After a few tests I think I understand it better, here's the outline.
Given the following struct:
```rust
struct Foo<T> {
    value: T
}
```
- It's not possible to implement a trait for a concrete type (eg `impl<String> Foo<String>`).
In that context String will be interpreted as the name of the generic, not the type `String`.
- It's not possible to define the same method for different trait constraints.

Through that, it's possible to see one difference between how interfaces and traits are implemented using generics.
In Java, a generic class can only have one implementation and hence only one constraint.
It's not possible to define a method in a generic class that is only available for one constrained generic (eg `<T extends Iterable>`).
The same is possible using Traits.

```java
impl<T> Foo<T> {
    fn do_foo(&self) {
        println!("foo!");
    }
}

impl<T: Display> Foo<T> {
    fn foo_for_display(&self) {
        println!("display foo");
    }
}
```

Another characteristic of Traits is that they allow for default implementations.
I don't know about other languages but default method implementation in Java wasn't a thing until later on.

Finally, the real money maker is blanket implementation.
Blanket implementations are something I remember from Haskell.
It allows for a tree of traits to be implemented, which means if type `Foo` implements trait `A` and there exists a trait `B` which implements on generics that implement `A`, `Foo` has `B`.

Ex:
```rust
impl<T: Display> ToString for T {
```

## Associated types

Associated types in traits are used by what was called a type constructor in Haskell, similar to the monad type class.
The monad type class would consoome a type constructor `m a` and define methods over the type of `a`.
Hmm, I don't know if my analogies to Haskell hold in this scenario...
Seems like a monad would be a generic. The `[a]` notation reminds me of generics. `m a`, `f a` are also generics.
Or are they.

Anyhow, associated types are used as a placeholder to define the methods in a trait.
Essentially, the trait implementing party will fill in the blank at definition time.

Why not a generic?
Can traits be generic in Rust?
Let's ponder...

```
trait Traity<T> {
  fn traity_fun(&self) -> T
}
```
A trait called `Traity` defining a method called `traity_fun`.
How would we go about implementing this?!...
I can't quite see a problem..

```rust
struct Foo{
    a: i32
}

impl Traity<i32> for Foo {
    fn traity_fun(&self) {
        self.a
    }
}
```

