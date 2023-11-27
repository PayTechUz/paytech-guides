---
title: Методы Subscribe API
description: Методы Subscribe API
---

# Методы Subscribe API

## [PaymeSubscribeCards](https://github.com/PayTechUz/payme-pkg/blob/master/lib/payme/cards/subscribe_cards.py){:target="_blank"}
_Класс PaymeSubscribeCards включает в себя все методы paycom, принадлежащие картам._

### cards_create()
_Чтобы создать токен новой карты_

| Аргумент | Тип     | Описание                                                                                                                                                                                                                                                                                                         |
|----------|---------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| number   | str     | _Oбязательный_. Номер карты. Максимальная длина 18 символов.                                                                                                                                                                                                                                                     |
| expire   | str     | _Oбязательный_. Строка срока действия карты. Максимальная длина 5 символов.                                                                                                                                                                                                                                      |
| save     | boolean | _Необязательный_. **По умолчанию оно равно true**. Тип токена. Опция включается или отключается в зависимости от бизнес-логики приложения. Если флаг true, токен можно использовать для дальнейших платежей. Если флаг false, токен можно использовать только один раз. Одноразовый токен удаляется после оплаты |

> Пример метода создания карточка
```python
from pprint import pprint

from payme.cards.subscribe_cards import PaymeSubscribeCards

client = PaymeSubscribeCards(
    base_url="https://checkout.test.paycom.uz/api/",
    paycom_id="paycom-id"
)

response = client.cards_create(
    number="8600069195406311",
    expire="0399",
    save=True
)

pprint(response)
```
> Пример ответа
```json
{
  "jsonrpc": "2.0",
  "result": {
    "card": {
      "number": "860006******6311",
      "expire": "03/99",
      "token": "63119784d15d8d8d093b37b8_ADHrAykwnAIc2hm4hPPriktZ8nnuvR96S9Kzmjb3Fcix25IrJmMKrGxP9VUEP9rRDKRhtYjUw0vsXON7PYEyMCHtDKpMuM4krrIk8jdnyK7bXkSBSCyiGs2aahIrep6TSodIAxqutMJ4g3O8FZ8vC1DSMKzOaX0UF8fDKNexXV039Qnj4bNQc6NcpKGJn0wUX8d0RBqkmKid4WyUQnT987ZQDM2mT2IGNZtugvN4tDJTXBVTpqCWkXnZ0YWj64Ye0ztr91Mibtndo0Y1s5nCA6wufUZZugJ6c7rse19XNFSSieFM7AWi9VqybMe4eeWiZEBriAbFhrf8kQvrpBmwUEp05GjvFMgH0ku3vyUtSuJI36exHheXuJK66KstcX1i69EaF3",
      "recurrent": true,
      "verify": false,
      "type": "22618"
    }
  }
}
```

### card_get_verify_code()
_Чтобы получить код подтверждения_

| Аргумент | Тип   | Описание                               |
|----------|-------|----------------------------------------|
| token    | str   | _Oбязательный_. Неактивный токен карты |

> Пример получения кода подтверждения карты
```python
from pprint import pprint

from payme.cards.subscribe_cards import PaymeSubscribeCards


client = PaymeSubscribeCards(
    base_url="https://checkout.test.paycom.uz/api/",
    paycom_id="paycom-id"
)

resp = client.card_get_verify_code(
    token="630e5ffdd15d8d8d093b379b_2fsaoABWafecn20kofV4PFafFZjeGDWS9adM1PmboQaEZbbaxMcnaskctMbU9Iv8qgrOuKGz8SnjvZvYXDK64m1eS9gA5jZ7BBRaQybMXrDPtFPJ1fwek5B1KoIv5cMiCWYXj7ezpYEdJAKTIQw0Np9HsTXjqco4gQG3m8MOfeH9ovkdm66O6yj45oKXRmJyAK5i0SchXNNomACH3Oq80KyoRE1VoBRxvoKyMkOx0xcepXovxK9d3v26a8z7UtyokwY33N8MupviM3A5WHB5Xh35WZJJyFnxTSi1vvnYnG7uVd6Bb1GjV2yAHnimss8aEZGW5V7ZiPrhf8r6WJAeHciYDGK3msRKZJBQTfjgOdE9tGrEnMezVkxr1JXX0xSn5qqec2"
)

pprint(resp)
```

