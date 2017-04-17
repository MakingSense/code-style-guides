# C# Style Guide

This is a _work in progress_.

## Table of Contents

1. [General](#general)

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

## Resources

- [CoreFX C# Coding Style](https://github.com/dotnet/corefx/blob/master/Documentation/coding-guidelines/coding-style.md)
- [Framework Design Guidelines](https://msdn.microsoft.com/en-us/library/ms229042(v=vs.110).aspx)
- [Microsoft C# Coding Conventions](https://msdn.microsoft.com/library/ff926074.aspx)
