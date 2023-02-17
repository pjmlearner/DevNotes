# C#

## **1. Intro C# and .NET**

------

### .Net - runtime and framework library

* ==runtime== - space to be able to run your code
* ==framework library== - library of already created-code by other developers made available for use

* .Net Core - cross platform

* .Net Framework - windows-only

* ![image-20200810165749468](C:\Users\PJMLEARNER\AppData\Roaming\Typora\typora-user-images\image-20200810165749468.png)

  

* a .NET Project is a collection of source code files that is put together for an application or library

### Creating First Project

```terminal
CLS
```

​	*command prompt command that clears all contents in the command prompt*

* ==console/terminal/shell== - a command-line environment

```terminal
dotnet new console
```

*command prompt command to create new dotnet console application*

* this creates two things:
  * [projectname].csproj
  * Program.cs

### Editing C# and Visual Studio Code

no notes

### Running and Building your project

#### dotnet run

* What happens when you do a `dotnet run`?
  * `dotnet restore`
    * looks through your project to see if there are external dependencies such as using packages from NuGet
  * `dotnet build`
    * compiles the source code
    * ![image-20200818164621460](C:\Users\PJMLEARNER\AppData\Roaming\Typora\typora-user-images\image-20200818164621460.png)
    * for .net core think of DLL is an assembly, or output from the dotnet build.
    * ![image-20200818164742991](C:\Users\PJMLEARNER\AppData\Roaming\Typora\typora-user-images\image-20200818164742991.png)
    * The path for which the DLL is placed:
      * \bin - stands for binary
      * \debug - because this is a debug build of the application



#### NuGet

* a package system of available code made by other developers (including Microsoft) that are available for use in your project.  These packages are separate from the pre-packaged dotnet library

#### Method

* a ==method== is a procedure/function in C#

##### Main Method (Entry Point)

```c#
        static void Main(string[] args)
        {
            Console.WriteLine("Hello Preston!");
        }
```

* the Main method is the entry point for the console.
* the Main method is looked for by the .Net runtime as the entry point to start the application

##### Method Anatomy

```C#
        static void Main(string[] args)
        {
            Console.WriteLine("Hello Preston!");
        }
```

`Main` is the name of the method

`string[]` is the type.  In this case it is a string array

`args` is/are the parameter/parameters



We can revise the code to take a parameter such as:

```c#
        static void Main(string[] args)
        {
            Console.WriteLine("Hello " + args[0] + "!");
        }
```

the `"Hello " + args[0] + "!"` uses ==string concatenation== to produce a result such as `Hello Jim`



We can further revise the code using ==string interpolation==, using <u>an expression within a string</u> to produce a value

```c#
        static void Main(string[] args)
        {
            Console.WriteLine($"Hello, {args[0]}!");
        }
```

`$"Hello, {args[0]} ! "`

`$` - starts string interpolation

`{args[0]}` - uses curly brackets for the expression

#### ==Start from Scratch==

When creating a new C# application in VS Code

1. Create a folder for your project
2. Run commands
   1. `dotnet new console`
   2. `dotnet restore`
   3. `dotnet run`
3. To Debug, need to add launch.json file
   1. try to debug > launch through .Net Core
   2. launch.json file will be created
   3. ensure to have the "program" path listed and replace placeholders

### Debugging C# Application

![image-20200819122026620](C:\Users\PJMLEARNER\AppData\Roaming\Typora\typora-user-images\image-20200819122026620.png)

.vscode/launch.json contains "args" which you can input parameters to supply and debug your application





## **2. C# Syntax**

------

### Adding Numbers and Creating Arrays

#### Variables

```C#
    class Program
    {
        static void Main(string[] args)
        {
            double x, y;
            x = 10.11;
            y = 9.89;

            Console.WriteLine(x + y);
        }
    }
```

`double` is the data type, which supports decimal values and `x` and `y` are the variable names



Another way of datatypes is through ==implicit typing==, which means C# will automatically set the datatype based on what it thinks the variable is

