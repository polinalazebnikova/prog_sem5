# Инвариантная самостоятельная работа

### [4.1 Используя свободные источники (bn.ru, avito.ru и т.д.), собрать данные о ценах на недвижимость, выставленную на продажу в разных районах города. Преобразовать данные в формат csv. Разработать скрипт для визуализации данных, используя библиотеку mathplotlib. Для визуализации использовать тип “точечная диаграмма” (scatterplot).](https://replit.com/@PolinaLazebniko/sem4-Tema1-ISR-11#main.py)
```python
"""
    Лазебникова Полина 
    ИВТ 2 курс
    группа 1.1

    Инвариантная самостоятельная работа 
    Задание 1.1: Разработка программы с реализацией функции для считывания json-данных из файла 
    и вывод их в табличном виде на экран. Реализовать базовый синтаксис для обработки исключений (try .. except).
"""

def json_read(name_file):
    """
    Функция для работы с файлом json
    Функция формирует строки таблицы из файла, при этом обрабатывая возможные исключения 
    """  
    try:
        file_open = open(name_file)
        try:
            import json
        except ImportError as e:
            import json
            print('Problem with import json')
        data = json.load(file_open)  
        t = []
        title = '| {:^3}| {:^10}| {:^13}| {:^30}| {:^6}| {:^15}|'.format('ID','First name','Last name','Email','Gender','IP-address')
        delimiter = '-'*len(title)
        val = '| {id:<3}| {first_name:10}| {last_name:13}| {email:30}| {gender:6}| {ip_address:15}|'
        t.append(delimiter)  
        t.append(title)
        t.append(delimiter)  
        for i in range(len(data)):
            tmp = data[i]
            res = val.format(**tmp)
            t.append(res)
            t.append(delimiter)
        return t
    except FileNotFoundError as e:
        print('File not found')  
    except IOError as e:
        print('Problem with input or output')
    except NameError as e:
        print('Name not found')

def main():
    """
    Функция, которая вызывает функцию json_read, в качестве аргумента используя файл json, и выводит результат
    """
    file_name = json_read('MOCK_DATA.json')
    for i in file_name:
        print(i)

main()
```
### [4.2 Разработать фрагмент программы с использованием библиотеки pyqrcode, позволяющей создавать изображение QR-кода на основе переданной в программу текстовой строки.
](https://replit.com/@PolinaLazebniko/sem5-Tema4-ISR-42#main.py)
```python
"""
    Лазебникова Полина 
    ИВТ 3 курс
    группа 1.1

    Инвариантная самостоятельная работа 
    Задание 4.2: Разработать фрагмент программы с использованием библиотеки pyqrcode, позволяющей создавать изображение QR-кода на основе переданной в программу текстовой строки.
"""
import pyqrcode
import png

def qr_simple(str_input):
    QR = pyqrcode.create(str_input)
    QR.png('qr.png', scale=13)

if __name__ == '__main__':
    input_str = input('Введите строку: ')
    qr_simple(input_str)
```
### [4.3 Реализовать модификацию изображения генерируемого QR-кода: раскрасить фрагменты изображения в несколько случайно определяемых цветов.](https://replit.com/@PolinaLazebniko/sem4-Tema1-ISR-13)
```python
"""
    Лазебникова Полина 
    ИВТ 2 курс
    группа 1.1

    Инвариантная самостоятельная работа 
    Задание 1.1: Дополнение программы (задание 1.1) для считывания данных с использованием 
    менеджера контекстов и реализации расширенного синтаксиса для обработки исключений.
"""
import json

try:
    with open('MOCK_DATA.json') as file_open:
        data = json.load(file_open)
except FileNotFoundError as e:
    print('File not found')
    
try:
    with open('MOCK_DATA.json') as file_open:
        data = json.load(file_open)
except IOError as e:
    print('Problem with input or output')

try:
    with open('MOCK_DATA.json') as file_open:
        data = json.load(file_open)
except NameError as e:
    print('Name not found')


def json_read(name_file):
    """
    Функция для работы с файлом json
    Функция формирует строки таблицы из файла
    """  
    with open(name_file) as file_open:
        data = json.load(file_open) 
 
    t = []
    title = '| {:^3}| {:^10}| {:^13}| {:^30}| {:^6}| {:^15}|'.format('ID','First name','Last name','Email','Gender','IP-address')
    delimiter = '-'*len(title)
    val = '| {id:<3}| {first_name:10}| {last_name:13}| {email:30}| {gender:6}| {ip_address:15}|'
    t.append(delimiter)  
    t.append(title)
    t.append(delimiter)  
    for i in range(len(data)):
        tmp = data[i]
        res = val.format(**tmp)
        t.append(res)
        t.append(delimiter)
    return t

def main():
    """
    Функция, которая вызывает функцию json_read, в качестве аргумента используя файл json, и выводит результат
    """
    file_name = json_read('MOCK_DATA.json')
    for i in file_name:
        print(i)

main()
```