> Пример ответа
```json
{
  "jsonrpc": "2.0",
  "result": {
    "sent": true,
    "phone": "99890*****66",
    "wait": 60000
  }
}
```

### cards_verify()
_Верификация карты с помощью кода, отправленного по SMS_

| Аргумент    |  Тип | Описание                               |
|-------------|------|----------------------------------------|
| verify_code | str  | _Oбязательный_. Код для проверки       |
| token       | str  | _Oбязательный_. Неактивный токен карты |

> Пример проверки карты
```python
from pprint import pprint

from payme.cards.subscribe_cards import PaymeSubscribeCards


client = PaymeSubscribeCards(
    base_url="https://checkout.test.paycom.uz/api/",
    paycom_id="paycom-id"
)

resp = client.cards_verify(
    verify_code="666666",
    token="630e691fd15d8d8d093b379c_70mKyzqS8d1wTWzovIGjt9dKmjpn1KI8Y9XakPrfpbUASTBaZYbC1DjDcjYRmuNJep9gZrTRtHyEGBQYmBaPufuozF51bv4qEPsQnodq1VcD7tYyREwUXjMXXZUeu7Ek0REQCekCvVHX6rtNBpb4vtViJoNVjp94XpTqu0Bn3yYYb0CHu951wFydzRsieGxjGNrvx1oKyBcq0CdOUwoffRIt2VPvx5R2aVmc6ahwyhn387FEEcpO1PnjIJkWKTBWdI35ZPQnb1u1oss5aPg06E279THXRkoTThixbeqiD2JkWSXweNVGGDhTS30V4j61G3NWEPO2H3k4uFmCjjIQSzx4TxKzUgHg1i2q953PRUGjT4JZBRHMDxaN5tWuctEMNmY06p"
)

pprint(resp)
```

> Пример ответа
```json
{
  "jsonrpc": "2.0",
  "result": {
    "card": {
      "number": "860006******6311",
      "expire": "03/99",
      "token": "63118a5dd15d8d8d093b37b7_X2j34OIJPnROfsgzYZCZ0w7OcC50zzwiowTsotEVO1uUbxkzaDrvdOno6jicQTrcRmxvibxrye4vUS3AynTNPaPCTGpfk3RCKmT9NaOAyyTmctAjWsjwvqGR5XUzAP1Xcx12GkhuQi6VJ4BeaIXOokSRu06rRjaivmJQ8HTiJiR9b3OmZtrhkIRNcNXnnp9zYm1mFP4BuqGpS8BMnY0ASIE6ffxWykjgBcDTAfWBFt4mg7O9Dsvx0aj3IB8z3RIbZYtDZJnUVhCZrwW7ONVI9uEAdxNthorjO6PbV7TQ8XCjrztgGf6uCtOwwxasiIUVZN6tCVDk8A8NvVSUzUHXQHVkaPn5heJNa3K4WsffIckq7SwMbiw3UbawipeZKyD3iwk1Km",
      "recurrent": true,
      "verify": true,
      "type": "22618"
    }
  }
}
```

### cards_check()
_Проверка активности или неактивности токена карты_

| Аргумент | Тип   | Описание                               |
|----------|-------|----------------------------------------|
| token    | str   | _Oбязательный_. Неактивный токен карты |

> Пример проверки карт
```python
from pprint import pprint

from payme.cards.subscribe_cards import PaymeSubscribeCards


client = PaymeSubscribeCards(
    base_url="https://checkout.test.paycom.uz/api/",
    paycom_id="paycom-id"
)

resp = client.cards_check(
    token="630e691fd15d8d8d093b379c_70mKyzqS8d1wTWzovIGjt9dKmjpn1KI8Y9XakPrfpbUASTBaZYbC1DjDcjYRmuNJep9gZrTRtHyEGBQYmBaPufuozF51bv4qEPsQnodq1VcD7tYyREwUXjMXXZUeu7Ek0REQCekCvVHX6rtNBpb4vtViJoNVjp94XpTqu0Bn3yYYb0CHu951wFydzRsieGxjGNrvx1oKyBcq0CdOUwoffRIt2VPvx5R2aVmc6ahwyhn387FEEcpO1PnjIJkWKTBWdI35ZPQnb1u1oss5aPg06E279THXRkoTThixbeqiD2JkWSXweNVGGDhTS30V4j61G3NWEPO2H3k4uFmCjjIQSzx4TxKzUgHg1i2q953PRUGjT4JZBRHMDxaN5tWuctEMNmY06p"
)

pprint(resp)
```

