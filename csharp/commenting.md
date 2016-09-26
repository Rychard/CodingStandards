# Commenting

## Intellisense Comments

Use triple slash `///` comments for documenting the public interface of each class. This will allow Visual Studio to pick 
up the method’s information for Intellisense. It is strongly suggested to add these types of comments before each 
`public`, `internal`, and `protected` class member, but it is up to the individual developer to determine whether 
to include these comments for `private` members.  There exists a free plugin for Visual Studio by the name of 
[GhostDoc](http://submain.com/products/ghostdoc.aspx) which facilitate the creation of these types of comments.

**Example:**
```csharp
/// <summary>
/// Attempts to set the specified flag on the current instance.
/// </summary>
/// <param name="flagName">The name of the flag that will be set.</param>
/// <returns><c>true</c> if the flag was set, otherwise <c>false<c/></returns>
/// <remarks>
/// This method will return <c>false</c> if the flag is invalid. <para />
/// To validate the name of a flag, refer to the <see cref="EntityFlag.IsValid"/> method.
/// </remarks>
public Boolean SetFlagValue(String flagName)
{
    // ... snip ...
}
```


## End-Of-Line Comments

There exist no scenarios where end-of-line comments are acceptable.  The following sub-sections provide examples 
regarding comment placement for those scenarios that are commonly encountered.

### Field Declarations

Rarely is it necessary to document fields directly.  As fields are *usually* only accessible from within the class, 
their purpose should be evident solely from their identifier.  In the event that you are unable to unambiguously 
convey its purpose in the identifier alone, the class may require refactoring to extract the complexity of the field 
to its own class.  Until this refactoring can be performed, a short comment on the preceding line is acceptable as a 
temporary solution.  

**Example:**

```csharp
public class TestClass
{
    // The difference between the number of accessible and inaccessible baz objects.
    private Int32 _bazObjectCountDifference;
}
```


### Conditional Blocks

Similar to field declarations, the purpose and intent of a conditional should be evident from the identifiers of 
the values being compared.  Before documenting the conditional, developers should make an attempt to reduce its 
complexity.  This can often be accomplished simply by lifting individual calculations into locally-scoped variables.  
If there is reasonable need for documentation after simplifying the conditional, a short comment can be placed on 
the line immediately preceding it.

**Example:**

```csharp
// Ensure that the current user is permitted to access this data.
// We also need to check for an active network connection.
if (canAccessData && isConnected)
{
    // Retrieve all the data and deliver it to the user.
}
else if (isconnected)
{
    // The user isn't permitted to access this data.
    // Because we have a connection, we should log this request.    
}
else
{
    // The user doesn't have access, and there's no connection.
    // This poses no risk, since there's no open connection. 
}
```


## Single Line Comments

Use single line comments above each block of code relating to a particular task within a method that performs a significant 
operation or when a significant condition is reached. Comments should _always_ begin with two slashes, and must be followed 
by a single space.

**Example:**
```csharp 
// Compute total price, including any applicable taxes.
Single stateSalesTax = this.CalculateStateSalesTax(amount, Customer.State);
Single citySalesTax = this.CalculateCitySalesTax(amount, Customer.City);
Single localSalesTax = this.CalculateLocalSalesTax(amount, Customer.Zipcode);
Single totalPrice = amount + stateSalesTax + citySalesTax + localSalesTax;
Console.WriteLine("Total Price: {0}", totalPrice);
```

## Incomplete/Missing Code

Use the `// TODO:` comment to indicate a section of code that needs further work before release. Source code should be 
periodically reviewed for these comments during development, as well as before each release build.  

> Resharper, a plugin for Visual Studio, can locate these comments using the following menu item:
>
> <kbd>Resharper</kbd> &raquo; <kbd>Tools</kbd> &raquo; <kbd>To-do Explorer</kbd>


## C-Style Comments

Use C-style (`/* */`) comments only for temporarily blocking out large sections of code during development and debugging. 
Code should not be committed with these sections commented out. Code that is no longer necessary should be deleted;  
leverage your source control tools to review additions and deletions from previous versions of the code. If code must be 
checked in with large sections commented out, include a `// TODO:` comment describing why it was committed in this manner.