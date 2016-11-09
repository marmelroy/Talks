## Swift Scripting

### Getting started

The first step is to add this to the top of your Swift script:
``` shell
#!/usr/bin/swift
```

The second step is to make it executable
``` shell
$ chmod +x script.swift
```
### What IDE to use

For simple scripts, Xcode Playgrounds are a great IDE. Your code runs the same way it would in the command line, you get autocomplete, live previews and a console output.

For more complex scripts, it is possible to hack Atom into a Swift scripting IDE with the following package installs:
``` shell
$ apm install script language-swift
```

### Adding frameworks
Third party libraries need to be compiled as dynamic frameworks - this can be achieved manually or with SPM, Carthage or Cocoapods (via the Rome plugin).

To include in your script, you need to specify a target and a framework path in your shebang
```shell
#!/usr/bin/swift -target x86_64-macosx10.12 -F /Library/Frameworks -F Rome
```

### Launch arguments and user input
You can access launch arguments using:
```swift
CommandLine.arguments
```

You can ask for user input using:
```swift
readLine()
```

### Shell

You can run shell commands using Process() (formerly NSTask) using this function (make sure to import Foundation):
```swift
func shell(_ command: String) {
    let arguments = command.components(separatedBy: " ")
    let process = Process()
    process.launchPath = "/usr/bin/env"
    process.arguments = arguments
    process.waitUntilExit()
    process.launch()
}
```

### Current file path
There's no NSBundle when writing a Swift script. To get the current path use
```swift
let currentPath = FileManager.default.currentDirectoryPath
```

### Color

You can format a line by adding color using the following struct:
```swift
struct commandLineFormat {
    static let black = "\u{001B}[0;30m"
    static let red = "\u{001B}[0;31m"
    static let green = "\u{001B}[0;32m"
    static let yellow = "\u{001B}[0;33m"
    static let blue = "\u{001B}[0;34m"
    static let magenta = "\u{001B}[0;35m"
    static let cyan = "\u{001B}[0;36m"
    static let white = "\u{001B}[0;37m"
}
```
