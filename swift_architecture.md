# Swift architecture

## MVC (Model View Controller)

`Model` Notify ---> <--- Update `Controller` Update ---> <--- User Action `View`

### Рекомандации по созданию представлений
* Используйте поставляемые со стандартным SDK классы view controllers
* Создавайте view controller максимально автономным
* Не храните во view controller данные
* Используйте view controller для реакции на внешние _объекты_