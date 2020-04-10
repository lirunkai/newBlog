1. `curl -sL https://rpm.nodesource.com/setup_10.x | sudo bash -` 

2. `sudo yum install nodejs` 安装nodejs

3. `sudo yum install git` 安装git

4. 安装yarn

   ```
    curl -sL https://dl.yarnpkg.com/rpm/yarn.repo | sudo tee /etc/yum.repos.d/yarn.repo
    sudo yum install yarn
   
   ```

5. 配置git公钥

```
ssh-keygen -t rsa -C lirunkaigod@gmail.com
cat ~/.ssh/id_rsa.pub
```

6. 开启防火墙

   `systemctel start firewalld`

   开机开启防火墙 `systemctl enable firewalld.service`

7. 开启端口 `firewall-cmd --zone=public --add-port=80/tcp --permanent`

   1. 查看开放的端口 `firewall-cmd --list-ports`
   2. 重新加载配置 `firewall-cmd --reload`