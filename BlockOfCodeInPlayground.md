
# Block Of Code In Playground
We love to play in a playground! I hate it when I see compiler errors in a playground. Must of the time it's related to a situation where you want to modify a duplicate thing.

### Helper Function
You can make a new file in the playground sources files and add this helper function:
```
public func block(label: String,
                    code: () -> Void) {
  print("\n", "-------- ", label, " --------")
  code()
}
```

This way you can use duplicate codes for each block and also it prints out in console with clear seperator.


### Reference
https://raywenderlich.com

