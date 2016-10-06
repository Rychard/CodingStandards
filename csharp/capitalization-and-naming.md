# Capitalization & Naming

## Capitalization

Follow the standard Naming Guidelines set by the .NET framework team by using only three capitalization styles: Pascal, Camel, and Upper casing.

- **Pascal**: The first letter of an identifier is capitalized as well as the first letter of each concatenated word.  
- **Camel**: The first letter of an identifier is lowercase but the first letter of each concatenated word is capitalized.
- **Upper**: All letters of an identifier are capitalized.

**Examples:**


| Identifier Type | Capitalization Style | Example |
| --------------- | -------------------- | ------- |
| Namespaces      | Pascal | `Microsoft.SqlServer`, `System.ComponentModel` |
| Classes & Structures (`class`/`struct`) | Pascal | `AppView` |
| Constants & Enumerations (`enum`) | Pascal | `TextStyles`, `PaymentMethod` (*See Note) |
| Interfaces      | Pascal | `IEditableObject` | 
| Enumeration values | Pascal | `TextStyles.BoldText` | 
| Properties      | Pascal | `BackColor` |
| Variables & Attributes (`public`) | Pascal | `WindowSize` |
| Variables & Attributes (`private`) | Camel with `_` prefix | `_windowWidth`, `_windowHeight` |
| Methods         | Pascal (`public`, `private`, `protected`) | `ToString()` |
| Method Parameters | Camel | `SetFilter(String filterValue)`
| Local Variables | Camel | `recordCount` |

**: Enumerations decorated with `[Flags]` should have plural identifiers, undecorated enumerations should use singular identifiers.*

Guidelines:

- Upper casing is used only for two-letter acronyms, such as `UI`.
  - Note that `Id` is an abbreviation, and should follow Pascal casing. 
  - Note that three-letter acronyms (ex. `URL`, `WPF`, `GUI`) should *not* use Upper (Use `Url`, `Wpf`, and `Gui`, respectively)
- The Resharper plugin for Visual Studio can be configured to enforce these naming conventions.


## Naming

Follow the standard set by the .NET framework team when it comes to naming. The Programming section of this document provides 
naming templates for each construct within the C# language. These templates can be used in conjunction with the tables provided 
in the appendix of this standard to yield meaningful names in most scenarios.


## Indicating Scope

Developers should be able to infer the scope simply by following the naming conventions above.  In the event of an identifier 
collision, consider choosing a different name for the conflicting identifier.  If the identifier cannot be changed, it must 
be fully-qualified.  It is advisable to insert a comment explaining the reasoning behind the decision. 

**Guidelines:**
- Omit the `this` keyword *unless* it is necessary to resolve ambiguity.