## 设置root登录ssh

```bash
sudo apt install openssh-server

sudo passwd root

#允许root用户SSH登录，编辑sshd_config
sudo vim /etc/ssh/sshd_config
#找到 Authentication项下的 PermitRootLogin prohibit-password改成PermitRootLogin yes

sudo systemctl restart sshd
```

