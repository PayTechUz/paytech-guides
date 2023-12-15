---
title: Setup
description: Setup
---

# Installation
Windows
```shell
pip install payme-pkg
```

Unix-based OS
```shell
pip3 install payme-pkg
```
<br/>

# Test-Credentials

```
Card Numer: 8600 4954 7331 6478 Expire Date: 03/99 SMS Code: 666666
Card Numer: 8600 0691 9540 6311 Expire Date: 03/99 SMS Code: 666666
```

# Setup (django)
1. Add `'payme'` to your installed apps
```python
INSTALLED_APPS = [
    ...
    'payme',
    ...
]
```

2. Add `payme` credentials to your settings
```python
PAYME: dict = {
    'PAYME_ID': 'payme-id',
    'PAYME_KEY': 'payme-key',
    'PAYME_URL': 'payme-checkout-url',
    'PAYME_CALL_BACK_URL': 'your-callback-url', # merchant api callback url
    'PAYME_MIN_AMOUNT': 'payme-min-amount', # integer field
    'PAYME_ACCOUNT': 'order-id',
}

ORDER_MODEL = 'your_app.models.Your_Order_Model'
```

3. Create a new view that about handling callbacks
```python
from payme.views import MerchantAPIView


class PaymeCallBackAPIView(MerchantAPIView):
    def create_transaction(self, order_id, action, *args, **kwargs) -> None:
        print(f"create_transaction for order_id: {order_id}, response: {action}")

    def perform_transaction(self, order_id, action, *args, **kwargs) -> None:
        print(f"perform_transaction for order_id: {order_id}, response: {action}")

    def cancel_transaction(self, order_id, action, *args, **kwargs) -> None:
        print(f"cancel_transaction for order_id: {order_id}, response: {action}")
```

4. Add a `payme` path to core of urlpatterns
```python
from django.urls import path

from your_app.views import PaymeCallBackAPIView

urlpatterns = [
    ...
    path("payments/merchant/", PaymeCallBackAPIView.as_view()),
    ...
]
```

5. Run migrations
```shell
python manage.py makemigrations
```

> 🎉 Congratulations you have been integrated merchant api methods with django, keep reading docs. After successfully migrations check your admin panel and see results what happened.
