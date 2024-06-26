# 安装

## 在线

## 离线

下载[docker离线包](https://download.docker.com/linux/static/stable/x86_64/)

```bash
tar -zxvf docker-26.1.4.tgz
cp ./docker/* /usr/bin
vim /etc/systemd/system/docker.service

#########vim编辑###############
[Unit]
Description=Docker Application Container Engine
Documentation=https://docs.docker.com
After=network-online.target firewalld.service
Wants=network-online.target

[Service]
Type=notify
ExecStart=/usr/bin/dockerd
ExecReload=/bin/kill -s HUP $MAINPID
TimeoutSec=0
RestartSec=2
Restart=always
StartLimitBurst=3
StartLimitInterval=60s
LimitNOFILE=1048576
LimitNPROC=1048576
LimitCORE=infinity
TasksMax=infinity
Delegate=yes
KillMode=process
OOMScoreAdjust=-500
StandardOutput=syslog
StandardError=syslog
SyslogIdentifier=docker

[Install]
WantedBy=multi-user.target
#########vim编辑###############

chmod 777 /etc/systemd/system/docker.service
sudo systemctl daemon-reload
sudo systemctl enable docker
sudo systemctl start docker
sudo systemctl status docker
```

### docker compse安装

来自[docker compose](https://github.com/docker/compose/releases)

```bash
下载好的就是可执行文件
sudo mv docker-compose /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```

