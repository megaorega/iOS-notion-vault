# Abstract
---
Реализует шаблон проектирования Flux.

Архитектура состоит из 5 модулей, последовательно связанных между собой. 
1. `State` (представляет состояние приложения)
2. `Store` (хранит и состояние приложения)
3. `Action` (нужно для однозначной смены одного состояния на другое)
4. `Reducer` (чистая функция, которая принимает состояние и действие и возвращает новое состояние. Единственный способ получать состояния)
5. `Subscriber` ( #tbd добавить описание)
Данные передаются в одном направлении (unidirectional flow) от одного модуля к другому

## Redux rules
- Единственное глобальное состояние (`State`) хранится в хранилище (`Storage`)
- Состояние неизменяемо (`State` is immutable)
- Новое состояние может быть задано только через передачу действия в хранилище
- New state can be set only by dispatching an action to store.
- New state can be calculated only by reducer which is a **pure function** (always returns the same result for the same inputs).
- **Store** notifies subscribers by broadcasting new state.
## Решаемые проблемы
- Обычно архитектуры содержат много элементов, которые независимо друг от друга меняют глобальное состояние приложения. Redux защищает глобальное состояние с помощью специально выделенной сущности и правил

# Questions
---
#need_research/development 
- [ ] 



# Learning materials
---
## Articles & Links
- [Ruslan Dzhafarov. How to use Redux architecture part 1](https://ruslandzhafarov.medium.com/how-to-use-redux-architecture-part-1-2357b14d2f6)
- [Ruslan Dzhafarov. How to use Redux architecture part 2](https://ruslandzhafarov.medium.com/how-to-use-redux-architecture-part-2-c59defedc220)
- [Wojciech Kulik. Redux architecture and mind-blowing features](https://wojciechkulik.pl/ios/redux-architecture-and-mind-blowing-features)
- [Kodeco. Redux Architecture (paid content)](https://www.kodeco.com/books/advanced-ios-app-architecture/v3.0/chapters/6-architecture-redux)
- [Архитектура Redux. Введение.](https://ovchinnikov.cc/writing/redux-intro/)
## Videos:
- 