```C#
    class Program
    {
        static void Main(string[] args)
        {
            var x = 10.11;
            var y = 9.89;

            Console.WriteLine(x + y);
        }
    }
```

`var` uses implicit typing



#### Arrays

to be able to use an array, it must be declared AND created/instantiated

an example of just declaring an array (Which will fail because it hasn't been created)

```c#
    class Program
    {
        static void Main(string[] args)
        {
            double[] numbers;
            numbers[0] = 2.1;
        }
    }
```

We declared the array through `double[] numbers;` but it hasn't been created.  To create the array, it can be done as so:

```C#
    class Program
    {
        static void Main(string[] args)
        {
            double[] numbers = new double[6];
            numbers[0] = 2.1;
        }
    }
```

We created the array by using `new double[6]`.  The `6` within the brackets designate how many items the array can hold.  We can further make the code simpler by using implicit typing:

```C#
    class Program
    {
        static void Main(string[] args)
        {
            var numbers = new double[6];
            numbers[0] = 2.1;
        }
    }
```



Example of adding Array items:

```C#
    class Program
    {
        static void Main(string[] args)
        {
            var numbers = new double[3];
            numbers[0] = 2.1;
            numbers[1] = 4.33;
            numbers[2] = 8.9;
            var result = numbers[0];

            result = result + numbers[1];
            result = result + numbers[2];
            System.Console.WriteLine(result);  //15.33
        }
    }
```



##### Looping through Arrays

We can simplify the above summation of the array items using a loop

```C#
    class Program
    {
        static void Main(string[] args)
        {
            var numbers = new[] {2.1, 4.33, 8.9};
            var result = 0.0;

            foreach (var number_item in numbers)
            {
                result += number_item;  
            }
            System.Console.WriteLine(result);  //15.33
        }
    }
```

`var numbers = new[] {2.1, 4.33, 8.9};` here we combined the variable declarations for the array by using the curly brackets and using `new[]` to create the array without specifying the amount of items in it, but implicitly doing so by the amount of items between the curly brackets (in this case 3)

`foreach (var number_item in numbers)` ==foreach== is the keyword to use a loop which states for reach item in the `numbers` array, we assign the variable `number_item` to

`result += number_item` we then loop through each item (`number_item`) and store it in the `result` variable.  The `+=` is a shorthand way of adding the last `result` to the next item in the array.



#### Lists

Lists are similar to arrays, whereby it can store a collection of items, but it differs in that the collection of items is dynamic.  Arrays collection of items is fixed - must specify a number of items that can be held.  With List you can keep adding or removing items.

```c#
using System;
using System.Collections.Generic;

namespace GradeBook
{
    class Program
    {
        static void Main(string[] args)
        {
            var result = 0.0;
            List<double> grades = new List<double>() {2.1, 4.33, 8.9};
            grades.Add(4.5);
            var total_grades = grades.Count;

            foreach (var number_item in grades)
            {
                result += number_item;
            }

            result /= total_grades;
            System.Console.WriteLine($"The average grade is {result}.");
        }
    }
}
```

`using System.Collections.Generic;` needs to be added to be able to use `List` class/data structure

`List<double> grades = new List<double>() {2.1, 4.33, 8.9};`

​	`List<double> grades` declares the list variable `grades` which is a `List` class of type `double`

​	`new List<double>()` creates the `List` class of type `double` by keyword `new` and `()`

​	`{2.1, 4.33, 8.9}` inserts these values into the list

`grades.Add(4.5)` adds `4.5` to the list `grades`

`grades.Count` gathers the # of items in the list



## **3. Classes and Objects**

------

### Creating a Class

* a class is just a type (type being something similar to other types like an array). it is the blueprint from which objects can be created.
* abstraction - showing/making available essential attributes and hiding unnecessary information
  * an example of this would be to take a portion of code that does a specific calculation, and break it off into its own method which is named and clearly defined on what that portion of the code does. This is also known as encapsulation.
* ==Abstraction is focused mainly on what should be done while Encapsulation is focused on how it should be done.==
  * abstraction - **designing** (*what should be done*) a class and making essential methods available to hide unnecessary information
  * encapsulation - **implementing** (*how should be done*) the code to be enclosed in a clearly defined named-method to hide the code complexity and know what it's doing
* every class should be within a namespace.  If it's not in a namespace it's in the Global namespace which can cause conflict on already defined/existing classes in the Global namespace
* 

### Adding State and Behavior

* conventional to only allow 1 class per file
* when creating a class you should ask yourself:
  * what is/are the ==behavior/behaviors (methods that will interact with state)== of this particular class?
  * what is the ==state (data that it holds)== that is going to be stored inside the instances of this class?

### Defining a Field

* cannot use implicit typing (var) to define a field. Must be explicit such as `private List<double> grades;`

### Adding a Constructor

```c#
using System;
using System.Collections.Generic;

namespace GradeBook
{
    class Book
    {
        public Book()  //explicit constructor
        {
            grades = new List<double>();
        }
        
        private List<double> grades;  //field

        public void AddGrade(double grade)  //method that uses field
        {
            grades.Add(grade);
        }

        public void PrintGrades() //method that displays field's state
        {
            Console.WriteLine("Your final grades are:");
            foreach (var final_grades in grades)
            {
                Console.WriteLine(final_grades);
            }

        }
    }
}
```

* Whenever you receive a NullReferenceException debug error, it is because you are using a field or variable that hasn't been initialized

* In the above code, the method AddGrade is calling for the grades field/property of the Book class.  If we don't explicitly construct the object, then the grades field would contain a null value.  We need to have an explicit constructor in the class to initialize itself and make any fields/methods within the constructor available for use within the classes own methods. In other words:

  * To be able to use the grades field `        private List<double> grades;  //field` ...       

  * ... in the AddGrade method

            public void AddGrade(double grade)  //method that uses field
            {
                grades.Add(grade);
            }`

  * we need to construct the object with that field

    ```
        public Book()  //explicit constructor
        {
            grades = new List<double>();
        }
    ```

* A constructor should also have the same name as the class in this case "Book"

#### Requiring Constructor Parameters

* keyword ==`public`== is an access modifier it allows outside code access

  * an access modifier is that which allows access to a method/member in a class

* keyword ==`private`== is an access modifier it does NOT allow outside code access, only can be accessed within the class

* ```C#
      class Book
      {
          public Book(string name)  //explicit constructor with req'd parameters
          {
              this.name = name;  
              grades = new List<double>();
          }
  
          private string name;  //field
  
      }
  ```

  * `public Book(string name)` forces a string parameter to be given when creating a Book object

##### this. 

`this.name = name;`

* the `this` keyword is used to differentiate between the parameter titled "name" to the class field also titled "name"
* `this` will reference the parameter/variable as defined within its constructor/method
* where as just `name` references the field property of the class and not the value of the constructor parameter

### ==Static Members==

* the `static` keyword makes it so that the members of a class (the method or fields) cannot be instantiated
  * e.g. if a field of a class was static, when you instantiate an object of that class, that static field cannot be called as it only lives within the class
* `static` members can only be accessed through the class itself.
* more often than not you would not use the static keyword as it negates the benefits of Object Orientation
* Helpful: https://www.codeproject.com/Articles/15269/Static-Keyword-Demystified





## **4. Testing**

------

`dotnet new xunit`

* xunit is not apart of the dotnet core library, so we will need additional libraries
* xunit is a NuGet package

==side note== - you can go to the NuGet website and search for packages and find the CLI command to run to add a NuGet package to your project.  In the example below, this would be another way to add the xunit package to our project instead of using `dotnet new xunit`

![image-20200908112914541](C:\Users\PJMLEARNER\AppData\Roaming\Typora\typora-user-images\image-20200908112914541.png)

```C#
using System;
using Xunit;

namespace GradeBook.Tests
{
    public class UnitTest1
    {
        [Fact]
        public void Test1()
        {
            //arrange
            var x = 5;
            var y = 2;
            var expected = 7;

            //act
            var actual = x + y;

            //assert
            Assert.Equal(expected, actual);
        }
    }
}
```



### Fact

* `Fact` is an attribute, which acts like a tag to let the compiler know that the following method is used to actually test against.  This is needed because a test Unit, can have methods within itself solely as method that can be used and called upon by code, but don't want the compiler to run a test against

### AAA - categorizing a Test method

A test method is usually broken down into three categories:

* arrange - declarations

* act - actual computations and manipulation

* assert - checking assertions are correct

  

### `dotnet test`

`dotnet test` is the CLI command to run your tests. The compiler will look for the `Fact` attribute and run the methods it is linked to



### Project Reference

to be able to test against another project's class we need to add a reference to that project into our test project.  In Visual Studio, this can be easily done by right-clicking "Dependencies" within the project  and then selecting "Adding Reference"



It can also be done using CLI:

`dotnet add reference [path of projectname.csproj]`

Example:

`dotnet add reference ..\..\src\GradeBook\GradeBook.csproj`



The reference will then be added to the .csproj file

```C#
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>netcoreapp3.1</TargetFramework>

    <IsPackable>false</IsPackable>
  </PropertyGroup>

  <ItemGroup>
    <PackageReference Include="Microsoft.NET.Test.Sdk" Version="16.2.0" />
    <PackageReference Include="xunit" Version="2.4.0" />
    <PackageReference Include="xunit.runner.visualstudio" Version="2.4.0" />
    <PackageReference Include="coverlet.collector" Version="1.0.1" />
  </ItemGroup>

  <ItemGroup>
    <ProjectReference Include="..\..\src\GradeBook\GradeBook.csproj" />  //added reference
  </ItemGroup>

</Project>
```



When constructing a class from another project, ensure that the latter project's class has the `Public` keyword.  Otherwise it will default to `Internal` which will limit its scope of use to its own project.

Example:

Src Project

![image-20200908145738203](C:\Users\PJMLEARNER\AppData\Roaming\Typora\typora-user-images\image-20200908145738203.png)



Test Project

![image-20200908145645001](C:\Users\PJMLEARNER\AppData\Roaming\Typora\typora-user-images\image-20200908145645001.png)	



### Return Method

a return method is when you replace the `void` keyword with a data type.  In our case we want to return an object type (statistics that returns multiple fields for average, low, and high numbers)

Example:

```C#
        public Statistics GetStatistics()  //replace void with Statistics
        {
            var result = new Statistics();
            result.avgGrade = 0.0;
            result.highGrade = double.MinValue;
            result.lowGrade = double.MaxValue;

            foreach (var grade in grades)
            {
                if (grade > result.highGrade)
                {
                   result.highGrade = grade;
                }
                if (grade < result.lowGrade)
                {
                    result.lowGrade = grade;
                }                

                result.avgGrade += grade;
            }
            result.avgGrade /= grades.Count;
            result.avgGrade =  Math.Round(result.avgGrade, 2);
            return result;
        }
```

Here we want to return the Statistics class, so we construct the class and store it in the `result` variable. the `result` object now has access to the properties of the class (`avgGrade`,`highGrade`,`lowGrade`).

The Statistics class is build as such:

```C#
namespace GradeBook
{
    public class Statistics
    {
        public double avgGrade;
        public double lowGrade;
        public double highGrade;
    }
}
```



Our unit test then looks like:

```C#
using System;
using Xunit;

namespace GradeBook.Tests
{
    public class BookTests
    {
        [Fact]
        public void Test1()
        {
            //arrange
            var book = new Book("");  ///construct a new Book as book object
            ///we now have access to the methods of Book, so we add grades to it using AddGrade method
            book.AddGrade(89.1);
            book.AddGrade(90.5);
            book.AddGrade(77.3);

            //act
            ///we create an object that uses the book.GetStatistics method which calls the Statistics method to store to the object
            var stats = book.GetStatistics();

            //assert
            ///we now have access to fields of the Statics class
            Assert.Equal(85.63, stats.avgGrade);
            Assert.Equal(77.3, stats.lowGrade);
            Assert.Equal(90.5, stats.highGrade);
        }
    }
}
```





## 5. Working with Reference and Value Types

------

### Difference between Reference and Value Types

* A Reference Type points to a location in memory where the data is stored
* A Value Type is stored directly into the variable
* ![image-20200909141927986](C:\Users\PJMLEARNER\AppData\Roaming\Typora\typora-user-images\image-20200909141927986.png)

### Create a Solution file

* A solution file is a file that keeps projects together
* Go to the parent folder and:
  * `dotnet new sln` - creates the solution file
  * `dotnet sln add [location of .csproj file]`
  * `dotnet build` will build the sln file (same command can be used on projects

### Testing Object References

* its conventional that whenever you make a property Public, then the name of the property is capitalized

![image-20200914144340983](C:\Users\PJMLEARNER\AppData\Roaming\Typora\typora-user-images\image-20200914144340983.png)



* name your test methods very specific to what is being tested

![image-20200914144609606](C:\Users\PJMLEARNER\AppData\Roaming\Typora\typora-user-images\image-20200914144609606.png)

### Referencing Different and Same Objects

```C#
        [Fact]
        public void GetBookReturnsDifferentObjects()
        {
        //Arrange
            var book1 = GetBook("Book 1");
            var book2 = GetBook("Book 2");
            var book3 = GetBook("Book 3");

        //Assert
            Assert.Equal("Book 1", book1.Name);
            Assert.Equal("Book 2", book2.Name);
            Assert.Equal("Book 3", book3.Name);            
        }

        [Fact]
        public void MultipleVarsCanRefSameObject()
        {
        //Arrange
            var book1 = GetBook("Book 1");
            var book2 = book1;

        //Assert
            Assert.Same(book1,book2);
            Assert.True(Object.ReferenceEquals(book1,book2)); //does the same as Assert.Same, just another way of using 																		ReferenceEquals method of the base Object class         
        }

        Book GetBook(string name)
        {
            return new Book(name);
        }
```



### Returning Object References

* in C#, when passing parameter to a method, you are <u>always passing a parameter by value</u>

#### Pass By Value

* ==pass by value== - taking a value of a variable and **copying** and placing into a parameter

  ```C#
          [Fact]
          public void CSharpIsPassByValue()
          {
          //Arrange
              var book1 = GetBook("Book 1");
              GetBookSetName(book1, "New Name");
  
          //Assert
              Assert.Equal("Book 1", book1.Name);           
          }
  
          Book GetBook(string name)
          {
              return new Book(name);
          }
  
          private void GetBookSetName(Book book, string name)
          {
              book = new Book(name);
              book.Name = name;
          } 
  ```

![image-20200914161228635](C:\Users\PJMLEARNER\AppData\Roaming\Typora\typora-user-images\image-20200914161228635.png)

#### Pass By Reference

* ==pass by reference== - what is received is **not a copy** of the value, but a reference to the memory location where that reference is stored
  * uses the "ref" keyword

```C#
        [Fact]
        public void CSharpCanPassByRef()
        {
        //Arrange
            var book1 = GetBook("Book 1");
            GetRefBookSetName(ref book1, "New Name");

        //Assert
            Assert.Equal("New Name", book1.Name);           
        }

        Book GetBook(string name)
        {
            return new Book(name);
        }

        private void GetRefBookSetName(ref Book book, string name)
        {
            book = new Book(name);
        }    
```

### Garbarage Collector

* You don't need to tell runtime to destroy/delete an object.  The .NET runtime knows when there is an object in memory when there are no pointers to the object, it knows to delete it.





## 5. Controlling the Flow of Execution

------

### For Loop

```C#
for ([declaration]; [condition]; [execution after end of each loop];)
{
	//block of code
}
```

example:

```c#
for (var index = 0; index < grades.Count; index +=1)
{
     result.lowGrade = Math.Min(grades[index], result.lowGrade);              
     result.highGrade = Math.Min(grades[index], result.lowGrade);  
     result.avgGrade += grades[index];
}
```

### Throwing Exceptions

Throwing exceptions is creating error conditions.  This is used to notify users an error has occurred and they have gone outside of the parameters/scope of the program.

* One built in exception is the `ArgumentException` - a Thrown Exception when you believe a parameter is being passed that is invalid

  ```C#
          public void AddGrade(double grade)
          {
              if (grade >= 0 && grade <= 100)
              {
                  grades.Add(grade);
              }
              else
              {
                  throw new ArgumentException($"Invalid {nameof(grade)}");
              }
          }
  ```

  

* ==`nameof()`== expression produces the name of a variable, type, or member as the string constant

The program will crash if the Exception is thrown.  To let the program to continue, we need to Catch/Handle the Exception:

### Catching Exceptions

n/a





## 6. Building Types

------

### Method Overloading

Method Overloading is a feature in which multiple methods can use the same name.

- C# is able to identify different methods using the same name, by its *method signature*. 
- Method signature - a method name and its parameter datatypes, and number of parameters
- Benfits:
  - Overloaded methods give programmers the **flexibility** to call a similar method for different types of data.
  - Overloading is also used on constructors to create new objects given different amounts of data.

```c#
        public void AddGrade(char letter)
        {
            switch(letter)
            {
                case 'A':
                AddGrade(90);
                break;

                case 'B':
                AddGrade(80);
                break;

                case 'C':
                AddGrade(70);
                break;

                default:
                AddGrade(0);
                break;                                                
            }
        }

        public void AddGrade(double grade)  //method that uses field
        {
            if (grade >= 0 && grade <= 100)
            {
                grades.Add(grade);
            }
            else
            {
                throw new ArgumentException($"Invalid {nameof(grade)}");
            }
        }
```

Above we have two methods with the same name `AddGrade` but different signatures: First method takes a Char datatype parameter, Second Method takes a Double datatype parameter.

### Properties

Similar to fields, but also allows some other features.

* you can validate the data/state for a property (e.g. a Name field can accept a Null value or empty string, but can't validate against it.  A property CAN validate to ensure there is some value)
* encapsulation - controls access to a private field using getters and setters

Defining a property - Long Form:

```c#
        public string Name
        {
            get
            {
                return name;
            }
            set
            {
                if(!string.IsNullOrEmpty(value))
                {
                    name = value;  //value is an implicit variable for set
                }
            }
        }
        private string name;
```

* Here we still have the private ==field== "name," and the public ==property== "Name."   This together is a long form property.   The public property allows to get and set a private field.
* the "value" variable in the set, is an implicit variable, which can always just be called without declaration

Defining a property - Short Form:

```C#
        public string Name
        {
            get; set;
        }
```

* uses auto-property which reads from the property using get, and writes to the property using set.

* similar to field `public string Name` 

  * biggest difference is you can use access-modifiers with the property such as:

  * ```C#
           public string Name
            {
                get;
                private set;
            }
    ```

    * `private set` makes it so that you can't write to the property Name outside of the class which the property is defined from.
      * The Name needs to be set from within the class (e.g. Name can be written through a constructor).
      * Cannot be written through specific assignment like `book.Name ='Book1'.`
      * A use case for this would be to set a name for a Book upon creation, and not allow the name to be changed thereafter.

### Read Only

Read only is a field that can **ONLY** be initialized, changed, written-to in a **constructor**.

`readonly string category = "Science";`

```C#
        public Book(string name)  //explicit constructor with req'd parameters
        {
            category = "";
            AddGradeBook(name);
            grades = new List<double>();
        }
```

* as seen in the above constructor, the readonly field category can be assigned (in this case it's an empty string).  If we tried to assign a value to category outside the constructor such as in a method of the object, an error would occur

### Const

keeps a value constant - cannot be changed

`    const string CATEGORY = "Science";` 

* field CATEGORY, is a constant and can never be changed.  If you try to assign a value to CATEGORY an error will occur
* it is common practice to uppercase the entire field name when it is a constant, to determine that the field is a constant value

if you want to make the constant field readable just add public to it

`public const string CATEGORY = "Science";`



### Events and Delegates



Delegate - allows to define a variable to point to and invoke a method ( a method with a specific shape and structure)

```C#
        public void WriteLogDelegateCanPointToMethod()
        {
            WriteLogDelegate log;

            log = ReturnMessage;  //point log to method

            var result = log("Hello!");
            Assert.Equal("Hello!",result);

        }

        string ReturnMessage(string message)  //method datatype should match delegate datatype(s)
        {
            return message;
        } 
```



## 7. Object-Oriented Programming with C#

------

### Pillars of OOP

1. Encapsulation
   1. Hide details of our code
2. Inheritance
   1. Ability to reuse code against similar classes
3. Polymorphism
   1. Have objects of the same type that can behave differently

### Inheritance

#### Deriving from a base class

* a ==base class=='s members can be inherited from by a ==derived class== (a class that is derived from a base class)

* the root base class - the class which all other classes are derived from is System.Object.

* Example - Have the Book Name be derived from a base class called NamedObject. 

  * This way we can use NamedObject for many other derived classes that will have a name (employees, buildings, etc.) 
  * We can drop the name property from the Book class, as we'll be deriving the name property we inherit from the NamedObject class

  ```C#
      public class NamedObject
      {
          public string Name  //name property
          {
              get; set;
          }
      }
      public class Book : NamedObject  //inherit from the baseclass Named Object
      {
          public Book(string name)
          {
              AddGradeBook(name);
              grades = new List<double>();
          }
      }
  ```

  

#### Chaining Constructors

* When defining a constructor for a base class, any derived class needs to supply how to construct that base class when it is initialized

* Example

  ```C#
      public class NamedObject
      {
          public NamedObject(string name)  //base class constructor with "name" required
          {
              Name = name;
          }
  
          public string Name
          {
              get; set;
          }
      }
      public class Book : NamedObject  //derived class from base class
      {
          public Book(string name) : base(name)  //Book constructor telling how to construct the base class by passing the name
          {
              AddGradeBook(name);
              grades = new List<double>();
          }
      }
  ```

  

  * `base` keyword is used to reference the base class (accessing the constructor method of the base class). 

### Polymorphism

#### Abstract Class

* A class cannot inherit from multiple base classes, but it can inherit from multiple interfaces

```C#
    public class NamedObject
    {
        public NamedObject(string name)
        {
            Name = name;
        }

        public string Name
        {
            get; set;
        }
    }

    public abstract class Book : NamedObject
    {
        protected Book(string name) : base(name)
        {
        }

        //Polymorphism classes derived from this class will have different implementations of the same named method
        public abstract void AddGrade(double grade);  //keyword abstract used for abstract method
    }

    public class InMemoryBook : Book
    {
        public InMemoryBook(string name) : base(name)
        {
            AddGradeBook(name);
            grades = new List<double>();
        }
        public List<double> grades;

        public override void AddGrade(double grade)
        {
            if (grade >= 0 && grade <= 100)
            {
                grades.Add(grade);
            }
            else
            {
                throw new ArgumentException($"Invalid {nameof(grade)}");
            }
        }
	}        
```

* `public abstract class Book : NamedObject` 
  * is an abstract class
  * it's derived from the NamedObject Class so we need to include the constructor `protected Book(string name) : base(name)`
  * has an ==abstract method== `public abstract void AddGrade(double grade);` 
    * the <u>abstract method enforces all derived classes to have this method</u>, but it can be implemented in its own way
    * a derived class that has includes the abstract method needs to use the `override` keyword to basically say it's overriding the base class method with its own implementation

#### Interface

* Only contains declarations of methods and properties, but not the implementations. 
* Child classes that inherit from the interface provide their own definitions
* Like an Abstract class that has abstract methods and properties
* Does NOT have constructors or fields

```C#
    public interface IBook
    {
        //keyword "public" not needed as the nature of interface makes all members available
        void AddGrade(double grade);
        Statistics GetStatistics();
        string Name{get;}
    }

    public abstract class Book : NamedObject, IBook
    {
        protected Book(string name) : base(name)
        {
        }

        public abstract void AddGrade(double grade);

        public virtual Statistics GetStatistics()
        {
            throw new NotImplementedException();
        }
    }

    public class InMemoryBook : Book
    {
        public InMemoryBook(string name) : base(name)
        {
            AddGradeBook(name);
            grades = new List<double>();
        }
        public List<double> grades;

        public override void AddGrade(double grade)  //method that uses field
        {
            if (grade >= 0 && grade <= 100)
            {
                grades.Add(grade);
            }
            else
            {
                throw new ArgumentException($"Invalid {nameof(grade)}");
            }
        }

        public override Statistics GetStatistics()
        {
            var result = new Statistics();
            result.avgGrade = 0.0;
            result.highGrade = double.MinValue;
            result.lowGrade = double.MaxValue;
            result.countGrade = 0;

            for (var index = 0; index < grades.Count; index +=1)
            {
                result.lowGrade = Math.Min(grades[index], result.lowGrade);              
                result.highGrade = Math.Max(grades[index], result.highGrade);  
                result.avgGrade += grades[index];
            }
            result.countGrade = grades.Count;
            result.avgGrade /= result.countGrade;
            result.avgGrade = Math.Round(result.avgGrade, 2);
            return result;
        }

```



```C#
    public interface IBook
    {
        //keyword "public" not needed as the nature of interface makes all members available
        void AddGrade(double grade);
        Statistics GetStatistics();
        string Name{get;}
    }

    public abstract class Book : NamedObject, IBook
    {
        protected Book(string name) : base(name)
        {
        }

        public abstract void AddGrade(double grade);

        public virtual Statistics GetStatistics()
        {
            throw new NotImplementedException();
        }
    }
```

* the abstract <u>class (Book) that inherits from an interface (IBook), needs to include ALL members of the interface</u> (AddGrade, GetStatistics, Name)

* the `virtual` keyword makes it so that its following method's implementation can be overwritten by a derived class

  ```c#
      public abstract class Book : NamedObject, IBook
      {
          protected Book(string name) : base(name)
          {
          }
  
          public abstract void AddGrade(double grade);
  
          public virtual Statistics GetStatistics()
          {
              throw new NotImplementedException();
          }
      }
  
      public class InMemoryBook : Book
      {
          public override Statistics GetStatistics()
          {
              var result = new Statistics();
              result.avgGrade = 0.0;
              result.highGrade = double.MinValue;
              result.lowGrade = double.MaxValue;
              result.countGrade = 0;
  
              for (var index = 0; index < grades.Count; index +=1)
              {
                  result.lowGrade = Math.Min(grades[index], result.lowGrade);              
                  result.highGrade = Math.Max(grades[index], result.highGrade);  
                  result.avgGrade += grades[index];
              }
              result.countGrade = grades.Count;
              result.avgGrade /= result.countGrade;
              result.avgGrade = Math.Round(result.avgGrade, 2);
              return result;
          }
      }        
  ```

  

* InMemoryBook's GetStatistics method overrides its base class's (Book) virtual method GetStatistics implementation. The base class (Book) itself inherits the GetStatistics method from the interface IBook

#### Writing Grades to a File

##### File Class

* This class lives in the System.IO namespace and deals open, read, write to files.

```C#
    public class DiskBook : Book
    {
        public DiskBook(string name) : base(name)
        {
        }
        public override void AddGrade(double grade)
        {
            using(var writer = File.AppendText($"{Name}.txt"))
            {
                writer.WriteLine(grade);
            }
        }
    }
```

* ==`using` keyword, when used within a method, it will tell the Garbage Collector to "clean up" the object being used after it's being used.   It will effectively dispose any resources that still open after the object is done being used==
* 