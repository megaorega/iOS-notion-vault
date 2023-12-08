# `get` и `set`
```swift
// переменная только для чтения (будет иметь только геттер)
var someReadonlyVar: String {get}

// переменные с геттером и сеттером можно объявить двумя эквивалентными способами:
var someVar: String
var someVar: String {get, set}
```

# `where` в `for in`
```swift
func sumOfPositives (_ numbers: [Int] ) -> Int {
    var sum = 0
    // в for in можно добавить условие срабатывания цикла через слово where
    // в данном случае тело цикла сработает только в случае, если num > 0
    for num in numbers where num > 0 {
      sum += num  
    }
    
    return sum
}
```


# `for in` vs `forEach`
```swift
// возьмем массив с целыми числами
let someArrayValues = [1, 2, 3, 4, 5]

// перебор всех элементов массива можно сделать двумя способами
// через for in цикл
for intValue in someArrayValues {
	print(intValue)
}

// через forEach цикл (метод у массива)
someArrayValues.forEach { intValue in
	print(intValue)
}

// оба способа эквивалентны, но есть 2 отличия:
// в forEach нельзя использовать break и continue
// return в случае forEach выйдет из метода, а не на 1 уровень выше
```

# Property wrappers
[Official documentation here](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/properties/#Property-Wrappers)
```swift
// перед объявлением структуры добавляем директиву @propertyWrapper
@propertyWrapper
struct NumberLessOrEqualTo50: Int {
	// в этом свойстве будет храниться само значение
	private var value: Int = 0
	
	// через computed property добавляем валидацию
	var valueWrapper: Int {
		get {
			// просто вернем значение, которое записано в приватном свойстве
			return value
		}
		set (newValue) {
			// присваеваем число, если оно меньше 50
			value = min(newValue, 50)
		}
	}
}


// как использовать:
// например, нам нужно сделать прямоугольник со сторонами не больше 50
struct Rectangle {
	@NumberLessOrEqualTo50 var width: Int
	@NumberLessOrEqualTo50 var height: Int
}

let rectangle = Rectangle()
rectangle.width = 30 // 30 меньше 50, это число запишется как есть
rectangle.height = 80 // 80 больше 50, запишется 50, потому что сеттер в NumberLessOrEqualTo50 присвоит 50 или меньше
```


# smarter switch!
[About metatypes in swift (check 'More uses of Metatypes' section)](https://swiftrocks.com/whats-type-and-self-swift-metatypes.html)
```swift
func handle(deepLink: DeepLink) {
  switch deepLink {
    case let deepLink as HomeDeepLink:
    //
    case let deepLink as PurchaseDeepLink:
    // 
    default:
    //
  }
}
```


# subscripts
[Official docs of subscripts here](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/subscripts#Subscript-Syntax)
```swift
subscript(index: Int) -> Int {
	get {
		// здесь нужно вернуть найденное значение по переданному индексу
	}
	set(newValue) {
		// здесь нужно записать переданное значение по переданному индексу
	}
}
```