> Пример ответа
```json
{
  "jsonrpc": "2.0",
  "result": {
    "card": {
      "number": "860006******6311",
      "expire": "03/99",
      "token": "63119b36d15d8d8d093b37c1_IJtHxZ46h5viyo8RIJCmQyE8qBw6PUWUdFKTMCVWrPoMMi4kJYsKyVdjQrIx6a12jDfEPVhhEqWm94FYvYh7IEjIs4xn0n3mM8Quw5dhd6ZT0dOK6u1spqWRMIDBpDMhHj2Ga8zZMAfeoiDAcrWScXS1AP2tkQHcJ40rBzHGHS6DoVeIheF70c0wO1kVQG0G5hDWguSGf2ZRFcBtpabv5BQkqSchxWKdCSVPIGiS6X7eF8YStdz1aGPzFyjDbaKT0vXNUMbQ7gaKh4PeQbruVVwFDfeIWqGeNmgCCPU4X0wCHFjTt8K61e9VOauNeU81ckoKHD8XGzCwGFJHrC4sHvNv4no3RifWhHCQF9GmFKf8cP2qh4pqTKwu3gOITaX5Ss71tC",
      "recurrent": true,
      "verify": true,
      "type": "22618"
    }
  }
}
```

### cards_remove()
_Удалить токен карты в случае успеха возвращает успех_

| Аргумент | Тип    | Описание                               |
|----------|--------|----------------------------------------|
| token    | str    | _Oбязательный_. Неактивный токен карты |

> Пример удаления карт
```python
from pprint import pprint

from payme.cards.subscribe_cards import PaymeSubscribeCards


client = PaymeSubscribeCards(
    base_url="https://checkout.test.paycom.uz/api/",
    paycom_id="paycom-id"
)

resp = client.cards_remove(
    token="630e691fd15d8d8d093b379c_70mKyzqS8d1wTWzovIGjt9dKmjpn1KI8Y9XakPrfpbUASTBaZYbC1DjDcjYRmuNJep9gZrTRtHyEGBQYmBaPufuozF51bv4qEPsQnodq1VcD7tYyREwUXjMXXZUeu7Ek0REQCekCvVHX6rtNBpb4vtViJoNVjp94XpTqu0Bn3yYYb0CHu951wFydzRsieGxjGNrvx1oKyBcq0CdOUwoffRIt2VPvx5R2aVmc6ahwyhn387FEEcpO1PnjIJkWKTBWdI35ZPQnb1u1oss5aPg06E279THXRkoTThixbeqiD2JkWSXweNVGGDhTS30V4j61G3NWEPO2H3k4uFmCjjIQSzx4TxKzUgHg1i2q953PRUGjT4JZBRHMDxaN5tWuctEMNmY06p"
)

pprint(resp)
```

> Пример ответа
```json
{
  "jsonrpc": "2.0",
  "result": {
    "success": true
  }
}
```


## [PaymeSubscribeReceipts](https://github.com/PayTechUz/payme-pkg/blob/master/lib/payme/receipts/subscribe_receipts.py){:target="_blank"}
_Класс PaymeSubscribeReceipts включает в себя все методы paycom, относящиеся к квитанциям._

### receipts_create()
_Чтобы создать новую квитанцию об оплате_

| Аргумент | Тип   | Описание                                     |
|----------|-------|----------------------------------------------|
| amount   | float | _Oбязательный_. Сумма платежа в тиынах       |
| order_id | int   | _Oбязательный_. Идентификатор объекта заказа |

> Пример создания квитанций
```python
from pprint import pprint

from payme.receipts.subscribe_receipts import PaymeSubscribeReceipts


rclient = PaymeSubscribeReceipts(
    base_url="https://checkout.test.paycom.uz/api/",
    paycom_id="paycom-id",
    paycom_key="paycom-key"
)

resp = rclient.receipts_create(
    amount=10000,
    order_id=1
)

pprint(resp)
```

