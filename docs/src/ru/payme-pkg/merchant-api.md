---
title: Методы Merchant API
description: Методы Merchant API
---

<!-- Google tag (gtag.js) -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-9BRKYLP6BB"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());

  gtag('config', 'G-9BRKYLP6BB');
</script>

# Методы Merchant API

### [CheckPerformTransaction](https://github.com/PayTechUz/payme-pkg/blob/master/lib/payme/methods/check_perform_transaction.py){:target="_blank"}
_Это используется для проверки выполнения транзакции_
> **Не имеет методов**


### [CreateTransaction](https://github.com/PayTechUz/payme-pkg/blob/master/lib/payme/methods/create_transaction.py){:target="_blank"}
_Это используется для создания транзакции_


#### Методы
- _convert_ms_to_datetime() -> конвертировать время из мс в формат даты и времени

| Аргумент | Тип  | Описание                               |
|----------|------|----------------------------------------|
| time_ms  | int  | _Oбязательный_. Время конвертации в мс |


### [PerformTransaction](https://github.com/PayTechUz/payme-pkg/blob/master/lib/payme/methods/perform_transaction.py){:target="_blank"}
_Это используется для выполнения транзакции_
> **Не имеет методов**


### [CancelTransaction](https://github.com/PayTechUz/payme-pkg/blob/master/lib/payme/methods/cancel_transaction.py){:target="_blank"}
_Используется для отмены транзакции_
> **Не имеет методов**


### [CheckTransaction](https://github.com/PayTechUz/payme-pkg/blob/master/lib/payme/methods/check_transaction.py){:target="_blank"}
_Это используется для проверки транзакции_
> **Не имеет методов**


### [GetStatement](https://github.com/PayTechUz/payme-pkg/blob/master/lib/payme/methods/get_statement.py){:target="_blank"}
_Информация о транзакциях используется для сверки транзакций продавца и Payme Business._
> **Не имеет методов**
