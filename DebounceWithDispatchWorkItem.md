# Changing Simulator Time For Screenshots
We can use `simctl` tool:
```(bash)
xcrun simctl status_bar booted override --time "HH:MM"
```
To change the time for specific simulator:
```(bash)
xcrun simctl status_bar "iPhone Xs" override --time "HH:MM"
```

### Reference
https://stackoverflow.com/questions/1699671/how-to-change-time-and-timezone-in-iphone-simulator
