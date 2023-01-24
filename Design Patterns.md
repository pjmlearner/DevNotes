# Design Patterns in C#

## Decorator Pattern

* An object that decorates another object, transparently adding behavior

* Subclassing is one way of implementing a Decorator, but not the best way.

  * Subclass decorates through inheritance, but inheritance limits the decorator
  * Inheritance and behavior overriding are a source for bugs

* Best way: implement through an interface

* *Review:* Copy Constructor

  * ```C#
    public WrappedBook(Book other): base(other)
    {
    }
    ```

    `base(other)` - State is being copied from the decorator object

* Example

  * ```C#
    public override Size Dimensions =>
    	base.Dimensions
    		.Add(new Size(7 * Length.Millimeter, 7 * Length.Millimeter, 7 * Length.Millimeter));
    ```

    `base.Dimensions` - take original behavior

    `.Add(new Size(7 * Length.Millimeter, 7 * Length.Millimeter, 7 * Length.Millimeter));` - transparently apply additional behavior

* 

