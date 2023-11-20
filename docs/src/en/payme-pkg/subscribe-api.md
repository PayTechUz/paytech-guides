---
title: Subscribe API methods
description: Subscribe API methods
---

# Subscribe API methods

## [PaymeSubscribeCards](https://github.com/PayTechUz/payme-pkg/blob/master/lib/payme/cards/subscribe_cards.py){:target="_blank"}
_The PaymeSubscribeCards class includes all paycom methods which are belongs to cards_

### cards_create()
_To create a new card's token_

| Argument | Type    | Description                                                                                                                                                                                                                                                                                                   |
|----------|---------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| number   | str     | _Required_. The card number maximum length 18 char                                                                                                                                                                                                                                                            |
| expire   | str     | _Required_. The card expiration string maximum length 5 char                                                                                                                                                                                                                                                  |
| save     | boolean | _Optional_. **By default it equals true**. Type of token. The option is enabled or disabled depending on the application's business logic. If the flag is true, the token can be used for further payments. If the flag is false the token can only be used once. The one-time token is deleted after payment |

> Example to cards create method
```python
from pprint import pprint

from payme.cards.subscribe_cards import PaymeSubscribeCards

client = PaymeSubscribeCards(
    base_url="https://checkout.test.paycom.uz/api/",
    paycom_id="your-paycom-id"
)

response = client.cards_create(
    number="8600069195406311",
    expire="0399",
    save=True
)

pprint(response)
```
> Example response
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
_To get the verification code_

| Argument | Type    | Description                             |
|----------|---------|-----------------------------------------|
| token    | str     | _Required_. The card's non-active token |

> Example to card get verify code
```python
from pprint import pprint

from payme.cards.subscribe_cards import PaymeSubscribeCards


client = PaymeSubscribeCards(
    base_url="https://checkout.test.paycom.uz/api/",
    paycom_id="your-paycom-id"
)

resp = client.card_get_verify_code(
    token="630e5ffdd15d8d8d093b379b_2fsaoABWafecn20kofV4PFafFZjeGDWS9adM1PmboQaEZbbaxMcnaskctMbU9Iv8qgrOuKGz8SnjvZvYXDK64m1eS9gA5jZ7BBRaQybMXrDPtFPJ1fwek5B1KoIv5cMiCWYXj7ezpYEdJAKTIQw0Np9HsTXjqco4gQG3m8MOfeH9ovkdm66O6yj45oKXRmJyAK5i0SchXNNomACH3Oq80KyoRE1VoBRxvoKyMkOx0xcepXovxK9d3v26a8z7UtyokwY33N8MupviM3A5WHB5Xh35WZJJyFnxTSi1vvnYnG7uVd6Bb1GjV2yAHnimss8aEZGW5V7ZiPrhf8r6WJAeHciYDGK3msRKZJBQTfjgOdE9tGrEnMezVkxr1JXX0xSn5qqec2"
)

pprint(resp)
```

> Example response
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
_Verification of the card using the code sent via SMS_

| Argument    | Type    | Description                             |
|-------------|---------|-----------------------------------------|
| verify_code | str     | _Required_. Code for verification       |
| token       | str     | _Required_. The card's non-active token |

> Example to cards verify
```python
from pprint import pprint

from payme.cards.subscribe_cards import PaymeSubscribeCards


client = PaymeSubscribeCards(
    base_url="https://checkout.test.paycom.uz/api/",
    paycom_id="your-paycom-id"
)

resp = client.cards_verify(
    verify_code="666666",
    token="630e691fd15d8d8d093b379c_70mKyzqS8d1wTWzovIGjt9dKmjpn1KI8Y9XakPrfpbUASTBaZYbC1DjDcjYRmuNJep9gZrTRtHyEGBQYmBaPufuozF51bv4qEPsQnodq1VcD7tYyREwUXjMXXZUeu7Ek0REQCekCvVHX6rtNBpb4vtViJoNVjp94XpTqu0Bn3yYYb0CHu951wFydzRsieGxjGNrvx1oKyBcq0CdOUwoffRIt2VPvx5R2aVmc6ahwyhn387FEEcpO1PnjIJkWKTBWdI35ZPQnb1u1oss5aPg06E279THXRkoTThixbeqiD2JkWSXweNVGGDhTS30V4j61G3NWEPO2H3k4uFmCjjIQSzx4TxKzUgHg1i2q953PRUGjT4JZBRHMDxaN5tWuctEMNmY06p"
)

pprint(resp)
```

> Example response
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
_Checking the card token active or non-active_

| Argument | Type    | Description                             |
|----------|---------|-----------------------------------------|
| token    | str     | _Required_. The card's non-active token |

