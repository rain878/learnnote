# 安装ollama

下载[olama](https://ollama.com/)

```
windows 的安装默认不支持修改程序安装目录，
默认安装后的目录：C:\Users\username\AppData\Local\Programs\Ollama
默认安装的模型目录：C:\Users\username\ .ollama
默认的配置文件目录：C:\Users\username\AppData\Local\Ollama

配置环境变量
OLLAMA_MODLES
D:\bigmodles\
```

# 下载docker

windows安装下载[docker](https://www.docker.com/products/docker-desktop/)

预先安装wsl2

# 安装open WebUi

```bash
docker run -d -p 3000:8080 --add-host=host.docker.internal:host-gateway -v open-webui:/app/backend/data --name open-webui --restart always ghcr.io/open-webui/open-webui:main
```

