# Условный оператор $cond

Аналог функции `IF` в SQL:
```sql
SELECT 
    name,
    IF(salary > 5000, 'High', 'Low') AS salary_level
FROM employees;
```

Удобен для замены значений в случае "либо то, либо другое".  
Если же условий несколько (больше двух) - удобнее использовать `$switch`.

---

### 📘 Синтаксис:
#### Полная форма
```mongodb
{ 
  $cond: { if: <условие>, then: <значение_если_истина>, else: <значение_если_ложь> } 
}
```

#### Короткая форма:

```mongodb
{ 
  $cond: [ <условие>, <значение_если_истина>, <значение_если_ложь> ] 
}
```

---

### Пример

В коллекцию `sales` надо добавить поле `status`.
```mongodb
{ "_id": 1, "item": "A", "amount": 120 }
{ "_id": 2, "item": "B", "amount": 80 }
{ "_id": 3, "item": "C", "amount": 150 }
```

Если `amount` > 100, `status` равен `"high"`.
Иначе `status` - `"low"`.

### Решение

```javascript
db.sales.aggregate([
  {
    $project: {
      item: 1,
      amount: 1,
      status: {
        $cond: { if: { $gt: ["$amount", 100] }, then: "high", else: "low" }
      }
    }
  }
])
```

---

### Результат:

```mongodb
{ "_id": 1, "item": "A", "amount": 120, "status": "high" }
{ "_id": 2, "item": "B", "amount": 80, "status": "low" }
{ "_id": 3, "item": "C", "amount": 150, "status": "high" }
```

