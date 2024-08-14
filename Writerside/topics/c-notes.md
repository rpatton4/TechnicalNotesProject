# C# Notes

{style="note"}

## Logging  

**Syntax:**  

**Notes:**  
- Nuget package: Microsoft.Extensions.Logging
- Nuget package: Microsoft.Extensions.Logging.Console

**Examples:**  

## Nullable  

**Syntax:**  
1. The old way to allow null in value types:  
`Nullable<int> x = null;`

2. The new way:  
`int? x = null;`  

3. Telling the compiler that a non-nullable type is actually going to be set to
 null anyway when it is created, because you know it will be given a value 
 before it is used.  
`private string RequiredValue = null!;`  
`public string RequiredValue { get; set; } = null!;`  
 
**Notes:**
- Everything since .NET 6 has defaulted to enabling "Nullable Reference Types"
  which, contrary to how it sounds, actually makes it so reference types do
  ***not*** support null values.  In order to allow null you must use syntax 1 
  or 2.
- You can configure enabling or disabling Nullable Reference Types in two ways: 
  file-based declaration or a project level flag. See examples.
- See [link](https://wildermuth.com/2023/02/13/nullable-reference-types-in-csharp/) 
  for a detailed explanation.

**Examples:**  
Enabling at the file level using a directive:  
```C#
#nullable enable
object x = null; // Doesn't work, null isn't supported
#nullable disable
```

Enabling in the project config:  
```C#
<!--csproj-->
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>net8.0</TargetFramework>
    <Nullable>enable</Nullable>
  </PropertyGroup>

</Project>
```

## `using`
**Syntax:**  
`using (var) <statement(s)>`  
or  
  
As an attribute in a variable declaration:  
`using <variable declaration>;`
**Notes:**
- The original syntax with a parenthesis followed by a statement/block is a way 
  of telling the compiler to dispose of the variable immediately when the 
  statement has completed, versus waiting until garbage collection.
- The c# 8+ addition of adding this as an attribute in a variable declaration 
  does the same thing except the variable is disposed of when it goes out of
  scope instead of an explicit statement or block.  
 
**Examples:**

## `yield`
**Syntax:**
`yield return <value>`

**Notes:**  
- Used to do lazy iteration over values in an abbreviated way rather than 
  implementing your own iterator.
- returns the next value in a sequence

**Examples:**
```C#
public void Consumer()
{
    foreach(int i in Integers())
    {
        Console.WriteLine(i.ToString());
    }
}

public IEnumerable<int> Integers()
{
    yield return 1;
    yield return 2;
    yield return 4;
    yield return 8;
    yield return 16;
    yield return 16777216;
}
```

This will return '1' on the first pass through the IEnumerable, then '2' on the
second pass etc.

## LINQ
**Syntax:**

**Notes:**
- you must include/use System.Linq
- Lets you use query syntax kinda sorta similar to SQL to select objects from a
  collection
- Gives you access to the Linq extension methods for querying
- MS says to use query syntax instead of method syntax whenever possible, for
  readability


**Examples:**

## `Predicate<T>`  
**Syntax:**

**Notes:**  
`Predicate<T>` is used with delegates and anonymous function to see whether 
something is true of the given T. It is an abbreviation basically, and afaik
just a visual indicator that the delegate will return a bool.  

Basically a predicate delegate is a reference to a function that returns true
or false. Predicates are very useful for filtering a list of values

**Examples:**  
```C#
Predicate<Person> oscarFinder = (Person p) => { return p.Name == "Oscar"; };
Person oscar = people.Find(oscarFinder);
```
As usual, this has been replaced in simple cases with Lambda functions, with
the same example below but using Lambda:
```C#
Person oscar = people.Find(p => p.Name == "Oscar");
```
## Func<T, TResult>
**Syntax:**
`Func<T, TResult>`

**Notes:**
This is used as a placeholder for code which follows a pattern but not specific
functionality.  The quick example is with sorting or selecting elements from a
list; you know the pattern but can't say up front what will be sorted on or the
filter for the select.

Often used in extension methods.

**Examples:**
`var names = people.Select(p => p.Name)` or `var ages = people.Select(p => 
p.Age);` use a Func which would be defined as 
`Func<T, bool>`

## Extension Methods
**Syntax:**

**Notes:**  
The extension method has not special indicator showing it is an extension, but
it does need to be static and part of a static class.  

The first parameter to an extension method is passed in automatically and does 
not need to be passed by the code. So if you have an extension method which 
operates on a List of Employee records, defined as  
`public static List<T> Filter(this List<T> records, Func<T, bool> func)`  
and call it as  
`employeeList.Filter(employee => employee.IsManager == true);`

Related to the above, using `this` keyword in the method definition tells the compiler that the 
parameter is the object upon which this method was invoked.

**Examples:**

## Ternary Operator: ?
**Syntax:** `condition ? consequent : alternative`

**Notes:** Condition must evaluate to true or false. If true, the result of the 
consequent is returned.  If false, the result of the alternative is returned.

**Example:**
```
X > Y ? "X is greater than Y" : "X is less than or equal to Y"
```

## Delegates
**Syntax:** `<access modifier> delegate <return type> <delegate name>(<parameters>)`

**Notes:**
A delegate is a type that represents references to methods with a particular 
parameter list and return type. When you instantiate a delegate, you can 
associate its instance with any method with a compatible signature and return 
type. You can invoke (or call) the method through the delegate instance.

Delegates are used to pass methods as arguments to other methods. Lambda 
expressions mostly superseded these.

**Examples:**  
The delegate declaration:  
`public delegate bool FilterDelegate(Person p)`

Usage example from Stack Overflow:  

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    
    namespace DelegateApp 
    {
    
        public class Person {
          public string Name { get; set; }
          public int Age { get; set; }
        }
    
        class Program 
        {
            //Our delegate
            public delegate bool FilterDelegate(Person p);
    
            static void Main(string[] args) 
            {
    
                //Create 4 Person objects
                Person p1 = new Person() { Name = "John", Age = 41 };
                Person p2 = new Person() { Name = "Jane", Age = 69 };
                Person p3 = new Person() { Name = "Jake", Age = 12 };
                Person p4 = new Person() { Name = "Jessie", Age = 25 };
        
                //Create a list of Person objects and fill it
                List<Person> people = new List<Person>() { p1, p2, p3, p4 };
        
                //Invoke DisplayPeople using appropriate delegate
                DisplayPeople("Children:", people, IsChild);
                DisplayPeople("Adults:", people, IsAdult);
                DisplayPeople("Seniors:", people, IsSenior);
        
                Console.Read();
            }
    
            static void DisplayPeople(string title, List<Person> people, 
                                      FilterDelegate filter) 
            {
                Console.WriteLine(title);
    
                foreach (Person p in people) 
                {
                    if (filter(p)) 
                    {
                        Console.WriteLine("{0}, {1} years old", p.Name, p.Age);
                    }
                }
    
                Console.Write("\n\n");
            }
    
            //==========FILTERS===================
            static bool IsChild(Person p) {
              return p.Age < 18;
            }
        
            static bool IsAdult(Person p) {
              return p.Age >= 18;
            }
        
            static bool IsSenior(Person p) {
              return p.Age >= 65;
            }
        }
    }

## Anonymous Methods
**Syntax:** `delegate (<paramaters>) {<sequence of statements>}`  
or  
`delegate {<sequence of statements>}`

**Notes:**  
This is another usage of `delegate` for the purpose of creating a function 
which is anonymous (has no name) and is typically used to avoid clutter when 
you need a pretty simple function. This way of doing it exists for historical
reasons, basically because it was introduced prior to Lambda Expressions.  

The compiler infers the return type. The input parameters can be omitted
entirely using the 2nd syntax format, which is useful for clarity in some 
cases.

**Examples:**  
```C#
public static int GetIndexOfFirstNonEmptyBin(int[] bins)
{
    return Array.FindIndex(
        bins,
        delegate (int value) { return value > 0; }
    );
}
```

## Lambda Expressions
**Syntax:** 
`<input parameter> => <expression>`  
or  
`<input parameter> => {<sequence of statements>}`  
or  
`(<input parameters>) => <expression>`  
or  
`(_, _) => <expression>`

**Notes:**  
The expression `x => x > y` could be read as "given the value x, return the 
boolean result of x > y"

Lambda expressions are used like anonymous functions, with the difference that 
in Lambda expressions you don't need to specify the type of the value that you 
input thus making it more flexible to use. This is basically just simpler and
more abbreviated; the delegate keyword is unnecessary now because of the =>
symbol, and the compiler infers the input parameter as well as the return 
value. The example below is functionally identical to the one given for 
anonymous methods.  

The syntax for the expressions has more flavors than shown above, depending on 
things like number of parameters. Note the use of parentheses for multiple
params (also used empty when there are no params)

Underscores can be used to discard input parameters when they are forced to be
sent, such as with event handlers.  `(_, _)` indicates that 2 params are sent
but neither are used.

**Examples:**  
Basic example:  
```C#
public static int GetIndexOfFirstNonEmptyBin(int[] bins)
{
    return Array.FindIndex(
        bins,
        value => value > 0
    );
}
```

Using a variable from the containing method:  
```C#
public static Predicate<int> IsGreaterThan(int threshold)
{
    return value => value > threshold;
}

Predicate<int> greaterThanTen = IsGreaterThan(10);
bool result = greaterThanTen(200);
```

## Topic
**Syntax:**

**Notes:**

**Examples:** 