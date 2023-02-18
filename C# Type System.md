# C# Type System

## 1. Built-in Data Types

### C# is a strongly typed language

* Every variable has a type

### Predefined (Primitive) Data Types

* bool (default value is false)
* int (default value is 0)
* float
* double
* decimal
* char
* byte (0 - 255 bytes)
* short
* object
* string

### Value and Reference Types

#### Value Data Types

* Predefined
  * Integer, Boolean
* User Defined
  * Enumeration, Struct

#### Reference Data Types

* Predefined
  * String
  * Array
* User Defined
  * Class
  * Interface

![image-20210826141535567](C:\Users\PJMLEARNER\AppData\Roaming\Typora\typora-user-images\image-20210826141535567.png)

### Operators

* special operators:
  * ++
    * increments by 1 (e.g. a++)
  * --
    * decrements by 1 (e.g. b--)

* equality operators:
  * ==
    * compares equal
  * !=
    * compares not equal
* assignment operators
  * +=
    * adds and assigns (e.g. a+  =>  a=a+3)
  * -=
    * subtracts and assigns (e.g. a-=3  =>  a=a-3)

### Date Types

* creating a specific date variable requires to instantiate a date using the DateTime constructor

  ```C#
  DateTime someDateTime = new DateTime(2021, 03, 28);
  ```

### Data Type Conversion

3 ways:

1. Implicit conversion

   ```c#
   int a = 123456789;
   long l = a;
   ```

2. Casting (Explicit Convesion)

   ```c#
   double d = 123456789.0
   int a = (int)d
   ```

3. Helpers

   ```C#
   double d = 123456.0;
   int a = (int)Convert.ChangeType(d.typeof(int))
   ```

   

## 2. Strings

* contains text, stored as collection of char objects

* strings are stored on the HEAP and are reference type.

* default value is NULL

* Properties of string can be called

  ```c#
  int l = myString.Length;
  ```

* Methods of string can be called

  ```c#
  string upper = myString.ToUpper();
  ```

### Concatenation

* links strings together to form a single string

* C# has different ways to handle this

  * "+" symbol

    ```c#
    string employeeName = "Bethany";
    int age = 34;
    string greetingText = "Hello" + employeeName + ", you are " + age " years";
    ```

  * "$" special character - String Interpolation

    ```c#
    string employeeName = "Bethany";
    int age = 34;
    string greetingText = $"Hello {employeeName}, you are {age} years";
    ```

### Escape Characters

* always start with a \

  ```C#
  Console.Writeline("Here are the employee details:\nBethany\tSmith");
  ```

  Returns

  ```
  Here are the employee details:
  Bethany  Smith
  ```

* a string with many escape characters (such as a Path name, which you would want to keep the backslashes, can be formatted with the ==@== character

  ```C#
  string verbatimFilePath = @"C:\Documents\readme.txt"
  ```

### Immutability of Strings

* Strings are Reference Types

  * point to actual string in memory
  * created in the Heap

* Once created it cannot be changed

  * a replace operation on a string doesn't actually replace the existing string, but creates a new one in memory
    * this could cause memory issues if, for example you have a loop that iterates countless times over a string and it just writes new strings to memory.  An answer to this is using StringBuilder

* StringBuilder Class

  * the StringBuilder can assist in creating a string without using up a lot of memory

    ```C#
    string firstName = "Bethany";
    string lastName = "Smith";
    
    StringBuilder builder = new StringBuilder();
    builder.Append("Last Name: ");
    builder.Append(lastName:);
    builder.Append("First Name: ");
    builder.Append(firstName:);
    string result = builder.ToString();
    ```

### Parsing

```C#
string enteredText = "true";
if (bool.TryParse(enteredText, out bool b))
{
	Console.WriteLine($"The value is {b}");
}
```



## 3. Methods



```C#
<access modifier> <return type> Method_Name (Parameters)
{
	//method statements
}
```

