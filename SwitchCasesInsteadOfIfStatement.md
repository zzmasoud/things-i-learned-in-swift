# Switch Cases Instead of If Statement

Sometimes we need to check a set of conditions for actions, consider this function as an exmaple:

```swift
\\ predefined enums

enum Location {
    case inside, outside
}

enum Weather {
    case sunny, cloudy, rainy
}

func alertUser(in location: Location, andWeather weather: Weather, needsEyeProtection: Bool) -> String? {
    if location == .inside {
        return "let's go out!"
    }
    else if location == .outside {
        return needsEyeProtection ? "Don't forget your sunglasses" : "What a beautiful day :)"
    }
    return nil
}
```
With the power of enums and switch/case statement, it can be easier:

```swift
func alertUser(in location: Location, andWeather weather: Weather, needsEyeProtection: Bool) -> String? {
    switch (location, weather) {
    case (.inside, _):
        return "let's go out!"
    case (.outside, _) where needsEyeProtection:
        return "Don't forget your sunglasses"
    case (.outside, _):
        return "What a beautiful day :)"
    }
}
```
