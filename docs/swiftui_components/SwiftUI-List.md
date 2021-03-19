---
layout: default
title: List
parent: SwiftUI's components
nav_order: 1
---

Khởi tạo một List với các cell static

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

Tạo struct cho các cell của List, ở đây cần kế thừa Identifiable để định danh các cell

```swift
struct Book: Identifiable {
    let id: UUID = UUID()
    let name: String
}
```

Khởi tạo mảng data và đưa vào List

```swift
struct Book: Identifiable {
    let id: UUID = UUID()
    let name: String
}

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
                Section(header: BookHeader(title: type.type), content: {
                    ForEach(type.books) { book in
                        Text(book.name)
                    }
                })
            }
        }
    }
}
```