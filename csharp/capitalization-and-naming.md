# Capitalization & Naming

## Capitalization

Follow the standard Naming Guidelines set by the .NET framework team by using only three capitalization styles: Pascal, Camel, and Upper casing. 

**Examples:**


| Identifier Type | Capitalization Style | Example |
| --------------- | -------------------- | ------- |
| Abbreviations   | Upper | `ID`, `REF` |
| Namespaces      | Pascal | `AppDomain`, `System.IO` |
| Classes & Structures (`class`/`struct`) | Pascal | `AppView` |
| Constants & Enumerations (`enum`) | Pascal | `TextStyles` |
| Interfaces      | Pascal | `IEditableObject` | 
| Enumeration values | Pascal | `TextStyles.BoldText` | 
| Properties      | Pascal | `BackColor` |
| Variables & Attributes (`public`) | Pascal | `WindowSize` |
| Variables & Attributes (`private`) | Camel with `_` prefix | `_windowWidth`, `_windowHeight` |
| Methods         | Pascal (`public`, `private`, `protected`) | `ToString()` |
| Method Parameters | Camel | `SetFilter(String filterValue)`
| Local Variables | Camel | `recordCount` |

Guidelines:
- In Pascal casing, the first letter of an identifier is capitalized as well as the first letter of each concatenated word.  
- In Camel casing, the first letter of an identifier is lowercase but the first letter of each concatenated word is capitalized. 
- Upper casing is used only for two-letter abbreviations, such as `UI`.
  - As an exception to this, `ID` should also use Upper.
  - Note that three-letter abbreviations (ex. `URL`, `WPF`, `GUI`) should *not* use Upper.
- The Resharper plugin for Visual Studio can be configured to enforce these naming conventions.


## Naming

Follow the standard set by the .NET framework team when it comes to naming. The Programming section of this document provides 
naming templates for each construct within the C# language. These templates can be used in conjunction with the tables provided 
in the appendix of this standard to yield meaningful names in most scenarios.