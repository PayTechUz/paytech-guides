---
title: Initializing payments
description: Initializing payments
---

# [Generate pay link](https://github.com/PayTechUz/payme-pkg/blob/master/lib/payme/methods/generate_link.py){:target="_blank"}

- Example
```python
from pprint import pprint

from payme.methods.generate_link import GeneratePayLink

pay_link = GeneratePayLink(
  order_id="999",
  amount=9999,
  callback_url="your-callback-url"
).generate_link()

pprint(pay_link)
```
- Output
```shell
https://checkout.paycom.uz/bT01ZTczMGU4ZTBiODUyYTQxN2FhNDljZWI7YWMub3JkZXItaWQ9OTk5O2E9OTk5OTtjPXlvdXItY2FsbGJhY2stdXJs
```

- Parameters

| Argument     | Type    | Description                                                                                                                      |
|--------------|---------|----------------------------------------------------------------------------------------------------------------------------------|
| order_id     | str     | _Required_. The order_id for paying                                                                                              |
| amount       | Decimal | _Required_. The amount belong to the order                                                                                       |
| callback_url | str     | _Optional_. The merchant api callback url to redirect after payment. By default, it takes PAYME_CALL_BACK_URL from your settings |

### Methods
- generate_link() -> to generate payment link.
> Does not take any arguments
- to_tiyin() -> convert from sum to tiyin.

| Argument | Type    | Description                  |
|----------|---------|------------------------------|
| amount   | Decimal | _Required_. The order amount |

- to_sum() -> convert from tiyin to sum.

| Argument | Type    | Description                  |
|----------|---------|------------------------------|
| amount   | Decimal | _Required_. The order amount |
