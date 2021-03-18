---
layout: default
title: NavigationView
parent: SwiftUI's components
nav_order: 8
---

```swift
struct SongRow: View {
    var song: Song
    @Binding var isPlaying: Bool

    var body: some View {
        HStack {
            VStack(alignment: .leading) {
                Text(song.name).bold()
                Text(song.artist.name)
            }
            Spacer()
            Button(
                action: { self.isPlaying.toggle() },
                label: {
                    if isPlaying {
                        PauseIcon()
                    } else {
                        PlayIcon()
                    }
                }
            )
        }
    }
}
```

Co the tach phan cac label cua button ra nhu duoi

```swift
private extension SongRow {
    func makeButtonLabel() -> some View {
        if isPlaying {
            return AnyView(PauseIcon())
        } else {
            return AnyView(PlayIcon())
        }
    }
}
```

Chỗ này phải return AnyView vì thằng PauseIcon và PlayIcon khác type nhau

Có một cách khác để xử lý vấn đề trên như sau:

```swift
private extension SongRow {
    @ViewBuilder func makeButtonLabel() -> some View {
        if isPlaying {
            PauseIcon()
        } else {
            PlayIcon()
        }
    }
}
```

Với ViewBuilder thì ta không cần phải dùng AnyView nữa

Lúc này có thể call như thằng

```swift
struct SongRow: View {
    ...

    var body: some View {
        HStack {
            ...
            Button(
                action: { self.isPlaying.toggle() },
                label: { makeButtonLabel() }
            )
        }
    }
}
```
