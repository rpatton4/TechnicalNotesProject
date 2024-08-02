# C# Notes

{style="note"}

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

## Lambda Expressions
**Syntax:** 
`<input parameters> => <expression>`  
or  
`<input parameters> => {<sequence of statements>}`

**Notes:**
Lambda expressions are used like anonymous functions, with the difference that 
in Lambda expressions you don't need to specify the type of the value that you 
input thus making it more flexible to use.

**Examples:**

## Topic
**Syntax:**

**Notes:**

**Examples:** 