# Abstract
---
## MRC
При ручном управлении памятью (MRC) для управления счетчиком ссылок нужно было вызывать специальные методы:
- `retain` для увеличения счетчика ссылок у объекта
- `release` для уменьшения счетчика ссылок у объекта

Возникала проблема с методами, которые создавали объект и возвращали его:
```objc
- (Test *) createNewTest {
	Test *newInstance = [[Test alloc] init];
	[newInstance release];
	return newInstance; // deallocated before return!
}
```

Поэтому такой объект нужно было поместить в `autorelease pool`:
```objc
- (Test *) createNewTest {
	Test *newInstance = [[Test alloc] init];
	[newInstance autorelease];
	return newInstance;
}
```

Авторелиз пул очищается в момент вызова у него метода `drain`. В этот момент ко всем объектам, которые содержатся у него внутри вызывается метод `release`.

[[Run Loop |Ран луп]] на каждой итерации цикла создает авторелиз пул и очищает его в конце итерации.

## ARC
В ARC авторелиз пул может использоваться для снижения максимального потребления оперативной памяти внутри какого-нибудь цикла, например.
![[autorelease_pool_optimization_1.png]]
В этом случае, итерация [[Run Loop |Ран Лупа]] не закончится до тех пор, пока весь цикл не закончит свою работу. 
Можно исправить вот так:
![[autorelease_pool_optimization_2.png]]
Этот код создает отдельный авторелиз пул, который очищается после каждой итерации.

# Questions
---
#need_research/development 
- [ ] 



# Learning materials
---
## Articles & Links
- 
## Videos:
- 