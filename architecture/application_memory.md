# Application memory

## Состояния приложения
<p align="justify"><font>✔️ </font><b>Design time</b> — когда разработчик пишет код или проектирует его.</p>
<p align="justify"><font>✔️ </font><b>Compile time</b> — запускаем приложение на компиляцию сборку.</p>
<p align="justify"><font>✔️ </font><b>Run time</b> — выполнение приложения, ошибки в runtime- ошибки у пользователя.</p>

## Память
<p align="justify"><b>Память</b> - это очень длинная последовательность <b>бит</b>.</p>
<p align="justify">8 <b>бит</b> = 1 <b>байт</b></p>
<p align="justify">8 <b>байт</b> = 1 <b>слово</b></p>

## Адрес и указатель
<p align="justify">У каждого байта есть <b>адрес</b></p>
<p align="justify">За одно обращение к памяти, мы модем получить 8 байт сразу</p>
<p align="justify"><b>Указатель</b> - это переменная, в которой хранится адрес памяти другой переменной</p>

## Адресное пространство
<p align="justify">Адресное пространство приложения iOS состоит из четырех сегментов</p>
<p align="justify"><font>✔️ </font><b>Сегмент Инструкций</b> содержит машинные инструкции, которые создаются компилятором, когда мы запускаем сборку приложения.</p>
<p align="justify"><font>✔️ </font><b>Сегмент Данных</b> хранит статические переменные Swift, константы и метаданные типов.</p>
<p align="justify"><font>✔️ </font>В <b>куче</b> хранятся объекты, у которых есть время жизни.</p>
<p align="justify"><font>✔️ </font>В <b>стеке</b> хранятся временные данные – параметры при вызове метода и его локальные переменные.</p>

## Stack
<p align="justify"><b>Stack</b> — это память, выделенная для потока выполнения.</p>
<p align="justify">Он организован по принципу «последним пришёл — первым вышел» (<b>LIFO</b>).</p>

### Как работает stack
<p align="justify"><font>✔️ </font>В точке вызова в стек помещаются параметры функции и адрес возврата.</p>
<p align="justify"><font>✔️ </font>Вызываемая функция во время работы размещает в нем локальные переменные.</p>
<p align="justify"><font>✔️ </font>По завершении работы, функция очищает стек от своих локальных переменных и сохраняет результат.</p>
<p align="justify"><font>✔️ </font>Возврат из функции считывает из стека адрес возврата и выполняет переход по этому адресу.</p>
<p align="justify"><font>✔️ </font>Либо перед, либо сразу после возврата из функции стек очищается от параметров.</p>

## Heap
<p align="justify"><b>Неар</b> - это память, используемая для динамического выделения памяти.</p>
<p align="justify">Неар используется, если неизвестен объем данных необходимый во время выполнения или если нужно выделить большой объем данных.</p>

### Как работает heap
<p align="justify"><font>✔️ </font>Сохраняется в оперативной памяти компьютера так же, как и stack.</p>
<p align="justify"><font>✔️ </font>Может иметь фрагментацию, когда есть много распределений и освобождений.</p>
<p align="justify"><font>✔️ </font>Выделением и освобождением блоков памяти в hеар занимается ARC.</p>
<p align="justify"><font>✔️ </font>Чтобы получить данные в hеар первым делом требуется найти с помощью «оглавления».</p>

<p align="justify">B heap хранятся данные динамических размеров, например, список, в который можно добавлять произвольное количество элементов.</p>

## Stack vs Heap
1. <p align="justify">И <b>Stack</b> и <b>Неар</b> размещаются в оперативной памяти.</p>
2. <p align="justify">Много S<b>tack</b> и одна <b>Heap</b>.</p>
3. <p align="justify"><b>Неар</b> используется, если не известен объем данных необходимый во время выполнения или если нужно выделить большой объем данных, в ней размещаются объекты reference type.</p>
4. <p align="justify"><b>Stack</b> используется, для потока выполнения и в нём размещаются объекты value type, размер которых известен ещё на этапе компиляции.</p>
5. <p align="justify"><b>Hеар</b> и <b>Stack</b> растут навстречу друг другу.</p>
6. <p align="justify">Затраты на выделение и освобождение памяти в <b>Неар</b> намного больше.</p>

## value types & reference types
### value types
<p align="justify"><font>✔️ </font>Tuple</p>
<p align="justify"><font>✔️ </font>Dictionary</p>
<p align="justify"><font>✔️ </font>Enum</p>
<p align="justify"><font>✔️ </font>Set</p>
<p align="justify"><font>✔️ </font>Array</p>
<p align="justify"><font>✔️ </font>Double</p>
<p align="justify"><font>✔️ </font>Int</p>
<p align="justify"><font>✔️ </font>String</p>
<p align="justify"><font>✔️ </font>Struct</p>

### reference types
<p align="justify"><font>✔️ </font>Class</p>
<p align="justify"><font>✔️ </font>Function</p>
<p align="justify"><font>✔️ </font>Closure</p>

## Выбор между классом и структурой
### Как определить что использовать?
<p align="justify"><font>✔️ </font>Это просто данные?</p>
<p align="justify"><font>✔️ </font>У него есть какое-то поведение?</p>
<p align="justify"><font>✔️ </font>Имеет ли смысл в копировании этих данных?</p>

