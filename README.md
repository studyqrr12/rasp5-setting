라즈베리파이5 개발 환경 세팅 메모<br/>
RAM:8GB / SDCard:512GB

```
이 설정은 개인 서버용 입니다.<br/>
설정을 따라하는것에 대한 책임은 본인에게 있습니다.
```

1. SDCard에 RPI 5 Lite (x64) 설치

2. DHCP 서버에서 RPI 5 찾기 및 아이피 고정

3. Update
```
sudo raspi-config
> Update - Update this tool to the latest version
sudo apt update
sudo apt full-upgrade -y
```

4. Expand Filesystem
```
sudo raspi-config
> Advanced Options - Configure advanced settings
> Expand Filesystem - Ensures that all of the SD card is available
> OK
> Finish
> Yes (Would you like to reboot now?)
```

5. Timezone
```
sudo raspi-config
> Localisation Options - Configure language and regional settings
> Timezone - Configure time zone
> Asia
> Seoul (Asia / Seoul)
> OK
> Finish
```

6. ssh port
```
sudo nano /etc/ssh/sshd_config
> #Port 22 항목 변경, 저장
cat /etc/ssh/sshd_config

sudo nano /etc/services
> ssh  22/tcp 항목 변경, 저장
cat /etc/services

sudo reboot
```

7. sudo 비밀번호 요구
```
# https://forums.raspberrypi.com/viewtopic.php?t=169212
sudo nano /etc/sudoers.d/010_pi-nopasswd
> NOPASSWD 를 PASSWD 로 변경, 저장
```

8. ssh로 스크립트 실행 (docker 설치)
```
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh ./get-docker.sh
```

9. ssh로 스크립트 실행 (docker 권한)
```
sudo usermod -aG docker $USER
newgrp docker
docker ps -a
```

10. ssh로 스크립트 실행 (docker/gitea 설치)
```
docker run -d -v /home/$USER/gitea:/data -p 2099:3000 -p 2022:22 --name gitea gitea/gitea
```

11. ssh로 스크립트 실행 (nodejs 설치)
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

12. ssh로 스크립트 실행 (pm2 설치)
```
sudo npm install -g npm@latest
sudo npm i -g pm2
sudo pm2 startup
pm2 list
```
