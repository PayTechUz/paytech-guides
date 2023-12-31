---
title: Настройка
description: Настройка
---

# Установка
Windows
```shell
pip install payme-pkg
```

Unix-based OS
```shell
pip3 install payme-pkg
```
<br/>

# Тестовые учетные данные

```
Номер карты: 8600 4954 7331 6478 Годен до: 03/99 СМС-код: 666666
Номер карты: 8600 0691 9540 6311 Годен до: 03/99 СМС-код: 666666
```

# Настройка (Джанго)
1. Добавьте `'payme'` в установленные приложения.
```python
INSTALLED_APPS = [
    ...
    'payme',
    ...
]
```

2. Добавьте учетные данные `'payme'` в свои настройки.
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

3. Создайте новое представление об обработке обратных вызовов.
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

4. Добавьте путь `payme` в ядро URL-шаблонов.
```python
from django.urls import path

from your_app.views import PaymeCallBackAPIView

urlpatterns = [
    ...
    path("payments/merchant/", PaymeCallBackAPIView.as_view()),
    ...
]
```

5. Запуск миграции
```shell
python manage.py makemigrations
```

> 🎉 Поздравляем, вы интегрировали методы торгового API с Django, продолжайте читать документацию. После успешной миграции проверьте панель администратора и посмотрите, что произошло.
