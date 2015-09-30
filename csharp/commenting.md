# Commenting

## Intellisense Comments

Use triple slash `///` comments for documenting the public interface of each class. This will allow Visual Studio to pick 
up the method’s information for Intellisense. It is strongly suggested to add these types of comments before each 
`public`, `internal`, and `protected` class member, but it is up to the individual developer to determine whether 
to include these comments for private fields.  There exists a free plugin for Visual Studio by the name of GhostDoc 
which facilitate the creation of these types of comments.

**Example:**
```csharp

```


## End-Of-Line Comments

There exist no scenarios where end-of-line comments are acceptable.  The following sub-sections provide examples 
regarding comment placement for those scenarios that are commonly encountered.

### Field Declarations
**Example:**

```csharp
public class TestClass
{
    // Value indicating whether this instance is ready to process data.
    private Boolean _isReady;
}
```


### Conditional Blocks
**Example:**

```csharp
// Ensure that the current user is permitted to access this data.
// We also need to check for an active network connection.
if(canAccessData && isConnected)
{
    // Retrieve all the data and deliver it to the user.
}
else if(isconnected)
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
operation or when a significant condition is reached. Comments should always begin with two slashes, and must be followed 
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
searched for these comments before each release build.  Resharper, a plugin for Visual Studio, will find these for you.


## C-Style Comments

Use C-style (`/* */`) comments only for temporarily blocking out large sections of code during development and debugging. 
Code should not be committed with these sections commented out. If the code is no longer necessary, it should be deleted.  
Leverage your source control tools to view changes and deletions from previous versions of the code. If code must be 
checked in with large sections commented out, include a `// TODO:` comment describing why it was committed in this manner.