# Инвариантная самостоятельная работа

### [3.1 Разработать фрагмент программы, позволяющий получать данные о текущих курсах валют с сайта Центробанка РФ с использованием сервиса, который они предоставляют. Применить шаблон проектирования «Одиночка» для предотвращения отправки избыточных запросов к серверу ЦБ РФ. Оформить решение в виде корректно работающего приложения, реализовать тестирование и опубликовать его в портфолио.](https://replit.com/@PolinaLazebniko/sem6-Tema3-ISR-31-1#main.py)
```python
"""
    Лазебникова Полина 
    ИВТ 3 курс
    группа 1.1

    Инвариантная самостоятельная работа 
    Задание 3.1: Разработать фрагмент программы, позволяющий получать данные о текущих курсах 
    валют с сайта Центробанка РФ с использованием сервиса, который они предоставляют. Применить 
    шаблон проектирования «Одиночка» для предотвращения отправки избыточных запросов к серверу ЦБ РФ.
"""
from urllib.request import urlopen
from xml.etree import ElementTree as ET

def singleton(cls):
    instances = {}

    def getinstance(*args):
        if cls not in instances:
            instances[cls] = cls(*args)
        return instances[cls]
    return getinstance

@singleton
def get_currencies(currencies_ids_lst=None):
    if currencies_ids_lst is None:
        currencies_ids_lst = [
                                'R01235',
                                'R01239',
                                'R01815',
                                'R01820',
                                'R01035'
        ]
    cur_res_str = urlopen("http://www.cbr.ru/scripts/XML_daily.asp")
    result = {}
    cur_res_xml = ET.parse(cur_res_str)
    root = cur_res_xml.getroot()
    valutes = root.findall('Valute')
    for el in valutes:
        valute_id = el.get('ID')
        if str(valute_id) in currencies_ids_lst:
            valute_cur_val = el.find('Value').text
            valute_cur_name = el.find('Name').text
            result[valute_id] = (valute_cur_name, valute_cur_val)
    return result

if __name__ == "__main__":
    result = get_currencies()
    for val in result:
        print('%40s%10s' % (result[val][0], result[val][1]))

    assert id(result) == id(get_currencies()), 'Not a singletone.'
```
### [3.2 На основе фрагмента программы, предложенного преподавателем, реализовать класс для получения данных с сайта Центробанка РФ с использованием сервиса, который они предоставляют. Применить шаблон проектирования «Декоратор» для реализации функционала, позволяющего преобразовывать данные о курсах валют в формат JSON. Реализовать сохранение (сериализацию) данных в файл формата JSON.](https://replit.com/@PolinaLazebniko/sem6-Tema3-ISR-32-1#main.py)
```python
"""
    Лазебникова Полина 
    ИВТ 3 курс
    группа 1.1

    Инвариантная самостоятельная работа 
    Задание 3.2: На основе фрагмента программы, предложенного преподавателем, реализовать 
    класс для получения данных с сайта Центробанка РФ с использованием сервиса, который они 
    предоставляют. Применить шаблон проектирования «Декоратор» для реализации функционала, 
    позволяющего преобразовывать данные о курсах валют в формат JSON. Реализовать сохранение 
    (сериализацию) данных в файл формата JSON.
"""
from urllib.request import urlopen
from xml.etree import ElementTree as ET

class BaseClass:
    def get_currencies(self) -> str:
        pass

class CurrenciesSimple(BaseClass):
    def get_currencies(self, currencies_ids_lst=None):
        if currencies_ids_lst is None:
            currencies_ids_lst = [
                'R01235',
                'R01239',
                'R01815',
                'R01820',
                'R01035'
            ]
        cur_res_str = urlopen("http://www.cbr.ru/scripts/XML_daily.asp")
        result = {}
        cur_res_xml = ET.parse(cur_res_str)
        root = cur_res_xml.getroot()
        valutes = root.findall('Valute')
        for el in valutes:
            valute_id = el.get('ID')
            if str(valute_id) in currencies_ids_lst:
                valute_cur_val = el.find('Value').text
                valute_cur_name = el.find('Name').text
                result[valute_id] = (valute_cur_name, valute_cur_val)
        return result


class CurrenciesJSON(BaseClass):

    def __init__(self, currencies) -> None:
        self.currencies = currencies

    def get_currencies(self, currencies_ids_lst=None):
        if currencies_ids_lst is None:
            currencies_ids_lst = [
                'R01235',
                'R01239',
                'R01815',
                'R01820',
                'R01035'
            ]
        cur_res_str = urlopen("http://www.cbr.ru/scripts/XML_daily.asp")
        result = {}
        cur_res_xml = ET.parse(cur_res_str)
        root = cur_res_xml.getroot()
        valutes = root.findall('Valute')
        for el in valutes:
            valute_id = el.get('ID')
            if str(valute_id) in currencies_ids_lst:
                valute_cur_val = el.find('Value').text
                valute_cur_name = el.find('Name').text
                result[valute_id] = (valute_cur_name, valute_cur_val)
        return result

    def write_json(self):
        with open('res.json', 'w', encoding='utf-8') as file:
            file.write(str(self.get_currencies()))

if __name__ == '__main__':
    simple_cur = CurrenciesSimple()
    json_cur = CurrenciesJSON(simple_cur)

    print(simple_cur.get_currencies())
    print(json_cur.get_currencies())

    json_cur.write_json()
```
### [3.3. Создание ЭОР на тему «Обзор современных фреймворков, реализующих шаблон архитектуры системы MVC», создание сравнительной таблицы 3-5 фреймворков.](https://www.dropbox.com/s/6765f2xp4djjjyn/%D0%A1%D0%B5%D0%BC%205%20%D0%A2%D0%B5%D0%BC%D0%B0%203%20%D0%98%D0%A1%D0%A0%203.3.docx?dl=0)

[Ссылка](https://www.dropbox.com/s/6765f2xp4djjjyn/%D0%A1%D0%B5%D0%BC%205%20%D0%A2%D0%B5%D0%BC%D0%B0%203%20%D0%98%D0%A1%D0%A0%203.3.docx?dl=0)
