# Antipatterns
<p align="justify"><b>Антипаттерн</b> - это широко используемое решение с явно отрицательными результатами, несмотря на то, что есть решения на много лучше.</p>

## Антипаттерны в легаси
<p align="justify"><font>✔️ </font>MVC как massive view controller.</p>
<p align="justify"><font>✔️ </font>Плохая архитектура или отсутствии архитектуры вообще.</p>
<p align="justify"><font>✔️ </font>Повсюду singletons.</p>
<p align="justify"><font>✔️ </font>Множество сторонних frameworks, даже для решения простых вещей.</p>
<p align="justify"><font>✔️ </font>Копипаст кода.</p>

## Одиночество
<p align="justify">Любой глобальный обьект опасен для приложения.</p>
<p align="justify">Используй Одиночку только при наличии веских аргументов для наличия единственного экземпляра класса.</p>
<p align="justify"><font>✔️ </font>Нарушает принцип SRP.</p>
<p align="justify"><font>✔️ </font>Маскирует плохой дизайн.</p>
<p align="justify"><font>✔️ </font>Проблемы многопоточности.</p>
<p align="justify"><font>✔️ </font>Проблемы при unit-тестировании.</p>

## Ambient Context
<p align="justify">Это глобальные переменные среды выполнения приложения.</p>
<p align="justify">Значительно похож на синглтон, но с изменяемым состоянием. Он имеет общий глобальный экземпляр, который может быть заменен в процессе работы.</p>
<p align="justify"><font>✔️ </font>Так как в случае его наличия, все модули начинают от него зависеть, что в свою очередь приводит к сильному связыванию и отсутствию масштабирования.</p>
<p align="justify"><font>✔️ </font>Более того, теперь при изменении модуля, в котором расположен Context, а это обычно appDelegate, необходимо перекомпилировать весь проект, что определенно плохо.</p>
<p align="justify"><font>✔️ </font>В тестах мы можем подправить текущую дату легко, но это убивает напрочь и приводит к условиям гонок при попытке запустить тесты параллельно.</p>

## ServiceLocator
<p align="justify">Это очень неоднозначный паттерн проектирования. С одной стороны, именно с его появлением началось активное развитие DI контейнеров и практик инверсии управления.</p>
<p align="justify"><font>✔️ </font>Есть некий обьект, который знает как предоставляет все зависимости, которые могут потребоваться в приложении.</p>
<p align="justify"><font>✔️ </font>Плох тем, что делает невидимые зависимости.</p>
<p align="justify"><font>✔️ </font>Если забыть зарегистрировать обьект, то проект соберется и про сбой мы узнаем уже в рантайме - неизвестно когда.</p>
<p align="justify">Нам приходится в рантайме проверять соответствия типов и приводить их к нужному классу, а это признак нарушения принципа LSP.</p>

#### Если у класса много зависимостей, то это оказатель плохой архитектуры
* <p align="justify">3 зависимости - много.</p>
* <p align="justify">5 зависимостей - некрасиво.</p>
* <p align="justify">5+ зависимостей - <b>недопустимо</b>.</p>

## Сухой антипаттерн
<p align="justify"><font>✔️ </font>Суть заключается в том, что повсеместное использование принципа DRY, приводит к очень запутанному коду.</p>
<p align="justify"><font>✔️ </font>В угоду DRY, разработчик жертвует принципом SRP, и выделяет общие методы.</p>

## Антипаттерн Стрелка
<p align="justify">Что если у нас много асинхронных запросов и они должны выполняться друг за другом? Как обычно это решается с двумя запросами? А если их 5? 10?</p>

## Антипаттерны в ООП
<p align="justify"><font>✔️ </font>Базовый класс-утилита (BaseBean)</b></p>
<p align="justify">Наследование функциональности из класса-утилиты вместо делегирования кнему.</p>

<p align="justify"><font>✔️ </font>Анемичная модель (Anemic Domain Model)</b></p>
<p align="justify">Боязнь размещать логику в объектах предметной области.</p>

<p align="justify"><font>✔️ </font>Объектная клоака (Object cesspool)</b></p>
<p align="justify">Переиспользование обьектов, находящихся в непригодном для переиспользования состоянии.</p>

<p align="justify"><font>✔️ </font>Полтергейст (Poltergeist)</b></p>
<p align="justify">Обьекты, чьё единственное предназначение - передавать информацию другим объектам.</p>

<p align="justify"><font>✔️ </font>Одиночество (Singletonitis)</b></p>
<p align="justify">Неуместное использование паттерна Одиночка.</p>

<p align="justify"><font>✔️ </font>Каша из интерфейсов (Interface soup)</b></p>
<p align="justify">Обьединение нескольких интерфейсов, разделенных согласно принципу изоляции интерфейсов ISP, в один.</p>

<p align="justify"><font>✔️ </font>Висящие концы</b></p>
<p align="justify">Интерфейс, большинство методов которого бессмысленны и реализуются «пустышками».</p>

<p align="justify"><font>✔️ </font>Заглушка (Stub)</b></p>
<p align="justify">Попытка «натянуть» на обьект уже имеющийся малоподходящий по смыслу интерфейс, вместо создания нового.</p>

## Антипаттерны при написании кода
<p align="justify"><font>✔️ </font>Ненужная сложность (Accidental complexity)</p>
<p align="justify"><font>✔️ </font>Действие на расстоянии (Action at a distance)</p>
<p align="justify"><font>✔️ </font>Накопить и запустить (Accumulate and fire)</p>
<p align="justify"><font>✔️ </font>Слепая вера (Blind faith)</p>
<p align="justify"><font>✔️ </font>Лодочный якорь (Boat anchor)</p>
<p align="justify"><font>✔️ </font>Активное ожидание (Busy spin, busy waiting)</p>
<p align="justify"><font>✔️ </font>Кэширование ошибки (Caching failure)</p>
<p align="justify"><font>✔️ </font>Воняющий подгузник (The Diaper Pattern Stinks)</p>
<p align="justify"><font>✔️ </font>Проверка типа вместо интерфейса (Checking type instead of membership, Checking type instead of interface)</p>
<p align="justify"><font>✔️ </font>Таинственный код (Cryptic code)</p>
<p align="justify"><font>✔️ </font>Жёсткое кодирование (Hard code)</p>
<p align="justify"><font>✔️ </font>Мягкое кодирование (Soft code)</p>
<p align="justify"><font>✔️ </font>Поток лавы (Lava flow)</p>
<p align="justify"><font>✔️ </font>Волшебные числа (Magic numbers)</p>
<p align="justify"><font>✔️ </font>Спагетти-код (Spaghetti code)</p>
<p align="justify"><font>✔️ </font>Лазанья-код (Lasagnia code)</p>
<p align="justify"><font>✔️ </font>Равиоли-код (Ravioli code)</p>
<p align="justify"><font>✔️ </font>Мыльный пузырь (Soap bubble)</p>
<p align="justify"><font>✔️ </font>Мьютексный ад (Mutex hell)</p>
<p align="justify"><font>✔️ </font>(Мета-)шаблонный рак (Template cancer)</p>
