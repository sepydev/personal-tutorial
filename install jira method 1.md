نصب Database
```
$ sudo apt-get update
$ sudo apt-get install postgresql postgresql-contrib
$ sudo update-rc.d postgresql enable
$ sudo service postgresql start
$ sudo su - postgres
$ psql
postgres=# CREATE USER jiradbuser WITH PASSWORD 'p@ssW0rd';
postgres=# CREATE DATABASE jiradb WITH ENCODING 'UNICODE' LC_COLLATE 'C' LC_CTYPE 'C' TEMPLATE template0;
postgres=# GRANT ALL PRIVILEGES ON DATABASE jiradb TO jiradbuser;
$ logout
```

نصب نرم‌افزار Jira
```
$ wget https://product-downloads.atlassian.com/software/jira/downloads/atlassian-jira-software-8.1.0-x64.bin
$ chmod a+x atlassian-jira-software-8.1.0-x64.bin
$ sudo ./atlassian-jira-software-8.1.0-x64.bin
```

سوال هشتم (مهم)
Installation of JIRA Software 8.1.0 is complete
Start JIRA Software 8.1.0 now?
Yes [y, Enter], No [n]

no


۱. در مرحله اول باید یکی از فایل های Jira به نام atlassian-extras-3.2.jar را با یک فایل دستکاری شده جایگزین کنیم.
۲. مرحله دوم،‌ وارد کردن شماره سریال جعلی برای Jira Software در هنگام بالا آمدن Jira برای اولین بار است.
۳. مرحله سوم، وارد کردن شماره سریال جعلی برای Jira Core در تنظیمات پنل Jira است.
```
$ sudo rm -f /opt/atlassian/jira/atlassian-jira/WEB-INF/lib/atlassian-extras-3.2.jar ; sudo wget http://bayanbox.ir/download/875654641841270819/atlassian-extras-3.2.jar -P /opt/atlassian/jira/atlassian-jira/WEB-INF/lib/
```

با خرید Plugin ها و افزودن آنها به Jira می‌توان امکانات تکمیلی ویژه ای مثل نمودار گانت، نمودار نقشه راه، اتصال به InvisionApp، ارتباط با Slack و تلگرام و ... را به این نرم‌افزار اضافه کرد. برای اینکه بتوانید Plugin های غیر رایگان را نیز در آینده کرک کنید، لازم است همین الان و قبل از اولین اجرای سرویس Jira دستور زیر را در ترمینال سرور اجرا کنید:

```
$ sudo rm -f /opt/atlassian/jira/atlassian-jira/WEB-INF/atlassian-bundled-plugins/atlassian-universal-plugin-manager-plugin-4.0.1.jar ; sudo wget http://bayanbox.ir/download/1902644824753031905/atlassian-universal-plugin-manager-plugin-4.0.1.jar -P /opt/atlassian/jira/atlassian-jira/WEB-INF/atlassian-bundled-plugins/

```

```
$ sudo service jira start
```

با زدن کلید Enter، صفحه تنظیمات اولیه Jira باز می‌شود. اگر این صفحه باز نشد، اول مطمین شوید کامپیوتر شما و سرور در یک شبکه قرار دارند (برای این کار می‌توانید سرور را از کامپیوتر خود Ping کنید) و اگر مشکل از شبکه نبود، احتمالا Firewall نصب شده روی سرور، پورت مورد استفاده ی Jira را مسدود کرده است. برای اطمینان می‌توانید باز بودن پورت روی سرور را با استفاده از این سایت بررسی کنید. اگر مطمین شدید که پورت استفاده شده بسته است می‌توانید از دستورات زیر در سرور برای باز کردن آن استفاده کنید:

```
$ iptables -A INPUT -m state --state NEW -p tcp --dport 8080 -j ACCEPT
$ /etc/init.d/iptables restart
```

در مرحله بعد (تصویر پایین) باید شماره سریالی که برای Jira خریده اید را وارد کنید. دقت کنید که اگر میخواهید Jira را کرک کنید از شماره سریال زیر استفاده کنید 
```
AAABmQ0ODAoPeJyFU9FOq0AQfecrSHymAa5V22QTDXAjBqiBauLjSqft3sDuZna32r+X0jairtzHPefMzJmdmYu/yNyc7t3g2g2u5uHNfDp10zJeuqEfzJwIgWomeEw1kAPi+VMvuHYiwTWtdUFbIC1sV2wb/Lma3W5ayppJLdqzIMk7gCgjpUB9i1QLRXkvWOCGcqb67KQcEBXgDjCNSX4ZL7x7v8i82f1d7GWp/+JUSWHFHw3WW6rgu8/CtK+Ai/WTAlTk0nf+MaQTOypRrEytJ4eHp8Rav1GEn9quI66BU15D8i4Z7k81Q/9QM/SdjNXA1S9kDKpGJvuuH7pCbnUqdPRQaYoakKxpo2DM1lfhBgH4VkgJOOl+ne2AaDSnBD8Ae8ahbJgPum5RIlPDFFbQntcq5aYtRQORMFwTLxiL/y49fe9yL6Ffv2iR50kZpXfZF9sjsr7Y/3i7mZGo89hXrB9uUiyT8rFMq8Rmy6IauvqNHjVlCWqOzHO3ugcmPJvsritLY+uBmdfPBe3nlexoY45n2i/bB3IidwkwLAIUYwdtWez2k7o6gccl3hU6CQpb4P4CFCQfFJDwdEBH3h7YcMhS5z+pKtUoX02jn
```

مرحله سوم کرک کردن برنامه
در این مرحله باید یک شماره سریال جعلی را در تنظیمات دشبورد برای Jira Core وارد کنیم.

از منوی بالای دشبورد، تصویر چرخ‌دنده و سپس گزینه Application را انتخاب کنید.
در پایین صفحه و زیر بخش Jira Core بر روی گزینه Paste licence کلیک کنید.
شماره سریال زیر را وارد کرده و بر روی دکنه Update licence کلیک کنید.
```
AAABlA0ODAoPeJyFU1FvgjAQfudXkOwZA8xpXNJkC7DIAmjQLdljhzftAm1zbc3890PUDAdsj/2+7+6+693dPCGzU3qwvantTe796b03s+M8XNu+682sAIFqJnhINZAj4rh3jje1AsE1LXRGKyAV7DZs591OZg/birJyVIjqIojSGiDKSClQPyDVQlHeCBa4pZypJjvJW8QKcA8YhyQdhwtn7maJM5s/hk4Su2/WKsp68aXBYkcV/PaZmeodcPHxogAVGbvWJ0M66kclio0p9Oj4cAqB0NXV3XANnPICoi/J8HCu57vHer5rJawArgbIEFSBTDYdP9dF7KAucqq90hQ1IPmgpYIhO9eiLQLwnZAScFT/NNsD0WjOwR2gm60taeeCukOUyFQ7vBfs5uyVcVPlooRAGK6J4w3F/padv3J9kNCsWbBI0ygP4sfkyu4fsqbQf3zXyB8Rl/FuWDPEKFtH+TKPV1GfpR5V29EQPWioJ6A8Ma/1eh4Z/2Kwvp4kDnsPyLz/LGEzo2hPS3M6w2axvgFmA2j4MCwCFBCT4uP9e8oYXy5+HvDKHZYt500iAhR5IbI2yXNPJc7Z6kehf1nS49e5hg==X02jj
```

