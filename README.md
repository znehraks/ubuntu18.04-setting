# Ubuntu 18.04 LTS 설치 및 기본환경 세팅

## 외장하드 SSD 512GB에 설치함

### 초기 세팅시 wifi 연결 오류 문제 발생

### 초기 세팅시 한글 설정 오류 발생

### 초기 세팅시 nodejs, nvm, anaconda3 설치

### 주피터노트북 초기세팅

####

그램에 우분투 설치 시 wifi 연결 오류 해결방법

1. 무선랜카드확인
   $ lspci -k
   출력결과에서
   Kernel driver in use: iwlwifi
   Kernel modules: iwlwifi
   등의 문구를 확인한다.

2. iwlwifi 드라이버를 설치한다.
   sudo apt update
   sudo apt install build-essential git
   git clone https://git.kernel.org/pub/scm/linux/kernel/git/iwlwifi/backport-iwlwifi.git
   cd backport-iwlwifi
   --
   sudo make
   sudo make install
   --
   sudo -i
   echo "options iwlwifi disable_msix=1" >> /etc/modprobe.d/iwlwifi.conf
   exit
   reboot 혹은 sudo reboot

3. 이래도 안뜬다면?
   cd backport-iwlwifi
   sudo make clean
   sudo make
   sudo make install

####

그램에 우분투 설치 시 한글 설정 오류 해결법

####

초기 세팅시 nodejs, nvm, anaconda3 설치법

####

yarn 설치 코드
sudo apt remove cmdtest
sudo apt remove yarn
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
sudo apt-get update
sudo apt-get install yarn -y

####

expo cli start 시 React Native Error: ENOSPC: System limit for number of file watchers reached 에러가
발생할 때,
#- insert the new value into the system config
echo fs.inotify.max_user_watches=524288 | sudo tee -a /etc/sysctl.conf && sudo sysctl -p

#- check that the new value was applied
cat /proc/sys/fs/inotify/max_user_watches

#- config variable name (not runnable)
fs.inotify.max_user_watches=524288
