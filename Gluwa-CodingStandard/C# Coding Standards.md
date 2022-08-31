# Preface

## Rule of Thumb

1. Readability first (your code should be your documentation most of the time)
2. Follow IDE's auto formatted style unless you have really good reasons not to do so. (Ctrl + K + D in Visual Studio)
3. Learn from existing code


## References

This coding standards is inspired by these coding standards
*   [Unreal engine 4 coding standard](https://docs.unrealengine.com/latest/INT/Programming/Development/CodingStandard/)
*   [Doom 3 Code Style Conventions](ftp://ftp.idsoftware.com/idstuff/doom3/source/codestyleconventions.doc)
*   [IDesign C# Coding Standard](http://www.idesign.net/downloads/getdownload/1985)


## IDE Helper

The settings that can be imported into your IDE can be found [here](https://github.com/popekim/CodingStyle/tree/master/CSharp).

# I. Naming Conventions and Style

1. Use Pascal casing for class and structs
```C#
class PlayerManager;
struct PlayerData;
```

2. Use camel casing for local variable names and function parameters
```C#
public void SomeMethod(int someParameter)
{
  int someNumber;
}
```

3. Use verb-object pairs for method names
```C#
public uint GetAge()
{
  // function implementation...
}
```

4. Use pascal casing for all method names except (see below)
```C#
public uint GetAge()
{
  // function implementation...
}
```

5. Use camel case for any non-public method. You might need to add custom Visual Studio style rule as described [here](https://stackoverflow.com/questions/40856186/naming-rule-violation)
```C#
private uint getAge()
{
  // function implementation...
}
```

6. Use ALL_CAPS_SEPARATED_BY_UNDERSCORE for constants
```C#
const int SOME_CONSTANT = 1;
```

7. Use pascal casing for namespaces
```C#
namespace System.Graphics
```

8. prefix boolean variables with `b` and prefix boolean properties with `Is`
```C#
bool bFired;	// for local variable
private bool mbFired;	// for private member variable
public bool IsFired { get; private set; }	// for property
```

9. prefix interfaces with `I`
```C#
interface ISomeInterface;
```

10. prefix enums with `E`
```C#
public enum EDirection
{
  North,
  South
}
```

11. Prefix protected/private member variables with `m`. Use Pascal casing for the rest of a member variable
```C#
Public class Employee
{
  public int DepartmentID { get; set; }
  protected string mName;
  private int mAge;
}
```

12. Methods with return values must have a name describing the value returned
```C#
public uint GetAge();
```

13. Use descriptive variable names. e.g `index `or `employee` instead of `i` or `e` unless it is a trivial index variable used for loops.

14. Capitalize every characters in acronyms only if there is no extra word after them.
```C#
public int OrderID { get; private set; }
public string HttpAddress { get; private set; }
```

15. Prefer properties over getter setter functions
Use:
```C#
public class Employee
{
  public string Name {get; set;}
}
```
Instead of:
```C#
public class Employee
{
  private string mName;
  public string GetName();
  public string SetName(string name);
}
```

16. Use Visual Studio's default for tabs. If another IDE is used, use 4 spaces instead of a real tab.

17. Declare local variables as close as possible to the first line where it is being used.

18. Always place an opening curly brace (`{`) in a new line

19. Add curly braces even if there's only one line in the scope
```C#
if (bSomething)
{
  return;
}
```

20. Use precision specification for floating point values unless there is an explicit need for a `double`.
```C#
float f = 0.5F;
```

21. Always have a `default:` case for a `switch` statement.
```C#
switch (number)
{
  case 0:
    ... 
    break;
  default:
    break;
```

22. If `default:` case must not happen in a `switch` case, always add `Debug.Assert(false);` or `Debug.Fail();`
```C#
switch (type)
{
  case 1:
    ... 
    break;
  default:
    Debug.Fail("unknown type");
    break;
}
```

23. Names of recursive functions end with `Recursive`
```C#
public void FibonacciRecursive();
```

24. Order of class variables and methods must be as follows:
    1. public variables/properties
    2. internal variables/properties
    3. protected variables/properties
    4. private variables
        1. Exception: if a private variable is accessed by a property, it should appear right before the mapped property.
    5. constructors
    6. public methods
    7. Internal methods
    8. protected methods
    9. private methods

25. Function overloading must be avoided in most cases

Use:
```C#
public Anim GetAnimByIndex(int index);
public Anim GetAnimByName(string name);
```
Instead of:
```C#
public Anim GetAnim(int index);
public Anim GetAnim(string name);
```

26. Each class must be in a separate source file unless it makes sense to group several smaller classes.

27. The filename must be the same as the name of the class including upper and lower cases.
```C#
public class PlayerAnimation {}
PlayerAnimation.cs
```

28. When a class spans across multiple files(i.e. partial classes), these files have a name that starts with the name of the class, followed by a dot and the subsection name.
```C#
public partial class Human;

Human.Head.cs
Human.Body.cs
Human.Arm.cs
```

29. Use assert for any assertion you have. Assert is not recoverable. (e.g, most function will have `Debug.Assert(not null parameters)`)

30. The name of a bitflag enum must be suffixed by `Flags`
```C#
public enum EVisibilityFlags
{
}
```

31. Prefer overloading over default parameters

32. When default parameters are used, restrict them to natural immutable constants such as `null`, `false` or `0`.

33. Shadowed variables are not allowed.
```C#
public class SomeClass
{
  public int Count { get; set; }
  public void Func(int count)
  {
    for (int count = 0; count != 10; ++count)
    {
      // Use count
    }
  }
}
```

34. Always use containers from `System.Collections.Generic` over ones from `System.Collections`. Using pure array is fine as well.

35. Prefer to use real type over implicit typing(i.e, `var`) unless the type is obvious from the right side of assignment, or when the type is unimportant. Some acceptable var usage includes `IEnumerable` and when `new` keyword is on the same line, showing what type of object is being created clearly.
```C#
var text = "string obviously";
var age = 28;
var employee = new Employee();

string accountNumber = GetAccountNumber();
```

36. Use static class, not singleton pattern

37. Use `async Task` instead of `async void`. The only place where `async void` is allowed is for event handler.

38. Validate any external data at the boundary and return before passing the data into our functions. This means that we assume all data is valid after this point.

39. Therefore, do not throw any exception from inside our function. This should be handled at the boundary only.

40. As an exception to the previous rule, exception throwing is allowed when switch-default is used to catch missing enum handling logic. Still, do not catch this exception
```C#
switch (accountType)
{
  case AccountType.Personal:
    return something;
  case AccountType.Business:
    return somethingElse;
  default:
    throw new ArgumentOutOfRangeException(nameof(AccountType));
}
```

41. Prefer not to allow `null` parameter in your function, especially from a `public` one.

42. If `null` parameter is used, and postfix the parameter name with `OrNull`
```C#
public Anim GetAnim(string nameOrNull)
{
}
```

43. Prefer not to return `null` from any function, especially from a public one. However, you sometimes need to do this to avoid throwing exceptions.

44. If `null` is returned from any function. Postfix the function name with `OrNull`.
```C#
public string GetNameOrNull();
```

45. Try not to use object initializer. Use explicit constructor with named parameters instead. Two exceptions.
    a. When the object is created at one place only. (e.g, one-time DTO)
    b. When the object is created inside a static method of the owning class. (e.g, factory pattern)


# II. Framework Specific Guidelines

## A. XAML Controls

1. Do not name (i.e, `x:name`) a control unless you absolutely need it

2. Use pascal casing with prefixed `x` character for the name.
```C#
xLabelName
```

3. Prefix the name with full control type
```C#
xLabelName
xButtonAccept
```


## B. ASP .NET Core

1. When using DTO(Data Transfer Object)s for a request body for a RESTful API, make each value-type property as nullable so that model validation is automatic
```C#
[Required]
public Guid? ID { get; set; }
```

2. Validate all the requests as the first thing in any controller method. Once validation passes, all inputs are assumed to be correct. So no [required] nullable properties will be null.

3. Unlike above, `[RouteParam]` will not have ?
```C#
public bool GetAsync([RouteParam]Guid userID)
```


## C. Service/Repo Pattern

1. For the DTO classes and enums that are only used internally (e.g, internal microservice or DTO between service and repo), prefix it with X. This means they are transient classes and enums
```C#
public sealed class XNode
{
}

public enum EXTransactionStatus
{
}
```