라즈베리파이5 개발 환경 세팅 메모<br/>
RAM:8GB / SDCard:512GB

1. SDCard에 RPI 5 Lite (x64) 설치

2. ssh로 스크립트 실행 (docker 설치)
```
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh ./get-docker.sh
```

3. ssh로 스크립트 실행 (docker/gitea 설치)
```
sudo usermod -aG docker $USER
newgrp docker
docker ps
docker run -d -v /home/$USER/gitea:/data -p 2099:3000 -p 2022:22 --name gitea gitea/gitea
```

4. ssh로 스크립트 실행 (nodejs 설치)
```
sudo apt-get remove nodejs

# 버전 지정, Current, LTS 중 선택
# sudo curl -sL https://deb.nodesource.com/setup_20.x | sudo -E bash -
# sudo curl -sL https://deb.nodesource.com/setup_current.x | sudo -E bash -
sudo curl -fsSL https://deb.nodesource.com/setup_lts.x | sudo -E bash

apt list | grep nodejs
sudo apt-get install nodejs -y
node -v
```

5. ssh로 스크립트 실행 (pm2 설치)
```
sudo npm install -g npm@latest
sudo npm i -g pm2
sudo pm2 startup
pm2 list
```
