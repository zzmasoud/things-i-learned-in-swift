# RandomNumberGenerator
It's a `protocol`, there's required `next()` method for conforming to it.
There's default implemetion that all types use it, called `SystemRandomNumberGenerator`. they are all elequivent:

```swift
// 1
let randomBool = Bool.random()
// 2
let generator = SystemRandomNumberGenerator()
let randomBool = Bool.random(using: &generator)
 ```
 
 `SystemRandomNumberGenerator` implemented [Fast Random Integer Generation in an Interval](https://arxiv.org/pdf/1805.10941.pdf)

Let's see how `random()` works in `Bool` type:

```swift
@inlinable
public static func random<T: RandomNumberGenerator>(
  using generator: inout T
) -> Bool {
  return (generator.next() >> 17) & 1 == 0
}
```

Old implemention was:

```swift
@inlinable
public static func random<T: RandomNumberGenerator>(
  using generator: inout T
) -> Bool {
  return generator.next() % 2 == 0
}
```

Still lots of thing to discover:

https://forums.swift.org/t/proposal-random-unification/6626/2

https://github.com/apple/swift-evolution/blob/master/proposals/0202-random-unification.md?plain=1

https://github.com/apple/swift/blob/main/stdlib/public/core/Random.swift
