# Quick hints
---



# Abstract
---
## Overview
Unit-test это функция, которая вызывает наш код, а потом утверждает, что он работает правильно. Результатом теста может быть только 2 состояния: `fail` и `success`
В XCode эти функции реализуются в специальных классах, которые наследуются от XCTestCase.



## Что покрывать тестами?
- Классы и методы модели
- Взаимодействие модели с контроллером
- Методы разных сервисов (сеть, БД и т.п.)
- Пограничные условия (методы валидации и подобные)



## Концепция FIRST
- __F – Fast.__ Тесты должны выполняться быстро
- __I – Independent / Isolated.__ Тесты не должны зависеть друг от друга и быть уникальными
- __R – Repeatable.__ Результат должен быть одинаковым, сколько бы ни запускался тест.
- __S – Self-validating.__ Тест должен быть самостоятельным и полностью автоматизированным, чтобы разработчику не нужно было ничего делать, чтобы тест работал. 
- __T – Timely.__ Своевременность. В идеале тест должен быть написан до написания продакшн кода, который он тестирует.



## Тесты в XCode
```swift
import XCTest
@testable import MadUnit // первое, что нужно сделать – импортировать таргет

// создаем класс, который наследуется от XCTestCase
class MadUnitTests: XCTestCase {

	// сработает перед вызовом каждого тестового метода в классе
	// в этом методе нужно создавать объекты, которые нужны для тестирования (например, модель)
	override func setUpWithError() throws {}

	// сработает после каждого тествого метода в классе
	// в этом методе нужно уничтожать объекты, которые были нужны для тестирования (например, модель), чтобы перед запуском следующего теста объект был создан заново и был в первоначальном состоянии
	override func tearDownWithError() throws {}



	// тестовые функции всегда должны начинаться со слова test
	func testExample() throws {}

	// пример функции для тестирования производительности. Она должна замерять время выполнения кода
	func testPerformanceExample() throws {
		// время выполнения всех инструкций в блоке measure будет измерено
		// будет произведено 10 запусков и высчитана средняя величина
		// можно установить baseline времени выполнения теста и допустимое отклонение от него
		// тест будет считаться пройденным, например, если среднее отклонение будет в пределах 10% от baseline
		self.measure {
			let someArray = Array(0...1000)
			var counter = 0
			
			someArray.forEach{
				counter += $0
			}
		}
	}
}
```




## Структура Given-When-Then
- __Given__ – описываем предварительные условия теста и задаем все параметры.
- __When__ – указываем действия для теста
- __Then__ – описываем изменения, которые ожидаем в результате теста

```swift
// sut означает system under test
var sut: MainViewModel!

override func setupWithError() throws {
	try super.setupWithError()
	sut = MainViewModel()
}

override func tearDownWithError() throws {
	sut = nil
	try super.tearDownWithError()
}



func testAsyncMethod() {
	// GIVEN блок
	let expectation = XCTestExpectation(description: "We should wait for the sample async method")
	
	// WHEN
	// тут делаем какое-то действие (здесь вызов асинхронной функции)
	sut.doSomethingAsync(
		delay: 2,
		completion:  {[weak expectation] result in 
			// THEN
			// тут мы вызываем одну из встроенных функций сравнения результата с нашими ожиданиями (здесь результат сравниваем с хардкод-строкой)
			XCTAssertEqual(result, "Hello, world")
			expectation?.fulfill()
		}
	)
	// строка ниже указывает, сколько времени допустимо ждать для выполнения асинхронной операции
	// В данном случае, тест будет считаться пройденным, если асинхронный метод отработает в пределах 3-х секунд
	self.wait(for: [expectation], timeout: 3)
}
```



## Testing ways

### Mock
__Mock__ это объект, который имитирует реальные объекты для тестирования.
1. Для исходного тестируемого объекта должна быть абстракция
2. Нужно реализовать mock-объект на основе абстракции
3. Подменить зависимость от реального объекта на зависимость от mock-объекта на время тестирования

### Stub
Stub это функция, которая всегда выведет один и тот же результат не зависимо от того, что подать ей на вход.

### Expectations


> [!  Stub vs Mock]
> Когда мы используем mock, то мы заменяем весь модуль на mock (ложный, тестовый объект, который имитирует настоящий)
> Mock используют, чтобы проверить была ли функция вызвана с правильными аргументами.
> Stub используют, чтобы проверить, как функция работает с полученным ответом.

# Questions
---
#need_research/development 
- [ ] What `@testable import` do?
	


# Learning materials
---
## Articles & Links
- [Bitrise article, used in video by MadBrains](https://bitrise.io/blog/the-ultimate-guide-to-unit-and-ui-testing-for-beginners-in-swift)
- [Vadim Bulavin article about async code testing (used in video by MadBrains)](https://www.vadimbulavin.com/unit-testing-async-code-in-swift/)
## Videos:
- [Mad Brains. What need to know? (42 min)](https://youtu.be/JWJDavnY_Es)
- 