# Abstract
---
Hit test это процесс рекурсивного поиска вью по всей иерархии отображения, которой коснулся пользователь. 

- `hitTest()`
- `pointInside()`

# Example
## Задача 1: увеличение области тапа: 
Нужно увеличить область тапа, но не увеличивать размер кнопки
### Решение:
Переопределить метод `pointInside()` у вьюхи, по которой тапает пользователь.
```swift
override func point(inside point: CGpoint, 
					with event: UIEvent?) -> Bool {
	let enlargedArea = bounds.insetBy(dx: -30, dy: -30)
	return enlargedArea.contains(point)
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
- [SwiftMagic. Hit test & responder chain](https://www.youtube.com/watch?v=xzzvV1WUfms&list=PL6ZiiwR0cAz6zkjJyJLmc928zHUtgABuw&index=10)
- 