---
layout: default
title: Button
parent: SwiftUI's components
nav_order: 4
---

```swift
struct ContentView: View {
    @State private var showDetails = false

    var body: some View {
        VStack(alignment: .leading) {
            Button("Show details") {
                showDetails.toggle()
            }

            if showDetails {
                Text("You should follow me on Twitter: @twostraws")
                    .font(.largeTitle)
            }
        }
    }
}
```
