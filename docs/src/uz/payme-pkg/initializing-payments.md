---
title: Tezkor to'lovlar
description: Tezkor to'lovlar
---

# [Generate pay link](https://github.com/PayTechUz/payme-pkg/blob/master/lib/payme/methods/generate_link.py){:target="_blank"}

> Namuna
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
> Natija
```shell
https://checkout.paycom.uz/bT01ZTczMGU4ZTBiODUyYTQxN2FhNDljZWI7YWMub3JkZXItaWQ9OTk5O2E9OTk5OTtjPXlvdXItY2FsbGJhY2stdXJs
```

- Parameterlar

| Argument     | Turi    | Izoh                                                                                                                                           |
|--------------|---------|------------------------------------------------------------------------------------------------------------------------------------------------|
| order_id     | str     | _Majburiy_. To'lanadigan buyurtmaning ID'si                                                                                                    |
| amount       | Decimal | _Majburiy_. Buyurtmaning miqdori                                                                                                               |
| callback_url | str     | _Ixtiyoriy_. Merchant API uchun to'lovdan keyingi yo'naltiriladigan link. Birlamchi holatda loyiha sozlamalaridan PAYME_CALL_BACK_URL ni oladi |

### Metodlari
- generate_link() -> to'lov linkini generatsiya qilish uchun.
> **Hech qanday argument olmaydi**

- to_tiyin() -> so'mdan tiyinga konvertatsiya qiladi.

| Argument | Turi    | Izoh                         |
|----------|---------|------------------------------|
| amount   | Decimal | _Majburiy_. Buyurtma miqdori |

- to_sum() -> tiyindan so'mga konvertatsiya qiladi.

| Argument | Turi    | Izoh                         |
|----------|---------|------------------------------|
| amount   | Decimal | _Majburiy_. Buyurtma miqdori |
