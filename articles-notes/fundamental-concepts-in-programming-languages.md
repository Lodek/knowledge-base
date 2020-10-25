```yaml
article:
  id: prog-lang-funds
  url: https://www.ics.uci.edu/~jajones/INF102-S18/readings/05_stratchey_1967.pdf
  author: CHRISTOPHER STRACHEY
  date-pub: 2000
  title: Fundamental Concepts in Programming Languages
  tags:
    - programming languages
    - language design
    - polymorphism
```

# notes
- distinction between r-values, l-values, names, expressions, commands and so on.
- l-values are expressions that point to *locations*, which store values. The concept of a location is abstract and does not necessarily map to an address in memory.
- r-values are also expressions but in the sense that the result of an r-value is the final result. in the case of the `2+3` r-value exp, the reuslt is `5`.
- command vs expr. -> commands make the computer execute an action, an instruction; an imperative action. expressions are mathematical constructs, which, often times, are translated to a chain of commands given the composability of expressions.
- expressions have either an r-value or an l-value
- assignment is a command
- l-value exp exist in the context of assignment
> In essence this means that if we wish to find the value of an expression which
contains a sub-expression, the only thing we need to know about the sub-expression is its
value. Any other features of the sub-expression, such as its internal structure, the number
and nature of its components, the order in which they are evaluated or the colour of the ink
in which they are written, are irrelevant to the value of the main expression.
- the author defines 3 scopes in the paper: non-local, own and local. those ideas are familiar with non-local being global, local being the local scope in different context and own being a hybrid private scope which is analogous to a function in C that makes use of `static` local variables. It's a non-volatile, private scope.
- first and second class citzens: functions are usually second class objects because one can't directly declare and assign a function to a name
- closure are the name of the r-value of a function. closures contain both the function body and a list of variables which were used in function definition. in other words, closures contain references to the scope outside of the function
- polymorphic operators: operators whose meaning are type dependent, leads to ambiguity. e.g `+` operator in python can both concat lists and add numbers
- dynamic type: the type of an expression is determmined based on its r-value and any r-value can be assigned to any l-value. as such, the r-value carries a hint of what its type is.

