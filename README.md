# Тестовое задание

Необходимо реализовать веб-сервис с использованием фреймворка Django и СУБД PostgreSQL имеющее один API метод (при желании можно использовать Django-Rest-Framework):

> Добавить в проект Swagger - (необязательно)

## 1. Метод для валидации и верификации данных
 Метод входним параметром должен получать вложенный JSON объект и провалидировать с соответствующими правилами. Входной JSON объект имеет вид:
 ```
 data = [
    {
        "key": "1",
        "mockData": [
            {
                "id": "12354",
                "objectName": "Город Москва",
                "numberChastot": "2685/2565",
                "longtitude": 205,
                "attitude": -5,
                "klass": "10M0D7W 10M0G7W",
            },
            {
                "id": "1254354",
                "objectName": "Город Питер",
                "numberChastot": "2685/2565",
                "longtitude": 205,
                "attitude": -5,
                "klass": "10M0D7W 10M0G7W",
            },
        ]
    },
    {
    "key": "2",
        "mockData":[
            {
                "id": "12356454",
                "objectName": "Город Тверь",
                "numberChastot": "2685/2565",
                "longtitude": 205,
                "attitude": -5,
                "klass": "10M0D7W 10M0G7W",
            },
            {
                "id": "1248354",
                "objectName": "Город Тула",
                "numberChastot": "2685/2565",
                "longtitude": 205,
                "attitude": -5,
                "klass": "10M0D7W 10M0G7W",
            }
        ]
    },
]
```

### Правила валидации данных
Свойство 
    "objectName" -> Использование кириллицы
    "numberChastot"  -> Пара числовых положительных значений, значения можно указать через пробел или '/'
    "longtitude" -> Только положительное число не превышающее 360
    "attitude" -> Только отрицательное число не превышающее -90
    "klass" -> Пара значений, в каждой группе до 9 буквенно-цифровых символов, написанных на латинице


## При возникновении ошибки, API должен возвращать где именно и какие свойства не валидны 
Пример (Необязательно, чтобы ответ был в таком виде, но сдлать так, чтобы с ответа можно было понять в каком объекте допушена невалидные данные )
```
{
 data: [],
 messages: [
    {
        "key": "1",
        "mockData": [
            {
                "id": 12354,
                "error": [
                    'Invalid format objectName'
                ]
            }
        ]
    },
    {
        "key": "2",
        "mockData": [
            {
                "id": 1248354,
                "error": [
                    'Invalid format longtitude'
                ]
            }
        ]
    },
 ]
}
```