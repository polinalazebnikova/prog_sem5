# Вариативная самостоятельная работа

### [2.1 Разработать функцию, возвращающую список чисел ряда Фибоначчи с использованием бесконечных итераторов (модуль itertools).](https://replit.com/@PolinaLazebniko/sem5-Tema2-VSR-21#main.py)
```python
"""
    Лазебникова Полина 
    ИВТ 2 курс
    группа 1.1

    Вариативная самостоятельная работа 
    Задание 2.1: Разработать функцию, возвращающую список чисел ряда Фибоначчи с использованием бесконечных 
    итераторов (модуль itertools).
"""
import itertools

def fib_numbers(n):
    fib_list = [0, 1]
    for i in itertools.count(0):
        if i > 1:
            fib_list += [fib_list[-2] + fib_list[-1]]
        if i >= n - 1:
            break
    return fib_list

def main():
    n = 16
    print(fib_numbers(n))

main()
```
