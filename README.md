# 13.3-Network-security

### Подготовка к выполнению заданий

1.  Подготовка защищаемой системы:

-   установите **Suricata**,
-   установите **Fail2Ban**.

2.  Подготовка системы злоумышленника: установите **nmap** и **thc-hydra** либо скачайте и установите **Kali linux**.

Обе системы должны находится в одной подсети.

---
### Задание 1

Подготовлены были 2 VDS, одна защищаяемая, другая атакующая.   
Установить ПО было просто.   

Далее были произведены атаки nmap, однако каких-либо результатов не было зафиксировано. Причем я пробовал атаковать как локальный IP, так и  внешний IP. Пробовал с включенным/выключенным firewall  
В общем, перепробовал все варианты, но логи fail2ban и suricata пустые  
Скрины  
Со включенным ufw результат атаки  
![ufw_enable](https://github.com/RSafin12/13.3-Network-security/blob/main/ufw_enable.png)  
С выключенным ufw результат уже другой, атака длилась дольше  
![ufw_disable](https://github.com/RSafin12/13.3-Network-security/blob/main/ufw_disable.png)  
вывод fail2ban-client status sshd  
![f2b_status](https://github.com/RSafin12/13.3-Network-security/blob/main/ufw_status.png)  
тут меня просто бот  
![bot](https://github.com/RSafin12/13.3-Network-security/blob/main/bot.png)
пустой лог f2b  
![f2b_log](https://github.com/RSafin12/13.3-Network-security/blob/main/f2b_log.png)
абсолютно пустой лог suricata
![suricata](https://github.com/RSafin12/13.3-Network-security/blob/main/suricata.png)

Тут вероятно потребуется какая-то тонкая настройка f2b и suricata, просто из коробоки они не дают ожидаемого результата(ну кроме блокировки ботов).   
Позже повторил эксперимент на локальных VM VirtualBoX, все также  
