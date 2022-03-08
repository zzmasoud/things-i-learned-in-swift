# Protocol + Extension

We can provide default implemention for `protocol` methods, variables so when a `class`/`struct` conforms to that, compiler won't force us to implement those, here's how it works:

```swift
// 1
protocol ProtocolA {
    func foo()
}

// 2
extension ProtocolA {
    func foo() {
        print("ProtocolA: foo")
    }
}

// 3
class ClassA: ProtocolA {
  // no need to implement 'foo()'
} ```

// 4
let obj: ProtocolA = ClassA()
obj.foo() // prints: "ProtocolA: foo"
```

Let's see how custom `foo()` works in `ClassA`:

```swift
// 3
class ClassA: ProtocolA {
    func foo() {
        print("foo")
    }
}

// 4
obj.foo() // prints: "foo"


```
I was curios to know what if I implement a new method in `extention` only, what will happen?

```swift
protocol ProtocolA {
    func foo()
}

extension ProtocolA {
    func foo() {
        print("ProtocolA: foo")
    }
    
    func bar() {
        print("ProtocolA: bar")
    }
}

class ClassA: ProtocolA {
    func foo() {
        print("foo")
    }
    
    func bar() {
        print("bar")
    }
}

let obj1: ProtocolA = ClassA()
obj1.bar() // prints "ProtocolA: bar", what ?!
```
We can see `obj1.bar()` prints "ProtocolA: bar" while I was excepted to see "bar".
Here is the point, if I change `let obj1: ProtocolA = ClassA()` to `let obj1 = ClassA()` it will print "bar".

That's because of **Static vs. Dynamic dispatch**, more key words? **witness table** or **virutal table**.
