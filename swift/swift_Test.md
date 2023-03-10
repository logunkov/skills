# Swift Test

## SUT - System (Subject) Under Test
<p align="justify">Все наши тесты должны быть:</p>
<p align="justify"><font>✔️ </font>Быть атомарными.</p>
<p align="justify"><font>✔️ </font>Быть достоверными.</p>
<p align="justify"><font>✔️ </font>Не зависеть от окружения.</p>
<p align="justify"><font>✔️ </font>Легко поддерживаться.</p>
<p align="justify"><font>✔️ </font>Легко читаться.</p>
<p align="justify"><font>✔️ </font>Соблюдать единую конвенцию именования.</p>
<p align="justify"><font>✔️ </font>Запускаться регулярно в автоматическом режиме.</p>


## Именование тестов
#### func test_login_withValidData_shouldSaveLoggedinStatusOnSuccess()

1. <p align="justify"><b>test</b> - начало тестовой функции.</p>
2. <p align="justify"><b>login</b> - тестируемая функция.</p>
3. <p align="justify"><b>with ValidData -</b> - параметры тестирования (если нужны).</p>
4. <p align="justify"><b>shouldSaveLoggedinStatusOnSuccess</b> - ожидаемый результат теста.</p>

## Объявление тестовых модулей

```swift
testable import MyModuleUnderTes
```

<p align="justify">Импорт модулей/подмодулей, а также отдельных объявлений (<b>class</b> , <b>enum</b>, <b>func</b> , <b>struct</b> , <b>var</b>) не тестируется.</p>
<p align="justify">Тестируются модули, импортированные с помощью <b>@testable</b> (присутствуют только в тестовых источниках).</p>
<p align="justify">Импорт тестируемого модуля располагается после остальных необходимых импортов.</p>

## Arrange - Act - Assert паттерн
<p align="justify"><b>Arrange (настройка)</b> - в этом блоке кода мы настраиваем тестовое окружение тестируемого юнита.</p>
<p align="justify"><b>Act (выполнение)</b> - выполнение или вызов тестируемого сценария.</p>
<p align="justify"><b>Assert (проверка)</b> - проверка того, что тестируемый вызов ведет себя определенным образом.</p>

```swift
// Arrange
let sut = makeSUT()
let taskTypes = TaskType.Inventory.allCases
let notificationSoundName = UNNotificationSoundName(rawValue: "taskNotificationSound.caf")

//Act
let result: [Bool] = taskTypes.map {
	sut.makeNotificationSoundName(taskType: TaskType.inventory($0)) = notificationSoundName
}

//Assert
result.forEach { XCTAssertTrue($0, "Ошибка создания звука задания для Inventory") }
```

## Given - When - Then паттерн
<p align="justify"><b>Given (настройка)</b> - в этом блоке кода мы настраиваем тестовое окружение тестируемого нита.</p>
<p align="justify"><b>When (действия)</b> - выполнение или вызов тестируемого сценария.</p>
<p align="justify"><b>Then (результат)</b> - проверка того, что тестируемый вызов ведет себя определенным образом.</p>

```swift
func test_loadview_shouldHaveCorrectTitle() {

	// given
	let sut = makesUT()

	// when 
	sut.loadViewIfNeeded)

	// Then
	XCTAssertEqual(
		sut.title,
		L10n.SearchViewController.title,
		"установлен неверный заголовок"
	)
}
```

## TDD
<p align="justify">Это подход к разработке на основе тестов  .</p>
<p align="justify">❌ Сначала вы пишите тест.</p>
<p align="justify">✅ Пишите достаточный код для того, чтобы тест был пройден.</p>
<p align="justify">🆗 Проверьте, есть ли код, который нужно рефакторить.</p>


## Unit Testing
<p align="justify">Представляет из себя тестовый метод созданный для тестирования какого то действия, выполняемого другим методом.</p>
<p align="justify"><b>Fast</b> - тесты должны выполняться быстро  .</p>
<p align="justify"><b>Independent/Isolated</b> - тесты должны быть независимы и изолированы друг от друга.</p>
<p align="justify"><b>Repeatable</b> - тесты должны выдавать одни и те же результаты при каждом запуске.</p>
<p align="justify"><b>Self-validating</b> - тесты должны быть полностью автоматизированы. Результат тестирования должен быть либо успешным либо провальным  .</p>
<p align="justify"><b>Timely</b> - в идеале тесты должны быть написаны до написания тестируемого продакшн кода (разработка на основе тестов: TDD) .</p>


## Integration Tests
<p align="justify">Процесс тестирования связей между различными модулями проекта.</p>

## Performance Tests
<p align="justify">Тесты на производительность, позволяют замерять время работы алгоритмов.</p>

## UI Testing
<p align="justify">Тестирование интерфейсов.</p>

## Test Doubles

### Stub
a. **Stub**
<p align="justify">Это заглушки предоставляют готовые ответы на вызовы.</p>
<p align="justify">Стабы предназначены для входящих взаимодействий (запросов) - взаимодействий, которые не оставляют побочных эффектов в зависимости.</p>

```swift
enum TaskStub {

	static var doingTask = Task {
		id: "20230101",
		code: "0049566-03",
		content: "",
		createTime: "2023-01-01701:01:01.000Z",
		operationDate: Date()
	)
}
```

b. **Dummy**
<p align="justify">Никогда не содержат ни какой логики! Обычно они нужны просто для заполнения списков параметров конструктора..</p>