> Example to cards check
```python
from pprint import pprint

from payme.cards.subscribe_cards import PaymeSubscribeCards


client = PaymeSubscribeCards(
    base_url="https://checkout.test.paycom.uz/api/",
    paycom_id="your-paycom-id"
)

resp = client.cards_check(
    token="630e691fd15d8d8d093b379c_70mKyzqS8d1wTWzovIGjt9dKmjpn1KI8Y9XakPrfpbUASTBaZYbC1DjDcjYRmuNJep9gZrTRtHyEGBQYmBaPufuozF51bv4qEPsQnodq1VcD7tYyREwUXjMXXZUeu7Ek0REQCekCvVHX6rtNBpb4vtViJoNVjp94XpTqu0Bn3yYYb0CHu951wFydzRsieGxjGNrvx1oKyBcq0CdOUwoffRIt2VPvx5R2aVmc6ahwyhn387FEEcpO1PnjIJkWKTBWdI35ZPQnb1u1oss5aPg06E279THXRkoTThixbeqiD2JkWSXweNVGGDhTS30V4j61G3NWEPO2H3k4uFmCjjIQSzx4TxKzUgHg1i2q953PRUGjT4JZBRHMDxaN5tWuctEMNmY06p"
)

pprint(resp)
```

> Example response
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
_Delete card's token on success returns success_

| Argument | Type    | Description                             |
|----------|---------|-----------------------------------------|
| token    | str     | _Required_. The card's non-active token |

> Example to cards remove
```python
from pprint import pprint

from payme.cards.subscribe_cards import PaymeSubscribeCards


client = PaymeSubscribeCards(
    base_url="https://checkout.test.paycom.uz/api/",
    paycom_id="your-paycom-id"
)

resp = client.cards_remove(
    token="630e691fd15d8d8d093b379c_70mKyzqS8d1wTWzovIGjt9dKmjpn1KI8Y9XakPrfpbUASTBaZYbC1DjDcjYRmuNJep9gZrTRtHyEGBQYmBaPufuozF51bv4qEPsQnodq1VcD7tYyREwUXjMXXZUeu7Ek0REQCekCvVHX6rtNBpb4vtViJoNVjp94XpTqu0Bn3yYYb0CHu951wFydzRsieGxjGNrvx1oKyBcq0CdOUwoffRIt2VPvx5R2aVmc6ahwyhn387FEEcpO1PnjIJkWKTBWdI35ZPQnb1u1oss5aPg06E279THXRkoTThixbeqiD2JkWSXweNVGGDhTS30V4j61G3NWEPO2H3k4uFmCjjIQSzx4TxKzUgHg1i2q953PRUGjT4JZBRHMDxaN5tWuctEMNmY06p"
)

pprint(resp)
```

> Example response
```json
{
  "jsonrpc": "2.0",
  "result": {
    "success": true
  }
}
```


## [PaymeSubscribeReceipts](https://github.com/PayTechUz/payme-pkg/blob/master/lib/payme/receipts/subscribe_receipts.py){:target="_blank"}
_The PaymeSubscribeReceipts class includes all paycom methods which are belongs receipts part_

### receipts_create()
_To create a new payment receipt_

| Argument | Type  | Description                          |
|----------|-------|--------------------------------------|
| amount   | float | _Required_. Payment amount in tiyins |
| order_id | int   | _Required_. Order object ID          |

> Example to receipts create
```python
from pprint import pprint

from payme.receipts.subscribe_receipts import PaymeSubscribeReceipts


rclient = PaymeSubscribeReceipts(
    base_url="https://checkout.test.paycom.uz/api/",
    paycom_id="your-paycom-id",
    paycom_key="your-paycom-key"
)

resp = rclient.receipts_create(
    amount=10000,
    order_id=1
)

pprint(resp)
```

> Example response
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
_To pay for an exist receipt_

| Argument   | Type | Description                                     |
|------------|------|-------------------------------------------------|
| invoice_id | str  | _Required_. Invoice id for identity transaction |
| token      | str  | _Required_. The card's active token             |
| phone      | str  | _Required_. The payer's phone number            |

