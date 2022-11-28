# Debouce With DispatchWorkItem
How to simulate user typing and a debouncer perform with GCD?
First, let's create a serial queue to represent user typing:
```(swift)
struct SimulateTyping {
    private let serialQueue = DispatchQueue(label: "typing.serial")
    private let typing = [
        "H"  : 0,
        "He" : 0.5,
        "Hello" : 1.1,
        "Hello " : 1.4,
        "Hello Wo" : 2.9,
        "Hello Worl" : 3,
        "Hello World" : 3.2,
    ]
    
    var eventHandler: ((String)->Void)?
    
    func start() {
        for (text, time) in typing {
            serialQueue.asyncAfter(deadline: .now() + .milliseconds(Int(time*1000)), execute: {
                eventHandler?(text)
            })
        }
    }
}
```
It will be used by something like this:
```(swift)
var typing = SimulateTyping()
typing.eventHandler = { text in
    // do something with the given text
}
typing.start()
```

Second, let's create a model wich gives a text and debounce it after a time period by using `DispatchWorkItem`. 
It will debounce the text on the main thread.
```(swift)
class Debouncer {
    private var workItem: DispatchWorkItem?
    
    public var eventHandler: ((String)->Void)?
    
    func receive(text: String, debounceAfter time: Int) {
        workItem?.cancel()
        
        let newWorkItem = DispatchWorkItem { [weak self] in
            self?.eventHandler?(text)
        }
        workItem = newWorkItem
        
        DispatchQueue.main.asyncAfter(deadline: .now() + .milliseconds(time), execute: workItem!)
    }
}
```

And then we can use them like this:
```(swift)
var typing = SimulateTyping()
let debouncer = Debouncer()

typing.eventHandler = { text in
    debouncer.receive(text: text, debounceAfter: 500)
}
typing.start()

debouncer.eventHandler = { text in
    print(text)
}
```
