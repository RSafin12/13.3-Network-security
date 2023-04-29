# 13.3-Network-security

### Подготовка к выполнению заданий

1.  Подготовка защищаемой системы:

-   установите **Suricata**,
-   установите **Fail2Ban**.

2.  Подготовка системы злоумышленника: установите **nmap** и **thc-hydra** либо скачайте и установите **Kali linux**.

Обе системы должны находится в одной подсети.

---
### Задание 1

Подготовлены были 2 VDS, 
- защищаяемая, vigdis 172.16.16.18 
- атакующая, strong 172.16.16.15   

Были некоторые проблемы, т.к. из коробки не было правил suricata.rules по  пути /var/lib/suricata/rules/  
Сработало такое решение   
- смотрим сначала список ruleset providers командой   
`sudo suricata-update list-sources`  
- находим какие-нибудь бесплатные и подгружаем, например  
`sudo suricata-update enable-source tgreen/hunting`  
Далее стандатный yaml-файл нормально работает

С первой VM  на вторую была произведена атака  
![attack](https://github.com/RSafin12/13.3-Network-security/blob/main/attack.png)
Атака была зафиксирована в fast_log  
![fast_log](https://github.com/RSafin12/13.3-Network-security/blob/main/fast_log.png)  
Также привожу логи suricata.log и stats.log  
![suricata.log](https://github.com/RSafin12/13.3-Network-security/blob/main/suricata_log.png)
![stats.log](https://github.com/RSafin12/13.3-Network-security/blob/main/suricata_stats.png)
Также проверил логи fail2ban, грепнул по 172.16.16  
IP атакующей машины 172.16.16.15  
![f2b](https://github.com/RSafin12/13.3-Network-security/blob/main/f2b_logs.png)
