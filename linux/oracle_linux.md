# 问题以及解决方案

1. 解决 root ssh 登录问题

```sh
sudo -i // 使用opc用户登录后切换root
echo root:123123 |sudo chpasswd root // 修改root的密码
sudo sed -i 's/^#\?PermitRootLogin.*/PermitRootLogin yes/g' /etc/ssh/sshd_config; // 开启root登录
sudo sed -i 's/^#\?PasswordAuthentication.*/PasswordAuthentication yes/g' /etc/ssh/sshd_config; // 开启密码验证
systemctl restart sshd.service // service sshd restart // 重启ssh服务
```

2. 安装 OPEN-VPN:

注意：不能在 Oracle-Linux 中进行安装

```sh
wget https://git.io/vpn -O openvpn-install.sh && bash openvpn-install.sh
```

3. CentOS 修复 ‘No module named ‘librepo’

```sh
sudo dnf install **python3-librepo**
```

4. 处理 Permissions 0644 for '\*.key' are too open. 报错问题

按照错误提示，该文件不能被其他人访问，只要将所属组和其他人的 read 权限取消即可

```sh
chmod 600 *.key
```

5. 安装 v2ray

一键安装：

```sh
# 推荐使用这个

# 1、切换到root用户
sudo -i

#开放所有端口
sudo iptables -P INPUT ACCEPT
sudo iptables -P FORWARD ACCEPT
sudo iptables -P OUTPUT ACCEPT
sudo iptables -F

#Oracle自带的Ubuntu镜像默认设置了Iptable规则，关闭它
apt-get purge netfilter-persistent
reboot

#强制删除
rm -rf /etc/iptables && reboot

# 重启后，安装/卸载v2ray
bash <(curl -s -L https://git.io/v2ray.sh)
```

```sh
bash <(curl -s -L https://raw.githubusercontent.com/xyz690/v2ray/master/go.sh)
```

可以自定义安装参数的设置：

```sh
bash <(curl -s -L https://raw.githubusercontent.com/xyz690/v2ray/master/install.sh)
```

相关链接：https://www.itblogcn.com/article/1501.html
