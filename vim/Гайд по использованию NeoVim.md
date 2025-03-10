# Гайд по использованию **NeoVim**

## Список команд
``` 
nvim    команда для открытия NeoVim
nvim demo.md  команда для создания файла с заданным именем и расширением

```

**Команда для установки Lua**
```
sudo apt install lua5.4
```
## Основные режимы

Normal Mode (Нормальный режим)
Стандартный режим при открытии документа, используется для перемещения по тексту без редактирования.

Insert Mode (Режим вставки)
Переход из Normal Mode с помощью клавиш a или i.
Позволяет вводить текст.
Возврат в Normal Mode через клавишу Esc.

CMD Mode (Командный режим)
Активируется с помощью двоеточия :.
Используется для введения команд, например, сохранения и выхода.
Команда для выхода без сохранения: :cq.

## Перемещение по **NeoVim** в режиме NormalMode

### Базовое перемещение

j - перемещение вниз  
k - перемещение вверх  
h - перемещение влево  
l - перемещение вправо  

w - перемещение на начало следующего слова  
b - перемещение до начала предыдущего слова  
shift + b - перемещение до начала предыдущего слова с игнорированием символов  
shift + w - перемещение на начало следующего слова с игнорированием символов  
e - переход к концу текущего слова  
shift + e - переход к концу слова с игнорированием символов  

### Комбинации передвижений

Для комбинаций можно испольовать такую схему:
{operator} + {count} + {Motion}
Пример: d2w

Основные комбинации  
d: удаляет текст и остается в нормальном режиме.  
c: удаляет текст и переходит в режим Insert.  

Работа с операторами и motion  
dw: удалить слово.  
dd: удалить строку.  
db: удалить назад до начала слова.  
de: удалить до конца слова.  

Примеры комбинирования  
d2w: удалить два слова.  
d$: удалить до конца строки.  
d10j: удалить 10 строк вниз.  

Переходы в режим Insert  
cw: удалить слово и сразу перейти в режим Insert.  
cb: удалить назад до начала слова и перейти в режим Insert.  

Упрощенные операции удаления  
Используемые команды для удаления могут быть комбинированы с count (числом удаляемых объектов) и motion (движением курсора), что позволяет эффективно удалять большие участки текста.  

Практические примеры в nvim  
Переход к началу слова: b  
Удаление слова: dw  
Удаление строки: dd  
Восстановление предыдущего состояния: u (undo)  

**Inside и Around**

Основные команды  
d – удалить  
i (inside) – внутри границ  
a (around) – вокруг границ  
w – слово  
t – тег  

Примеры использования  

Удаление слов  
Задача: Удалить слово внутри текста.  
Способ: Позиционируемся в середине слова, используем d  
i  
w.  
Пример: purple school → Позиция внутри слова → Команда: diw.  

Удаление внутри кавычек  
Задача: Удалить текст внутри кавычек.  
Способ: Позиционируемся внутри кавычек, используем d  
i (inside) + вид кавычек.  
Пример: "example" → Команда: di".  

Удаление внутри тегов  
Задача: Удалить содержимое внутри HTML тега.  
Способ: Позиционируемся в начале тега, используем d  
i  
t.  
Пример: <title>Школа разработки Purple School</title> → Команда: dit.  

