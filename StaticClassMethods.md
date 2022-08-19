# Static Class Methods

### First approach
I was working on a piece of code that needed a handy tool, a handy `class` for just calling a method, something like this:
``` Swift
class Foo {

    private func a() { }
    
    private func b() { }

    func bar() {
      a()
      b()
    }
}
```
But
1. I didn't want to allow subclassing:
``` Swift
class Boo: Foo { 
  override bar() { 
    // do something else
  }
}
```
2. There was no point to instantiate it `(#2)` to call a method:

``` Swift
#2
let object = Foo().bar()
```

to solve the 1st issue, made `init()` private:
``` Swift
class Foo {
  private init() {}
  // ....
  // ....
}
```

and to fix the 2nd issue, changed the methods to `static` methods.

``` Swift
class Foo {
    private init() {}
    
    private static func a() { }
    
    private static func b() { }

    static func bar() {
      a()
      b()
    }
}
```
 
And then it was OK to continue coding.
But I've been thinking of another approach to achieve the same functionality today and then I've just noticed `enum`s!

### Second approach
Defining an `enum` with no cases.

``` Swift
enum Foo {
    
    private static func a() { }
    
    private static func b() { }

    static func bar() {
      a()
      b()
    }
}
```

In both approaches it's possible to call `Foo.bar()` and not possible to call `Foo()`.
