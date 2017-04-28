# C# Style Guide

This is a _work in progress_.

## Table of Contents

1. [General](#general)
1. [Layout](#layout)
1. [Naming](#naming)
1. [Testing Code](#testing-code)
1. [Acknowledgments](#acknowledgments)
1. [References](#references)

## General

### Use var instead of explicit types

Exceptions are allowed. For more information read [this fantastic post from Eric Lippert](https://blogs.msdn.microsoft.com/ericlippert/2011/04/20/uses-and-misuses-of-implicit-typing/).

```csharp
// Bad
HttpClient httpClient = new HttpClient();

// Good
var httpClient = new HttpClient();

// Allowed for using an interface instead of a class
IUserService userService = new UserService();
```

### Don't use explicit *this* reference

It is redundant and does not add for readability. For more information read [this SO post](http://stackoverflow.com/questions/5885249/to-use-or-not-to-use-the-this-qualifier-in-c-sharp).

```csharp
// Bad
this.ValidateParameters();

// Good
ValidateParameters();
```

### Use language built-in alias instead of class names

```csharp
// Bad
String.IsNullOrEmpty(name);

// Good
string.IsNullOrEmpty(name);
```

### Use readonly fields when possible

### Prefer string interpolation to *string.Format*

```csharp
// Bad
var message = string.Format("My name is {0} {1}.", person.FirstName, person.LastName);

// Good
var message = $"My name is {person.FirstName} {person.LastName}.";
```

## Layout

### Use *four spaces* per indentation level

You can enable the "View White Space" option and use CTRL+R/CTRL+W keyboard shortcuts.

```csharp
// Bad
public void SomeMethod()
{
∙∙DoSomethingFirst();
∙∙DoSomethingLater();
}

// Good
public void SomeMethod()
{
∙∙∙∙DoSomethingFirst();
∙∙∙∙DoSomethingLater();
}
```

### Don't use more than one empty line in a row

```csharp
// Bad
public void SomeMethod()
{
    DoSomethingFirst();
    DoSomethingLater();


    DoSomethingAtTheEnd();
}

// Good
public void SomeMethod()
{
    DoSomethingFirst();
    DoSomethingLater();

    DoSomethingAtTheEnd();
}
```

### Remove unused or redundant *using* statements (or directives)

### Use single line and lambda getters for simple methods and read-only properties

```csharp
// Good
public string Name { get; private set; }

// Good
public string UppercaseName => Name.toUpperCase(); 
```

### Curly braces for multi line statements must not share line

```csharp
// Bad
public void SomeMethod() {
    // ...
}

// Good
public void SomeMethod()
{
    // ...
}
```

### Opening or ending curly braces must not be followed/preceded by a blank line

```csharp
// Bad
public void SomeMethod() 
{

    DoSomethingFirst();
    DoSomethingLater();

}

// Good
public void SomeMethod()
{
    DoSomethingFirst();
    DoSomethingLater();
}
```

### Don't use braces for just one line

```csharp
// Bad
if (payment == null)
{
    return "A payment is required.";
}

// Good
if (payment == null)
    return "A payment is required.";
```

### Use spaces in array/object initializers

```csharp
// Bad
var names = new string[] {"Marie","John","Paul"};

// Bad
var names = new string[] {"Marie", "John", "Paul"};

// Good
var names = new string[] { "Marie", "John", "Paul" };
```

### Use spaces between operators but avoid spaces *after opening* and *before closing* parenthesis/brackets

```csharp
// Bad
var result =(4 / 2) + 6; // missing space to the left of opening parenthesis
var result = ( 4 / 2) + 6; // extra space to the right of opening parenthesis
var result = (4 / 2 ) + 6; // extra space to the left of closing parenthesis
var result = (4 / 2)+ 6; // missing space to the right of closing parenthesis
var element = myArray [result] + 1; // extra space to the left of opening bracket
var element = myArray[ result] + 1; // extra space to the right of opening bracket

// Good
var result = (4 / 2) + 6;
var element = myArray[result];
```

### Use spaces around the *=* operator when assigning values

```csharp
// Bad
var result=2;

// Good
var result = 2;
```

## Naming

### Be descriptive with your naming, avoid abbreviations and single letter names

```csharp
// Bad
var hc = new HttpClient();

// Good
var httpClient = new HttpClient();
```

```csharp
// Bad
var e = "test@test.com";

// Good
var email = "test@test.com";
```

### Use *PascalCase* for namespaces, classes, enums, structs, constants, delegates, events, methods and properties

```csharp
// Bad
public class file_reader
{
    // ...
}

// Good
public class FileReader
{
    // ...
}
```

```csharp
// Bad
public const int TIME_IN_SECONDS = 5;

// Good
public const int TimeInSeconds = 5;
```

```csharp
// Bad
public string secondAddress { get; set; }

// Good
public string SecondAddress { get; set; }
```

### Use *camelCase* for variables

```csharp
// Bad
var FileReader = new FileReader();
var file_reader = new FileReader();
var _fileReader = new FileReader();

// Good
var fileReader = new FileReader();
```

### Use *_underscoreCase* for private instance/static fields

```csharp
// Bad
private IUserService UserService;
private IUserService userService;
private IUserService user_service;

// Good
private IUserService _userService;
```

### Interface names must begin with "I"

```csharp
// Bad
public interface LoggerInterface
{
    // ...
}

// Good
public interface ILogger
{
    // ...
}
```

### Include *Async* suffix on async methods

```csharp
// Bad
public async Task<int> GetLatestPosition()
{
    // ...
}

// Good
public async Task<int> GetLatestPositionAsync()
{
    // ...
}
```

## Testing Code

We all know testing code is not built the same way that regular code is, because its purpose is different. This is why we have special guidelines for this type of code.

### Test Class naming: {TargetTestClass}Tests

```csharp
// Bad
namespace MyProject.UnitTests
{
    [TestClass]
    public class MyService
    { }
}

// Good
namespace MyProject.UnitTests
{
    [TestClass]
    public class MyServiceTests
    { }
}
```

### Test Class Location: keep a correspondence with the code being tested

Use the same folder structure / namespace structure as the code that's being tested. This makes it easier to find test classes for a particular class and classes being tested by a particular test class.

### Method naming: {TargetTestMethod}_{Expectation}[_When{Condition}]

The name needs to express:

- **What** is being tested
- **What** should happen.
- Under **which** conditions.

What is being tested will usually be a particular method. (These are unit tests, after all.) For integration tests, there is more freedom in choosing this portion, but should still be a good name indicating the scenario being tested.

What should happen should be concise and to the point. Avoid _should_ or _must_ or expressions of rule/desire. The test itself is that validation, there's no need to specify it.

The conditions can be avoided if "normal" conditions are easy to assume and they're the one being tested. For example, a "must work under regular conditions" test says nothing. A good name would be "SaveToDatabase_PersistsChanges"

```csharp
// Bad: Uses filler words
public void SaveToDatabase_ShouldPersistChanges() { }

// Bad: does not correctly indicate responsibility
public void SaveToDatabase_Works() { }

// Good
public void SaveToDatabase_PersistsChanges() { }

// Also good
public void SaveToDatabase_ThrowsArgumentException_WhenConnectionStringIsNotPresent() { }
```

### Group tests by test target

We generally avoid using `#region` since it is a symptom of poorly designed code. However, tests classes are likely to grow if the same class handles several scenarios to be tested, or if several methods are exposed. Group them by the method being tested.

Include overloaded verions of methods in the same region.

```csharp
#region SaveToDatabase
public void SaveToDatabase_PersistsChanges() { }

public void SaveToDatabase_ThrowsArgumentException_WhenConnectionStringIsNotPresent() { }
#endregion

#region RetrieveFromDatabase
public void RetrieveFromDatabase_RetrievesClientById() { }

public void RetrieveFromDatabase_RetrievesClientsByName() { }

public void RetrieveFromDatabase_ThrowsArgumentOutOfRangeException_WhenIdIsEmptyGuid() { }
#endregion
```

## Acknowledgments

Thank you to all who contributed to any of the styles in this document or mentioned references.

## References

- [StyleCop](http://stylecop.soyuz5.com/StyleCop%20Rules.html)
- [CoreFX C# Coding Style](https://github.com/dotnet/corefx/blob/master/Documentation/coding-guidelines/coding-style.md)
- [Framework Design Guidelines](https://msdn.microsoft.com/en-us/library/ms229042(v=vs.110).aspx)
- [Microsoft C# Coding Conventions](https://msdn.microsoft.com/library/ff926074.aspx)
- [Ruby Style Guide by bbatsov](https://github.com/bbatsov/ruby-style-guide)
- [Airbnb JavaScript Style Guide](https://github.com/airbnb/javascript)
