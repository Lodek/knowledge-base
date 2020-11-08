```yaml
book:
  id: graham-haskell
  author: Graham Hutton
  title: Programming in Haskell
  publish-date: 2016
  tags:
    - haskell
    - fp
```

# 12
- Functors encapsulate the concept of mapping a function over every element in a data structure
- Typeclasses make use of type inference in the typeclass function signatures to specify the kind of the the type variable.
Eg. functor is defined as `class Functor f ...` which defines `fmap` as `fmap :: (a -> b) -> fa -> fb`.
Since `f` is the type variable of functor and in the definition of `fmap`, `f` is used as a type constructor, it follows that `f` must be of kind `* -> *`.
- Applicative functors are an extension on map.
While Functors are restricted to functions of a single argument, applicatives encapsulate this pattern and make use of currying to build applicatives with partially applied functions, until it gets fully evaluated.
- Just as in Learn you a Haskell, the general idea of applicatives and monads are clear: handle stateful computations.
- Applicatives encapsulate the pattern of applying an N argument function over N applicative values 
- Monads encapsulate the pattern of applying a stateful computation that takes a pure value and return a state over a stateful value.
- A control monad is a function that consumes a state and return a result-state pair. The brain boom is the concept of using a function as a type, which makes sense, but it's not something i've seen before. i'm digesting it.
# 13
- Once again, a function is used to define a type, this time a parser. Brain boom

# 14
- Monoid: Set with an associative operator and identity element
- Monoid type class define 3 functions: `mempty`, `mappend` and `mconcat`. For the list monoids those functions are, respectively, `[]`, `++`, `foldr mappend mempty`.
- There are wrapper monoid definitions for the Integers, sum and product.
