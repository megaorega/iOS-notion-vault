### Abstract
Enum это способ определить насколько разных кейсов в свободной форме.

###### Литералы
```swift
public func intEnumTest() {

  enum FooBar: Int {

    case a
    case b = 1000
    case c = 5000
    case d = 2000
    case e
  }

  print("case a = \(FooBar.a.rawValue)") // prints 0
  print("case b = \(FooBar.b.rawValue)") // prints 1000
  print("case c = \(FooBar.c.rawValue)") // prints 5000
  print("case d = \(FooBar.d.rawValue)") // prints 2000
  print("case e = \(FooBar.e.rawValue)") // prints 2001
}
```

###### Можно использовать переменные, например:
```swift
public enum WorkingDayType: Int, Codable {
    case working = 0
    case off = 1
    case error = 100
    case notSelected = -1

    var title: String {
        switch self {

        case .working: return "Рабочий день"
        case .off: return "Выходной день"
        case .error: return "Ошибка"
        case .notSelected: return "Дата не выбрана"
        }
    }
}
```


### Learning materials
##### Articles
- 
##### Videos:
- 