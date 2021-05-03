# Вариативная самостоятельная работа

### [1.3 Создание программы для считывания данных формата CSV с использованием функционала модуля contextlib.](https://replit.com/@PolinaLazebniko/sem4-Tema1-VSR-11#main.py)
```python
"""
    Лазебникова Полина 
    ИВТ 2 курс
    группа 1.1

    Вариативная самостоятельная работа 
    Задание 1.1: Создание программы для считывания данных формата CSV с использованием функционала модуля contextlib
"""
import csv

with open('file.csv') as csv_file:
    csv_reader = csv.reader(csv_file, delimiter=',')
    for row in csv_reader:
        print(row)
```