> Пример ответа
```json
{
  "jsonrpc": "2.0",
  "result": {
    "receipt": {
      "_id": "63119becc4420cbf2712a24c",
      "create_time": 1662098412270,
      "pay_time": 0,
      "cancel_time": 0,
      "state": 0,
      "type": 2,
      "external": false,
      "operation": -1,
      "category": null,
      "error": null,
      "description": "",
      "detail": null,
      "amount": 400000,
      "currency": 860,
      "commission": 0,
      "account": [
        {
          "name": "transaction",
          "title": "Номер чека",
          "value": "2326",
          "main": true
        }
      ],
      "card": null,
      "merchant": {
        "_id": "5e730e8e0b852a417aa49ceb",
        "name": "test",
        "organization": "ЧП «test test»",
        "address": "",
        "business_id": "5e730e740b852a417aa49cea",
        "epos": {
          "merchantId": "106600000050000",
          "terminalId": "20660000"
        },
        "date": 1584598670296,
        "logo": null,
        "type": "Internet",
        "terms": null
      },
      "meta": {
        "source": "subscribe",
        "owner": "5e730e8e0b852a417aa49ceb"
      },
      "processing_id": null
    }
  }
}
```

### receipts_pay()
_Для оплаты существующего чека_

| Аргумент   | Тип   | Описание                                                         |
|------------|-------|------------------------------------------------------------------|
| invoice_id | str   | _Oбязательный_. Идентификатор счета для идентификации транзакции |
| token      | str   | _Oбязательный_. Неактивный токен карты                           |
| phone      | str   | _Oбязательный_. Телефон плательщика                              |

> Пример оплаты квитанций
```python
from pprint import pprint

from payme.receipts.subscribe_receipts import PaymeSubscribeReceipts


rclient = PaymeSubscribeReceipts(
    base_url="https://checkout.test.paycom.uz/api/",
    paycom_id="paycom-id",
    paycom_key="paycom-key"
)

resp = rclient.receipts_pay(
    invoice_id="631186b6c4420cbf2712a243",
    token="63118a5dd15d8d8d093b37b7_X2j34OIJPnROfsgzYZCZ0w7OcC50zzwiowTsotEVO1uUbxkzaDrvdOno6jicQTrcRmxvibxrye4vUS3AynTNPaPCTGpfk3RCKmT9NaOAyyTmctAjWsjwvqGR5XUzAP1Xcx12GkhuQi6VJ4BeaIXOokSRu06rRjaivmJQ8HTiJiR9b3OmZtrhkIRNcNXnnp9zYm1mFP4BuqGpS8BMnY0ASIE6ffxWykjgBcDTAfWBFt4mg7O9Dsvx0aj3IB8z3RIbZYtDZJnUVhCZrwW7ONVI9uEAdxNthorjO6PbV7TQ8XCjrztgGf6uCtOwwxasiIUVZN6tCVDk8A8NvVSUzUHXQHVkaPn5heJNa3K4WsffIckq7SwMbiw3UbawipeZKyD3iwk1Km",
    phone="998901304527"
)

pprint(resp)
```

> Пример ответа
```json
{
  "jsonrpc": "2.0",
  "id": 123,
  "result": {
    "receipt": {
      "_id": "63119becc4420cbf2712a24c",
      "create_time": 1662098438706,
      "pay_time": 1662098438804,
      "cancel_time": 0,
      "state": 4,
      "type": 2,
      "external": false,
      "operation": -1,
      "category": null,
      "error": null,
      "description": "",
      "detail": null,
      "amount": 400000,
      "currency": 860,
      "commission": 0,
      "account": [
        {
          "name": "transaction",
          "title": "Номер чека",
          "value": "2326",
          "main": true
        }
      ],
      "card": {
        "number": "860006******6311",
        "expire": "9903"
      },
      "merchant": {
        "_id": "5e730e8e0b852a417aa49ceb",
        "name": "test",
        "organization": "ЧП «test test»",
        "address": "",
        "business_id": "5e730e740b852a417aa49cea",
        "epos": {
          "merchantId": "106600000050000",
          "terminalId": "20660000"
        },
        "date": 1584598670296,
        "logo": null,
        "type": "Internet",
        "terms": null
      },
      "meta": {
        "source": "subscribe",
        "owner": "5e730e8e0b852a417aa49ceb"
      },
      "processing_id": 0
    }
  }
}
```

### receipts_send()
_Отправить квитанцию об оплате в SMS-сообщении_

| Аргумент   | Тип   | Описание                                                         |
|------------|-------|------------------------------------------------------------------|
| invoice_id | str   | _Oбязательный_. Идентификатор счета для идентификации транзакции |
| phone      | str   | _Oбязательный_. Телефон плательщика                              |