> Example to receipts pay
```python
from pprint import pprint

from payme.receipts.subscribe_receipts import PaymeSubscribeReceipts


rclient = PaymeSubscribeReceipts(
    base_url="https://checkout.test.paycom.uz/api/",
    paycom_id="your-paycom-id",
    paycom_key="your-paycom-key"
)

resp = rclient.receipts_pay(
    invoice_id="631186b6c4420cbf2712a243",
    token="63118a5dd15d8d8d093b37b7_X2j34OIJPnROfsgzYZCZ0w7OcC50zzwiowTsotEVO1uUbxkzaDrvdOno6jicQTrcRmxvibxrye4vUS3AynTNPaPCTGpfk3RCKmT9NaOAyyTmctAjWsjwvqGR5XUzAP1Xcx12GkhuQi6VJ4BeaIXOokSRu06rRjaivmJQ8HTiJiR9b3OmZtrhkIRNcNXnnp9zYm1mFP4BuqGpS8BMnY0ASIE6ffxWykjgBcDTAfWBFt4mg7O9Dsvx0aj3IB8z3RIbZYtDZJnUVhCZrwW7ONVI9uEAdxNthorjO6PbV7TQ8XCjrztgGf6uCtOwwxasiIUVZN6tCVDk8A8NvVSUzUHXQHVkaPn5heJNa3K4WsffIckq7SwMbiw3UbawipeZKyD3iwk1Km",
    phone="998901304527"
)

pprint(resp)
```

> Example response
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
_To send a receipt for payment in an SMS message_

| Argument   | Type | Description                                     |
|------------|------|-------------------------------------------------|
| invoice_id | str  | _Required_. Invoice id for identity transaction |
| phone      | str  | _Required_. The payer's phone number            |

> Example to receipts send
```python
from pprint import pprint

from payme.receipts.subscribe_receipts import PaymeSubscribeReceipts


rclient = PaymeSubscribeReceipts(
    base_url="https://checkout.test.paycom.uz/api/",
    paycom_id="your-paycom-id",
    paycom_key="your-paycom-key"
)

resp = rclient.receipts_send(
    invoice_id="631186b6c4420cbf2712a243",
    phone="998901304527"
)

pprint(resp)
```

> Example response
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
_A paid check in the queue for cancellation_

| Argument   | Type | Description                                     |
|------------|------|-------------------------------------------------|
| invoice_id | str  | _Required_. Invoice id for identity transaction |

> Example to receipts cancel
```python
from pprint import pprint

from payme.receipts.subscribe_receipts import PaymeSubscribeReceipts


rclient = PaymeSubscribeReceipts(
    base_url="https://checkout.test.paycom.uz/api/",
    paycom_id="your-paycom-id",
    paycom_key="your-paycom-key"
)

resp = rclient.receipts_cancel(
    invoice_id="63119303c4420cbf2712a245"
)

pprint(resp)
```

> Example response
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
_Check for an exist receipt_

| Argument   | Type | Description                                     |
|------------|------|-------------------------------------------------|
| invoice_id | str  | _Required_. Invoice id for identity transaction |

> Example to receipts check
```python
from pprint import pprint

from payme.receipts.subscribe_receipts import PaymeSubscribeReceipts


rclient = PaymeSubscribeReceipts(
    base_url="https://checkout.test.paycom.uz/api/",
    paycom_id="your-paycom-id",
    paycom_key="your-paycom-key"
)

resp = rclient.receipts_check(
    invoice_id="63119303c4420cbf2712a245"
)

pprint(resp)
```

> Example response
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
_Check status for an exist receipt_

| Argument   | Type | Description                                     |
|------------|------|-------------------------------------------------|
| invoice_id | str  | _Required_. Invoice id for identity transaction |

> Example to receipts get
```python
from pprint import pprint

from payme.receipts.subscribe_receipts import PaymeSubscribeReceipts


rclient = PaymeSubscribeReceipts(
    base_url="https://checkout.test.paycom.uz/api/",
    paycom_id="your-paycom-id",
    paycom_key="your-paycom-key"
)

resp = rclient.receipts_get(
    invoice_id="6311946bc4420cbf2712a247"
)

pprint(resp)
```

> Example response
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
_Get all complete information, on checks for a certain period_

| Argument | Type | Description                                          |
|----------|------|------------------------------------------------------|
| count    | int  | _Required_. The number of checks. Maximum value - 50 |
| _from    | int  | _Required_. The date of the beginning                |
| _to      | int  | _Required_. The date of the ending                   |
| offset   | int  | _Required_. The number of subsequent skipped checks  |

> Example to receipts get all
```python
from pprint import pprint

from payme.receipts.subscribe_receipts import PaymeSubscribeReceipts


rclient = PaymeSubscribeReceipts(
    base_url="https://checkout.test.paycom.uz/api/",
    paycom_id="your-paycom-id",
    paycom_key="your-paycom-key"
)

resp = rclient.receipts_get_all(
    count=2,
    _from=1636398000000,
    _to=1636398000000,
    offset=0
)

pprint(resp)
```

> Example response
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
