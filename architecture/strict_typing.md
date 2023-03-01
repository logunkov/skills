# Strict typing
<p align="justify">Используем компилятор и строгую типизацию для защиты инвариантов</p>

<p align="justify">Допустим нам надо авторизоваться и метод принимает на вход 2 параметра - логин и пароль. И как мы сделаем это? Мы с вероятностью в 90% укажем, что оба параметра у нас String. И теперь метод должен сам разобраться с тем, передели ему логин в поле логина и пароль в поле пароли.</p>

```swift
func auth(login: String, pass: String) -> Bool {
	login == "123@abc.ru" && pass == "12345"
}
```

## Simple Wrapper
<p align="justify">Допустим, у нас есть замыкание и там $0 и $1. Теперь элементарно перепутать логин и пароль местами, ведь они оба одного типа. Но этого не случиться, если мы будем использовать <b>Wrapper</b>.</p>

```swift
struct Wrapper {
	let rawValue: String
}
```
<p align="justify">Теперь мы никогда не перепутаем их местами! Это касается и WareID -- UserID -- Barcode -- BarcodeID. Ситуаций масса и компилятор проверит наши типы и просто не даст нам запутаться!</p>

## Parsed Wrapper
<p align="justify">Отлично, но если нам недостаточно просто хранить данные, если у нас есть некоторые условия, которым эти данные должны удовлетворять? Тогда мы можем сделать обертку с парсером. Предположим, что пароль не менее 5 символов.</p>

```swift
struct Pass {
	let rawValue: String
	
	private init(rawValue: String) {
		self.rawValue = rawValue
	}
	
	enum ParseError: Error {
		case tooShort
	}
	
	static func parse(_ rawValue: String) -> Result<Pass, ParseError> {
		if rawValue.count > 4 {
			return .success(Pass(rawValue: rawValue))
		}
		
		return .failure(ParseError.tooShort)
	}
}
```

<p align="justify">Тут для реализации нужно закрыть init и сделать статичный метод parse, который нам создаст наш экземпляр класса, но обратите внимание, что мы вернем Result и, избавляясь от Boolean Blindness или Optional Blindness, теперь сможем узнать что пошло не так.</p>
<p align="justify">Теперь у нас есть гарантия того, что логин с паролем не перепутают и что внутри этих типов валидные данные!</p>

## NonEmpty
<p align="justify">Массив, который не может быть пустым.</p>
<p align="justify">Любой массив может быть пустым, но что если у нас массив предоставляет список чего-либо, что обязательно должно присутствовать... Например, множественный выбор пользователя.</p>
<p align="justify">Тогда можно воспользоваться следующей концепцией:</p>

```swift
struct NonEmptyArray<T> {
	let head: T
	let tail: [T]
	
	var all: [T] {
		[head] + tail
	}
}
```

## Algebraic Data Types
<p align="justify">Алгебраический тип данных — в информатике наиболее общий составной тип, представляющий собой тип-сумму из типов-произведений.</p>

### Combination
<p align="justify">Тип произведения, объединяющий данные. Тип-произведений, позволяет объединить данные под общий знаменатель.</p>

```swift
struct Email {}
struct Password {}

struct TrueCredentials {
	let email: Email
	let password: Password
}
```

### Sum
<p align="justify">Тип-сумма. Тип позволяющий выбирать вариант из данных. Его можно сделать на основе перечислений.</p>

```swift
struct AnonymousUser {}

struct SignedInUser {
	let email: Email
	let password: Password
}

enum User {
	case anonynous
	case signedIn(SignedInUser)
}
```

<p align="justify">Мы можем на этого User навесить призму и пользоваться полями AnonymousUser и SignedInUser, будто это структура, без боязни, что они пересекутся и будут единовременно иметь значение.</p>

## Tags
<p align="justify">Но что если нам нужно какое-то быстрое решение, в котором 2 поля одинакового типа стали бы несовместимыми? Например ID, ответ -- Тэги.</p>

```swift
struct NormalTask {
	let ID: ID<NormalTask>
	let title: String
	var isDone: Bool
}

struct ID<Tag> {
	let rawValue: String
	
	init(_ rawValue: String) {
		self.rawValue = rawValue
	}
}
```
<p align="justify">Мы вводим фантомный дженерик, который нигде не участвует и никак не влияет ни на размер приложение, ни на его работу, но позволяет компилятору сличать переданные типы. Теперь на наш ID можно повесить тэг, кому этот ID принадлежит. Ну или более универсально, с возможностью указать тип для которого навешиваем тэг.</p>

## Prism
<p align="justify">Призма -- это такая сущность, которая позволяет из enum, не теряя его преимуществ получить удобства struct. Как это работает? Мы добавить вычисляемые поля для нашего enum и вернем необходимую нам информацию.</p>
<p align="justify">Не очень удобно в прошлый раз было достать после парсинга значения логина и пароля, но мы знаем, как реализован Result в Swift, а потому сделаем призму:</p>

```swift
extension Result {
	var error: Failure? {
		guard case let .failure(error) = self else { return nil }
		return error
	}
	
	var value: Success? {
		guard case let .success(value) = self else { return nil }
		return value
	}
}
```

<p align="justify">Enum позволяет нам защищать свой инвариант, а призма добавляет удобства к доступу хранимых переменных.</p>

```swift
let login = Login.parse("1234u.ru")
let pass = Pass.parse("123456")

if login.error == nil {
	print(login.value!)
}
	
if let login = login.value, let pass = pass.value {
	auth(login: login, pass: pass)
} else {
	print("\(login.error)\n\(pass.error)")
}
```

<p align="justify">Теперь доступ к полям как к простому опционалу, что в разы чище и понятнее.</p>

## Witness
<p align="justify">Свидетель времени выполнения - это значение, которое каким-то образом содержит некоторую информацию на уровне типов, связанную с полиморфным значением, и делает ее доступной для процесса проверки типов.
Это пустая структура и параметр <b>T</b> от дженерика никак не используется.</p>

```swift
struct Witness<T>: Equatable {}
```

<p align="justify">Но он позволяет засвидетельствовать то, что передан именно тот тип данных, который нам требуется. Он вообще нигде и никак не используется и нужен только для того, чтобы компилятор не дал нам во время компиляции перепутать используемые данные или вызываемые методы, которым данные не нужны.</p>

```swift
class VC1: UIViewController {}
class VC2: UIViewController {}

// Мы добавляем свидетеля, указывая, что сцена будет работать только с VC1.
// Сама VC1, нам не нужна, потому у нас параметр как _
func showScene1(_: Witness<VC1>) {} //showScene1()
// Сцена будет работать только с VC2.
func showScene2(_: Witness<VC2>) {} //showScene2()
```

<p align="justify">Укажем State для приложения, который показывает либо scene1, либо scene2. Чтобы нам зафиксировать VC с которым будут работать сцены, сохраним их хранимых переменных.</p>

```swift
enum State {
// Сразу проинициализируем пустым свидетелем, чтобы дальше при работе не касаться этого дела
	case scene1(Witness<VC1> = Witness())
	case scene2(Witness<VC2> = Witness())
}

let state = State.scene1()

switch state {
case .scene1(let witness):
	showScene2(witness)
case .scene2(let witness):
	showScene2(witness)
}
```

<p align="justify">Мы не можем теперь вызвать метод, который нарушает наше свидетельство, тем самым предохраняем нашу BL и защизаем инвариант. Это даже не надо покрывать тестами. Компилятор сам проверить это для нас.</p>