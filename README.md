# Домашнее задание к занятию 13.3. «Защита сети» - Кувайсков Дмитрий


### Подготовка к выполнению заданий

1. Подготовка защищаемой системы:

- установите **Suricata**,
- установите **Fail2Ban**.

2. Подготовка системы злоумышленника: установите **nmap** и **thc-hydra** либо скачайте и установите **Kali linux**.

Обе системы должны находится в одной подсети.

------

### Задание 1

Проведите разведку системы и определите, какие сетевые службы запущены на защищаемой системе:

**sudo nmap -sA < ip-адрес >**

**sudo nmap -sT < ip-адрес >**

**sudo nmap -sS < ip-адрес >**

**sudo nmap -sV < ip-адрес >**

По желанию можете поэкспериментировать с опциями: https://nmap.org/man/ru/man-briefoptions.html.


*В качестве ответа пришлите события, которые попали в логи Suricata и Fail2Ban, прокомментируйте результат.*

![Suricata](https://github.com/Fameq/13.03-hw/blob/master/img/suricata_log_scan_sT.png)
![Suricata](https://github.com/Fameq/13.03-hw/blob/master/img/suricata_log_scan_sS.png)
![Suricata](https://github.com/Fameq/13.03-hw/blob/master/img/suricata_log_scan_sV.png)

	При сканировании -sT в логах Suricata видно что есть попытки подключение в различным бд
	


------

### Задание 2

Проведите атаку на подбор пароля для службы SSH:

**hydra -L users.txt -P pass.txt < ip-адрес > ssh**

1. Настройка **hydra**: 
 
 - создайте два файла: **users.txt** и **pass.txt**;
 - в каждой строчке первого файла должны быть имена пользователей, второго — пароли. В нашем случае это могут быть случайные строки, но ради эксперимента можете добавить имя и пароль существующего пользователя.

Дополнительная информация по **hydra**: https://kali.tools/?p=1847.

2. Включение защиты SSH для Fail2Ban:

-  открыть файл /etc/fail2ban/jail.conf,
-  найти секцию **ssh**,
-  установить **enabled**  в **true**.

Дополнительная информация по **Fail2Ban**:https://putty.org.ru/articles/fail2ban-ssh.html.



*В качестве ответа пришлите события, которые попали в логи Suricata и Fail2Ban, прокомментируйте результат.*

![Fail2ban](https://github.com/Fameq/13.03-hw/blob/master/img/hydra_fail2ban_auth.png)
![Fail2ban](https://github.com/Fameq/13.03-hw/blob/master/img/hydra_fail2ban_log.png)
![Fail2ban](https://github.com/Fameq/13.03-hw/blob/master/img/hydra_suricata.png)

	В логах видно что после нескольких неудачных попыток подключиться по ssh ip-адресс был заблокирован
