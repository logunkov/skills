# Swift basic & OOP

### camelCase
### комментарий `//, /* */, /** */`

## базовые операторы
```swift
-a, !a
!, &&, ||
+, -, *, /, %
>, <, >=, <=, !=, ==
a ? b : c
name1 = name2 ?? name3
```

## data type
`nil` ничего  
`let` константа  
`var` переменная  
 
### Int
`Int8`	8 бит от -128 до 127  
`Int16` 16 бит от -32768 до 32767  
`Int32` 32 бита от -2147483648 до 2147483647  
`Int64` 64 бита от -9223372036854775808 до 9223372036854775807

### UInt
`UInt8` 8 бит от 0 до 255  
`UInt16` 16 бит от 0 до 65535  
`UInt32` 32 бита от 0 до 4294967295  
`UInt64` 64 бита от 0 до 18446744073709551615

### Float
`Float` 32-битное число с плавающей точкой, содержит до 6 чисел в дробной части  
`Double` 64-битное число с плавающей точкой, содержит до 15 чисел в дробной части  
`Float32` 32-битное число с плавающей точкой  
`Float64` 64-битное число с плавающей точкой  
`Float80` 80-битное число с плавающей точкой 

### Bool 
`true`  
`false`

### Character
### String

### система счисления
`0b` двоичное число  
`0o` восьмеричное число  
`0x` шестнадцатеричное число 

### работа со строкой
`\u{ }` unicode  
`\n` новая строка  
`\t` табуляция  
`\#` экранирование символа  
`""" """` многострочный текст

### свой тип данных
`typealias name = Int`

### узнать тип данных
`type(of:)`

## cycles

### while
```swift
repeat { } while x < 2
while x < 2 { }
```

### for
```swift
for _ in items
for item in items
for index in 1...5
for index in 1..<5
for (index, item) in enumurate(list)
```

### switch
```swift
switch name {
	case name2: print()
	default: print() }
	
switch name {
	case 1	: print()
	case 1...5: print()
	case 1..<5: print()
	case _	: print()
	case let n: print(n)
	case let n where n > 0 : print(n)
	case 1	: fallthrough
}
```
	
`continue` прекратить текущую итерацию и начать новую  
`break` остановить выполнениесоперации  
`fallthrough` продолжить операцию  
`return` отправить значение  
`throw` вывести ошибку

## conditions
### if
```swift
if num1 > num2 {
	print(num1)
} else if (num1 < num2 ) {
	print(num2)
} else {
	print("num1 = num2")
}
```

### guard
```swift
guard let name = name2 { }
```

## functions
```swift
func name { }
func name(name: String) -> String { }
func name(name: String = "name") -> String { }
func name(extName newNname: String) -> String { }
func name(name: Int...) -> Int { }
func name(_ name :Int...) -> Int { }
func name(newFunc: (Int, Int)) -> Int { }
	
func swapTwoInts (_ a: inout Int, _ b: inout Int) { }
swapTwoInts(&someInt, &anotherInt)
```

## collections

### array
```swift
let name: [Int] = [1,2,3]

let first = [Тип]()
let second: [Тип] = []
let third: Array<Тип> = Array()
let fourth: Array<Тип> = []
let fifth = Array<Тип>.init()
let sixth: [String] = ["Eggs", "Milk")
let seventh = ["Alex", "Sergey"]
```

### dictionary
```swift
let name = ["key1": "value1", "key2": "value2"]
let name: [String: String] = ["key1": "value1", "key2": "value2"]
let name: Dictionary[String: String] = [:]
let name: [String: String] = [:]
let name = [String: String]()
```

### set
```swift
let name: Set<Int> = [1,2,3]
```

`a.intersection(b)` пересечение  
`a.symmetricDifference(b)` симметрическая разность  
`a.union(b)` объединение  
`a.subtract(b)` разность  

