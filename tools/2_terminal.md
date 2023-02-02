# Terminal

## command
#### `Ctrl + A` переместиться в начало строки
#### `Ctrl + E` переместиться в конец строки
#### `Alt + F` пер`еместиться на слово вперед
#### `Alt + B` переместиться на слово назад
#### `Ctrl + Y` вставить из буфера
#### `Ctrl + K` удалить строку в буфер
#### `Ctrl + U` удалить текст в буфер от начало строки до курсора
#### `Ctrl + F` переместиться вперед
#### `Ctrl + B` переместиться назад
#### `Alt + D` удалить слово вперед
#### `Ctrl + backspace`	удалить слово назад
#### `Ctrl + H` удалить слева символ
#### `Ctrl + D` удалить справа символ
#### `Ctrl + -` отмена действий
#### `Alt + U` перевод слово в верхний регистр
#### `Alt + L` перевод слово в нижний регистр
#### `Alt + C` перевод первой буквы в слове в верхний регистр
#### `Сtrl + T` поменять местами 2 символа
#### `Alt + T` поменять местами 2 слова

## `ls`
#### `/bin` список содержимого
#### `-a` отображение скрытых файлов
#### `-F` отображение типа файлов
#### `-i` вывод дополнительной информации
#### `-l` более подробная форма вывода
#### `-m` вывод содержимого через запятые
#### `-R` список содержимого - рекурсивно
#### `-r` список содержимого - реверсивно
#### `-s` группировать по размеру файлов
#### `-t` группировать по дате и времени
#### `-x` группировать файлы ###
#### `--сolor` отображение в цвете
 
## `cd`		
#### `/bim` перейти в каталог
#### `..` выйти на уровень выше
#### `-` возврат в предыдущий каталог
#### `~` переход в домашний каталог

## `pwd` напечатать текущий каталог
## `touch` создать файл
## `mkdir` создать катало
## `mkdir -p` создать вложенные каталоги
## `cp` копировать файл
## `mv` переместить, переименовать файл
## `rm` удалить файл

## `rmdir` удалить каталог
#### `-f` без вопросов
#### `-R` рекурсивно
#### `-i` с предупреждением
#### `-v` с отображением

## su
#### `sudo -l user`	switch user и перейти в его окружение
#### `sudo passwd root` устаовка пароля для root
#### `adduser user` добавляем пользователя user
#### `deluser user` удаляем пользователя user
#### `-remove-home` удаляем пользователя user с его домашним каталогом
#### `Ctrl + D` выход из другого пользователя
 
## `man`
#### `-k` поиск функции
#### `-f` краткое описание функции
#### `-u` принудительное формирование описание о команде

## `apropos` поиск функции

## `whereis`
#### `-s` директория с исходными файлами
#### `-b` директория с исполняемым файлом
#### `-m` директория со справочной информацией

## `which` директория с исполняемым файлом

## `whatis`
#### `-w` поиск по командам

## объединение команд
#### `;` Command1 -> Command2
#### `&&` Command1 {true} -> Command2
#### `||` Command1 {false} -> Command2 {true} | Command1 {true} -> Command2 {false}
#### `()` mkdir $(date "+%Y-%m-%d")
#### `|` результат Command1 передан Command2
#### `>` записать данные в файл
#### `>>` записать данные в конец файла
#### `<` прочитать данные из файла

## `cat` вывод содержимого файл
#### `-n` с пронумерованными строками

## `less` постраничный вывод содержимого файл

## `head` вывод первых 10 строк файла
#### `-n` вывод первых n строк файла
#### `-c n` вывод первых n Kbyte

## `tail` вывод последних 10 строк файла
#### `-n` вывод последних n строк файла
#### `-c n` вывод последних n Kbyte

## `chgrp` изменяем группу для файлов и каталогов
## `chown	` изменяем владельца для файлов и каталогов
## `chmod 777` изменяем права доступа для файлов и каталогов
```
User	Group	Other
r-4		w-2		x-1
```

## `zip name.zip name` архивирование и сжатие
#### `-[0-9]` степень сжатия
#### `-P` установка пароля видно
#### `-e` установка пароля не видно 

## `unzip name.zip`
#### `-t` проверяет целостность архива
#### `-l` выводит информацию о файлах внутри
#### `gzip` архивирование и сжатие, с удалением файла
#### `gunzip`
#### `bzip2` архивирование и сжатие, с удалением файла
#### `bunzip2`

## `tar -cf` создает архив
#### `-zcvf` создает архив и сжимает --gzip
#### `-jcvf` создает архив и сжимает --bzip2
#### `-zvtf` проверка архива --gzip
#### `-jvtf`	проверка архива --bzip2
#### `-zxvf` разархивация --gzip
#### `-jxvf` разархивация --bzip2

## `locate` поиск файла
#### `-i` поиск файла без учета регистра
## `updatedb` обновлнение индекса файлов

## `grep` поиск в файле
#### `-w` поиск в файле - полное соответствие

## `find`	 поиск файла
#### `-name` поиск по имени
#### `-group` поиск по группе
#### `-user` поиск по владельцу
#### `-size` поиск по размеру
#### `!` отрицание

## `RPM` установка программ в RedHat
#### `yum install` установка
#### `yum remove` удаление
#### `yum update` обновление
#### `yum upgrade` обновление
			
## `DEB` установка программ в Debian
#### `apt install` установка
#### `apt remove` удаление
#### `apr --purge remove` удаление программы full
#### `apt clean` удаление установочных пакетов
#### `apt update` обновление
#### `-f install` установка зависимостей
#### `apt upgrade` обновление
#### `apt dist -upgrade` обновление OS

## .bash_profile
## .bashrc
## .bash_logout