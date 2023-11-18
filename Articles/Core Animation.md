# Abstract
Анимации на iOS делаются с помощью фреймворка Core Animation.
Классы из этого фреймворка имеют префикс `CA`:
- `CALayer`
- `CAShapeLayer`
- `CATextLayer`
- `CAAnimation`
- `CAGradientLayer`
- `CABasicAnimation`
- `CAKeyFrameAnimation`



#### Внутри UIView
Внутри `UIView` находится как минимум один экземпляр `CALayer` (root).
![[inside_uiview.png]]
##### CALayer
`CALayer` это класс, который представляет графическое содержимое. `UIView`, которыми мы обычно оперируем это обертка над `CALayer`.
`CALayer` может содержать вложенные в него слои – экземпляры `CALayer`



##### Как работают анимации? (`CABasicAnimation`)
Анимации отображаются на отдельном слое анимации. Мы его создаем, прописываем параметры, а потом добавляем на объект, который анимируем. После того, как анимация закончится, этот слой удалится.

Пример с кодом анимации для прогрессбара:
```swift
let progress = 0.5
// progressLayer это сам слой графики (CALayer) с заполнением шкалы прогрессбара
// здесь необходимо задать конечное значение, потому что анимация не меняет это значение. Слой анимации только отображает изменение значения, а настоящее значение нужно задавать руками
progressLayer?.strokeEnd = progress

// здесь создается анимация заполнения прогрессбара (в инициализатор передается название свойства, которое нужно анимировать)
let strokeEndAnimation = CABasicAnimation(keyPath: "strokeEnd")
strokeEndAnimation.fromValue = 0
strokeEndAnimation.toValue = progress
strokeEndAnimation.duration = duration

// добавляем слой анимации для проигрывания
// В параметр forKey передаем произвольный уникальный ключ, через который можно удалить эту анимацию
// мы можем удалять либо все анимации сразу, либо конкретную по такому ключу 
progressLayer?.add(strokeEndAnimation, forKey: "strokeEndAnimation")
```

##### НО!
Если анимация создается через `UIView.animate()`, то помимо анимации и _настоящее свойство_ у слоя тоже меняется.
```swift
UIView.animation(withDuration: 2) { [weak self] in
	// под капотом будет создан слой анимации, а этот блок изменит настоящее свойство у объекта progressLayer
	self?.progressLayer?.strokeEnd = self?.progress
}
```

##### CAKeyFrameAnimation
Этот класс позволяет задать у анимации не только начальное и конечное значение, а еще промежуточные.
```swift
// создаем массив значений цвета для плавного перехода между ними в ходе анимации
let intermediateColors = getIntermediateColor(forProgress: progress)

// так же, как и в случае с CABaseAnimation тут нужно задать конечное значение, которое будет отображено после проигрывания и удаления анимации
progressLayer.strokeColor = intermediateColors.last

// создаем анимацию для свойства strokeColor
let strokeColorAnimation = CAKeyFrameAnimation(keyPath: "strokeColor")
// задаем все значения, которые должна отобразить анимация
strokeColorAnimation.values = intermediateColors
// задаем длительность анимации
strokeColorAnimation.duration = duration

// добавляем анимацию на объект, у которого нужно анимировать свойство strokeColor
progressLayer?.add(strokeColorAnimation, forKey: "strokeColorAnimation")
```
Также можно задать неравномерную смену значений
```swift
// массив keyTimes это временные точки, в которые будет происходить смена значения. Количество временных точек должно совпадать с количеством значений.
// временные точки в этом массиве это, по сути, значение прогресса, на котором значение должно поменяться
strokeColorAnimation.keyTimes = [0, 0.4, 0.5, 1]
```

---
# Learning materials
##### Articles
- [Kodeco. CALayer tutorial ](https://www.kodeco.com/10317653-calayer-tutorial-for-ios-getting-started)
##### Videos:
- [Mad Brains video about animations (duration 1hr 7m)](https://youtu.be/zrFqpRelI9I)
- [CALayers tutorial on Kodeco](https://www.kodeco.com/3246-calayers)
- 