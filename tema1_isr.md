# Инвариантная самостоятельная работа

### [1.1 Исследовать функционал одного из модулей стандартной библиотеки (string, re, datetime, math, random, os, и т.д.) и, используя инструмент Jupyter Notebook, создать документ с описанием и примерами использования его функционала.](https://www.dropbox.com/s/3ngtdqq7fa94gtf/sem5-Tema1-ISR-1.1.ipynb?dl=0)
[Ссылка на HTML](https://www.dropbox.com/s/sm84k027nxsy6on/sem5-Tema1-ISR-1.1.html?dl=0)

[Ссылка на Markdown](https://github.com/polinalazebnikova/prog_sem5/blob/main/sem5-Tema1-ISR-1.1.md)
### [1.2 Создание пользовательского пакета для приложения «Гостевая книга» с прототипами методов, позволяющих взаимодействовать с JSON-файлом (создание, удаление, переименование, чтение, запись).](https://replit.com/@PolinaLazebniko/sem5-Tema1-ISR-12-1#main.py)
```python
"""
    Лазебникова Полина 
    ИВТ 3 курс
    группа 1.1

    Инвариантная самостоятельная работа 
    Задание 1.2: Создание пользовательского пакета для приложения «Гостевая книга» с прототипами методов, позволяющих взаимодействовать с JSON-файлом (создание, удаление, переименование, чтение, запись).
"""
import json

class Client:
    def __init__(self, fn):
        try:
            self.handler = open(fn, 'r+')
        except FileNotFoundError:
            open(fn, 'w')
            self.handler = open(fn, 'r+')
        finally:
            self.json = json.loads(self.handler.read() or '{}')

    def register(self, uid, name, city):
        if uid in self.json.keys():
            print('You have already registered.')
        else:
            self.json.update({'id': uid, 'name': name, 'city': city})

    def update(self, uid, name, city):
        self.json.update({'id': uid, 'name': name, 'city': city})

    def read(self):
        print('\n'.join('{}: {}'.format(a, b) for a, b in self.json.items()))


guest = Client('data')
guest.register(uid=1, name='Seungwoo', city='Seoul')
guest.read()
print('\n')
guest.update(uid=2, name='Han Seungwoo', city='Seoul')
guest.read() 
```
