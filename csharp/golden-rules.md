# C# Golden Rules

The following guidelines are applicable to all aspects of C# development:

## Simplicity

- Code should be as simple and readable as possible.  Assume that others will read your code.
- Classes should be small and cohesive.  Avoid large/monolithic classes. 
- Iteration over collections should use the `while` and `foreach` constructs.
- Refrain from using "magic" values in code (i.e. hard-coded strings and numbers)
  - When *necessary*, define these values as either `const`, `static readonly`, `enum`, or read the values from an external resource.

## Organization

- Use a separate file for each `class`, `struct`, `interface`, `enum`, and `delegate`.
- Avoid nesting of classes.

## Documentation

- Documentation is required for any class accessible outside of its assembly, and all methods accessible outside of their containing class.  
- Ideally, *all* classes and methods would be documented.
- Documentation should be in the format supported by the Intellisense feature in Visual Studio, [XML Documentation Comments](https://msdn.microsoft.com/en-us/library/b2s063f7.aspx).  
  - There exists a free plugin for Visual Studio, [GhostDoc](http://submain.com/products/ghostdoc.aspx), which facilitates this process greatly.
  - The addition of meaningful comments within the code is strongly encouraged to document its purpose.
- Indicate incomplete/missing code using `// TODO:` comments.
  - If a method has been written with no body (a method 'stub'), it's body should contain `throw new NotImplementedException();`
  - The [Resharper](https://www.jetbrains.com/resharper/) plugin will recognize both of the above scenarios as incomplete code.  
    - If you have Resharper, this functionality is found here: `[Resharper] > [Tools] > [To-Do Items]`


## Performance 

- Do not use the `String` concatenation operator (`+=`).
  - Instead, create a `StringBuilder` and use it's `Append()`, `AppendFormat()`, and `ToString()` methods, as they are vastly more efficient.
- If a class implements `IDisposable`, ensure that it is wrapped within a `using` block.
  - If this is unavoidable, ensure that the `Dispose()` method is called before the reference to the object falls out of scope.
  - When calling `Dispose()` manually, wrap the usage in `try`/`catch`/`finally`, and call `Dispose()` within the `finally` block.


## Debugging 

- Never present debug information to yourself or the end user via the UI (e.g. `MessageBox`).
- Use tracing and logging facilities to output debug information.  If these facilities do not exist, they must be created.