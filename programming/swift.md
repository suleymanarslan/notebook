# Swift 

## Shorthand for `if ... != nil`

Long version:

```swift
if let chosenEmoji = emojis[card.identifier] != nil {
  return emojis[card.identifier]!
} else {
  return "?"
}
```

Short equivalent:

```swift
emojis[card.identifier] ?? "?"
```


