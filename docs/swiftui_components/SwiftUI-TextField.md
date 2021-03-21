---
layout: default
title: TextField
parent: SwiftUI's components
nav_order: 3
---
Khi sử dụng TextField cần phải sử dụng 1 biến có thể two-way binding, có nghĩa là khi update text của TextField thì value của biến đấy cũng sẽ thay đổi theo, hoặc update giá trị của biến thì text của TextField cũng sẽ thay đổi theo.

```swift
struct ContentView: View {
    @State private var text: String = ""
    
    var body: some View {
        TextField("Placeholder", text: $text, onEditingChanged: { isEditing in
            if isEditing {
                print("startEdit")
            } else {
                print("endEdit")
            }
        }, onCommit: {
            print("commit")
        })
    }
}
```
TextField cũng sẽ có Placeholder giống UITextField, bên cạnh đấy TextField cũng có 2 callback là onEditingChanged, onCommit.  
Trong đấy thì onEditingChanged sẽ được gọi khi TextField bắt đầu hoặc kết thúc editing, onCommit được gọi khi tap vào Return.