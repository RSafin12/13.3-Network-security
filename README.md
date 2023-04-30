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

### Задание 2

Теперь проведем подбор паролей, с выключенным и включенным fail2ban  
fail2ban остановлен  
Результат работы hydra, как видно пароль подобран.   
![hydra_1](https://github.com/RSafin12/13.3-Network-security/blob/main/2-hydra_OK.png)  
Смотрим fast.log suricata и видим сообщения предупреждающего характера  
![fast_log_before](https://github.com/RSafin12/13.3-Network-security/blob/main/2-fast_log_before.png)  

fail2ban теперь включен  
В этот раз пароль подобрать не удалось  
![hydra_NOT_OK](https://github.com/RSafin12/13.3-Network-security/blob/main/2-hydra_NOT_OK.png)  
Смотрим fast.log suricata, также зафиксирована попытка, но в этот раз только одна запись, вместо нескольких  
![ast_log_after](https://github.com/RSafin12/13.3-Network-security/blob/main/2-f2b_fast_log_after.png)  
Далее проверяем auth.log  
![f2b_auth_log](https://github.com/RSafin12/13.3-Network-security/blob/main/2-f2b_auth_log.png)  
И также fail2ban.log
![f2b_log](https://github.com/RSafin12/13.3-Network-security/blob/main/2-f2b_log.png)  

По итогу становится очевидным, что просто наличие fail2ban значительно затрудняет работу злоумышленника и повышает степень защищенности сервера, must have!   
ДЗ делал на VDS  у которого есть публичный IP, невероятно много ботов стучалось по 22 порту, что также показывает, насколько важно иметь fail2ban. Грепнул по IP 172.16.16.15, чтобы было читабельно.   











































