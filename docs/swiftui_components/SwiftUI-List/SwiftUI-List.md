---
layout: default
title: List
parent: SwiftUI's components
nav_order: 1
---
Là component đối ứng với TableView của UIKit, List cũng có cell, section, header, footer giống với TableView  
Đầu tiên chúng ta sẽ khởi tạo một static List

```swift
struct Bookcase: View {
    
    var body: some View {
        List {
            Text("Harry Potter")
            Text("The Victory Garden")
            Text("Dragons of Autumn Twilight")
        }
    }
}
```

Tiếp theo chúng ta sẽ cùng làm một dynamic List  
Để tạo dynamic List chúng ta cần tạo struct cho các cell của List, ở đây cần kế thừa Identifiable để định danh các cell

```swift
struct Book: Identifiable {
    let id: UUID = UUID()
    let name: String
}
```

Khởi tạo mảng data và đưa vào List

```swift
struct Bookcase: View {
    private let books: [Book] = [Book(name: "Harry Potter"),
                                 Book(name: "The Victory Garden"),
                                 Book(name: "Dragons of Autumn Twilight")]
    
    var body: some View {
        List(books) { book in
            Text(book.name)
        }
    }
}
```

Hoặc có thể dùng ForEach như sau

```swift
struct Bookcase: View {
    private let books: [Book] = [Book(name: "Harry Potter"),
                                 Book(name: "The Victory Garden"),
                                 Book(name: "Dragons of Autumn Twilight")]
    
    var body: some View {
        List {
            ForEach(books) { book in
                Text(book.name)
            }
        }
    }
}
```

Tạo List với các Section khác nhau

```swift
struct Book: Identifiable {
    let id: UUID = UUID()
    let name: String
}

struct BookType: Identifiable {
    let id: UUID = UUID()
    let type: String
    let books: [Book]
}

struct Bookcase: View {
    private let bookTypes: [BookType] = [BookType(type: "Action", books: [Book(name: "Harry Potter"),
                                                                          Book(name: "The Victory Garden"),
                                                                          Book(name: "Dragons of Autumn Twilight")]),
                                         BookType(type: "Romantic", books: [Book(name: "Harry Potter"),
                                                                            Book(name: "The Victory Garden"),
                                                                            Book(name: "Dragons of Autumn Twilight")]),
                                         BookType(type: "Adventure", books: [Book(name: "Harry Potter"),
                                                                             Book(name: "The Victory Garden"),
                                                                             Book(name: "Dragons of Autumn Twilight")])]
    
    var body: some View {
        List {
            ForEach(bookTypes) { type in
                Section(header: Text(type.type), content: {
                    ForEach(type.books) { book in
                        Text(book.name)
                    }
                })
            }
        }
    }
}
```

Header, Footer của Section có thể tách ra như sau

```swift
struct BookHeader: View {
    let title: String

    var body: some View {
        HStack {
            Text("Book")
            Text(title)
        }
    }
}
```

Cho struct vừa tạo vào Header của Section là được

```swift
var body: some View {
        List {
            ForEach(bookTypes) { type in
                Section(header: BookHeader(title: type.type), content: {
                    ForEach(type.books) { book in
                        Text(book.name)
                    }
                })
            }
        }
    }
```

Với List trong SwiftUI thì ở các cell sẽ luôn có các separator line, để loại bỏ các line đấy đi thì cần set lại inset và background color cho cell

```swift
var body: some View {
        List {
            ForEach(bookTypes) { type in
                Section(header: BookHeader(title: type.type), content: {
                    ForEach(type.books) { book in
                        Text(book.name)
                            .listRowInsets(EdgeInsets(top: -1, leading: -1, bottom: -1, trailing: -1))
                            .background(Color.white)
                    }
                })
            }
        }
        .environment(\.defaultMinListRowHeight, 0)
    }
```

```.environment(\.defaultMinListRowHeight, 0)``` dùng để set lại chiều cao nhỏ nhất mặc định cho cell, nếu không set thì nó sẽ là 49.  
Bạn chỉ có thể ẩn separator line khi chiều cao cell của bạn bằng hoặc lớn hơn defaultMinListRowHeight của cell.