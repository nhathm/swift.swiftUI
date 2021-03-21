---
layout: default
title: Text
parent: SwiftUI's components
nav_order: 2
---
Giống như Label trong UIKit, Text được sinh ra với nhiệm vụ hiển thị dữ liệu dưới dạng text

```swift
struct ContentView: View {
    private let name: String = "Rai"
    
    var body: some View {
        Text("Hello, world! My name is \(name)")
    }
}
```

Một số Modifier cho Text:  
- Set max line cho Text: ```.lineLimit(10)```
- Set alignment cho Text: ```.multilineTextAlignment(.leading)```
- Set màu cho Text: ```.foregroundColor(.blue)```
- Set font cho Text: ```.font(.system(size: 12, weight: .bold))```
- Set kiểu trim text: ```.truncationMode(.head)```
- Set khoảng cách giữa các line: ```.lineSpacing(10)```