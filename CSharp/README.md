# C# Style Guide

This is a _work in progress_.

## Table of Contents

1. [General](#general)
1. [Layout](#layout)

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

### Remove unused or redundant *using* statements (or directives)

### Use single line and lambda getters for simple methods and read-only properties

```csharp
// Good
public string Name { get; private set; }

// Good
public string UppercaseName => Name.toUpperCase(); 
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

## Resources

- [CoreFX C# Coding Style](https://github.com/dotnet/corefx/blob/master/Documentation/coding-guidelines/coding-style.md)
- [Framework Design Guidelines](https://msdn.microsoft.com/en-us/library/ms229042(v=vs.110).aspx)
- [Microsoft C# Coding Conventions](https://msdn.microsoft.com/library/ff926074.aspx)