> Пример отправки квитанций
```python
from pprint import pprint

from payme.receipts.subscribe_receipts import PaymeSubscribeReceipts


rclient = PaymeSubscribeReceipts(
    base_url="https://checkout.test.paycom.uz/api/",
    paycom_id="paycom-id",
    paycom_key="paycom-key"
)

resp = rclient.receipts_send(
    invoice_id="631186b6c4420cbf2712a243",
    phone="998901304527"
)

pprint(resp)
```

> Пример ответа
```json
{
  "jsonrpc": "2.0",
  "id": 123,
  "result": {
    "success": true
  }
}
```


### receipts_cancel()
_Оплаченный чек в очереди на аннулирование_

| Аргумент   | Тип   | Описание                                                         |
|------------|-------|------------------------------------------------------------------|
| invoice_id | str   | _Oбязательный_. Идентификатор счета для идентификации транзакции |

> Пример отмены чеков
```python
from pprint import pprint

from payme.receipts.subscribe_receipts import PaymeSubscribeReceipts


rclient = PaymeSubscribeReceipts(
    base_url="https://checkout.test.paycom.uz/api/",
    paycom_id="paycom-id",
    paycom_key="paycom-key"
)

resp = rclient.receipts_cancel(
    invoice_id="63119303c4420cbf2712a245"
)

pprint(resp)
```

> Пример ответа
```json
{
  "jsonrpc": "2.0",
  "id": 123,
  "result": {
    "receipt": {
      "_id": "63119becc4420cbf2712a24c",
      "create_time": 1662098438706,
      "pay_time": 1662098438804,
      "cancel_time": 0,
      "state": 21,
      "type": 2,
      "external": false,
      "operation": -1,
      "category": null,
      "error": null,
      "description": "",
      "detail": null,
      "amount": 400000,
      "currency": 860,
      "commission": 0,
      "account": [
        {
          "name": "transaction",
          "title": "Номер чека",
          "value": "2326",
          "main": true
        }
      ],
      "card": {
        "number": "860006******6311",
        "expire": "9903"
      },
      "merchant": {
        "_id": "5e730e8e0b852a417aa49ceb",
        "name": "test",
        "organization": "ЧП «test test»",
        "address": "",
        "business_id": "5e730e740b852a417aa49cea",
        "epos": {
          "merchantId": "106600000050000",
          "terminalId": "20660000"
        },
        "date": 1584598670296,
        "logo": null,
        "type": "Internet",
        "terms": null
      },
      "meta": {
        "source": "subscribe",
        "owner": "5e730e8e0b852a417aa49ceb",
        "source_cancel": "subscribe"
      },
      "processing_id": null
    }
  }
}
```


### receipts_check()
_Проверьте наличие квитанции_

| Аргумент   | Тип  | Описание                                                         |
|------------|------|------------------------------------------------------------------|
| invoice_id | str  | _Oбязательный_. Идентификатор счета для идентификации транзакции |

> Пример проверки чеков
```python
from pprint import pprint

from payme.receipts.subscribe_receipts import PaymeSubscribeReceipts


rclient = PaymeSubscribeReceipts(
    base_url="https://checkout.test.paycom.uz/api/",
    paycom_id="paycom-id",
    paycom_key="paycom-key"
)

resp = rclient.receipts_check(
    invoice_id="63119303c4420cbf2712a245"
)

pprint(resp)
```

> Пример ответа
```json
{
  "jsonrpc": "2.0",
  "id": 123,
  "result": {
    "state": 0
  }
}
```


### receipts_get()
_Проверить статус существующего чека_

| Аргумент   | Тип  | Описание                                                         |
|------------|------|------------------------------------------------------------------|
| invoice_id | str  | _Oбязательный_. Идентификатор счета для идентификации транзакции |

> Пример получения квитанций
```python
from pprint import pprint

from payme.receipts.subscribe_receipts import PaymeSubscribeReceipts


rclient = PaymeSubscribeReceipts(
    base_url="https://checkout.test.paycom.uz/api/",
    paycom_id="paycom-id",
    paycom_key="paycom-key"
)

resp = rclient.receipts_get(
    invoice_id="6311946bc4420cbf2712a247"
)

pprint(resp)
```