```swift
class IdentificationMarkServiceDummy: IdentificationMarkService {
	func gettinDataAndWare(from datamatrix: BarcodeModel) -> IdentificationMarkDataModel? {
		nil
	}
	
	func getMarkData(ware: WareInfoModel, completion: @escaping ((IdentificationMarkPrintModel?) -> Void)) {
	}
	
	func checkBarcode(barcode: BarcodeModel, playSound: @escaping ((SoundMelody) -> Void), completion: @escaping (Result<(ware: WareInfoModel?, status: IdentificationMarkService.StickerStatus), IdentificationMarkService.ServiceError>) -> Void) {
	}
	
	func processStatus(ware: WareInfoModel, status: IdentificationMarkService.StickerStatus, completion: @escaping ((Bool) -> Void)) {
	}
```

c. **Fake**
<p align="justify">Фальшивые обьекты, содержащие упрощенную логику, не годную для продакшена.</p>

```swift
class HardwareHandlerFake: IHardwareScanHandler {

	var resultBarcode: Barcode?
	var isConnected = false

	func connect() {
		isConnected = true
	}
	
	func connected() {
	isConnected = true
	}
	
	func disconnected(){
	isConnected = false
	}
	
	func hardwareScanned(barcode: String?, type: BarcodeType) {
		resultBarcode: Barcode(code: barcode, type: type)
	}
}
```

### Mock
a. **Mock**
<p align="justify"><b>Mock</b> - очень похож на <b>Stub</b>, но основан на взаимодействии, а не на состоянии.</p>
<p align="justify">Это означает, что вы не ожидаете, что <b>Моск</b> вернет какое-то значение, но предполагаете, что выполняется определенный порядок вызовов методов.</p>
<p align="justify">Моки предназначены для исходящих взаимодействий (команд) - взаимодействий, которые оставляют побочный эффект в зависимости.</p>

b. **Spy**
<p align="justify">Это фрагмент кода, который перехватывает некоторые вызовы реального кода, позволяя вам проверять вызовы без замены всего исходного обьекта.</p>

```swift
class UITableViewSpy: UITableView {
	var deselectRowCalled = false
	var cellReuseIdentifier: String!
	override func deselectRow(at indexPath: IndexPath, animated: Bool) {
		deselectRowCalled = true
		super.deselectRow(at: indexPath, animated: animated)
	}
}
```

```swift
func test_didSelectRowAt_callsDeselectRow() {
	let sut = makesUT()
	let tableView = makeTableViewMock(dataSourceAndDelegate: sut)
	
	sut.tableView(tableView, didSelectRowAt: IndexPath(row: 0, section: 0))
	XCTAssert (tableView.deselectRowCalled, "deselectRow не был вызван")
}
```

```swift
func makeTableViewMock(
dataSourceAndDelegate: UITableViewDataSource & UITableViewDelegate) -> UITableViewSpy {
	let tableView = UITableViewSpy()
	tableView.frame = CGRect(x: 0, y: 0, width: 500, height: 500)
	tableView.dataSource = datasourceAndDelegate
	tableView.delegate = dataSourceAndDelegate
	tableView.register(
		WareDescriptionTableViewCellMock.self,
		forCellReuseIdentifier: makeCellReuseIdentifier()
	)
	tableView. register(
	TaskSectionViewMock.self,
	forHeaderFooterViewReuseIdentifier: makeHeaderFooterReuseIdentifier()
	)
	tableView.cellReuseIdentifier = makeCellReuseIdentifier()
	return tableView
}
```

## Mocks vs Stubs
### Mock [mock, spy]
* Mock - это про взаимодействие.
* Моск отвечает на вопрос Как достигли результата?
* Mock может провалить тест.

### Stub [stub, dummy, fake]
* Stub - это про состояние.
* Stub отвечает на вопрос: Какой результат?
* Stub не проваливают ваши тесты.

<p align="justify">Нельзя мокать саму тестируемую систему (SUT), так как это бессмысленно.</p>

## Жизненный цикл тестов

### Жизненный цикл тестов со Stub
- Setup - подготовка обьекта SUT и его Stub.
- Exercise - проверка функциональности.
- Verify state - проверка состояния объекта.
- Teardown - очистка ресурсов.

```swift
func test_saveAndRestoreTask_taskShouldBeRestored() {
	let content = StoredTaskContent(id: "ID", content: Data())
	
	sut.saveTaskContent(coltent)
	let restoredTaskContent = sut.restoreTaskContent(forTaskID: "ID0")

	XCTAssertNotNil(restoredTaskContent, "Ошибка восстановления задания.")
	XCTAssertEqual (content, restoredTaskContent, "Данные в восстановленном задании отличаются от сохраненных.")
}
```

### Жизненный цикл тестов с Mock
- Setup - подготовка объекта SUT.
- **Setup expectations - Подготовка ожиданий в Моск.**
- Exercise - проверка функциональности.
- **Verify expectations - проверка, что в Моск были вызваны правильные методы.**
- Verify state - проверка состояния объекта.
- Teardown - очистка ресурсов.

```swift
func testAddPortion) throws {
	let sut - getManager (withResponseBody: String?.none)
	let completionExpectation = expectation (description: "Обработка асинхронного запроса")
	let completion = { (result: Result‹Void, IPCClientError>) in
		do {
		try result.get()
		} catch
		XCTFail("Ошибка при получении ответа")
		completionExpectation.fulfill()
	}
	try sut.addPortion(
		for: "ware",
		portionId: 123,
		LineCount: 1,
		size: 1,
		completion: completion
	)
	waitforExpectations(timeout: 10)
}
```