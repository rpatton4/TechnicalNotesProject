# C# Notes

{style="note"}

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