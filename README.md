dns更换

wget -O dns.sh https://raw.githubusercontent.com/linlin8866/DNS0/main/dns.sh && chmod +x dns.sh && bash dns.sh


wget -O dns.sh https://raw.githubusercontent.com/linlin8866/DNS0/main/dns.sh && chmod +x dns.sh && bash dns.sh

# 一键下载并运行
bash <(curl -sL https://raw.githubusercontent.com/linlin8866/DNS0/main/dns.sh)


解锁dns

chattr -i /etc/resolv.conf

锁定dns

chattr +i /etc/resolv.conf

系统关闭防火墙
ufw disable

systemctl stop firewalld && systemctl disable firewalld

关闭ipv4

for iface in $(ls /sys/class/net/); do ip addr flush dev $iface scope global; done

