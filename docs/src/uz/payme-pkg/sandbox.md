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

!!! info "Ma'lumot"
    Test serverda qo'shimcha yuk yaratadi. Noto'g'ri ishlaydigan ilovalar bilan bog'liq hisoblar bloklanadi.

### Sandbox haqida

**Sandbox** — _amalga oshirilgan [Merchant API](merchant-api.md){:target="_blank"} xavfsiz sinov muhiti. Sandbox testlari joriy qilingan API ning Payme Business bilan o‘zaro aloqasini tekshirishga yordam beradi. Sandbox testi [xatolar](https://developer.help.paycom.uz/protokol-merchant-api/obschie-oshibki){:target="_blank"} batafsil tavsifini olish imkonini beradi._

???+ info "Ma'lumot"
    Merchant dasturchisi testlashni boshlaydi va testlarni o'tkazadi. Test [so'rovlar](https://developer.help.paycom.uz/protokol-merchant-api/format-zaprosa){:target="_blank"} va [javoblar](https://developer.help.paycom.uz/protokol-merchant-api/format-otveta){:target="_blank"}. So'rovlar Payme Business serveri tomonidan yuboriladi, javoblar merchant serveri tomonidan yuboriladi.


### Testga tayyorgarlik

Merchantning hisobiga veb-kassa apparatini qo'shing. Veb-kassa apparatini yaratgandan so'ng Payme Business ikkita kalitni chiqaradi:

- kabinet uchun kalit — key;
- sandbox uchun kalit — TEST_KEY.

!!! info ""
    **[Sandbox](https://test.paycom.uz/){:target="_blank"}ga kiring. Sandboxda Merchant ID (veb-kassa ID'si) va TEST_KEY kiriting.**

!!! info "Ma'lumot"
    Merchant ID veb-kassa dasturchisi sozlamalarida saqlanadi.

<img src="https://i.ibb.co/jVY9Lzq/image.png" width="100%" border="0">

!!! info "Ma'lumot"
    Endpoint URL manzili kassa sozlamalarida - hisob-kitob veb-manzilida ko'rsatilishi muhim. Payme Business ushbu manzilga so'rov yuboradi.

Sandboxda tranzaktsiyalarni yaratishda hisob turini to'g'ri ko'rsatish muhimdir:

- Pulni **jamg'arma hisob raqamiga** cheklanmagan miqdorda o'tkazish mumkin. Jamg'arma hisobiga misol sifatida uyali aloqa operatorining hisob raqamini ko'rsatish mumkin;
- **bir martalik hisobga** pulni faqat 1 marta olish mumkin. Bir martalik hisob-fakturaga misol - onlayn-do'kondagi buyurtma.

!!! info "Ma'lumot"
    [Tezkor to'lovlar](initializing-payments.md){:target="_blank"} testini sinov muhitida testdan muvaffaqiyatli oʻtgandan keyingina oʻtkazish tavsiya etiladi: avval tezkor to'lovlarni test muhitida, keyin esa productionda sinab koʻring.

**Sandbox sayti:** [https://test.paycom.uz](https://test.paycom.uz){:target="_blank"}

**Sandboxda chek yuborish uchun:** [https://test.paycom.uz](https://test.paycom.uz){:target="_blank"}

**Productionda chek yuborish uchun:** [https://checkout.paycom.uz](https://checkout.paycom.uz){:target="_blank"}


### Testlash

Test 2 senariy bo'yicha amalga oshiriladi:

1. [Tasdiqlanmagan tranzaksiyani yaratish va bekor qilish](#_4)
2. [Tasdiqlangan moliyaviy operatsiyani yaratish, tasdiqlash va bekor qilish](#_5)

Birinchi senariy xavfsizlik tekshiruvini o'z ichiga oladi, shuning uchun birinchi senariy avval sinovdan o'tkaziladi, keyin ikkinchisi.

!!! info "Ma'lumot"
    Merchant API allaqachon to'lov plaginida joriy qilingan, shuning uchun to'lov plaginini sinovdan o'tkazish xuddi shu senariylar bo'yicha amalga oshiriladi.

#### Tasdiqlanmagan tranzaksiyani yaratish va bekor qilish

Do'konga mijoz sifatida kiring. Buyumni savatga qo'shing va buyurtmangiz uchun Payme orqali to'lang. To'lovdan so'ng moliyaviy operatsiyani yaratish sahifasiga "Sandbox" ga avtomatik o'tish amalga oshiriladi.

**Noto'g'ri hisob ma'lumotlari bilan avtorizatsiyani tekshiring**

"Yaroqsiz ma'lumotlar" bo'limida "Yaroqsiz avtorizatsiya" havolasini bosing va testni o'tkazing.

<img src="https://i.ibb.co/DkyRw6m/image.png"  width="25%" border="0">

!!! info "Ma'lumot"
    Amalga oshirilgan usullarga so'rovlar uchun joriy Merchant API javoblarni -32504 xato bilan qaytaradi: "Usulni bajarish uchun imtiyozlar etarli emas".

**To'lovni noto'g'ri yoki mavjud bo'lmagan summa bilan tekshiring**

"Неверные данные" bo'limida "Неверная сумма" havolasini bosing.

<img src="https://i.ibb.co/QX1ybh3/image.png"  width="25%" border="0">

"Неверные данные" bo'limida "Неверная сумма" havolasini bosing. Test parametrlarida to'g'ri buyurtma raqamini, noto'g'ri miqdorni belgilang va testni o'tkazing.

<img src="https://i.ibb.co/6v5QBYR/image.png"  width="100%" border="0">

!!! info "Ma'lumot"
    Amalga oshirilgan [CheckPerformTransaction](merchant-api.md#checkperformtransaction){:target="_blank"} va [CreateTransaction](merchant-api.md#checktransaction){:target="_blank"} metodlariga so'rovlar uchun Merchant API javoblarni -31001 xatosi bilan qaytaradi: "Noto'g'ri miqdor".

**Mavjud bo'lmagan hisob-fakturaning to'lovini tekshiring**

"Неверные данные" bo'limida "Несуществующий счёт" havolasini bosing.

<img src="https://i.ibb.co/Dw4hnR5/image.png"  width="25%" border="0">

Test parametrlarida haqiqiy buyurtma miqdorini, noto'g'ri buyurtma raqamini belgilang va testni o'tkazing.

<img src="https://i.ibb.co/DMcCcsh/image.png"  width="100%" border="0">

!!! info "Ma'lumot"
    Amalga oshirilgan [CheckPerformTransaction](merchant-api.md#checkperformtransaction){:target="_blank"} va [CreateTransaction](merchant-api.md#checktransaction){:target="_blank"} metodlariga so'rovlar uchun Merchant API -31050 - -31099 xatolar bilan javoblarni qaytaradi: “Buyurtma kodi noto'g'ri”.

**Moliyaviy operatsiyani yaratish imkoniyatini tekshiring**

!!! info "Ma'lumot"
    Moliyaviy operatsiyani yaratish imkoniyatini tekshirish amalga oshirilgan [CheckPerformTransaction](merchant-api.md#checkperformtransaction){:target="_blank"} metodi bilan ta'minlanadi.

"Платежные запросы" bo'limida "CheckPerformTransaction" havolasini bosing.

<img src="https://i.ibb.co/rfTnDZL/image.png"  width="25%" border="0">

Test parametrlari Hisob parametri qiymatini va tiyinlardagi toʻlov miqdorini oʻz ichiga olganligiga ishonch hosil qiling va testni oʻtkazing.

<img src="https://i.ibb.co/T4NsGQ7/image.png"  width="100%" border="0">

Amalga oshirilgan CheckPerformTransaction metodiga so'rov yuborilganda, joriy Merchant API xatosiz javob qaytaradi.

**Tranzaksiya yarating**

!!! info "Ma'lumot"
    Tranzaktsiyani yaratish amalga oshirilgan [CreateTransaction](merchant-api.md#checktransaction){:target="_blank"} metodi bilan ta'minlanadi.

"Платежные запросы" bo'limida "CreateTransaction" havolasini bosing.

<img src="https://i.ibb.co/S5d5qsK/image.png"  width="25%" border="0">

Testni ishga tushirish parametrlarida hisob turi “Одноразовый” va hisob holati “Ожидает оплаты” ekanligiga ishonch hosil qiling va testni oʻtkazing.

<img src="https://i.ibb.co/mv3ZFhb/image.png"  width="100%" border="0">

!!! info "Ma'lumot"
    CreateTransaction, PerformTransaction va CancelTransaction metodlari uchun so'rovlar ikki marta yuboriladi. Agar birinchi so'rov bajarilmasa, ikkinchisi albatta o'tadi. CreateTransaction, PerformTransaction, CancelTransaction metodlari takroriy so'rovlar bo'lsa, javob birinchi so'rovdagi javobga mos kelishi kerak.

Amalga oshirilgan Merchant API qaytaradi:

- amalga oshirilgan [CheckPerformTransaction](merchant-api.md#checkperformtransaction){:target="_blank"} metodi bo'yicha so'rovga - "allow": true;
- amalga oshirilgan [CreateTransaction](merchant-api.md#createtransaction){:target="_blank"} metodi bo'yicha so'rovga - xatosiz javob;
- amalga oshirilgan [CreateTransaction](merchant-api.md#createtransaction){:target="_blank"} metodiga takroriy so'rov uchun - xatosiz javob;
- amalga oshirilgan [CheckTransaction](merchant-api.md#checktransaction){:target="_blank"} metodi bo'yicha so'rovga - xatosiz javob;
- amalga oshirilgan [CreateTransaction](merchant-api.md#createtransaction){:target="_blank"} metodiga yangi tranzaksiya va hisob holati “В ожидании оплаты” soʻroviga -31008 xatoli javob: “Невозможно выполнить операцию".

**Tasdiqlanmagan tranzaksiyani bekor qiling**

!!! info "Ma'lumot"
    Tranzaksiyani bekor qilish joriy qilingan [CancelTransaction](merchant-api.md#canceltransaction){:target="_blank"} metodi bilan ta'minlanadi.

"Платежные запросы" bo'limida "CancelTransaction" havolasini bosing.

<img src="https://i.ibb.co/92qWbJw/image.png"  width="25%" border="0">

Testni ishga tushirish parametrlarida tranzaksiya identifikatori va tranzaksiya holati “1” (tranzaksiya yaratilgan) mavjudligiga ishonch hosil qiling va testni bajaring.

<img src="https://i.ibb.co/2KdF3Bh/image.png"  width="100%" border="0">

!!! info "Ma'lumot"
    Amalga oshirilgan [CancelTransaction](merchant-api.md#canceltransaction){:target="_blank"} va [CheckTransaction](merchant-api.md#checktransaction){:target="_blank"} metodlariga so'rovlar uchun Merchant API javoblarni xatosiz qaytaradi.

#### Tasdiqlangan moliyaviy operatsiyani yaratish, tasdiqlash va bekor qilish

Do'konga mijoz sifatida kiring. Buyumni savatga qo'shing va buyurtmangiz uchun Payme orqali to'lang. To'lovdan so'ng moliyaviy operatsiyani yaratish sahifasiga "Sandbox" ga avtomatik o'tish amalga oshiriladi.

**Moliyaviy operatsiyani yaratish imkoniyatini tekshiring**

!!! info "Ma'lumot"
    Moliyaviy operatsiyani yaratish imkoniyatini tekshirish amalga oshirilgan [CheckPerformTransaction](merchant-api.md#checkperformtransaction){:target="_blank"} usuli bilan ta'minlanadi.

"Платежные запросы" bo'limida "CheckPerformTransaction" havolasini bosing.

<img src="https://i.ibb.co/hZS7KNQ/image.png"  width="25%" border="0">

Test parametrlari Hisob parametri qiymatini va tiyinlardagi toʻlov miqdorini oʻz ichiga olganligiga ishonch hosil qiling va testni oʻtkazing.

<img src="https://i.ibb.co/7SJHKvf/image.png"  width="100%" border="0">

Amalga oshirilgan CheckPerformTransaction metodiga so'rov yuborilganda, joriy Merchant API xatosiz javob qaytaradi.

**Tranzaksiya yarating**

!!! info "Ma'lumot"
    Tranzaktsiyani yaratish amalga oshirilgan [CreateTransaction](merchant-api.md#createtransaction){:target="_blank"} usuli bilan ta'minlanadi.

"Платежные запросы" bo'limida "CreateTransaction" havolasini bosing.

<img src="https://i.ibb.co/S5d5qsK/image.png"  width="25%" border="0">

Testni ishga tushirish parametrlarida hisob turi “Одноразовый” va hisob holati “Ожидает оплаты” ekanligiga ishonch hosil qiling va testni oʻtkazing.

<img src="https://i.ibb.co/S3YrpD5/image.png"  width="100%" border="0">

Amalga oshirilgan Merchant API qaytaradi:

- amalga oshirilgan [CheckPerformTransaction](merchant-api.md#checkperformtransaction){:target="_blank"} metodi bo'yicha so'rovga - "allow": true;
- amalga oshirilgan [CreateTransaction](merchant-api.md#createtransaction){:target="_blank"} metodi bo'yicha so'rovga - xatosiz javob;
- amalga oshirilgan [CreateTransaction](merchant-api.md#createtransaction){:target="_blank"} metodi takroriy so'rov uchun - xatosiz javob;
- amalga oshirilgan [CheckTransaction](merchant-api.md#checktransaction){:target="_blank"} metodi bo'yicha so'rovga - xatosiz javob;
- joriy qilingan [CreateTransaction](merchant-api.md#createtransaction){:target="_blank"} metodiga yangi tranzaksiya va hisob holati “В ожидании оплаты” soʻroviga -31008 xatoli javob: “ Невозможно выполнить операцию"

**Tranzaktsiyani tasdiqlang**

!!! info "Ma'lumot"
    Tranzaksiyani tasdiqlash joriy qilingan [PerformTransaction](merchant-api.md#performtransaction){:target="_blank"} metodi bilan ta'minlanadi.

"Платежные запросы" bo'limida "PerformTransaction" havolasini bosing.

<img src="https://i.ibb.co/QPbn0n0/image.png"  width="25%" border="0">

Testni ishga tushirish parametrlarida tranzaksiya identifikatori va tranzaksiya holati “1” (yaratilgan) mavjudligiga ishonch hosil qiling va testni bajaring.

<img src="https://i.ibb.co/FY85s7t/image.png"  width="100%" border="0">

Amalga oshirilgan Merchant API javobni xatosiz qaytaradi:

- amalga oshirilgan [PerformTransaction](merchant-api.md#performtransaction){:target="_blank"} metodiga so'rovga;
- amalga oshirilgan [PerformTransaction](merchant-api.md#performtransaction){:target="_blank"} metodiga takroriy so'rov uchun;
- amalga oshirilgan [CheckTransaction](merchant-api.md#checktransaction){:target="_blank"} metodiga so'rovga.

**Tasdiqlangan tranzaksiyani bekor qiling**

!!! info "Ma'lumot"
    Tranzaksiyani bekor qilish joriy qilingan [CancelTransaction](merchant-api.md#canceltransaction){:target="_blank"} metodi bilan ta'minlanadi.

"Платежные запросы" bo'limida "CancelTransaction" havolasini bosing.

<img src="https://i.ibb.co/gJTgQfh/image.png"  width="25%" border="0">

Testni ishga tushirish parametrlarida tranzaksiya identifikatori va tranzaksiya holati “1” (tranzaksiya yaratilgan) mavjudligiga ishonch hosil qiling va testni bajaring.

<img src="https://i.ibb.co/D1x3qTV/image.png"  width="100%" border="0">

!!! info "Ma'lumot"
    Amalga oshirilgan [CancelTransaction](merchant-api.md#canceltransaction){:target="_blank"} va [CheckTransaction](merchant-api.md#checktransaction){:target="_blank"} metodlariga so'rovlar uchun Merchant API javoblarni xatosiz qaytaradi.
