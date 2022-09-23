
# Block Of Code In Playground
We love to play in a playground! I hate it when I see compiler errors in a playground. Must of the time it's related to a situation where you want to modify a duplicate thing.

### Helper Function
You can make a new file in the playground sources files and add this helper function:
```swift
public func block(_ label: String,
                    code: () -> Void) {
  print("\n", "-------- ", label, " --------")
  code()
}
```

### How To Use It
In the playground:

```swift
block("first try") {
    var x = 10
    
    func test(_ x: Int) {
        print(x+3)
    }
    
    test(x+5)
}

block("second try") {
    var x = 10
    
    func test(_ x: Int) {
        print(x-3)
    }
    
    test(x+5)
}
```
And the output in the console will be:
```

 --------  first try  --------
18

 --------  second try  --------
12
```

This way you can use duplicate codes for each block and also it prints out in console with clear seperator.


### Reference
https://raywenderlich.com

