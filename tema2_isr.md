# Инвариантная самостоятельная работа

### [1.1. Разработать программу с реализацией функции для считывания jsonданных из файла и вывод их в табличном виде на экран. Реализовать базовый синтаксис для обработки исключений (try .. except)](https://replit.com/@PolinaLazebniko/sem4-Tema1-ISR-11#main.py)
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
### [1.2. Дополнение программы для считывания данных проверкой утверждений или высказываний (assert). Создание отдельного блока для такой проверки (с помощью __name__) и скрипта командной строки для запуска этих проверок.](https://replit.com/@PolinaLazebniko/sem4-Tema1-ISR-12#main.py)
```python
"""
    Лазебникова Полина 
    ИВТ 2 курс
    группа 1.1

    Инвариантная самостоятельная работа 
    Задание 1.2: Дополнение программы (задание 1.1) для считывания данных проверкой 
    утверждений или высказываний (assert). Создание отдельного блока для такой проверки (с помощью __name__) 
    и скрипта командной строки для запуска этих проверок.
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

if __name__ == "__main__":
    assert json_read('MOCK_DATA.json') is not  tuple
    #assert json_read('MOCK_DATA.json') is list, 'Типы не совпадают'
    #assert json_read('MOCK_DATA.json') is set, 'Типы не совпадают' 
```
### [1.3. Дополнение программы для считывания данных с использованием менеджера контекстов и реализации расширенного синтаксиса для обработки исключений.](https://replit.com/@PolinaLazebniko/sem4-Tema1-ISR-13)
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
