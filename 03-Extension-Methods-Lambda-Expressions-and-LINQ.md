# Extension Methods, Lambda Expressions and LINQ

## Extension Methods
* Extension methods allow existing compiled types to gain new functionality
  * Without recompilation
  * Without touching the original assembly
* Defining Extension Methods
  * Defined in a static class
  * Defined as ```static```
  * Use ```this``` keyword before its first argument to specify the class to be extended
* Extension methods are "attached" to the extended class
* Can also be called from statically through the defining static class
* Example:

```csharp
public static void IncreaseWidth(this IList<int> list, int amount) {
  for (int i = 0; i < list.Count; i++) {
    list[i] += amount;
  }
}
// ...
static void Main() {
  List<int> ints = new List<int> { 1, 2, 3, 4, 5 };
  ints.IncreaseWidth(5); // 6, 7, 8, 9, 10
}
```
## Anonymous Types
* Encapsulate a set of read-only properties and their value into a single object
* No need to explicitly define a type first
* To define an anonymous type, use of the new var keyword in conjunction with the object initialization syntax

```csharp
// Use an anonymous type representing a car
var myCar = new { Color = "Red", Brand = "BMW", Speed = 180 };
Console.WriteLine("My car is a {0} {1}.", myCar.Color, myCar.Brand);
```
* At compile time, the C# compiler will autogenerate an uniquely named class
* The class name is not visible from C#
  * Using implicit typing (var keyword) is mandatory

## Delegates in .NET Framework
* Delegates are special .NET types that hold a method reference
* Describe the signature of given method
  * Number and types of the parameters
  * The return type
* Their "values" are methods
  * These methods match their signature (parameters and return types)
  * Delegates are reference types
* Delegates are roughly similar to function pointers in C and C++
  * Strongly-typed pointer (reference) to a method
  * Pointer (address) to a callback function
* Can point to static and instance methods
* Can point to a sequence of multiple methods
  * Known as multicast delegates
* Used to perform callback invocations
* Implement the "publish-subscribe" model
* Example:
```csharp
// Declaration of a delegate
public class DelegatesExample {
  delegate void SimpleDelegate(string param);
  static void Main() {
    // Instantiate the delegate
    SimpleDelegate d = delegate(string param) {
      Console.WriteLine("I was called by a delegate.");
      Console.WriteLine("I got parameter: {0}.", param);
    }
    // Invocation of the method, pointed by delegate
    d("test");
  }
}
```
* Predefined delegates in .NET:
  * ```Action<T1, T2, T3>``` - generic predefined void delegate with parameters of types  T1, T2 and T3
  * ```Func<T1, T2, TResult>``` - generic predefined delegate with return value of type TResult
  * Both have quite a lot of overloads

## Lambda Expressions
* A lambda expression is an anonymous function containing expressions and statements
  * Used to create delegates or expression tree types
* Lambda expressions
  * Use the lambda operator ```=>```
    * Read as "goes to"
  * The left side specifies the input parameters
  * The right side holds the expression or statement
* Example:

```csharp
List<int> list = new List<int>() { 1, 2, 3, 4 };
List<int> evenNumbers = list.FindAll(x => (x % 2) == 0);
foreach (var num in evenNumbers) {
  Console.Write("{0} ", num);
}
Console.WriteLine();
// 2 4

list.RemoveAll(x => x > 3); // 1 2 3
```

* ```Action<T>``` - void delegate with parameter T
* ```Func<T, TResult>``` - result delegate returning T

```csharp
Action<int> act = (number) => { Console.WrileLine(number); };
act(10); // logs 10

Func<string, int, string> greet = (name, age) => { return "Name: " + name + "Age: " + age; };
Console.WriteLine(greet("Ivaylo", 10));
```

## LINQ and Query Keywords
* LINQ is a set of extensions to .NET Framework
  * Encompasses language-integrated query, set, and transform operations
  * Consistent manner to obtain and manipulate "data" in the broad sense of the term
* Query expressions can be defined directly within the C# programming language
  * Used to interact with numerous data types
  * Converted to expression trees at compile time and evaluated at runtime
* Language Integrated Query (LINQ) query keywords
  * ```from``` – specifies data source and range variable
  * ```where``` – filters source elements
  * ```select``` – specifies the type and shape that the elements in the returned sequence
  * ```group``` – groups query results according to a specified key value
  * ```orderby``` – sorts query results in ascending or descending order
  * Example:
  
```csharp
int[] numbers = { 5, 4, 1, 3, 9, 8, 6, 7, 2, 0 };
var querySmallNums = from num in numbers where num < 5 select num;
foreach (var num in querySmallNums) {
  Console.Write(num.ToString() + " ");
}
// The result is 4 1 3 2 0
```

* Standard Query Operators

```csharp
string[] games = {"Morrowind", "BioShock", "Half Life", "The Darkness", "Daxter", "System Shock 2"};
// Build a query expression using extension methods
// granted to the Array via the Enumerable type
var subset = games.Where(game => game.Length > 6).OrderBy(game => game).Select(game => game);
foreach (var game in subset) {
  Console.WriteLine(game);
}
```

* Operations
  * ```Where()```
    * Searches by given condition
  * ```First()/FirstOrDefault()```
    * Gets the first matched element
  * ```Last()/LastOrDefault()```
    * Gets the last matched element
  * ```Select()/Cast()```
    * Makes projection (conversion) to another type
  * ```OrderBy()/ThenBy()/OrderByDescending()```
    * Orders a collection
  * ```Any()```
    * Checks if any element matches a condition
  * ```All()```
    * Checks if all element matches a condition
  * ```ToArray()/ToList()/AsEnumerable()```
    * Converts the collection type
  * ```Reverse()```
    * Reverses a collection
* Aggregation Methods
  * Average()
    * Calculates the average value of a collection
  * Count()
    * Counts the elements in a collection
  * Max()
    * Determines the maximum value in a collection
  * Sum()
    * Sums the values in a collection

## Syntactic Sugar and Language Features in C&#35;
* Optional Parameters

```csharp
BankAccount(string accountHolder, decimal money = 1000) { … }
// We can use both BankAccount("X") and BankAccount("X", 100)
```

* Using yield

```csharp
IEnumerable<int> EvenNumbers(int from, int to) {
  for (int i = from; i <= to; i++) {
    if (i % 2 == 0) {
      yield return i;
    }
  }
}
foreach (var n in EvenNumbers(51, 60)) {
  Console.WriteLine(n);
}
```

* Constraining Generics

```csharp
class TemplateClass<T> where T : SomeClass
class TemplateClass<T> where T : class // where T : struct
class TemplateClass<T> where T : new()
```