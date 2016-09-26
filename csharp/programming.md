# Programming

## Namespaces

Namespaces represent the logical packaging of component layers and subsystems.  The declaration template for namespaces 
is: `CompanyName.ProjectOrDomainName.PackageName.SubsystemName` 

**Examples:** 
- `Microsoft.Data.DataAccess`
- `Microsoft.Logging.Listeners`

**Guidelines:**
- Project and package level namespaces will normally be predetermined by an application architect for each project.
- Use Pascal casing when naming sub-system namespaces.

## Classes & Structures

Classes and structures represent the 'Nouns' of a system. As such, they should be declared using the following template: 
`Noun + Qualifier(s)`. Classes and structures should be declared with qualifiers that reflect their derivation from a 
base class whenever possible.  

**Examples:**   
- `CustomerForm : Form`
- `CustomerCollection : CollectionBase`

**Guidelines:**
- Use Pascal casing when naming classes and structures.
- Classes and structures should be broken up distinct `#regions` as previously described in the class layout guidelines. 
- Default values for fields should be assigned on the line where the field is declared. These values are assigned at runtime just before the constructor is called. This keeps code for default values in one place, especially when a class contains multiple constructors.


## Interfaces

Interfaces express behavior contracts that derived classes must implement. Interface names should use Nouns, Noun Phrases, or 
Adjectives that clearly express the behavior that they declare.

**Examples:**
- `IComponent`
- `IFormattable`
- `ITaxableProduct`

**Guidelines:**
- Prefix interface names with the letter `I`.
- Use Pascal casing when naming interfaces.


## Constants

Constants and static read-only variables should be declared using the following template: `Adjective(s) + Noun + Qualifier(s)`

**Example:**
- `public const Int32 DefaultValue = 25;`
- `public static readonly String DefaultDatabaseName = "Membership";`

**Guidelines:**
- Use Pascal casing when naming constants and static read only variables.
- Prefer the use of `static readonly` over `const` for public constants whenever possible. Constants declared using `const` 
are substituted into the code accessing them at compile time. Using `static readonly` variables ensures that constant 
values are accessed at runtime. This is safer and less prone to breakage, especially when accessing a constant value from 
a different assembly.


## Enumerations

Enumerations should be declared using the following template: `Adjective(s) + Noun + Qualifier(s)`

**Example:** 

```csharp
/// <summary>
/// Represents the various ways in which a customer may purchase goods.
/// </summary>
[Flags]
public enum PurchaseMethod
{	
  All = ~0,
  None = 0,
  Cash = 1 << 0,
  Check = 1 << 1,
  CreditCard = 1 << 2,
  DebitCard = 1 << 3,
  Voucher = 1 << 4,
}
```

**Guidelines:**
- Use Pascal casing when naming enumerations.
- Use the `[Flags]` attribute *only* to indicate that the enumeration can be treated as a bit field; that is, a set of flags.
  - When using this attribute, values should be assigned to the enumeration values via bit-shifts. 


## Variables, Fields & Parameters

Variables, fields, and parameters should be declared using the following template: Adjective(s) + Noun + Qualifier(s)

**Examples:** 
- `Int32 lowestCommonDenominator = 10;`
- `Single firstRedBallPrice = 25.0f;`

**Guidelines:**
- Use Camel casing when naming variables, fields, and parameters.
- Define variables as close as possible to the first line of code where they are used.
- Declare each variable and field on a separate line. This allows the use of End-Of-Line comments for documenting their purpose.
- Assign initial values when they differ from the type’s default value
- Avoid meaningless names like i, j, k, and temp.  Take the time to describe what the object really is (e.g. use index instead of i; use swapInt instead of tempInt).
- Use a positive connotation for boolean variable names (e.g. isOpen as opposed to notOpen).


## Properties

Properties should be declared using the following template: `Adjective(s) + Noun + Qualifier(s)`

**Examples:**
```csharp
public Decimal TotalPrice
{
    get { return _totalPrice; }
    set
    {
        // Set value and fire changed event if new value is different
        if(!Object.Equals(value, _totalPrice))
        {
            _totalPrice = value;
            OnTotalPriceChanged();
        }
    }
}
```
	
