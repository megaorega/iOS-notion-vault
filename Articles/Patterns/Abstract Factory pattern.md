# Abstract
---
Порождающий паттерн
__Abstract Factory__ это такой паттерн, позволяет клиентскому коду получать экземпляры классов без привязки к конкретным классам. Зависеть такой код будет только от _протокола абстрактной фабрики_ и _протоколов объектов_.

## Код
У нас есть задача создавать транспорт. Самолеты, лодки и машины.

### Шаг 1: протоколы для типов объектов
Для каждого типа транспорта создаем свои протоколы. Сколько __типов__ транспорта, столько и __протоколов__ для типов создаваемых объектов
```swift
// описываем самолеты через протокол
protocol Plane {
	var name: String
	
	func turnEngineOn()
	func takeOff()
	func land()
	func turnEngineOff()
}

// описываем лодки через протокол
protocol Boat {
	var name: String
	
	func turnEngineOn()
	func fullForward()
	func fullStop()
	func turnEngineOff()
}

// описываем машины через протокол
protocol Car {
	var name: String
	
	func turnEngineOn()
	func accelerate()
	func brake()
	func turnEngineOff()
}
```

### Шаг 2: протокол абстрактной фабрики
Создаем протокол абстрактной фабрики. По протоколу она должна создавать транспорт всех типов, описанных выше. Сколько __типов__, столько и __методов для создания__ объектов.
```swift
protocol TransportFactory {
	func createPlane() -> Plane
	func createBoat() -> Boat
	func createCar() -> Car
}
```

### Шаг 3: классы вариантов каждого типа объектов
Пишем классы, которые реализуют протоколы типов объектов. 
Каждый класс это вариант объекта. Нужно определиться, сколько __разных вариантов каждого объекта__ мы хотим создавать. И для каждого из вариантов создать свой класс. Например, мы хотим делать 3 вида транспорта: частный, коммерческий и военный. Поэтому создаем три класса для самолетов.
```swift
// делаем класс для самолета Цессна, он реализует протокол Plane
class CessnaPlane: Plane {
	// объявляем свойства и задаем значения
	var name: String = "Cessna"
	
	// реализуем все объявленные в протоколе методы
	func turnEngineOn() {
		print("\(name) engine turned ON")
	}
	
	func takeOff() {
		print("\(name) taking off...")
	}
	
	func land() {
		print("\(name) landing...")
	}
	
	func turnEngineOff() {
		print("\(name) engine turned OFF")
	}
}

// подобным образом делаем класс для пассажирского Боинга
class BoeingPlane: Plane {
	var name: String = "Boeing 777"
	// реализуем методы...
}

// и класс для истребителя F-14
class JetFighterF14: Plane {
	var name: String = "F-14"
	// реализуем методы...
}
```

### Шаг 4: фабрики, создающие каждый вариант объекта
Теперь нужно сделать фабрики, производящие каждый вариант объекта. Каждая фабрика делает и самолеты и лодки и машины. Одна фабрика делает только личный транспорт, другая только коммерческий, третья – только военный.
```swift
// реализуем фабрику, которая производит личный транспорт
class PrivateTransportFactory: TransportFactory {
	func createPlane() -> Plane {
		// создаем экземпляр конкретного класса, который реализует протокол Plane
		return CessnaPlane()
	}

	func createBoat() -> Boat {
	// создаем экземпляр конкретного класса, который реализует протокол Boat (представим, что у нас это KayakBoat)
		return KayakBoat()
	}
	
	func createCar() -> Car {
		// создаем экземпляр конкретного класса, который реализует протокол Car (представим, что у нас это )
		return SubaruBRZCar()
	}
}
```

Описываемый код будет производить объекты, которые можно свести в таблицу:

| | `Plane` | `Boat` | `Car` |
| --- | --- | --- | --- |
| __`PrivateTransportFactory`__ | `CessnaPlane` | `KayakBoat` | `SubaruBRZCar` |
| __`CommercialTransportFactory`__ | `Boeing777Plane` | `TankerBoat` | `TeslaSemiCar` |
| __`MilitaryTransportFactory`__ | `JetF14Plane` | `AirCraftCarrierBoat` | `HummerCar` |

Код, использующий абстрактную фабрику будет импортировать только протокол `TransportFactory` и каждый из типов объектов: `Plane`, `Boat`, `Car`. 

## Важное
Код, использующий абстрактную фабрику должен использовать внедренную зависимость каким-то внешним кодом, чтобы не привязываться к классу конкретной фабрики.
```swift
class TransportViewerVC: UIViewController {
	// класс должен иметь свойство с типом абстрактной фабрики. Какой-то внешний код должен создать экземпляр конкретной фабрики и присвоить этому свойству
	var transportFactory: TransportFactory?
	
	override func viewDidLoad() {
		super.viewDidLoad()

		// создаем самолет
		transportFactory.createPlane()
		// создаем судно
		transportFactory.createBoat()
		// создаем машину
		transportFactory.createCar()
	}
}
```



# Questions
---
#need_research/development 
- [ ] 



# Learning materials
---
## Articles & Links
- 
## Videos:
- [The Swift Developers video. Design patterns в swift с нуля: урок 3 - Abstract Factory (Абстрактная фабрика)](https://youtu.be/kjQGfFV_lM0)
- 