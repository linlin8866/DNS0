dns更换

wget -O dns.sh https://raw.githubusercontent.com/linlin8866/DNS0/main/dns.sh && chmod +x dns.sh && bash dns.sh


wget -O dns.sh https://raw.githubusercontent.com/linlin8866/DNS0/main/dns.sh && chmod +x dns.sh && bash dns.sh

解锁dns

chattr -i /etc/resolv.conf

锁定dns

chattr +i /etc/resolv.conf

系统关闭防火墙