**Guidelines:**
- Use the common prefixes for inspection properties (properties that return query information about an object). Refer to the appendix for a list of common names and prefixes.
- When there is a property setter that sets another property, use the property setter for the other property.  The other property setter could run its own set of code that is required to propagate the changed value.  


## Methods

Methods should be named using the following format: Verb + Adjective(s) + Noun + Qualifier(s)

**Example:**
- `private IEnumerable<Can> FindRedCansByPrice(Single price, ref Int32 canListToPopulate)`

**Guidelines:**
- Parameters should be grouped by their mutability (from least to most mutable) as shown in the example above.
- If at all possible, avoid exiting methods from their middles.  A well written method should only exit from the same general point: its end.  
- Avoid large methods. As a method’s body approaches 20 to 30 lines of code, look for blocks that could be split into their own methods and possibly shared by other methods.
- If you find yourself using the same block of code more than once, it’s a good candidate for a separate method.
- Group like methods within a class together into a region and order them by frequency of use (i.e. more frequently called methods should be near the top of their regions.


## Event Handlers
Event handlers should be declared using the following format: `ObjectName_EventName`


**Example:** 
- `private HelpButton_Click(object sender, EventArgs e)`


## Error Handling

Use exceptions *only* for exceptional cases, do *not* rely on them for routine program flow. Exceptions have comparatively significant performance overhead. 

**Guidelines:**
- Pass a descriptive string into the constructor when throwing an exception. 
- Use grammatically correct error messages, including ending punctuation. 
  - Each sentence in the description string of an exception should end in a period. 
- If a property or method throws an exception in some cases, document this in the comments for the method.
  - In the documentation, include which exception is thrown and what causes it to be thrown. 
  - **Example:** "Gets or sets the total cost of an `Order`. If the `TotalCost` property is set when the cost should be calculated, an `InvalidOperationException` is thrown." 
- Use the following exceptions if appropriate:
  - `Argument_`, `ArgumentNull_`, `ArgumentOutOfRange_`, `IndexOutOfRange_` (`Exception`): Use for parameter validation
  - `InvalidOperationException`: Used when a method call is invalid for the current state of an object. 
    - **Example:** `TotalCost` cannot be set if the cost should be calculated. If the property is set and it fails this rule, an `InvalidOperationException` is thrown. 
  - `NotSupportedException`: Used when a method call is invalid for the class. 
    - **Example:** `Quantity`, a `virtual` read/write property, is overridden by a derived class. In the derived class, the property is read-only. If the property is set, a `NotSupportedException` is thrown. 
  - `NotImplementedException`: Used when a method is not implemented for the current class. 
    - **Example:** A interface method is stubbed in and not yet implemented. This method should throw a `NotImplementedException`.
- Derive your own exception classes for a programmatic scenarios. 
  - All new derived exceptions should be based upon the core `Exception` class.
  - **Example:** `DeletedByAnotherUserException : Exception`. Thrown to indicate a record being modified has been deleted by another user.
- Rethrow caught exceptions correctly.  
  The following example throws an exception caught and rethrown incorrectly:

  ```csharp
  catch(Exception ex)
  {
      LogManager.Publish(ex);
      throw ex; // Incorrect - we lose the call stack of the exception. 
  }  
  ```
  We log all unhandled exceptions in our applications, but may sometimes throw them again to let the higher level systems determine 
  how to proceed. The problem comes in with the `throw`; it works much better to do this: 
  ```csharp
  catch(Exception ex)
  {
      LogManager.Publish(ex);
      throw; // correct - rethrows the exception that was just caught. 
  }  
  ```
  Notice the absence of an argument to the `throw` statement in the second variation. 

  The difference between the above variations is very subtle, but is *very* important. With the first example, the higher level 
  caller won't receive all the information about the original exception. The call stack in the exception is replaced with a new 
  call stack that originates at the `throw ex` statement - which is *not* what we want to record. The second example is the only 
  one that actually re-throws the original exception, preserving the stack trace where the original error occurred. 
