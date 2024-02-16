# CLSS.ExtensionMethods.IList.FillBy

### Problem

[`Array.Fill`](https://docs.microsoft.com/en-us/dotnet/api/system.array.fill) is a convenient method to fill an array first introduced in .NET Standard 2.1. It has the following drawbacks:

- It is not available in .NET runtime environments earlier than .NET Standard 2.1, which are most of the .NET runtime environments. Learn more about the availability of .NET Standard 2.1 [here](https://dotnet.microsoft.com/en-us/platform/dotnet-standard#versions).
- It only supports filling with a value, not with a factory function.
- It only supports raw arrays.
- It returns void and therefore is not very friendly to a functional-style call chain.

### Solution

This package provides `FillBy` to all [`IList<T>`](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.ilist-1) types for .NET Standard 1.0 & 2.0. It rectified the above drawbacks.

Filling a `List<T>` with a factory function, passing through the element's index number:

```csharp
using CLSS;
using System.Linq;

var numbers = Enumerable.Repeat(0, 5).ToList();
numbers.FillBy(i => i * i); // { 0, 1, 4, 9, 16, }
```

`FillBy` returns source collection, saving some lines of code and functional-style friendly:

```csharp
using CLSS;
using System.Linq;

// Create and fill array the standard way
var numbers1 = new int[5];
Array.Fill(numbers1, 4);

// Create and fill array with FillBy
var numbers2 = new int[5].FillBy(4);

// Easy functional syntax
bool allValid = new int[5].FillBy(FactoryFunction)
  .Append(existingResults)
  .All(VerifyResult);
```

**Note**: `ExclusiveSample` works on all types implementing the [`IList<T>`](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.ilist-1) interface, *including raw C# array*.

##### This package is a part of the [C# Language Syntactic Sugar suite](https://github.com/tonygiang/CLSS).