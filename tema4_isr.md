# Инвариантная самостоятельная работа

### [4.1 Используя свободные источники (bn.ru, avito.ru и т.д.), собрать данные о ценах на недвижимость, выставленную на продажу в разных районах города. Преобразовать данные в формат csv. Разработать скрипт для визуализации данных, используя библиотеку mathplotlib. Для визуализации использовать тип “точечная диаграмма” (scatterplot).](https://replit.com/@PolinaLazebniko/sem5-Tema4-ISR-41#main.py)
```python
"""
    Лазебникова Полина 
    ИВТ 3 курс
    группа 1.1

    Инвариантная самостоятельная работа 
    Задание 4.1: Используя свободные источники (bn.ru, avito.ru и т.д.), собрать данные о ценах на недвижимость, выставленную на продажу в разных районах города. Преобразовать данные в формат csv. Разработать скрипт для визуализации данных, используя библиотеку mathplotlib. Для визуализации использовать тип “точечная диаграмма” (scatterplot).
"""
import csv
import matplotlib.pyplot as plt
import datetime
import random

def get_random_color():
    r = lambda: random.randint(0, 255)
    return '#%02X%02X%02X' % (r(), r(), r())

def diag(lable, args):
    print(args)
    k = len(args)
    for i in range(k):
        [x, y] = args[i]
        print(x, y)
        numbers = len(y)
        colors = (get_random_color())
        area = 70
        # Plot
        plt.scatter(x, y, s=area, c=colors, alpha=1.)
    plt.xlabel('x')
    plt.ylabel('y')
    plt.legend(lable, loc="best")
    plt.savefig("result.png")
    plt.show()

def csv_reader(file_csv):
    reader = csv.reader(file_csv, delimiter=';')
    datas = {'date': [], 'first': [], 'changesFirst': [], 'second': [], 'changesSecond': []}
    for line in reader:
        datas['date'] += [line[0]]
        datas['first'] += [float(line[1])]
        datas['changesFirst'] += [line[2]]
        datas['second'] += [float(line[3])]
        datas['changesSecond'] += [line[4]]
    data_1 = datas['date']
    time = []
    for i in range(len(data_1)):
        data_1[i] = data_1[i].split('.')
        data_1[i] = [int(k) for k in data_1[i]]
        data_1[i] = (data_1[i][::-1])
        k = datetime.date(data_1[i][0], data_1[i][1], data_1[i][2])
        time += [k]
    return time, datas['first']

if __name__ == "__main__":
    csv_path = "data.csv"  # Приморский район
    csv_path_1 = "data2.csv"  # Василеостровский район
    datas_for_diag = []
    paths = [csv_path, csv_path_1]
    labels = ['Приморский район', 'Василеостровский район']
    for i in range(len(paths)):
        with open(paths[i], encoding='utf-8', newline='') as f_obj:
            datas_for_diag += [csv_reader(f_obj)]
    diag(labels, datas_for_diag)
```
### [4.2 Разработать фрагмент программы с использованием библиотеки pyqrcode, позволяющей создавать изображение QR-кода на основе переданной в программу текстовой строки.](https://replit.com/@PolinaLazebniko/sem5-Tema4-ISR-42#main.py)
```python
"""
    Лазебникова Полина 
    ИВТ 3 курс
    группа 1.1

    Инвариантная самостоятельная работа 
    Задание 4.2: Разработать фрагмент программы с использованием библиотеки pyqrcode, позволяющей создавать изображение 
    QR-кода на основе переданной в программу текстовой строки.
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
### [4.3 Реализовать модификацию изображения генерируемого QR-кода: раскрасить фрагменты изображения в несколько случайно определяемых цветов.](https://replit.com/@PolinaLazebniko/sem5-Tema4-ISR-43#main.py)
```python
"""
    Лазебникова Полина 
    ИВТ 3 курс
    группа 1.1

    Инвариантная самостоятельная работа 
    Задание 4.3: Реализовать модификацию изображения генерируемого QR-кода: раскрасить фрагменты изображения в несколько 
    случайно определяемых цветов.
"""
import pyqrcode
import png
import random

def get_random_color():
    r = lambda: random.randint(0, 255)
    return (r(), r(), r())

def qr_color(str_input):
    QR = pyqrcode.create(str_input)
    QR = QR.text().split('\n')[0:-1]

    pallet = []
    for row in QR:
        pallet_line = ()
        for c in row:
            if int(c) == 1:
                pallet_line += get_random_color()
            else:
                pallet_line += (255, 255, 255)
        pallet += [pallet_line]

    file = open('qrcode.png', 'wb')
    w = png.Writer(len(QR[0]), len(QR), greyscale=False)
    w.write(file, pallet)
    file.close()

if __name__ == '__main__':
    input_str = input('Введите строку: ')
    qr_color(input_str)
```
