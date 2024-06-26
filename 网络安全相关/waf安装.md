# 雷池waf

[雷池docker镜像](https://demo.waf-ce.chaitin.cn/image.tar.gz)

[在线文档参考](https://docs.waf-ce.chaitin.cn/zh/)

## 安装

```bash
mkdir -p /data/safeline
cd /data/safeline
wget "https://waf-ce.chaitin.cn/release/latest/compose.yaml"
vim .env
##################
SAFELINE_DIR={safeline-dir}  #/data/safeline路径
IMAGE_TAG=latest
MGT_PORT=9443  #雷池平台端口
POSTGRES_PASSWORD={postgres-password}
SUBNET_PREFIX=172.22.222
IMAGE_PREFIX=chaitin
##################

    SAFELINE_DIR: 雷池安装目录，如 /data/safeline
    IMAGE_TAG: 要安装的雷池版本，保持默认的 latest 即可
    MGT_PORT: 雷池控制台的端口，保持默认的 9443 即可
    POSTGRES_PASSWORD: 雷池所需数据库的初始化密码，请随机生成一个
    SUBNET_PREFIX: 雷池内部网络的网段，保持默认的 172.22.222 即可
    IMAGE_PREFIX: 雷池镜像源的前缀，保持默认的 chaitin 即可
#安装    
cat image.tar.gz | gzip -d | docker load
#启动
docker compose up -d
docker exec safeline-mgt resetadmin  #初始admin账号和密码
```

