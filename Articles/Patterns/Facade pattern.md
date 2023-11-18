# Abstract
---
#programming/pattern/structural
__Facade__ ("fəˈsäd" читается как _"фасад"_) это структурный паттерн.
Фасад скрывает низкоуровневые детали использования сложных объектов и дает более высокоуровневый способ обращаться с ними.

Пример кода:
```swift
// класс системы управления водоснабжением с низкоуровневыми деталями
class PlumberSystem {
	func setPressure(to value: Int) {}
	func turnOn() {}
	func turnOff() {}
}
// класс системы управления электричеством с низкоуровневыми деталями
class ElectricSystem {
	func setVoltage(to value: Int) {}
	func turnOn() {}
	func turnOff() {}
}

// House это класс-фасад для систем, которые будут скрыты внутри него
class House {
	private let plumbing = PlumberSystem()
	private let electrical = ElectricSystem()

	// метод, который скрывает в себе низкоуровневые вызовы для скрытых от пользователя систем
	func turnOnSystems() {
		plumbing.setPressure(to 12)
		plumbing.turnOn()
		electrical.setVoltage(to: 220)
		electrical.turnOn()
	}
	
	func shutDown() {
		plumbing.turnOff()
		electrical.turnOff()
	}
}

// для использования мы создаем объект House и через его высокоуровневое API управляем системами, не зная деталей
let client = House()
client.turnOnSystems()
client.shutDown()
```



## Что даёт?
- Позволяет не зависеть от деталей реализации. Пользователь сложной системы будет иметь зависимость от фасада, а подсистемы можно будет менять
- Удобные методы управления подсистемами
- Сокрытие низкоуровневых методов подсистемы



## Когда применять
- Когда нужно использовать несколько систем аналитики одновременно. 
  Мы можем создать фасад с названием Analytics, а внутри использовать Firebase, AppsFlyer, Facebook. При вызове метода регистрации события мы будем вызывать сразу 3 метода регистрации события – у каждой библиотеки свой.
- 



# Questions
---
#need_research/development 



# Learning materials
---
## Articles & Links
- 
## Videos:
- [The Swift Developers video. Design patterns в swift с нуля: урок 12 - (Фасад)Facade](https://youtu.be/tQOTjtMDX38)
- 