<p align="justify">Будте внимательнее при использовании структуры! Особенно, когда ее содержимое является <b>ССЫЛОЧНЫМ ТИПОМ</b></p>

### Как выбрать?
<p align="justify">Используйте <b>reference type</b>, когда:</p>
<p align="justify">1. Сравнение идентичности экземпляра с === имеет смысл.</p>
<p align="justify">2. Вы хотите создать общее изменяемое состояние.</p>

<p align="justify">Используйте <b>value type</b>, когда:</p>
<p align="justify">1. Сравнение данных экземпляра с == имеет смысл.</p>
<p align="justify">2. Вы хотите, чтобы копии имели независимое состояние.</p>
<p align="justify">3. Данные будут использоваться в коде в нескольких потоках.</p>

### Кто где размещается?
<p align="justify">Reference typ</p>
<p align="justify"><b>1. Reference typе</b> всегда размещаются в <b>hеар</b></p>

<p align="justify">Компилятор Swift может продвигать reference type для размещения в стеке, когда их размер фиксирован или время жизни может быть предсказано. Эта оптимизация происходит на этапе генерации SIL (Swift Intermediate Language)</p>

<p align="justify"><b>Value type</b> может размещаться в <b>hеар</b>, когда:</p>
<p align="justify">1. При реализации протокола</p>
<p align="justify">2. При смешивании <b>value type</b> и <b>reference type</b></p>
<p align="justify">3. <b>Generi</b>c c <b>value type</b></p>
<p align="justify">4. <b>Escaping closur</b>e captures</p>
<p align="justify">5. <b>Inout</b> аргумент</p>

<p align="justify">При смешивании <b>value type</b> и <b>reference type</b>.</p>
<p align="justify">Обычно ссылка на класс хранится в структуре, а структура является полем класса.</p>

## Memory Layout
### Управление памятью
<p align="justify"><font>✔️ </font><b>alloc</b> – для выделения памяти.</p>
<p align="justify"><font>✔️ </font><b>retain</b> – для удержания ссылки объекта.</p>
<p align="justify"><font>✔️ </font><b>release</b> – для освобождение ссылки объекта.</p>
<p align="justify"><font>✔️ </font><b>autorelease</b> – для пометки на автоматическое освобождение ссылки объекта.</p>
<p align="justify"><font>✔️ </font><b>dealloc</b> - освобождение памяти.</p>

## Struct Allocation
<p align="justify">Когда мы только объявляем нашу константу point1, то в стеке у нас выделяется память под это и указатель сдвигается.</p>
<p align="justify">Стоит создать вторую переменную point2, как в стеке у нас разместиться точная копия данных, а после присвоения point2.x = 5 данные изменяться.</p>

## Class Allocation
<p align="justify">Когда мы объявим нашу константу point1, в случае с классом, в куче будет найден подходящий по размеру блок памяти для размещения данных.</p>
<p align="justify">Далее данные будут записаны в кучу, а в стеке будет размещена ссылка на кучу, где лежит наш класс.</p>

## Жизненный цикл объекта
![](resources/objectLifeCycle.png)

## Memory Leaks
<p align="justify"><font>✔️ </font>Увеличивает объем памяти.</p>
<p align="justify"><font>✔️ </font>Нежелательные побочные эффекты.</p>
<p align="justify"><font>✔️ </font>Краши.</p>

## Memory Warnings
<p align="justify"><font>✔️ </font>Вызывая <b>applicationDidReceiveMemoryWarning(_:)</b> B <b>AppDelegate</b>.</p>
<p align="justify"><font>✔️ </font>Вызывая <b>didReceiveMemoryWarning()</b> в каждом из активных <b>UViewController</b>.</p>
<p align="justify"><font>✔️ </font>С помощью <b>didReceiveMemoryWarningNotification</b> во все зарегистрированные <b>observers</b>.</p>
<p align="justify"><font>✔️ </font>Каждая из <b>dispatch queues</b> получает <b>warning</b> типа <b>DISPATCH_SOURCE_TYPE_MEMORYPRESSURE</b>.</p>

<p align="justify">Если системе не хватает свободной памяти и она не может восстановить её, завершив приостановленные приложения, <b>UIKit</b> отправляет предупреждение о нехватке памяти работающим приложениям..</p>

## EXC BAD ACCESS
<p align="justify"><font>✔️ </font>Использование памяти, которая была освобождена.</p>
<p align="justify"><font>✔️ </font>Попытка записи за конец массива или буфера другого типа.</p>
<p align="justify"><font>✔️ </font>Использование указателя, который не был инициализирован.</p>
<p align="justify"><font>✔️ </font>Bad access по причине гонок в многопоточности.</p>

<p align="justify"></p>Всякий раз, когда вы встречаете EXC_BAD_ACCESS, это означает, что вы отправляете сообщение объекту, который уже был освобожден.</p>

<p align="justify"></p>Exception Type: EXC_BAD_ACCESS (SIGSEGV)</p>
<p align="justify"></p>Exception Subtype: KERN_INVALID_ADDRESS at 0x0000000000000000</p>


