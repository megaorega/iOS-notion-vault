# Abstract
---
`Builder` это паттерн, который позволяет создавать объект по частям. Добавление частей не должно зависеть друг от друга. 

## Код
### Пример про хот доги
```swift
class HotDog {
	var bun: String
	var ketchup: Bool
	var mustard: Bool
	var kraut: Bool
}

// чтобы создать хотдог через конструктор, понадобится код:
let newHotdog = HotDog(bun: "wheat", 
					   ketchup: true, 
					   mustard: true, 
					   kraut: true)
```

Можно переписать класс для более удобного создания хотдогов:
```swift
class HotDog {
	var bun: String
	var ketchup: Bool = false
	var mustard: Bool = false
	var kraut: Bool = false
	
	func addKetchup() -> HotDog {
		ketchup = true
		return self
	}
	func addMustard() -> HotDog {
		mustard = true
		return self
	}
	func addKraut() -> HotDog {
		kraut = true
		return self
	}
}

// теперь можно создать хотдог, вызывая по цепочке нужные методы
let newHotDog = HotDog(bun: "wheat")
					.addKetchup()
					.addMustard()
					.addKraut()
```



### Экран из нескольких модулей
Задача – создавать экраны, состоящие из нескольких модулей. `UIViewController`, `Interactor`, `Presenter`

#### Сначала создадим необходимые протоколы и классы модулей
```swift
// Presenter это модуль для экрана, у нас тут функционала не будет, он просто выводит информацию о себе
protocol Presenter {
	var information: String {get}
}

class ScreenPresenter: Presenter {
	var information = "This is presenter for screen"

	weak var viewController: ScreenViewController?
}
```

```swift
protocol Interactor {
	init(presenter: Presenter)
}

class ScreenInteractor: Interactor {
	var presenter: Presenter!
	
	required init(presenter: Presenter) {
		self.presenter = presenter
		super.init()
	}
}
```

```swift
class ScreenVC: UIViewController {
	let interactor: Interactor! = nil

	init(title: String, interactor: Interactor) {
		self.interactor = interactor
		super.init(nibName: nil, bundle: nil)
		self.title = title
	}

	required init?(coder aDecoder: NSCoder) {
		fatalError("init(coder:) has not been implemented")
	}
}
```

#### Создадим билдер экранов
```swift
// протокол-абстракция для создания любого экрана со всеми модулями внутри.
// В самом простом виде билдер должен иметь функцию сборки и возвращать готовый объект
protocol ModuleBuilder {
	func build() -> UIViewController
}

class ScreenBuilder: ModuleBuilder {
	var title: String?

	// функция, с помощью которой можно задать название экрана. Она нужна, чтобы в готовый контроллер можно было передать название
	func setTitle(_ title: String) -> ScreenBuilder {
		self.title = title
		return self
	}

	// реализация build в конкретном билдере создает необходимые модули для конкретного экрана и возвращает готовый экран со всеми соединенными модулями
	func build() -> UIViewController {
		guard let title = title else {fatalError("Need to set title first!")}

		// создаем модули и соединяем их, передавая нужные ссылки
		let presenter = ScreenPresenter()
		let interactor = ScreenInteractor(presenter: presenter)
		let controller = ScreenViewController(title: title, interactor: interactor)
	presenter.viewController = controller

	// возвращаем готовый контроллер экрана
	return controller
	}
}
```

#### Код пользователя
```swift
// viewDidLoad в некотором контроллере:
override func viewDidLoad() {
	super.viewDidLoad()
	
	let screenVC = ScreenBuilder().setTitle("Some screen").build()
	self.present(screenVC, animated: true, completion: nil)	
}
```



## Когда применять
- Для сложных архитектур типа [[VIPER architecture\|VIPER]] или [[YARCH architecture\|YARCH]]. Экраны в таких архитектурах состоят из множества модулей, например `UIViewController`, `Intercator`, `Presenter`, `Router` и т.д. Все эти модули можно добавлять с помощью билдера, чтобы получать готовый экран для работы.
- `Builder` будет иметь смысл, если нужно создавать сложные объекты. В таком случае конструктор не будет содержать огромную кучу кода. Также такой паттерн позволит изменять объект в любой момент его жизни, а не только при создании.



# Questions
---
#need_research/development 
- [ ] 



# Learning materials
---
## Articles & Links
- 
## Videos:
- [The Swift Developers video. Design patterns в swift с нуля: урок 5 - Builder (Строитель)](https://youtu.be/okRGGuPL34M)
- 