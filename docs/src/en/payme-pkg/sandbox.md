---
title: Sandbox
description: Sandbox
---

<!-- Google tag (gtag.js) -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-9BRKYLP6BB"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());

  gtag('config', 'G-9BRKYLP6BB');
</script>

# Sandbox


!!! info
    Testing on a production server creates additional load. Accounts associated with malfunctioning applications are blocked.

### About sandbox

**Sandbox** — _environment for safe testing of the implemented [Merchant API](merchant-api.md){:target="_blank"}. Sandbox tests will help verify the interaction of the implemented API with Payme Business. Sandbox testing allows you to get a detailed description of the [errors](https://developer.help.paycom.uz/protokol-merchant-api/obschie-oshibki){:target="_blank"}._

???+ info
    The merchant developer initiates testing and runs tests. Testing is carried out using [requests](https://developer.help.paycom.uz/protokol-merchant-api/format-zaprosa){:target="_blank"} and [responses](https://developer.help.paycom.uz/protokol-merchant-api/format-otveta){:target="_blank"}. Requests are sent by the Payme Business server, responses are sent by the merchant server.


### Preparing for testing

Add a web cash register in the merchant's account. After creating a web cash register, Payme Business will issue 2 keys:

- key for cabinet — key;
- key for sandbox — TEST_KEY.

!!! info ""
    **Go to [sandbox](https://test.paycom.uz/){:target="_blank"}. In the sandbox, enter Merchant ID (web cash register ID) and TEST_KEY.**

!!! info
    Merchant ID is stored in the web cash register developer settings.

<img src="https://i.ibb.co/jVY9Lzq/image.png" width="100%" border="0">

!!! info
    It is important that the Endpoint URL is specified in the cash register settings - the billing web address. Payme Business will send inquiries to this address.

When creating transactions in the sandbox, it is important to correctly specify the account type:

- Money can be transferred to your **savings account** an unlimited number of times. An example of a savings account is a mobile operator account;
- To a **one-time account**, money can be received only 1 time. An example of a one-time invoice is an order in an online store.

!!! info
    Testing of [payment initialization](initializing-payments.md){:target="_blank"} is recommended to be carried out only after successful completion of testing in the sandbox: first test the payment initialization in the sandbox, then in production.

**Sandbox url:** [https://test.paycom.uz](https://test.paycom.uz){:target="_blank"}

**URL for sending a check to the sandbox:** [https://test.paycom.uz](https://test.paycom.uz){:target="_blank"}

**URL for sending a check to the production:** [https://checkout.paycom.uz](https://checkout.paycom.uz){:target="_blank"}


### Testing

Testing is carried out according to 2 scenarios:

1. [Creating and canceling an unconfirmed transaction](#_4)
2. [Creating, confirming and canceling a confirmed financial transaction](#_5)

The first scenario includes a security check, so the first scenario is tested first, then the second.

!!! info
    The Merchant API has already been implemented in the payment plugin, so testing of the payment plugin is carried out according to the same scenarios.

#### Creating and canceling an unconfirmed transaction

Log in to the store as a customer. Add the item to your cart and pay for your order using Payme. After payment there will be an automatic transition to the “Sandbox” to the page for creating a financial transaction.

**Check authorization with incorrect credentials**

In the “Invalid Data” section, click on the “Invalid Authorization” link and run the test.

<img src="https://i.ibb.co/DkyRw6m/image.png"  width="25%" border="0">

!!! info
    For requests to implemented methods, the implemented Merchant API returns responses with error -32504: “Insufficient privileges to execute the method.”

**Check payment with incorrect or invalid amount**

In the “Incorrect Data” section, click on the “Invalid Amount” link.

<img src="https://i.ibb.co/QX1ybh3/image.png"  width="25%" border="0">

In the test parameters, specify a valid order number, an incorrect amount and run the test.

<img src="https://i.ibb.co/6v5QBYR/image.png"  width="100%" border="0">

!!! info
    For requests to the implemented methods [CheckPerformTransaction](merchant-api.md#checkperformtransaction){:target="_blank"} and [CreateTransaction](merchant-api.md#checktransaction){:target="_blank"}, implemented by the Merchant API returns responses with error -31001: "Invalid amount."

**Check payment of a non-existent invoice**

In the “Invalid data” section, click on the “Nonexistent account” link.

<img src="https://i.ibb.co/Dw4hnR5/image.png"  width="25%" border="0">

In the test parameters, specify the actual order amount, an incorrect order number and run the test.

<img src="https://i.ibb.co/DMcCcsh/image.png"  width="100%" border="0">

!!! info
    For requests to the implemented methods [CheckPerformTransaction](merchant-api.md#checkperformtransaction){:target="_blank"} and [CreateTransaction](merchant-api.md#checktransaction){:target="_blank"}, implemented by the Merchant API returns responses with errors -31050 - -31099: “Invalid order code.”

**Check the possibility of creating a financial transaction**

!!! info
    Checking the possibility of creating a financial transaction is ensured by the implemented method [CheckPerformTransaction](merchant-api.md#checkperformtransaction){:target="_blank"}.

In the “Payment Requests” section, click on the “CheckPerformTransaction” link.

<img src="https://i.ibb.co/rfTnDZL/image.png"  width="25%" border="0">

Make sure that the test parameters include the value of the Account parameter and the payment amount in tiyins and run the test.

<img src="https://i.ibb.co/T4NsGQ7/image.png"  width="100%" border="0">

When a request is made to the implemented CheckPerformTransaction method, the implemented Merchant API returns a response without errors.

**Create a transaction**

!!! info
    The creation of a transaction is ensured by the implemented method [CreateTransaction](merchant-api.md#checktransaction){:target="_blank"}.

In the Payment Requests section, click on the “CreateTransaction” link.

<img src="https://i.ibb.co/S5d5qsK/image.png"  width="25%" border="0">

Make sure that in the test launch parameters the account type is “One-time” and the account status is “Awaiting payment” and run the test.

<img src="https://i.ibb.co/mv3ZFhb/image.png"  width="100%" border="0">

!!! info
    Requests for the CreateTransaction, PerformTransaction, and CancelTransaction methods are sent twice. If the first request fails, the second one will definitely pass. When repeated calls to the CreateTransaction, PerformTransaction, CancelTransaction methods, the response must match the response from the first request.

The implemented Merchant API returns:

- to a request to the implemented method [CheckPerformTransaction](merchant-api.md#checkperformtransaction){:target="_blank"} - response with the result “allow”: true;
- to a request to the implemented method [CreateTransaction](merchant-api.md#createtransaction){:target="_blank"} - response without errors;
- for a repeated request to the implemented method [CreateTransaction](merchant-api.md#createtransaction){:target="_blank"} - response without errors;
- to a request to the implemented method [CheckTransaction](merchant-api.md#checktransaction){:target="_blank"} - response without errors;
- to a request to the implemented method [CreateTransaction](merchant-api.md#createtransaction){:target="_blank"} with a new transaction and the account status “Waiting for payment” - a response with error -31008: “The operation cannot be completed.”

**Cancel an unconfirmed transaction**

!!! info
    Transaction cancellation is ensured by the implemented [CancelTransaction](merchant-api.md#canceltransaction){:target="_blank"} method.

Cancellation of a transaction is ensured by the implemented one. In the “Payment requests” section, click on the “CancelTransaction” link. method [CancelTransaction](merchant-api.md#canceltransaction){:target="_blank"}.

<img src="https://i.ibb.co/92qWbJw/image.png"  width="25%" border="0">

Make sure that the test launch parameters include the transaction id and transaction status “1” (transaction created) and run the test.

<img src="https://i.ibb.co/2KdF3Bh/image.png"  width="100%" border="0">

!!! info
    For requests to the implemented methods [CancelTransaction](merchant-api.md#canceltransaction){:target="_blank"} and [CheckTransaction](merchant-api.md#checktransaction){:target="_blank"}, implemented by the Merchant API returns responses without errors.

#### Creating, confirming and canceling a confirmed financial transaction

Log in to the store as a customer. Add the item to your cart and pay for your order using Payme. After payment there will be an automatic transition to the “Sandbox” to the page for creating a financial transaction.

**Check the possibility of creating a financial transaction**

!!! info
    Checking the possibility of creating a financial transaction is ensured by the implemented method [CheckPerformTransaction](merchant-api.md#checkperformtransaction){:target="_blank"}.

In the “Payment Requests” section, click on the “CheckPerformTransaction” link.

<img src="https://i.ibb.co/hZS7KNQ/image.png"  width="25%" border="0">

Make sure that the test parameters include the value of the Account parameter and the payment amount in tiyins and run the test.

<img src="https://i.ibb.co/7SJHKvf/image.png"  width="100%" border="0">

When a request is made to the implemented CheckPerformTransaction method, the implemented Merchant API returns a response without errors.

**Create a transaction**

!!! info
    The creation of a transaction is ensured by the implemented method [CreateTransaction](merchant-api.md#createtransaction){:target="_blank"}.

In the Payment Requests section, click on the “CreateTransaction” link.

<img src="https://i.ibb.co/S5d5qsK/image.png"  width="25%" border="0">

Make sure that in the test launch parameters the account type is “One-time” and the account status is “Awaiting payment” and run the test.

<img src="https://i.ibb.co/S3YrpD5/image.png"  width="100%" border="0">

The implemented Merchant API returns:

- to a request to the implemented method [CheckPerformTransaction](merchant-api.md#checkperformtransaction){:target="_blank"} - response with the result “allow”: true;
- to a request to the implemented method [CreateTransaction](merchant-api.md#createtransaction){:target="_blank"} - response without errors;
- for a repeated request to the implemented method [CreateTransaction](merchant-api.md#createtransaction){:target="_blank"} - response without errors;
- to a request to the implemented method [CheckTransaction](merchant-api.md#checktransaction){:target="_blank"} - response without errors;
- to a request to the implemented method [CreateTransaction](merchant-api.md#createtransaction){:target="_blank"} with a new transaction and the account status “Waiting for payment” - a response with error -31008: “The operation cannot be completed.”

**Confirm the transaction**

!!! info
    Transaction confirmation is provided by the implemented [PerformTransaction](merchant-api.md#performtransaction){:target="_blank"} method.

In the “Payment Requests” section, click on the “PerformTransaction” link.

<img src="https://i.ibb.co/QPbn0n0/image.png"  width="25%" border="0">

Make sure that the test launch parameters include the transaction id and transaction status “1” (created) and run the test.

<img src="https://i.ibb.co/FY85s7t/image.png"  width="100%" border="0">

The implemented Merchant API returns a response without errors:

- to a request to the implemented method [PerformTransaction](merchant-api.md#performtransaction){:target="_blank"};
- for a repeated request to the implemented method [PerformTransaction](merchant-api.md#performtransaction){:target="_blank"};
- to a request to the implemented method [CheckTransaction](merchant-api.md#checktransaction){:target="_blank"}.

**Cancel a confirmed transaction**

!!! info
    Transaction cancellation is ensured by the implemented [CancelTransaction](merchant-api.md#canceltransaction){:target="_blank"} method.

In the Payment Requests section, click on the “CancelTransaction” link.

<img src="https://i.ibb.co/gJTgQfh/image.png"  width="25%" border="0">

Make sure that the test launch parameters include the transaction id and transaction status “1” (transaction created) and run the test.

<img src="https://i.ibb.co/D1x3qTV/image.png"  width="100%" border="0">

!!! info
    For requests to the implemented methods [CancelTransaction](merchant-api.md#canceltransaction){:target="_blank"} and [CheckTransaction](merchant-api.md#checktransaction){:target="_blank"}, implemented by the Merchant API returns responses without errors.
