
# Bypass Encryption Warning When Testing
We've faced this warning and checked "No" a thousand times!

>  Export Compliance Information </br>
>Does your app use encryption? Select Yes even if your app only uses the standard encryption in iOS and macOS. 

### How to Silent the Warning
Add this key to the `info.plist` with `NO` value:
```
ITSAppUsesNonExemptEncryption
```

The unraw key name is:
```
App Uses Non-Exempt Encryption
```

### Reference
https://developer.apple.com/documentation/bundleresources/information_property_list/itsappusesnonexemptencryption
