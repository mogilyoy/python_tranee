## Задание 1. Разработать функцию количества проданных билетов

### Задача
В примере кода ниже генерируется список фиксаций состояния количества проданных билетов на концерт в течение времени.
Разработайте функцию get_tickets(sales_stamps, offset), которая вернет количество проданных билетов (сумму regular и vip) на момент offset в списке sales_stamps. 

``` Python
from pprint import pprint
import random
import math

TIMESTAMPS_COUNT = 50000

PROBABILITY_TICKETS_SOLD = 0.005

PROBABILITY_REGULAR_TICKETS = 0.45

OFFSET_MAX_STEP = 3

INITIAL_STAMP = {
    "offset": 0,
    "tickets": {
        "regular": 0,
        "vip": 0
    }
}


def generate_stamp(previous_value):
    tickets_sold = random.random() < PROBABILITY_TICKETS_SOLD
    regular_tickets_sold = 1 if tickets_sold and random.random() < PROBABILITY_REGULAR_TICKETS else 0
    vip_tickets_sold = 1 if tickets_sold and regular_tickets_sold == 0 else 0
    offset_change = math.floor(random.random() * OFFSET_MAX_STEP) + 1

    return {
        "offset": previous_value["offset"] + offset_change,
        "tickets": {
            "regular": previous_value["tickets"]["regular"] + regular_tickets_sold,
            "vip": previous_value["tickets"]["vip"] + vip_tickets_sold
        }
    }


def generate_sales():
    stamps = [INITIAL_STAMP, ]
    current_stamp = INITIAL_STAMP
    for _ in range(TIMESTAMPS_COUNT):
        current_stamp = generate_stamp(current_stamp)
        stamps.append(current_stamp)

    return stamps


sales_stamps = generate_sales()

pprint(sales_stamps)


def get_tickets(sales_stamps, offset):
    '''
    Takes list of sales' stamps and time offset for which returns the number of regular and VIP tickets sold.
    Please pay attention to that for some offsets the sales_stamps list may not contain     ticket sales data.
    '''
    # return regular, vip
```
	
Пример вызова: 
``` python
offset = 100
sales_stamps = generate_sales()

regular, vip = get_tickets(sales_stamps, offset)
```


## Задание 2. Телеграм бот 

### Задача
Реализуйте бота в телеграм для автоматического принятия юзера в закрытый канал. Пример: https://t.me/+omiXL8tOtetlMWIy 

### Часть № 1 (обязательная) 
- Используйте библиотеку pyTelegramBotAPI 
- Для принятия заявки юзера ипользуйте метод approve_chat_join_request
- Добавьте файл requirements.txt
- При необходимости используйте комментарии

### Часть №2 (каждый пункт опционален)
- Добавьте логирование 
- Добавьте файл(ы) для запуска бота в Docker контейнере
- Используйте асинхронную версию pyTelegramBotAPI 
- Создайте git репозиторий, загрузите на GItHub

## Задание 3. SQL (Опционально)

### Задача
Вам предоставляется база данных с двумя таблицами: employees (сотрудники) и departments (отделы).

Таблица employees: 
<table>
<tr><td>employee_id </td>	<td>first_name</td>	<td>last_name</td>	<td>department_id</td>	<td>salary</td></tr>

<tr><td>1</td>	<td>John</td>	<td>Doe</td>	<td>1</td>	<td>50000</td></tr>

<tr><td>2</td>	<td>Jane</td>	<td>Smith</td>	<td>2</td>	<td>60000</td></tr>

<tr><td>3</td>	<td>Mike</td>	<td>Johnson</td><td>1</td>	<td>45000</td></tr>

<tr><td>4</td>	<td>Emily</td>	<td>Davis</td>	<td>3</td>	<td>70000</td></tr>

<tr><td>5</td>	<td>Anna</td>	<td>Brown</td>	<td>2</td>	<td>80000</td></tr>
</table>

Таблица departments: 
<table>
<tr><td>department_id</td>	<td>department_name</td></tr>
<tr><td>1</td>	<td>HR</td></tr>
<tr><td>2</td>	<td>IT</td></tr>
<tr><td>3</td>	<td>Marketing</td></tr>
</table>

1. Напишите запрос, который вернет все имена сотрудников (first_name и last_name), работающих в отделе IT.

2. Напишите запрос, который выведет среднюю зарплату сотрудников в каждом отделе.

3. Напишите запрос, который выведет информацию о сотрудниках, чья зарплата выше средней зарплаты по всем сотрудникам.