`isSubset(of:)` все ли значения множества содержатся в указанном множестве  
`isSuperset(of:)` содержит ли множество все значения указанного множества  
`isStrictSubset(of:)` является ли множество подмножеством  
`isStrictSuperset(of:)` является ли множество надмножеством  
`isDisjoint(with:)` отсутствуют ли общие значения в двух множествах или нет

## Опциональные типы данных
### Int, Double, String, Bool и т.д.
```swift
let name = Optional(42)
let name = Optional<Int>(42)
let name = Int?(42)
```

### явно опциональная строка
```swift
let name: Int? = 42
let name: Int = name!
```

### неявно опциональная строка
```swift
let name: Int! = 42
let name: Int = name
```

## closure
```swift
name = sort(names, {s1:String, s2:String) -> Bool in return s1 > s2})
name = sort(names, {s1, s2 in return s1 > s2})
name = sort(names, {s1, s2 in s1 > s2})
name = sort(names, {$0 > $1})
name = sort(names, >)
name = sort(names) {$0 > $1}

func makeIncrementor(forIncrement amount:Int) -> () -> Int {
let runningTotal = 0
func incrementor() -> Int {
	runningTotal += amount
	return runningTotal}
	return incrementor
}
```

`@escaping` замыкание, переданное как параметр в функцию и вызываемое после выполнения функций  
`@autoclosure` замыкание, автоматически создаваемое для оборачивания выражения, которое передается как параметр в функцию

# OOP
## области видимости
`open` доступ из других модулей  
`public` доступ к публичным объектам других модулей  
`internal` доступ внутри модуля  
`fileprivate` доступ к свойствам и методам внутри класса  
`private` доступ к свойствам и методам внутри класса ограничен

## enum
```swift
enum Name {case North}
let name2 = name.North
name2 =.North
	
enum Planet: String {case Mercury, Venus}
enum Planet: Int {case Mercury = 1, Venus}
```

### связанные значения перечислений
```swift
enum Barcode {
case UPCA (Int, Int, Int)
case QRCode (String)
```

### исходные значения перечислений
```swift
enum Name:Character {case Tab = "\t"}
```

### рекурсивные перечисления
```swift
enum Name { indirect case name2(name)}
```

## protocol { }

## struct { }
`struct` передает данные

## class { }
`class` передает ссылку и класс может содержать в себе struct

### properties:   
`lazy` ленивые свойства  
`mutating` изменить  
`private` приватные свойства, объект не доступен  
`private(set)` приватные свойства, объект доступен на чтение  
`static` статические свойства  
`unowned` бесхозная ссылка  
`weak` слабая ссылка  

### methods:
`convenience` вспомогательный  
`mutating` изменить  
`override` переопределять  
`required` требует инициализации  
`throws` генерировать ошибку  

### вычисляемые свойства
`get` вызывается перед тем как получить  
`set` вызывается перед тем как установить  

### инициализаторы
`init` вызывает перел инициализацией  
`deinit` вызывает после инициализации  

### наблюдатели свойства
`willSet` вызывается перед присваиванием  
`didSet` вызывается после присваивания  

### subscripts
```swift
struct TimesTable {
	let multiplier: Int
	subscript(index: Int) -> Int {
		return multiplier * index
	}
}

let threeTimesTable = TimesTable(multiplier: 3)
print("6 * 3 = \(threeTimesTable[6])")
```

### inheritance
```swift
class Vehicle { }
class Bicycle: Vehicle { }
```

### extensions
#### вычисляемые свойства
```swift
extension Int {let km {return self * 1000}}
```

#### инициализаторы в расширениях
```swift
class name { }
extension name {init{ }}
```

#### методы в расширениях
```swift
extension Int {func name() { }}
```

#### сабскрипты
```swift
extension Int {subscript() { }}
```

#### опциональные требования протокола
```swift
@objc protocol name {@objc optional let name2}
```

#### errors
```swift
enum name: Error { }
func name() throws { }
```

#### error handling
```swift
func name() throws { }
do {try name() } catch { }
let x = try? name()
```