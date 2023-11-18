# Abstract
---
__State__ это класс, описывающий принципиально разные состояния объекта. Класс состояния реализует поведение, нужное для конкретного случая.
Код пользователя обращается к исходному объекту, который предоставляет высокоуровневый доступ к поведению. Но реализация поведения делегируется в объект состояния.

Например, есть такой код:
```swift
class Human {
	// 
	func think(withMood mood: String) {
		switch mood {
		case "happy":
			print("I am happy now")
		case "sad":
			print("I am sad now")
		default:
			print("I am neutral now")
		}
	}
}
```

В этом коде будут плодиться свитчи, которые сложно поддерживать. Сложно писать разное поведение для разных стейтов. Свитч будет становиться большим.

С паттерном State можно переписать так:
```swift
// создаем описание состояния, которое может быть по-разному реализовано в классах, подчиняющихся этому протоколу
protocol HumanState {
	func think() -> String
}

// класс состояния реализует объявленные методы, и свою логику поведения в них
class HappyState: HumanState {
	func think() -> String {
		return "I am happy"
	}
}

class SadState: HumanState {
	func think() -> String {
		return "I am sad"
	}
}

class NeutralState: HumanState {
	func think() -> String {
		return "I am neutral"
	}
}

// теперь класс человека может делать те же действия, 
class Human {
	// теперь состояние хранится как свойство и можно понять контекст
	var state: HumanState = HappyState()

	// предыдущее поведение здесь заменяется на вызов логики, описанной в конкретном состоянии. Детали реализации скрыты в классе состояния
	func think() -> String {
		print(state.think())
	}
	
	func changeState(to newState: HumanState) {
		state = newState
	}
}
```



## Когда применять
- Можно применить для UI, чтобы менять сразу несколько свойств у отображаемых элементов. Можно применить для экрана, который показывает несколько разных состояний:
	- Пустой экран
	- Загрузка данных
	- Отображение загруженных данных



# Questions
---
#need_research/development 
- [ ] Чем State отличается от делегата?
- [ ] Где можно применить?



# Learning materials
---
## Articles & Links
- 
## Videos:
- 