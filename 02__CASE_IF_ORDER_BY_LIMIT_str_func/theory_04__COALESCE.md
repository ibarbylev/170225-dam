Функция COALESCE() относится к функциям управления значениями NULL (Control Flow Functions).
📌 Что делает COALESCE()?

Она возвращает первое ненулевое значение из списка аргументов.
📌 Синтаксис:

COALESCE(value1, value2, ..., valueN)

    Если value1 не NULL, вернётся value1.
    Если value1 — NULL, но value2 не NULL, вернётся value2.
    Если все значения NULL, функция вернёт NULL.

📌 Примеры:
Замена NULL на значение по умолчанию
```
SELECT COALESCE(NULL, 'Default');
-- 'Default'
```

Выборка из таблицы
```
SELECT name, COALESCE(phone, 'Нет номера') AS phone 
FROM users;
```
Если phone содержит NULL, в результате будет Нет номера.

Работа с числами
```
SELECT COALESCE(NULL, NULL, 100, 200);
-- 100
```
Возвращается 100, так как это первое ненулевое значение.

Дополнительно:

    В MySQL есть ещё IFNULL(expr1, expr2), но он принимает только два аргумента.
    В PostgreSQL и SQL Server COALESCE() работает так же.

Функция полезна, когда нужно заменить NULL на дефолтные значения или выбрать первое доступное значение из нескольких колонок.