> Пример ответа
```json
{
  "jsonrpc": "2.0",
  "id": 123,
  "result": {
    "receipt": {
      "_id": "6311946bc4420cbf2712a247",
      "create_time": 1662096491076,
      "pay_time": 0,
      "cancel_time": 0,
      "state": 0,
      "type": 2,
      "external": false,
      "operation": -1,
      "category": null,
      "error": null,
      "description": "",
      "detail": null,
      "amount": 400000,
      "currency": 860,
      "commission": 0,
      "account": [
        {
          "name": "transaction",
          "title": "Номер чека",
          "value": "2325",
          "main": true
        }
      ],
      "card": null,
      "merchant": {
        "_id": "5e730e8e0b852a417aa49ceb",
        "name": "test",
        "organization": "ЧП «test test»",
        "address": "",
        "business_id": "5e730e740b852a417aa49cea",
        "epos": {
          "merchantId": "106600000050000",
          "terminalId": "20660000"
        },
        "date": 1584598670296,
        "logo": null,
        "type": "Internet",
        "terms": null
      },
      "meta": {
        "source": "subscribe",
        "owner": "5e730e8e0b852a417aa49ceb"
      },
      "processing_id": null
    }
  }
}
```


### receipts_get_all()
_Получите всю полную информацию по проверкам за определенный период_

| Аргумент | Тип  | Описание                                                        |
|----------|------|-----------------------------------------------------------------|
| count    | int  | _Oбязательный_. Количество проверок. Максимальное значение - 50 |
| _from    | int  | _Oбязательный_. Дата начала                                     |
| _to      | int  | _Oбязательный_. Дата окончания                                  |
| offset   | int  | _Oбязательный_. Количество последующих пропущенных проверок     |

> Пример квитанций получить все
```python
from pprint import pprint

from payme.receipts.subscribe_receipts import PaymeSubscribeReceipts


rclient = PaymeSubscribeReceipts(
    base_url="https://checkout.test.paycom.uz/api/",
    paycom_id="paycom-id",
    paycom_key="paycom-key"
)

resp = rclient.receipts_get_all(
    count=2,
    _from=1636398000000,
    _to=1636398000000,
    offset=0
)

pprint(resp)
```

> Пример ответа
```json
{
  "jsonrpc": "2.0",
  "id": 123,
  "result": [
    {
      "_id": "6311946bc4420cbf2712a247",
      "create_time": 1662096491076,
      "pay_time": 0,
      "cancel_time": 0,
      "state": 0,
      "type": 2,
      "external": false,
      "operation": -1,
      "category": null,
      "error": null,
      "description": "",
      "detail": null,
      "amount": 400000,
      "currency": 860,
      "commission": 0,
      "account": [
        {
          "name": "transaction",
          "title": {
            "ru": "Номер чека",
            "uz": "Chek raqami"
          },
          "value": 2325,
          "main": true
        }
      ],
      "card": null,
      "merchant": {
        "_id": "5e730e8e0b852a417aa49ceb",
        "name": "test",
        "organization": "ЧП «test test»",
        "address": "",
        "business_id": "5e730e740b852a417aa49cea",
        "epos": {
          "merchantId": "106600000050000",
          "terminalId": "20660000"
        },
        "date": 1584598670296,
        "logo": null,
        "type": {
          "ru": "Internet",
          "uz": "Internet"
        },
        "terms": null
      },
      "meta": {
        "source": "subscribe",
        "owner": "5e730e8e0b852a417aa49ceb"
      },
      "processing_id": null
    },
    {
      "_id": "63119303c4420cbf2712a245",
      "create_time": 1662096131667,
      "pay_time": 0,
      "cancel_time": 1662096182979,
      "state": 50,
      "type": 2,
      "external": false,
      "operation": -1,
      "category": null,
      "error": null,
      "description": "",
      "detail": null,
      "amount": 400000,
      "currency": 860,
      "commission": 0,
      "account": [
        {
          "name": "transaction",
          "title": {
            "ru": "Номер чека",
            "uz": "Chek raqami"
          },
          "value": 2324,
          "main": true
        }
      ],
      "card": null,
      "merchant": {
        "_id": "5e730e8e0b852a417aa49ceb",
        "name": "test",
        "organization": "ЧП «test test»",
        "address": "",
        "business_id": "5e730e740b852a417aa49cea",
        "epos": {
          "merchantId": "106600000050000",
          "terminalId": "20660000"
        },
        "date": 1584598670296,
        "logo": null,
        "type": {
          "ru": "Internet",
          "uz": "Internet"
        },
        "terms": null
      },
      "meta": {
        "source": "subscribe",
        "owner": "5e730e8e0b852a417aa49ceb",
        "source_cancel": "subscribe"
      },
      "processing_id": null
    }
  ]
}
```
