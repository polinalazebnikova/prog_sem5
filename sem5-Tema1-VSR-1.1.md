# Модуль PrettyTable

**Модуль prettytable** - полезен при создании простых таблиц и вывода их в терминал или текстовый файл. Он был вдохновлен таблицами ASCII, используемыми в оболочке PostgreSQL.

Возможности модуля:
+ установка ширина заполнения столбца, выравнивание текста или граница таблицы;
+ сортировка данных;
+ выбор отображения столбцов и строк в окончательном выводе;
+ чтение данных из CSV, HTML или курсора базы данных;
+ вывод данных в ASCII или HTML.

Установка модуля PrettyTable:
```
pip install -U prettytable
```

## Создание таблицы и добавление данных.
Для начала, необходимо создать экземпляр PrettyTable(), а затем можно добавлять в него некоторые данные. 

Eсть несколько вариантов добавления данных.


```python
# импорт установленного модуля
from prettytable import PrettyTable

# создание экземпляра
mytable = PrettyTable()
```

### Добавление данных построчно.
Можно добавлять данные по одной строке за раз. Для этого необходимо сначала установить имена полей, используя атрибут **PrettyTable.field_names**, а затем добавлять строки по одной, используя метод **PrettyTable.add_row()**:


```python
from prettytable import PrettyTable

mytable = PrettyTable()

# имена полей таблицы
mytable.field_names = ["Name", "Age", "City"]

# добавление данных по одной строке за раз
mytable.add_row(["Seungwoo", 26, "Busan"])
mytable.add_row(["Byungchan", 23, "Ulsan"])
mytable.add_row(["Yohan", 21, "Seoul"])
mytable.add_row(["Seungyoun", 24, "Gwangju"])

# вывод таблицы в терминал
print(mytable)
```

    +-----------+-----+---------+
    |    Name   | Age |   City  |
    +-----------+-----+---------+
    |  Seungwoo |  26 |  Busan  |
    | Byungchan |  23 |  Ulsan  |
    |   Yohan   |  21 |  Seoul  |
    | Seungyoun |  24 | Gwangju |
    +-----------+-----+---------+
    

### Добавление сразу всех строк.
Когда есть список строк, то можно добавить их за один раз с помощью метода **PrettyTable.add_rows()**:


```python
from prettytable import PrettyTable

mytable = PrettyTable()

# имена полей таблицы
mytable.field_names = ["Name", "Age", "City"]

# добавление списка строк
mytable.add_rows(
    [
        ["Seungwoo", 26, "Busan"],
        ["Byungchan", 23, "Ulsan"],
        ["Yohan", 21, "Seoul"],
        ["Seungyoun", 24, "Gwangju"],
    ]
)

print(mytable)
```

    +-----------+-----+---------+
    |    Name   | Age |   City  |
    +-----------+-----+---------+
    |  Seungwoo |  26 |  Busan  |
    | Byungchan |  23 |  Ulsan  |
    |   Yohan   |  21 |  Seoul  |
    | Seungyoun |  24 | Gwangju |
    +-----------+-----+---------+
    

### Добавление данных колонками.
Также можно добавлять данные по одному столбцу за раз. Для этого необходимо использовать метод **PrettyTable.add_column()**, который принимает два аргумента - строку, которая является именем поля таблицы добавляемого столбца, и список или кортеж, содержащий данные столбца:


```python
from prettytable import PrettyTable

mytable = PrettyTable()

# Добавление колонки таблицы с именем 'Name'
mytable.add_column("Name", ["Seungwoo", "Byungchan", "Yohan", "Seungyoun"])

# Добавление колонки таблицы с именем 'Age'
mytable.add_column("Age", [26, 23, 21, 24])

# Добавление колонки таблицы с именем 'City'
mytable.add_column("City", ["Busan", "Ulsan", "Seoul", "Gwangju"])

print(mytable)
```

    +-----------+-----+---------+
    |    Name   | Age |   City  |
    +-----------+-----+---------+
    |  Seungwoo |  26 |  Busan  |
    | Byungchan |  23 |  Ulsan  |
    |   Yohan   |  21 |  Seoul  |
    | Seungyoun |  24 | Gwangju |
    +-----------+-----+---------+
    

### Импорт данных из файла CSV.
Если данные таблицы хранятся в файле CSV, то можно прочитать эти данные и добавить в таблицу PrettyTable() следующим образом:


```python
# импорт загрузчика `from_csv`
from prettytable import from_csv

with open("myfile.csv") as fp:
    
    # создание таблицы из `myfile.csv`
    mytable = from_csv(fp)

    print(mytable)
```

### Импорт данных из курсора базы данных.
Если данные таблицы хранятся в базе данных, к которой можно получить доступ с помощью модуля имеющего Python DB-API (например, база данных SQLite, доступная с помощью модуля sqlite3), то можно создать экземпляр PrettyTable() с данными, используя объект курсора, например:


```python
import sqlite3
# импорт загрузчика `from_db_cursor`
from prettytable import from_db_cursor

connection = sqlite3.connect("mydb.db")
cursor = connection.cursor()
cursor.execute("SELECT field1, field2, field3 FROM my_table")

# создание таблицы из объекта курсора
mytable = from_db_cursor(cursor)

print(mytable)
```

## Удаление данных
Существует три способа удаления данных:

+ Метод **del_row** принимает целочисленный индекс одной строки для удаления.
+ Метод **clear_rows** не принимает аргументов и удаляет все строки в таблице, но сохраняет имена полей такими, какими они были, чтобы вы могли повторно заполнить их данными.
+ Метод **clear** не принимает аргументов и удаляет все строки и все имена полей. Это не совсем то же самое, что создание нового экземпляра таблицы, хотя связанные со стилем настройки сохраняются.
