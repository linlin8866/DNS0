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

关闭ipv4

# 1. 先获取网卡名（这里是eth0）
ip addr

# 2. 临时关闭eth0的IPv4（重启恢复）
ip addr flush dev enp6s18 scope global

关闭ipv4

# 1. 自动获取物理网卡名
NIC=$(ip -4 addr show | awk '/inet/ && $2 !~ /^127/ {print $NF; exit}')

# 2. 写入 systemd-networkd 配置，永久禁用该网卡 IPv4
cat > /etc/systemd/network/00-${NIC}.network << EOF
[Match]
Name=${NIC}

[Network]
DHCP=ipv6
IPv6AcceptRA=yes

[Address]
# 仅保留 IPv6 地址（系统自动获取）
EOF

# 3. 禁用该网卡的 IPv4 DHCP 与自动配置
cat > /etc/systemd/network/01-disable-ipv4.network << EOF
[Match]
Name=${NIC}

[Network]
DHCP=no
LinkLocalAddressing=no
EOF

# 4. 重启 systemd-networkd 生效
systemctl restart systemd-networkd



