[ОПІСМ_практична_01_бланк.md](https://github.com/user-attachments/files/32243972/_._01_.md)
# OPISM_pr01_Iovchev# Практична робота № 1

**Дисципліна:** Основи побудови інформаційних систем та мереж

**Тема:** Спостереження за процесом звернення до вебресурсу. Побудова власної моделі рівнів взаємодії

| | |
|---|---|
| **Прізвище, ім'я** | Іовчев Артем |
| **Група** | ІПЗ-2.01 |
| **Номер варіанта** | 7 |
| **Домен варіанта** | r-project.org |
| **Середовище виконання** |  Windows  |
| **Версія curl** | curl 8.21.0 (Windows) libcurl/8.21.0 Schannel zlib/1.3.2 WinIDN WinLDAP |
| **Дата виконання** |13.09.2026 |

---

## Частина A. Збір експериментальних даних

### A.1. Запит із діагностичним виводом

**Команда:**

```
curl -v https://r-project.org
```

**Вивід:**

```
* Host r-project.org:443 was resolved.
* IPv6: (none)
* IPv4: 137.208.57.37
*   Trying 137.208.57.37:443...
* schannel: disabled automatic use of client certificate
* ALPN: curl offers http/1.1
* ALPN: server accepted http/1.1
* Established connection to r-project.org (137.208.57.37 port 443) from 192.168.0.199 port 62009
* using HTTP/1.x
> GET / HTTP/1.1
> Host: r-project.org
> User-Agent: curl/8.21.0
> Accept: */*
>
* Request completely sent off
* schannel: remote party requests renegotiation
* schannel: renegotiating SSL/TLS connection
* schannel: SSL/TLS connection renegotiated
* schannel: remote party requests renegotiation
* schannel: renegotiating SSL/TLS connection
* schannel: SSL/TLS connection renegotiated
< HTTP/1.1 301 Moved Permanently
< Date: Wed, 09 Sep 2026 13:19:54 GMT
< Server: Apache
< Location: https://www.r-project.org/
< Content-Length: 338
< Content-Type: text/html; charset=iso-8859-1
<
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">
<html><head>
<title>301 Moved Permanently</title>
</head><body>
<h1>Moved Permanently</h1>
<p>The document has moved <a href="https://www.r-project.org/">here</a>.</p>
<hr>
<address>Apache Server at r-project.org Port 443</address>
</body></html>
* Connection #0 to host r-project.org:443 left intact
```

---

### A.2. Запит без захисту з'єднання

**Команда:**

```
curl -v http://r-project.org
```

**Вивід:**

```
* Host r-project.org:80 was resolved.
* IPv6: (none)
* IPv4: 137.208.57.37
*   Trying 137.208.57.37:80...
* Established connection to r-project.org (137.208.57.37 port 80) from 192.168.0.199 port 60526
* using HTTP/1.x
> GET / HTTP/1.1
> Host: r-project.org
> User-Agent: curl/8.21.0
> Accept: */*
>
* Request completely sent off
< HTTP/1.1 301 Moved Permanently
< Date: Wed, 09 Sep 2026 13:23:36 GMT
< Server: Apache
< Location: http://www.r-project.org/
< Content-Length: 336
< Content-Type: text/html; charset=iso-8859-1
<
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">
<html><head>
<title>301 Moved Permanently</title>
</head><body>
<h1>Moved Permanently</h1>
<p>The document has moved <a href="http://www.r-project.org/">here</a>.</p>
<hr>
<address>Apache Server at r-project.org Port 80</address>
</body></html>
* Connection #0 to host r-project.org:80 left intact
```

---

### A.3. Запит до служби доменних імен

*Windows: `Resolve-DnsName ВАШ_ДОМЕН`*

**Команда (перше виконання):**

```
Resolve-DnsName r-project.org
```

**Вивід:**

```
Name                                           Type   TTL   Section    IPAddress
----                                           ----   ---   -------    ---------
r-project.org                                  A      7200  Answer     137.208.57.37
```

**Команда (повторне виконання через 5–7 хвилин):**

```
Resolve-DnsName r-project.org 
```

**Вивід:**

```
Name                                           Type   TTL   Section    IPAddress
----                                           ----   ---   -------    ---------
r-project.org                                  A      0     Answer     137.208.57.37
```

**Зафіксовані значення:**

| Параметр | Перше виконання | Повторне виконання |
|---|---|---|
| Час виконання (год:хв) | 9:24| 9:29|
| IP-адреса |137.208.57.37 | 137.208.57.37|
| Значення TTL | 7200 | 0|

> Якщо друге значення TTL виявилося більшим за перше — це нормально: кеш резолвера встиг оновитися. Зафіксуйте як є.

---

### A.4. Контрольний ресурс

**Команда:**

```
curl -v https://google.com
```

**Вивід:**

```
* Host google.com:443 was resolved.
* IPv6: (none)
* IPv4: 142.250.130.139
*   Trying 142.250.130.139:443...
* schannel: disabled automatic use of client certificate
* ALPN: curl offers http/1.1
* ALPN: server accepted http/1.1
* Established connection to google.com (142.250.130.139 port 443) from 192.168.0.199 port 50137
* using HTTP/1.x
> GET / HTTP/1.1
> Host: google.com
> User-Agent: curl/8.21.0
> Accept: */*
>
* Request completely sent off
* schannel: remote party requests renegotiation
* schannel: renegotiating SSL/TLS connection
* schannel: SSL/TLS connection renegotiated
< HTTP/1.1 301 Moved Permanently
< Location: https://www.google.com/
< Content-Type: text/html; charset=UTF-8
< Content-Security-Policy-Report-Only: object-src 'none';base-uri 'self';script-src 'nonce-6vXRCxV5tQWDc2454YdxGg' 'strict-dynamic' 'report-sample' 'unsafe-eval' 'unsafe-inline' https: http:;report-uri https://csp.withgoogle.com/csp/gws/other-hp
< Date: Wed, 09 Sep 2026 13:38:47 GMT
< Expires: Fri, 09 Oct 2026 13:38:47 GMT
< Cache-Control: public, max-age=2592000
< Server: gws
< Content-Length: 220
< X-XSS-Protection: 0
< X-Frame-Options: SAMEORIGIN
< Alt-Svc: h3=":443"; ma=2592000,h3-29=":443"; ma=2592000
<
<HTML><HEAD><meta http-equiv="content-type" content="text/html;charset=utf-8">
<TITLE>301 Moved</TITLE></HEAD><BODY>
<H1>301 Moved</H1>
The document has moved
<A HREF="https://www.google.com/">here</A>.
</BODY></HTML>
* Connection #0 to host google.com:443 left intact
```

---

### A.5. Ресурси з некоректною конфігурацією сертифіката

**Випадок 1**

```
curl -v https://expired.badssl.com
```

```
* Host expired.badssl.com:443 was resolved.
* IPv6: (none)
* IPv4: 104.154.89.105
*   Trying 104.154.89.105:443...
* schannel: disabled automatic use of client certificate
* ALPN: curl offers http/1.1
* schannel: next InitializeSecurityContext failed: SEC_E_CERT_EXPIRED (0x80090328) - The received certificate has expired.
* closing connection #0
curl: (35) schannel: next InitializeSecurityContext failed: SEC_E_CERT_EXPIRED (0x80090328) - The received certificate has expired.
```

**Випадок 2**

```
curl -v https://wrong.host.badssl.com
```

```
*   Trying 104.154.89.105:443...
* Host wrong.host.badssl.com:443 was resolved.
* IPv6: (none)
* IPv4: 104.154.89.105
* schannel: disabled automatic use of client certificate
* ALPN: curl offers http/1.1
* schannel: SNI or certificate check failed: SEC_E_WRONG_PRINCIPAL (0x80090322) - The target principal name is incorrect.
* closing connection #0
curl: (60) schannel: SNI or certificate check failed: SEC_E_WRONG_PRINCIPAL (0x80090322) - The target principal name is incorrect.
More details here: https://curl.se/docs/sslcerts.html

curl failed to verify the legitimacy of the server and therefore could not
establish a secure connection to it. To learn more about this situation and
how to fix it, please visit the webpage mentioned above.
```

**Випадок 3**

```
curl -v https://self-signed.badssl.com
```

```
*   Trying 104.154.89.105:443...
* Host self-signed.badssl.com:443 was resolved.
* IPv6: (none)
* IPv4: 104.154.89.105
* schannel: disabled automatic use of client certificate
* ALPN: curl offers http/1.1
* schannel: SEC_E_UNTRUSTED_ROOT (0x80090325) - The certificate chain was issued by an authority that is not trusted.
* closing connection #0
curl: (60) schannel: SEC_E_UNTRUSTED_ROOT (0x80090325) - The certificate chain was issued by an authority that is not trusted.
More details here: https://curl.se/docs/sslcerts.html

curl failed to verify the legitimacy of the server and therefore could not
establish a secure connection to it. To learn more about this situation and
how to fix it, please visit the webpage mentioned above.
```

> Якщо використано альтернативний спосіб із параметром `--resolve` — зазначити це та навести фактичну команду.

---

## Частина B. Власна модель рівнів

**Кількість виділених груп:** ___

| № | Назва групи (власне формулювання) | Рядки виводу, віднесені до групи | Обґрунтування |
|---|---|---|---|
| 1 | Передача даних| > GET / HTTP/1.1 
< HTTP/1.1 301 Moved Permanently | Взаємодія клієнта з сервером під час отримання ресурсу|
| 2 | Захист з'єднання | schannel: ... SSL/TLS connection SEC_E_CERT_EXPIRED SEC_E_WRONG_PRINCIPAL SEC_E_UNTRUSTED_ROOT | Забезпечує захищенний обмін данними та перевірку сертифікату сервера |
| 3 | Пошук сервера | Host r-project.org:443 was resolved. Host google.com:443 was resolved. | Перетворює доменне ім’я на IP-адресу сервера, до якого потрібно підключитися. |
| 4 | Мережеве підключення| Trying 137.208.57.37:443... Established connection to r-project.org | Забезпечує фізичну та мережеву передачу даних між клієнтом і сервером.|


*Групи впорядковано від найближчої до користувача (№ 1) до найближчої до апаратного забезпечення. Зайві рядки вилучити, за потреби — додати.*

**Рядки, які не вдалося віднести до жодної групи:**

| Рядок виводу | Причина утруднення |
|---|---|
| | |
| | |
| | |

---

## Контрольні питання

**1. Скільки рядків діагностичного виводу передує отриманню даних сторінки (завдання A.1)?**

> 26 рядків діагностичного виводу передує отриманню даних сторінки з завдання А.1

**2. Які рядки наявні у виводі A.1 і відсутні у виводі A.2? Чим це зумовлено?**

> У А.1 наявні рядки про запит узгодження з'єднання з сервером, у виводі А.2 вони відсутні. Це зумовлено тим, що запит був зроблений без захисту з'єднання.

**3. Звідки у виводі з'явилося значення `443`, якщо його не було вказано в адресі?**

> 443 це стандартний порт для HTTPS-з'єднання, який використовується за замовчуванням, якщо не вказано інший порт у URL.

**4. Як змінилося значення TTL між двома запитами (A.3)? Що означає це число?**

> Значення TTL між двома запитами змінився у 7200 секунд. Це число значить час життя DNS, протягом якого сервер зберігає відповідь.

**5. Чим відрізняються між собою три причини помилок із завдання A.5? Сформулювати кожну однією фразою.**

| Випадок | Причина недовіри |
|---|---|
| `expired` | вичерпаний термін дії сертифікату |
| `wrong.host` | сертифікат видано не для цього домену|
| `self-signed` | не підтверджений сертифікат |

**6. Три рядки з власних виводів, про які не йшлося на лекції 1:**

| № | Рядок виводу | Джерело (номер завдання) |
|---|---|---|
| 1 | ALPN: curl offers http/1.1 | А.1|
| 2 | ALPN: server accepted http/1.1 |А.1 |
| 3 | | |

*Пояснення до цих рядків не потрібне.*

---

## Висновки

*150–300 слів. Спиратися на власні спостереження, а не на матеріал лекції.*

**D.1. Що виявилося неочевидним або несподіваним**

*Назвати конкретно, з посиланням на рядок виводу.*

> У пункті А.3 було неочевидним та несподіваним значення TTL. Перший запит TTL був 7200, а після повторного запиту вже був 0, пробував декілька разів, та значення ніяк не змінювалося, перевіривши інформацію, виявилося чому значення TTL у другому запиті дорівнює 0, це означає, що кеш резолвера оновився і більше не зберігає запис про домен, тому при повторному запиті він повертає 0, та ніяких проблем, виходить, не було.

**D.2. Чому саме така кількість груп у частині B**

*На якій підставі ухвалено рішення. Що змусило б його змінити.*

> Я вважаю що 4 групи буде достатньо, оскільки вони охоплюють всі аспекти взаємодії клієнта з сервером. Якщо б з'явилися додаткові специфічні рядки виводу, які не вписуються в ці категорії, можливо, довелося б додати ще одну групу.

**D.3. Питання, яке залишилося без відповіді**

> 

---

## Використання штучного інтелекту

*Розділ обов'язковий. Заповнюється незалежно від того, чи використовувався ШІ. Детальні вимоги — у документі «Політика використання технологій штучного інтелекту».*

**Факт використання:** використано / не використано *(потрібне залишити)*

**Установлений рівень для цієї роботи:** Р3 — ШІ як співвиконавець

**Фактичний рівень використання:** Р-3 

### Використані системи

| Система | Версія або модель | Період використання |
|---|---|---|
| ChatGPT | GPT-5.6 Luna | 14.09.2026 |

### Промпти

*Наводити дослівно, у тому вигляді, у якому запит було надано системі. Переказ не приймається.*

| № | Розділ роботи | Текст промпта |
|---|---|---|
| 1 |A| Що відбувається в цих строках : Request completely sent off...  | 
| 2 |B|Поясни, як розташувати ці групи від найближчої до користувача до найближчої до апаратного забезпечення.|
| 3 | | |

### Дії з отриманим результатом

| № промпта | Що перевірено | Що змінено | Що відхилено і чому |
|---|---|---|---|
| 1 |Що відбувається в строках | Нічого| Було запитано для розуміння
| 2 |Було перевірено взаємодію груп з клієнтом і сервером | Майже нічого| Запропонування додати ще декілько груп. Відхилив тому, що на мою думку, такої кількості яка є, вистачить|
| 3 | | | |

### Підтвердження

Підтверджую, що всі наведені в цьому звіті виводи команд отримано мною особисто внаслідок фактичного виконання відповідних дій, а відомості цього розділу є повними та достовірними.

> Виводи `curl`, `dig` та інші артефакти не можуть бути згенеровані. Це стосується будь-якого рівня використання ШІ.

---

## Примітки виконавця

*(необов'язковий розділ: що не спрацювало, які команди довелося змінити, які виникли труднощі)*

>Дуже багато часу було проведено з завданням В, доводилося переробляти через неправильне оформлення, не обійшлося без ШІ, який було використано лише в навчальному плані. 
