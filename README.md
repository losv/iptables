        Описание стенда
        две ВМ на базе Centos 7
        1-я centralRouter имеет две сетевые карты eth0 (смотрит в интернет) и eth1 внутренняя с ip addr=192.168.3.1
        2-я ВМ одна сетевая карта с ip addr=192.168.3.10 и установленном, запущенном nginx
        
    1.	установить на centralRouter софт и остановить firewalld, выполнив команды:
        - sudo systemctl stop firewalld
        - sudo yum install iptables iptables-services -y
    
    2.	Настройка iptables через восстановления. Cкачав и запустив скрипт iptables_rules
        командой iptables-restore < iptables_rules
        
    3.	Для подключения к centralRouter нужно скачать файлик knocking.sh
        и запустив его
        chmod +x knock.sh && ./knock.sh XXX.XXX.XXX.XXXX 1111 2222 3333
        
    4.  для того чтобы centralRouter стал раздовать интернет нужно выполнить команды
        sudo bash -c 'echo "net.ipv4.conf.all.forwarding=1" >> /etc/sysctl.conf'; sudo sysctl -p
        sudo iptables -t nat -A POSTROUTING ! -d 192.168.3.0/24 -o eth0 -j MASQUERADE;
        
    5.  пробросить 80-й порт на 8080
        на centralRouter нужно ввести команду
        sudo iptables -t nat -A PREROUTING -i eth0 -p tcp -m tcp --dport 8080 -j DNAT --to-destination 192.168.3.10:80
        теперь на сервер nginx можно зайти набрав ip addr centralRouter, что смотрит в инет, и порт :8080
