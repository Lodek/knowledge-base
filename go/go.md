# Topics to study
- interfaces
- echo
- structs / user defined data types 
- go tooling

# notes
- newlines are converted to ; in go.
- slicing works the same as in python. half open interval and uses `:`.
- package `os` has variable `Args` for CLI args.
- public members of a package are declared with capital letters
- `++` operator in Go is a statement not an expression. It is only postfix. Neat because i've seen some hacky stuff using `i++` in C, not to mention the whole deal with `i++` and `++i`. Talk about extra.
- comp error with unused local variables
- comp error with unused imports

# Interfaces
- Go interfaces are satisfied implicitly. So long as a type implement all the methods declared by an interface, the compiler will allow it.
- Type assertions are used to cast interface values to other types. The value must be an interface type and the value it is being cast may be an interface or a concrete type. `x.(T)` is the general syntax.
- There are two forms to type assertions. In the single return value case the code will panic if the types don't match, in the double return value case it will return a boolean indicating whether the operation was succesful or not.

# Packages
- It seems to me like packages in go are "logical" in that it doesn't care about the folder structure or the path to a file, just the name of the package in the file.
- Under that logic, any global in any file of a package is visible cross files. 

# Pointers
> It is perfectly safe for a function to return the address of a local variable. For instance, in the code below, the local variable v created by this particular call to f will remain in existence even after the call has returned. I can't accept that. That is so odd. nvm it has garbage collection. i can accept it
- `new` seems to be a factory function for types. It returns a pointer to the given type; `malloc` for types instead of size. glorious type safety

# Tooling
- `go fmt` formats code
- `goimports` for dealing with imports
