# Abstract
---
Порождающий паттерн проектирования.
Prototype это такое название для клона. Этот паттерн должен производить глубокое копирование объекта.



## Код
^ededf9

### Самая простая, базовая реализация в лоб
Просто создаем новый экземпляр и все свойства заполняем значениями оригинала.
```swift
class Person {
	var name = ""
	
	func clone() -> Person {
		let clonedPerson = Person()
		clonedPerson.name = name
		return clonedPerson
	}
}

// пользовательский код может создавать клоны уже существующих объектов с помощью вызова метода clone()
let person1 = Person()
person1.name = "Alice"

// чтобы создать отдельный объект, не связанный с оригиналом
let person2 = person1.clone()
person2.name = "Bob" // поле name было такое же, как у оригинала (Alice), мы меняем его на другое (Bob), а оригинал останется неизменным
```



## Когда применять
- когда нужно создать копию объекта без вызова конструктора (и всей иерархии конструкторов его предков)



# Questions
---
#need_research/development 
- [x] Как сделать в Свифте?
      Смотри [[Prototype pattern#^ededf9]]



# Learning materials
---
## Articles & Links
- 
## Videos:
- [The Swift Developers. Design patterns в swift с нуля: урок 4 - Prototype (Прототип)](https://youtu.be/_IZDdkRYX_c)