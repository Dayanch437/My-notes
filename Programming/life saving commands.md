

git config --global url."git@github.com:".insteadOf "https://github.com/"


ffmpeg -i video.mp4 -i audio.mp3 -c:v copy -c:a aac -strict experimental output.mp4


sudo ufw allow from <Allowed-IP> to any port <Proxy-Port>


sudo ufw allow from 192.168.1.100 to any port 10808


sudo ip addr del 37.252.22.59/24 dev eth0
sudo ip addr del 37.252.22.51/24 dev eth0






installing python3.13

sudo add-apt-repository ppa:deadsnakes/ppa -y
sudo apt update
sudo apt install python3.13 python3.13-venv python3.13-dev -y

sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.13 1
sudo update-alternatives --config python3







