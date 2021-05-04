# Инвариантная самостоятельная работа

### [2.1 Разработать функцию, возвращающую элементы ряда Фибоначчи по данному максимальному значению.](https://replit.com/@PolinaLazebniko/sem5-Tema2-ISR-21#main.py)
```python
"""
    Лазебникова Полина 
    ИВТ 2 курс
    группа 1.1

    Инвариантная самостоятельная работа 
    Задание 2.1: Разработать функцию, возвращающую элементы ряда Фибоначчи по данному максимальному значению.  
"""

def fib_max(max_num):
    fib_list = [0, 1]
    current_fib = fib_list[-1]
    while (current_fib < max_num):
        fib_list += [fib_list[-2] + fib_list[-1]]
        current_fib = fib_list[-1]
    return fib_list

print(fib_max(601))
```
### [2.2 Создание программы, возвращающей список чисел Фибоначчи с помощью итератора.](https://replit.com/@PolinaLazebniko/sem5-Tema2-ISR-22#main.py)
```python
"""
    Лазебникова Полина 
    ИВТ 2 курс
    группа 1.1

    Инвариантная самостоятельная работа 
    Задание 2.2: Создание программы, возвращающей список чисел Фибоначчи с помощью итератора.  
"""

class FibIterator:
    def __init__(self, n):
        self.n = n - 1
        self.count = 0
        self.fib_list = [0, 1]

    def __next__(self):
        if self.count == 0 or self.count == 1:
            self.count += 1
            return self.fib_list[self.count - 1]
        elif self.count <= self.n:
            self.fib_list += [self.fib_list[-2] + self.fib_list[-1]]
            self.count += 1
            return self.fib_list[-1]
        else:
            raise StopIteration

def main():
    num = 16
    iterator_init = FibIterator(num)
    list = []
    for i in range(num):
        list += [next(iterator_init)]
    print(list)

main()
```
