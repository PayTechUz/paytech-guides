---
title: Песочница (Sandbox)
description: Песочница (Sandbox)
---

# Песочница (Sandbox)

!!! info "К СВЕДЕНИЮ"
    Тестирование на рабочем сервере создает дополнительную нагрузку. Учетные записи, которые связаны с некорректно работающими приложениями, блокируются.

### О песочнице

**Песочница** — _среда для безопасного тестирования реализованного [Merchant API](merchant-api.md){:target="_blank"}. Тесты в песочнице помогут проверить взаимодействие реализованного API с Payme Business. Тестирование в песочнице позволяет получить детальное описание возникающих [ошибок](https://developer.help.paycom.uz/protokol-merchant-api/obschie-oshibki){:target="_blank"}._

???+ info "Инфо"
    Инициирует тестирование и запускает тесты — разработчик мерчанта. Тестирование проводится с помощью [запросов](https://developer.help.paycom.uz/protokol-merchant-api/format-zaprosa){:target="_blank"} и [ответов](https://developer.help.paycom.uz/protokol-merchant-api/format-otveta){:target="_blank"}. Запросы отправляет сервер Payme Business, ответы — сервер мерчанта.


### Подготовка к тестированию

Добавьте веб кассу в кабинете мерчанта. После создания веб-кассы, Payme Business выдаст 2 ключа:

- ключ для кабинета — key;
- ключ для песочницы — TEST_KEY.

!!! info ""
    **Перейдите в [песочницу](https://test.paycom.uz/){:target="_blank"}. В песочнице введите Merchant ID (ID веб-кассы) и TEST_KEY.**

!!! info "К СВЕДЕНИЮ"
    Merchant ID хранится в параметрах разработчика веб-кассы.

<img src="https://i.ibb.co/jVY9Lzq/image.png" width="100%" border="0">

!!! info "К СВЕДЕНИЮ"
    Важно чтобы в настройках кассы был указан Endpoint URL — веб-адрес биллинга. По этому адресу Payme Business будет посылать запросы.

При создании транзакций в песочнице, важно правильно указать тип счёта:

- На **накопительный счёт** деньги могут поступать неограниченное количество раз. Пример накопительного счёта — счет мобильного оператора;
- На **одноразовый счёт**, деньги могут поступать только 1 раз. Пример одноразового счёта — заказ в интернет магазине.

!!! info "К СВЕДЕНИЮ"
    Тестирование [инициализации платежа](initializing-payments.md){:target="_blank"} рекомендуется проводить только после успешного завершения тестирования в песочнице: вначале протестируйте инициализацию платежа в песочнице, затем в продакшене.

**Веб-адрес песочницы:** [https://test.paycom.uz](https://test.paycom.uz){:target="_blank"}

**URL отправки чека в песочницу:** [https://test.paycom.uz](https://test.paycom.uz){:target="_blank"}

**URL отправки чека в продакшн:** [https://checkout.paycom.uz](https://checkout.paycom.uz){:target="_blank"}


### Тестирование

Тестирование проводится по 2 сценариям:

1. [Создание и отмена неподтвержденной транзакции](#_4)
2. [Создание, подтверждение и отмена подтверждённой финансовой транзакции](#_5)

В первый сценарий включена проверка безопасности, поэтому вначале проводится тестирование по первому сценарию, затем по второму.

!!! info "К СВЕДЕНИЮ"
    В платёжном плагине Merchant API уже реализовано, поэтому тестирование платёжного плагина проводится по тем же сценариям.

#### Создание и отмена неподтвержденной транзакции

Войдите в магазин как покупатель. Добавьте товар в корзину и оплатите заказ с помощью Payme. После оплаты произойдёт автоматический переход в «Песочницу» на страницу создания финансовой транзакции.

**Проверьте авторизацию с неверными учетными данными**

В разделе «Неверные данные» нажмите на ссылку «Неверная авторизация» и запустите тест.

<img src="https://i.ibb.co/DkyRw6m/image.png"  width="25%" border="0">

!!! info "К СВЕДЕНИЮ"
    На запросы к реализованным методам, реализованное Merchant API возвращает ответы с ошибкой -32504: «Недостаточно привилегий для выполнения метода».

**Проверьте оплату неверной или недопустимой суммой**

В разделе «Неверные данные» нажмите на ссылку «Неверная сумма».

<img src="https://i.ibb.co/QX1ybh3/image.png"  width="25%" border="0">

В параметрах теста укажите действительный номер заказа, неверную сумму и запустите тест.

<img src="https://i.ibb.co/6v5QBYR/image.png"  width="100%" border="0">

!!! info "К СВЕДЕНИЮ"
    На запросы к реализованным методам [CheckPerformTransaction](merchant-api.md#checkperformtransaction){:target="_blank"} и [CreateTransaction](merchant-api.md#checktransaction){:target="_blank"}, реализованное Merchant API возвращает ответы с ошибкой -31001: «Неверная сумма».

**Проверьте оплату несуществующего счёта**

В разделе «Неверные данные» нажмите на ссылку «Несуществующий счёт».

<img src="https://i.ibb.co/Dw4hnR5/image.png"  width="25%" border="0">

В параметрах теста укажите действительную сумму заказа, неверный номер заказа и запустите тест.

<img src="https://i.ibb.co/DMcCcsh/image.png"  width="100%" border="0">

!!! info "К СВЕДЕНИЮ"
    На запросы к реализованным методам [CheckPerformTransaction](merchant-api.md#checkperformtransaction){:target="_blank"} и [CreateTransaction](merchant-api.md#checktransaction){:target="_blank"}, реализованное Merchant API возвращает ответы с ошибками -31050 — -31099: «Неверный код заказа».

**Проверьте возможность создания финансовой транзакции**

!!! info "К СВЕДЕНИЮ"
    Проверку возможности создания финансовой транзакции обеспечивает реализованный метод [CheckPerformTransaction](merchant-api.md#checkperformtransaction){:target="_blank"}.

В разделе «Платежные запросы» нажмите на ссылку “CheckPerformTransaction”.

<img src="https://i.ibb.co/rfTnDZL/image.png"  width="25%" border="0">

Убедитесь что в парметрах теста присутствует значение парметра Account, сумма оплаты в тийинах и запустите тест.

<img src="https://i.ibb.co/T4NsGQ7/image.png"  width="100%" border="0">

На запрос к реализованному методу CheckPerformTransaction, реализованное Merchant API возвращает ответ без ошибок.

**Создайте транзакцию**

!!! info "К СВЕДЕНИЮ"
    Создание транзакции обеспечивает реализованный метод [CreateTransaction](merchant-api.md#checktransaction){:target="_blank"}.

В разделе «Платежные запросы» нажмите на ссылку “CreateTransaction”.

<img src="https://i.ibb.co/S5d5qsK/image.png"  width="25%" border="0">

Убедитесь что в параметрах запуска теста тип счета «Одноразовый», статус счета «Ожидает оплаты» и запустите тест.

<img src="https://i.ibb.co/mv3ZFhb/image.png"  width="100%" border="0">

!!! info "К СВЕДЕНИЮ"
    Запросы по методам CreateTransaction, PerformTransaction, CancelTransaction посылаются два раза. В случае, если первый запрос даст сбой - второй обязательно пройдет. При повторных вызовах методов CreateTransaction, PerformTransaction, CancelTransaction ответ должен совпадать с ответом из первого запроса.

Реализованное Merchant API возвращает:

- на запрос к реализованному методу [CheckPerformTransaction](merchant-api.md#checkperformtransaction){:target="_blank"} — ответ с результатом “allow”: true,;
- на запрос к реализованному методу [CreateTransaction](merchant-api.md#createtransaction){:target="_blank"} — ответ без ошибок;
- на повторный запрос, к реализованному методу [CreateTransaction](merchant-api.md#createtransaction){:target="_blank"} — ответ без ошибок;
- на запрос к реализованному методу [CheckTransaction](merchant-api.md#checktransaction){:target="_blank"} — ответ без ошибок;
- на запрос к реализованному методу [CreateTransaction](merchant-api.md#createtransaction){:target="_blank"} c новой транзакцией и состоянием счета «В ожидании оплаты» — ответ с ошибкой -31008: “Невозможно выполнить операцию”.

**Отмените неподтвержденную транзакцию**

!!! info "К СВЕДЕНИЮ"
    Отмену транзакции обеспечивает реализованный метод [CancelTransaction](merchant-api.md#canceltransaction){:target="_blank"}.

В разделе «Платежные запросы» нажмите на ссылку “CancelTransaction”.

<img src="https://i.ibb.co/92qWbJw/image.png"  width="25%" border="0">

Убедитесь что в параметрах запуска теста присутствует id транзакции, статус транзакции “1” (транзакция создана) и запустите тест.

<img src="https://i.ibb.co/2KdF3Bh/image.png"  width="100%" border="0">

!!! info "К СВЕДЕНИЮ"
    На запросы к реализованным методам [CancelTransaction](merchant-api.md#canceltransaction){:target="_blank"} и [CheckTransaction](merchant-api.md#checktransaction){:target="_blank"}, реализованное Merchant API возвращает ответы без ошибок.

#### Создание, подтверждение и отмена подтвержденной транзакции

Войдите в магазин как покупатель. Добавьте товар в корзину и оплатите заказ с помощью Payme. После оплаты произойдет автоматический переход в «Песочницу» на страницу создания финансовой транзакции.

**Проверьте возможность создания финансовой транзакции**

!!! info "К СВЕДЕНИЮ"
    Проверку возможности создания финансовой транзакции обеспечивает реализованный метод [CheckPerformTransaction](merchant-api.md#checkperformtransaction){:target="_blank"}.

В разделе «Платежные запросы» нажмите на ссылку “CheckPerformTransaction”.

<img src="https://i.ibb.co/hZS7KNQ/image.png"  width="25%" border="0">

Убедитесь что в парметрах теста присутствует значение парметра Account, сумма оплаты в тийинах и запустите тест.

<img src="https://i.ibb.co/7SJHKvf/image.png"  width="100%" border="0">

На запрос к реализованному методу CheckPerformTransaction, реализованное Merchant API возвращает ответ без ошибок.

**Создайте транзакцию**

!!! info "К СВЕДЕНИЮ"
    Создание транзакции обеспечивает реализованный метод [CreateTransaction](merchant-api.md#createtransaction){:target="_blank"}.

В разделе «Платежные запросы» нажмите на ссылку “CreateTransaction”.

<img src="https://i.ibb.co/S5d5qsK/image.png"  width="25%" border="0">

Убедитесь что в параметрах запуска теста тип счета «Одноразовый», статус счета «Ожидает оплаты» и запустите тест.

<img src="https://i.ibb.co/S3YrpD5/image.png"  width="100%" border="0">

Реализованное Merchant API возвращает:

- на запрос к реализованному методу [CheckPerformTransaction](merchant-api.md#checkperformtransaction){:target="_blank"} — ответ с результатом “allow”: true,;
- на запрос к реализованному методу [CreateTransaction](merchant-api.md#createtransaction){:target="_blank"} — ответ без ошибок;
- на повторный запрос, к реализованному методу [CreateTransaction](merchant-api.md#createtransaction){:target="_blank"} — ответ без ошибок;
- на запрос к реализованному методу [CheckTransaction](merchant-api.md#checktransaction){:target="_blank"} — ответ без ошибок;
- на запрос к реализованному методу [CreateTransaction](merchant-api.md#createtransaction){:target="_blank"} c новой транзакцией и состоянием счета «В ожидании оплаты» — ответ с ошибкой -31008: “Невозможно выполнить операцию”.

**Подтвердите транзакцию**

!!! info "К СВЕДЕНИЮ"
    Подтверждение транзакции обеспечивает реализованный метод [PerformTransaction](merchant-api.md#performtransaction){:target="_blank"}.

В разделе «Платежные запросы» нажмите на ссылку “PerformTransaction”.

<img src="https://i.ibb.co/QPbn0n0/image.png"  width="25%" border="0">

Убедитесь что в параметрах запуска теста присутствует id транзакции, статус транзакции “1” (создана) и запустите тест.

<img src="https://i.ibb.co/FY85s7t/image.png"  width="100%" border="0">

Реализованное Merchant API возвращает ответ без ошибок:

- на запрос к реализованному методу [PerformTransaction](merchant-api.md#performtransaction){:target="_blank"};
- на повторный запрос, к реализованному методу [PerformTransaction](merchant-api.md#performtransaction){:target="_blank"};
- на запрос к реализованному методу [CheckTransaction](merchant-api.md#checktransaction){:target="_blank"}.

**Отмените подтвержденную транзакцию**

!!! info "К СВЕДЕНИЮ"
    Отмену транзакции обеспечивает реализованный метод [CancelTransaction](merchant-api.md#canceltransaction){:target="_blank"}.

В разделе «Платежные запросы» нажмите на ссылку “CancelTransaction”.

<img src="https://i.ibb.co/gJTgQfh/image.png"  width="25%" border="0">

Убедитесь что в параметрах запуска теста присутствует id транзакции, статус транзакции “1” (транзакция создана) и запустите тест.

<img src="https://i.ibb.co/D1x3qTV/image.png"  width="100%" border="0">

!!! info "К СВЕДЕНИЮ"
    На запросы к реализованным методам [CancelTransaction](merchant-api.md#canceltransaction){:target="_blank"} и [CheckTransaction](merchant-api.md#checktransaction){:target="_blank"}, реализованное Merchant API возвращает ответы без ошибок.
