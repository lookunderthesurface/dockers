# Docker
安装docker toolkit https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html
安装docker https://docs.docker.com/engine/install/ubuntu/#uninstall-docker-engine
配置docker代理 https://blog.csdn.net/qq_45975878/article/details/143161306
权限问题 sudo groupadd docker && sudo usermod -aG docker $USER && newgrp docker
拉取镜像 https://hub.docker.com/r/pytorch/pytorch/tags 
```bash
docker pull pytorch/pytorch:2.6.0-cuda12.4-cudnn9-runtime
docker pull pytorch/pytorch:2.5.1-cuda12.1-cudnn9-devel
```
创建实例(改用docker compose)
```bash
docker run --gpus all -it --network host --shm-size=8g --name torch pytorch/pytorch:2.6.0-cuda12.4-cudnn9-runtime bash
```
实例中配置代理 
```bash
export http_proxy=http://127.0.0.1:7890 && export https_proxy=http://127.0.0.1:7890
```
宿主机开放显示器
```bash
xhost +local:root
```
# docker daemon
sudo nano /etc/docker/daemon.json
```json
{
    "registry-mirrors": [
        "https://do.nark.eu.org",
        "https://dc.j8.work",
        "https://docker.m.daocloud.io",
        "https://dockerproxy.com",
        "https://docker.mirrors.ustc.edu.cn",
        "https://docker.nju.edu.cn"
    ],
    "runtimes": {
      "nvidia": {
        "path": "/usr/bin/nvidia-container-runtime",
        "runtimeArgs": []
      }
    }
}
```
sudo mkdir -p /etc/systemd/system/docker.service.d
sudo nano /etc/systemd/system/docker.service.d/http-proxy.conf
```conf
[Service]
Environment="HTTP_PROXY=http://127.0.0.1:7890/"
Environment="HTTPS_PROXY=http://127.0.0.1:7890/"
Environment="NO_PROXY=localhost,127.0.0.1,::1"
```
sudo systemctl daemon-reexec
sudo systemctl daemon-reload
sudo systemctl restart docker
 
# docker compose
sudo curl -L "https://github.com/docker/compose/releases/download/v2.24.6/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

sudo chmod +x /usr/local/bin/docker-compose

docker-compose --version
