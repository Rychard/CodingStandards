# Formatting

## Class Layout

The order of code within every class in the application should follow a common pattern throughout the application.  

When the amount of code within a class becomes large enough that it becomes unwieldy, determine whether it is possible to split 
the class into smaller, more manageable classes.  In the event that a class cannot be split up any further, but is still difficult 
to read, consider wrapping sections of code into regions.  Smaller classes do not usually benefit from regions, but as the 
complexity of the class increases, wrapping the larger sections into regions may provide some help when navigating through the code.
    
**Example:**

``` csharp
// Custom Class layout example
class Purchasing
{
    #region Events / Delegates

    #region Fields 
    
    #region Properties
        
    #region Constructors

    #region Instance Methods

    #region Static Methods

    #region Designer Generated Code
}
```

**Guidelines:**
- Be consistent about the layout of all classes within each project.
- Omit regions if their associated class elements are not needed.
- The `Designer Generated Code` region created by Visual Studio's Visual Designer should *never* be modified by hand. 
  - Many of these files are generated with T4 Text Templates, which should be modified instead.


## Indentation & Braces

Statements should be indented (using 4 spaces, which is the default setting in Visual Studio) into blocks that show 
relative scope of execution.  Braces should be placed directly below and aligned with the statement that begins a 
new scope of execution. Visual Studio includes a keyboard short-cut that will automatically apply this format to 
a selected block of code.

> For further reading, refer to [Allman Style](https://en.wikipedia.org/wiki/Indent_style#Allman_style).

**Example:**

``` csharp
Decimal CalculateDiscountedAmount(Decimal amount, PurchaseMethod purchaseMethod)
{
    Decimal discount = 0.0f;
    switch(purchaseMethod)
    {
        case PurchaseMethod.Cash:
            discount = CalculateCashDiscount(amount);
            Trace.WriteLine("Cash discount of {0} applied.", discount);
            break;

        case PurchaseMethod.CreditCard:
            discount = CalculateCreditCardDiscount(amount);
            Trace.WriteLine("Credit card discount of {0} applied.", discount);
            break;

        default:
            // No discount applied for other purchase methods
            Trace.WriteLine("No discount applied.");
            break;
    }

    Decimal discountedAmount = (amount - discount);

    // A negative amount indicates a discount greater than the normal amount.
    // Ensure that it is reset to 0 to avoid giving money away.
    if(discountedAmount < 0.0f)
    {
        discountedAmount = 0.0f;
    }

    LogManager.Publish(discountedAmount.ToString());

    // Return the discounted amount
    return discountedAmount;
}
```

## Whitespace

Liberal use of white space is highly encouraged.  This provides enhanced readability and is extremely helpful during 
debugging and code reviews. The indentation example above shows an example of the appropriate level of white space.

**Guidelines:**
- Blank lines should be used to separate logical blocks of code. 
  - Note the clean separation between each `case` in the `switch` statement of the previous code example. 
- When declaring or invoking methods, do not include whitespace characters between the opening parenthesis and the parameters.
  - By extension, do not include whitespace characters between the last parameter and the closing parenthesis.  
  - A single space *should*, however, be included after the comma that separates each parameter.


## Long Lines of Code

Under *no* circumstances should a single statement wrap across multiple lines.

Individual lines of code should (but are not required to) fit within the visible area of the screen using the 
default configuration and layout of Visual Studio.  Instead, long statements should be broken into multiple 
statements.  This improves readability and minimizes the chance that something will be overlooked.

Comments are not subject to this rule, and can span multiple lines.  Care should be taken to ensure 
readability and proper representation of the scope of the information in the broken lines.

**Example:**

``` csharp
String Win32FunctionWrapper(Int32 arg1, String arg2, Boolean arg3)
{
    // Perform a PInvoke call to a win32 function, providing default values for obscure parameters
    // to hide the complexity from the caller
    if(Win32.InternalSystemCall(null, arg1, arg2, arg3, null))
    {
        return "Win32 system call succeeded.";
    }
    else
    {
        return "Win32 system call failed.";
    }
}
```

**Guidelines:**
- When breaking comments across multiple lines, match the indentation level of the code that is being commented upon.
- Consider embedding large string constants in resources and retrieving them dynamically using the `ResourceManager` class.