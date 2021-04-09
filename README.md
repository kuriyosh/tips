# Yoshiki の tips
## Introduction
環境構築手順とかたまにしか使わないけど有益なコマンドとか毎回ググるのが面倒なので、よく使うものをまとめておく

## Editor (Emacs)
自分の設定を持ってきて、 ~~/.emacs.d/init.el~ に保存
```sh
$ sudo yum install emacs-nox
$ curl https://raw.githubusercontent.com/yosyos36/dotfiles/master/.emacs.d/cli.el -o ~/.emacs.d/init.el
```

## Docker
### Amazon Linux 2
```
$ sudo amazon-linux-extras install docker
$ sudo groupadd docker
$ sudo usermod -a -G docker ec2-user
$ sudo curl -L "https://github.com/docker/compose/releases/download/1.25.5/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
$ sudo chmod +x /usr/local/bin/docker-compose
$ sudo service docker start
```

## Python
### pyenv
```sh
$ git clone https://github.com/pyenv/pyenv.git ~/.pyenv
$ echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bash_profile
$ echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bash_profile
```

## JavaScript
### nodebrew
https://github.com/hokaccha/nodebrew
```sh
$ curl -L git.io/nodebrew | perl - setup
$ export PATH=$HOME/.nodebrew/current/bin:$PATH
```

## Bash コマンド
#### sudo 権限で rsync
```sh
$ rsync -auv -e "ssh -i <SSH 鍵>" --rsync-path="sudo rsync " <ユーザー名>@<ホスト名>:/remotedir /localdir
```

## Linux
### NAT 構築
```
$ sudo su -
$ iptables -L
$ iptables -F
$ echo net.ipv4.ip_forward=1 >> /etc/sysctl.conf
$ iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
$ iptables -t nat -L
```