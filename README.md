# CentOS7-SELinux-
脚本 | CentOS7一键配置yum源、永久关闭防火墙及SELinux等

#!/bin/bash
yum install -y wget vim
mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.backup
wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo
yum install -y epel-release
yum clean all
yum makecache fast
echo "1" > /proc/sys/net/ipv4/ip_forward
sysctl -p
systemctl disable firewalld
sed -i 's/enforcing/disabled/' /etc/selinux/config
yum install -y ntp
timedatectl set-timezone Asia/Shanghai
sed -i 's/0.centos.pool.ntp.org/ntp1.aliyun.com/g' /etc/ntp.conf
systemctl enable ntpd
yum install bash-completion -y
yum update -y  && yum upgrade -y
reboot


来源：https://naiyu.club/109.html
