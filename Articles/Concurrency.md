# Abstract

Многопоточность
## Multithreading
### POSIX(Unix) thread
Это самый базовый и низкоуровневый примитив. POSIX thread, сокращенно `pthread`.
#### Как создать
```swift
var thread = pthread_t(bitPattern: 0)
var attr = pthread_attr_t()

pthread_attr_init(&attr)
pthread_create(&thread, &attr, 
	{ pointer in 
		print("test")
		return nil
	}, nil)
```
Unix поток будет выполняться сразу после создания.

### `NSThread`
`NSThread` (в Swift это просто `Thread`) это ObjC обертка над `pthread` для более удобного создания и использования
#### Как создать
```swift
var nsthread = Thread(block: {
	print("test")
})
nsthread.start()
```


## Debugging
Чтобы посмотреть, в каком потоке выполняется код, можно поставить брейкпоинт на строку и увидеть, в каком потоке сейчас выполняется код. Главный поток, в котором выполняется интерфейс это Thread 1

Как посмотреть, в каком треде выполняется код?
- Принт текущего треда
  ```swift
	print("Current thread is \(Thread.current)")
	```
- Через брейкпоинты:
	![[how_to_check_which_thread_is_now.png]]


# Learning materials
##### Courses
- [Stepik.org. Курс по многопоточности](https://stepik.org/course/3278/syllabus)
##### Articles
- [Habr. Article about concurrency](https://habr.com/ru/post/320152/)
##### Videos:
- [Mad Brains video about concurrency foundation (46 mins)](https://youtu.be/JgUBBoRydoE)
- [Swift Developers playlist with 16 videos about multithreading in iOS](https://www.youtube.com/playlist?list=PLmTuDg46zmKCKjZqxXqJFjGXwzqGQi4D3)
- 