Удаление внутри фигурных скобок  
Задача: Удалить содержимое внутри фигурных скобок.  
Способ: Позиционируемся внутри фигурных скобок, используем d  
i  
{.  
Пример: { button: sample } → Команда: di{.  

**Копирование и вставка**

Основные моменты:  
Удаление текста и регистры:  
При удалении текста в Vim с помощью команды d (например, dd для удаления строки), текст автоматически попадает в регистр, который действует как временное хранилище или буфер обмена.  
В зависимости от настроек, регистр может интегрироваться с буфером обмена вашей операционной системы.  

Вставка текста:  
Команда P вставляет текст из регистра ниже текущей строки.  
Команда Shift + P вставляет текст выше текущей строки.  
Эти команды помогают вернуть удаленный или скопированный текст в нужное место.  
 
Копирование текста:  
Команда y копирует текст, аналогично удалению, но не удаляя его. Этот процесс в Vim называется "yanking".  
yy копирует всю строку.  
Можно использовать комбинации, аналогичные удалению, для копирования отдельных частей текста (например, yi" для копирования текста внутри кавычек).  
 
Модификаторы движения и копирование:  
Они работают аналогично тем, что используются при удалении:  
yw копирует слово.  
y$ копирует текст до конца строки.  
yi<тег> копирует текст внутри HTML-тега. 

**Регистры**

```
:registers - отображает список регистров
```

Дефолтный регистр: Место, куда текст попадает по умолчанию при копировании.  
Именованные регистры: Регистры с уникальными именами или номерами для хранения различных наборов данных.  

Копирование текста  
Команда: "<регистр>y<текст> (e.g. "2yiw  копировать слово в регистр 2)  
Вставка текста  
Команда: "<регистр>p (e.g. "2p вставить текст из регистра 2)  

*Шаги для работы с регистрами*

Копирование текста в дефолтный регистр  
Пример: yiw (копирование слова)  
По умолчанию текст попадет в дефолтный регистр.  
Копирование текста в именованный регистр  
Пример: "2yiw  
Текст копируется в регистр 2, не затирая данные в дефолтном регистре.  
Вставка текста из дефолтного регистра  
Пример: p  
Текст вставляется из дефолтного регистра.  
Вставка текста из именованного регистра  
Пример: "2p  
Текст вставляется из регистра 2.  

**Замена текста**

Режим замены (Replace Mode) активируется нажатием Shift + R.  
x - для удаления одного символа  

**Поиск по буферу**

Поиск по текущему слову (звездочка *)  
Используйте n для перехода к следующему совпадению и Shift+n для перехода к предыдущему.    

Снятие выделений:  
Чтобы убрать подсветку поиска, используйте команду :noh.  
Подсветка исчезнет, и перемещение с помощью n перестанет работать до нового поиска.  

Ввод поиска вручную:  
Команда поиска (/):  
Нажмите / и введите слово или фразу, которую нужно найти (например, "styles").  
Совпадения подсветятся при вводе, переходите к ним Enter.  

**Замена в файле**

Команда замены  
Замена в одной строке:  
Начните с :, затем команда s для замены, через слэш введите что ищем и на что заменяем.  
Пример: :s/styles/aaa/ — заменяет первое вхождение "styles" в текущей строке на "aaa".  

Глобальная замена в одной строке:  
Пример: :s/styles/aaa/g — заменяет все вхождения "styles" в текущей строке на "aaa".  

Замена по всему буферу:  
Используйте %s для поиска и замены по всему буферу.  
Пример: :%s/styles/aaa/g — заменяет все вхождения "styles" на "aaa" во всех строках буфера.  

        
### Продвинутое перемещение

Переход к закрывающемуся/открывающемуся тегу - %

Перемещение по страницам:  
Вверх: Ctrl + U  
Вниз: Ctrl + D  

Горизонтальные движения:  
К началу строки: 0  
К концу строки: $  
К первому символу строки: _  
К началу предыдущей/'следующей строки: - и +  

Перемещаться между разрывами строк для быстрого перехода по параграфам: 
Вниз: Shift + [  
Вверх: Shift + ]  

Быстрое перемещение к началу/концу документа:  
В начало: gg  
В конец: Shift + G  


## Visual Mode

Простой визуальный режим (v):  
Активируется клавишей v.  
Текст выделяется при перемещении курсора.  
Выделенный текст можно удалять, копировать, корректировать.  
Переход в нормальный режим выполняется клавишей Escape. 

Режим визуального выделения строк (Shift + v):  
Активируется комбинацией Shift + v.  
Выделяются целые строки.  
Удобен для копирования больших блоков текста.  

Визуальный блок-режим (Ctrl + Shift + v):    
Активируется комбинацией Ctrl + Shift + v.  
Выделяется прямоугольный блок текста.  
Полезен для операций с текстом в столбцах.  


Отмена изменений (обычный режим vs визуальный режим):  
U в обычном режиме — отменяет изменения.  
U в визуальном режиме — имеет другое значение.  

Изменение регистра слова:  
Для выбора слова:  
v — активация визуального режима.  
ve — выбор слова.  
Для изменения регистра:  
Shift+U (большая буква) — меняет на верхний регистр.  
u (маленькая буква) — меняет на нижний регистр.  

Перемещение строк:  
С конкретной строки на первую: :m1.  
Относительно текущей строки: :m-2 или :m+10.  

Комбинирование с визуальным выделением:  
Выделите строки: Shift + V.  
Введите команду: : и затем m + N (например, m + 2 для перемещения на 2 строки вниз).  

**Введение в Визуальный Блочный Режим**  
Вход в режим: Control + Shift + V  
Направления выделения: вверх, вниз, влево, вправо  

Основные Особенности  
Мультикурсор: Позволяет редактировать несколько строк одновременно  
Выделение блока: Создание прямоугольного или квадратного выделения  

Шаги для Редактирования  
Вход в визуальный блок: Control + Shift + V  
Выделение нужного текста: Нахождение нужного блока текста  
Переход в режим редактирования: Shift + I (важно: просто I не работает)  
Внесение изменений: Например, добавление "ABC"  
Применение изменений к выделенным строкам: Выход из режима вставки  

Дополнительные Возможности  
Удаление блока текста: Выделить блок → Нажать D  
Вставка текста в несколько строк: Текст вставляется во все строки ниже  

# Управление сворачиванием (Folding) в Neovim

В Neovim вы можете управлять сворачиванием кода с помощью специальных команд и сочетаний клавиш. Вот полное руководство.

---

## Основные команды управления сворачиванием

### Переключение состояния сворачивания:
- `za` — Переключить состояние текущего блока (открыть/закрыть).
- `zA` — Переключить состояние текущего блока и всех вложенных блоков.

### Открытие блоков:
- `zo` — Открыть текущий блок.
- `zO` — Открыть текущий блок и все вложенные блоки.

### Закрытие блоков:
- `zc` — Закрыть текущий блок.
- `zC` — Закрыть текущий блок и все вложенные блоки.

### Открытие/закрытие всех блоков:
- `zR` — Открыть все блоки в файле.
- `zM` — Закрыть все блоки в файле.

---

## Дополнительные команды

### Уровень сворачивания:
- `zv` — Раскрыть текущую строку и её родительские блоки.
- `zx` — Пересчитать свёртки для всего файла.
- `zX` — Полностью пересчитать свёртки и закрыть их.

### Создание/удаление ручных свёрток (при `foldmethod=manual`):
- `zf` — Создать свёртку вручную. Выделите блок (в визуальном режиме) и нажмите `zf`.
- `zd` — Удалить свёртку в текущем блоке.
- `zD` — Удалить свёртки для всех вложенных блоков.

### Перемещение между свёртками:
- `[z` — Перейти к началу предыдущего свёрнутого блока.
- `]z` — Перейти к началу следующего свёрнутого блока.

---

## Список команд для режима CMD **NeoVim**
```
:w - Для записи буфера в файл
:q - Для выхода из файла
:wq - Для одновременного сохранения и выхода
:edit(Tab) {demo.md} - для редактирования выбранного файла 
:cq - для сброса текущих изменений и выхода 
:terminal - для перехода в терминал NeoVim 
```

### Дополнительные настройки
```
:set nu - включает отображение строк
:set relarivenumber - делает текущую строку нулевой
```

## Работа с файловым менеджером в **NeoVim**
```
:buffers - отображает список буферов
:edit + . - отображает файлы текущей директории
:buffer <ID>: переключение на буфер по его идентификатору
:bnext: переход к следующему буферу
:bprevious: переход к предыдущему буферу
```
В представлении просмотра используем Shift-R для переименования файлов.  

## Работа с терминалом в NeoVim  
Переход в режим ввода в терминале: Нажмите I.  
Выход из терминального режима:  
Введите exit для выхода и закрытия терминала.  
Для перехода в режим Visual Terminal нажмите Ctrl+\ потом Ctrl+N.  
В режиме Visual Terminal можно использовать :q для выхода из терминала.  