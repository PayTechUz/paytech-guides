---
title: Sozlash (Setup)
description: Sozlash (Setup)
---

# O'rnatish
Windows
```shell
pip install payme-pkg
```

Unix-ga asoslangan OS'larda (Linux, macOS, ...)
```shell
pip3 install payme-pkg
```
<br/>

# Sozlash (django)
1. Loyihangiz sozlamarining INSTALLED_APPS qismiga `'payme'` ni qo'shing
```python
INSTALLED_APPS = [
    ...
    'payme',
    ...
]
```

2. `payme` hisob ma'lumotlarini qo'shing
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

3. Callbacklarni boshqarish uchun yangi view yarating
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

4. Loyihangizning asosiy urlpatternlari qatoriga `payme` ni qo'shing.
```python
from django.urls import path

from your_app.views import PaymeCallBackAPIView

urlpatterns = [
    ...
    path("payments/merchant/", PaymeCallBackAPIView.as_view()),
    ...
]
```

5. Migratsiya qiling
```shell
python manage.py makemigrations
```

> 🎉 Tabriklaymiz! Siz merchant api va django loyihangizni integratsiya qildingiz, yo'riqnomani o'qishda davom eting. Migratsiyalar muvaffaqiyatli amalga oshganidan so'ng, nima sodir bo'lganini ko'rish uchun admin panelni tekshiring.
