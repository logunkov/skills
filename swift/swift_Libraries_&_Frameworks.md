# Libraries and Frameworks

> A **module** is a single unit of code distribution - a framework or application that's built and shipped as a single unit and that can be imported by another module with Swift's **import** keyword. (c) Apple

## Цели вынесения кода во framework
<p align="justify"><font>✔️ </font>Переиспользование модуля в разных приложениях.</p>
<p align="justify"><font>✔️ </font>Изолирование кода модуля от протекания в него кода приложения.</p>
<p align="justify"><font>✔️ </font>Упрощение процесса разработки.</p>
<p align="justify"><font>✔️ </font>Уменьшение времени выполнения тестов.</p>
<p align="justify"><font>✔️ </font>Параллельная разработка модулей.</p>

## Libraries
<p align="justify"><font>✔️ </font>Библиотека может быть использована просто как набор подпрограмм близкой функциональности, не влияя на архитектуру.</p>
<p align="justify"><font>✔️ </font>Статические библиотеки могут содержат только код, они не могут содержать ресурсы.</p>
<p align="justify"><font>✔️ </font>Библиотеки могут быть <b>Dynamic Library</b> и <b>Static Library</b>.</p>

## Frameworks
<p align="justify"><font>✔️ </font>Фреймворк диктует правила построения архитектуры приложения.</p>
<p align="justify"><font>✔️ </font>Фреймворк это фактически папка, которая позволяет делиться кодом и может содержать в себе ресурсы.</p>
<p align="justify"><font>✔️ </font>Фреймворками проще управлять, чем библиотеками.</p>
<p align="justify"><font>✔️ </font>Фрейморки внутри себя содержат библиотеки.</p>

## Static Library
<p align="justify"><font>✔️ </font>Статические библиотеки связаны во время компиляции статическим компоновщиком.</p>
<p align="justify"><font>✔️ </font>Они могут быть быстрее, особенно заметно при старте приложения, так как мы пропускаем стадию динамической компоновки.</p>
<p align="justify"><font>✔️ </font>Не нужно встраивать статические библиотеки, так как они уже связаны во время компиляции и находятся внутри кода твоего приложения.</p>
<p align="justify"><font>✔️ </font>Но если твой фреймворк со статической библиотекой содержит ресурсы, тебе придется его встроить, чтобы иметь доступ к ресурсам.</p>

## Dynamic Library
<p align="justify"><font>✔️ </font>Dynamic Library связаны в runtime с использованием динамического компоновщика.</p>
<p align="justify"><font>✔️ </font>Dynamic Library, представляют собой скомпилированные библиотеки, которые загружаются во время выполнения.</p>
<p align="justify"><font>✔️ </font>Экономят на размере приложения тем, что можно не встраивать системные библиотеки.</p>
<p align="justify"><font>✔️ </font>Если не встроить свою Dynamic Library, то приложение упадет, так как не найдет зависимость.</p>

## Режимовы встраивания frameworks
<p align="justify"><font>✔️ </font>Static Library</p>
<p align="justify"><font>✔️ </font>Dynamic Library</p>
<p align="justify"><font>✔️ </font>Embedded Static Library</p>
<p align="justify"><font>✔️ </font>Embedded Dynamic Library</p>

## Менеджеры зависимостей
<p align="justify"><font>✔️ </font>Cocoa Pods</p>
<p align="justify"><font>✔️ </font>Carthage</p>
<p align="justify"><font>✔️ </font>Swift Package Manager</p>

## CocoaPods
<p align="justify"><font>✔️ </font>Библиотеки должны создавать, обновлять и содержать Podspec файлы.</p>
<p align="justify"><font>✔️ </font>При добавлении в проект «pod», CocoaPods создает новый Xcde проект с таргетом для каждого отдельного pod.</p>
<p align="justify"><font>✔️ </font>Необходимо использовать workspace и полагаться, что CocoaPods проект работает правильно.</p>
<p align="justify"><font>✔️ </font>Хранилище данных Podspecs централизовано, значит могут быть проблемы, если оно исчезло или стало недоступным.</p>
<p align="justify"><font>✔️ </font>В команде нужно работать с CocoaPods только с Bundler.</p>

## Carthage
<p align="justify"><font>✔️ </font>Carthage не изменяет ваш проект и не вынуждает Вас использовать workspace.</p>
<p align="justify"><font>✔️ </font>Нет необходимости Podspecs или централизованного хранилища данных.</p>
<p align="justify"><font>✔️ </font>Ваш проект может быть разработан как фреймворк, он может быть использован с Carthage. Он использует существующую информацию прямо из Git и Xcode.</p>
<p align="justify"><font>✔️ </font>Carthage не делает ничего волшебного; вы всегда контролируете ситуацию. Вручную добавляете зависимости в проект и Carthage, извлекаете и создаете их.</p>

## Swift Package Manager
<p align="justify"><font>✔️ </font>Нативность и интеграция в экосистему.</p>
<p align="justify"><font>✔️ </font>В отличие от <b>Cocoapods</b>, больше не обязательно иметь <b>workspace</b> для работы над проектом с зависимостями.</p>
<p align="justify"><font>✔️ </font>Добавив новую зависимость, не нужно делать /b>pod install</b> и пересобирать весь проект.</p>
<p align="justify"><font>✔️ </font>Удобно использовать локальные зависимости: не меняется структура папок, быстрее пересобирается.</p>
<p align="justify"><font>✔️ </font>SPM не меняет структуру файла проекта, как это делает <b>Cocoapods</b>, не требует зависимости от <b>Ruby</b>.</p>
<p align="justify"><font>✔️ </font>Не нужно создавать проект Ехатре для каждого репозитория: Ходе умеет открывать Package.swift файл как проект.</p>

<!---
## Cheatsheet Cocoapods
## Cheatsheet Carthage
## Cheatsheet XCFramework
## Cheatsheet Bundler
## Cheatsheet Artifactory
--->