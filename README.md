1.	реализовать knocking port
  нужно скачать файл ююю
    1.	установить на centralRouter софт и остановить firewalld. скачав и запустив скрипт ....
    
    2.	Настройка iptables через восстановления. Cкачав и запустив скрипт iptables_rules
        командой iptables-restore < iptables_rules
        
    3.	Для подключения к centralRouter нужно скачать файлик knocking.sh
        и запустив его
        chmod +x knock.sh && ./knock.sh XXX.XXX.XXX.XXXX 1111 2222 3333
