---
title: Инициализация платежей
description: Инициализация платежей
---

# [Generate pay link](https://github.com/PayTechUz/payme-pkg/blob/master/lib/payme/methods/generate_link.py){:target="_blank"}

> Пример
```python
from pprint import pprint

from payme.methods.generate_link import GeneratePayLink

pay_link = GeneratePayLink(
  order_id="999",
  amount=9999,
  callback_url="callback-url"
).generate_link()

pprint(pay_link)
```
> Результат
```shell
https://checkout.paycom.uz/bT01ZTczMGU4ZTBiODUyYTQxN2FhNDljZWI7YWMub3JkZXItaWQ9OTk5O2E9OTk5OTtjPXlvdXItY2FsbGJhY2stdXJs
```

- Параметры

| Аргумент     | Тип     | Описание                                                                                                                                                     |
|--------------|---------|--------------------------------------------------------------------------------------------------------------------------------------------------------------|
| order_id     | str     | _Oбязательный_. ID заказа для оплаты                                                                                                                         |
| amount       | Decimal | _Oбязательный_. Сумма принадлежит заказу                                                                                                                     |
| callback_url | str     | _Необязательный_. URL обратного вызова API продавца, который будет перенаправлен после оплаты. По умолчанию требуется PAYME_CALL_BACK_URL из ваших настроек. |

### Методы
- generate_link() -> создать ссылку для оплаты.
> **Не принимает никаких аргументов**

- to_tiyin() -> перевести сум в тийин.

| Аргумент | Тип     | Описание                     |
|----------|---------|------------------------------|
| amount   | Decimal | _Oбязательный_. Сумма заказа |

- to_sum() -> convert from tiyin to sum.

| Аргумент | Тип     | Описание                     |
|----------|---------|------------------------------|
| amount   | Decimal | _Oбязательный_. Сумма заказа |
