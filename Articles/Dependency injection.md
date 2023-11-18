# Abstract
Структурный паттерн проектирования.
DI реализует принцип инверсии контроля (inversion of control, IoC).

Внедрение зависимости позволяет написать программу так, чтобы компоненты не были сильно связаны (coupling).

Как можно внедрить зависимость:
- Через инициализатор
	 Наиболее предпочтительно, если нужно хранить ссылки на внедренные зависимости.
	 
	 Code example:
	 ```swift
	 class QuizVC: UIViewController {
			private let settings: Settings
			private let gameCenter: GameCenterable
			private let quiz: Quiz
		
			init(setings: Settings, 
				 quiz: Quiz, 
				 analyticsService: AnalyticsServiceable, 
				 gameCenter: GameCenterable) {
				 
			self.setings = setings
			self.gameCenter = gameCenter
			...
			}
	}
	```
- __Property injection__
	Используется для внедрения зависимостей, если их нужно хранить. Это менее предпочтительный способ. Мы не знаем, существует ли делегат. Также это позволяет менять делегат по ходу работы программы (например, у таблицы можно менять `dataSource`, чтобы показывать разные данные)
	
	Code example:
	```swift
	public var someProperty: String
	weak public var delegate: UIViewControllerDelegate?
	```
- Method injection
	Используется, когда ссылки на внедренный объект хранить **не нужно**
	
	Code example:
	```swift
	public protocol NSCoding {
		func encodeWithCoder(aCoder: NSCoder)
	}
	```
- Ambient context
	Code example	```
	```swift
	public class URLCache: NSObject {
		public class func setSharedURLCache(cache: URLCache) {}
		public class func sharedURLCache() -> URLCache {}
	}
	```

# Libs:
- ##### [Swinject](https://github.com/Swinject/Swinject)
  При резолве нужно делать форс анрап, это может привести к крашу приложения в рантайме, если где-то накосячить.
  Code example:
  ```swift
  let secureStorage = resolver.resolve(SecureStoragable.self, name: nil)!
  ```
- ##### Needle (not suitable for VIPER (don't know why))
- ##### PureDI
- ##### ~~Typhoon (objC)~~



# Questions
#need_research/development about DI
- [ ] Правильно ли говорить, что DI реализует IoC?



# Learning materials
## Articles
- 
## Videos:
- [Mad Brains video about dependency injection in iOS](https://youtu.be/poo81s5nky4)
- 