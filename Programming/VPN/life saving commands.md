psql: error: connection to server on socket "/var/run/postgresql/.s.PGSQL.5432" failed: FATAL:  Peer authentication failed for user "postgres"
	

~~~bashALTER USER postgres WITH PASSWORD 'your_new_password';


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






pg_dump -U your_db_user -h localhost -d your_db_name > backup.sql

~~~


psql
~~~bash
CREATE DATABASE e_university;
CREATE USER postgres WITH PASSWORD 'postgres';
ALTER ROLE postgres SET client_encoding TO 'utf8';
ALTER ROLE postgres SET default_transaction_isolation TO 'read committed';
ALTER ROLE postgres SET timezone TO 'Asia/Ashgabat';
GRANT ALL PRIVILEGES ON DATABASE e_university TO postgres;
\q

~~~




~~~bash
psql -U postgres -d e_university -f E_University_Production-2025_03_20_20_04_01-dump.sql

~~~

~~~bash
sudo nano /etc/postgresql/*/main/pg_hba.conf


local   all   all   peer
Change `peer` to `md5`:

sudo systemctl restart postgresql
~~~


					For network errors
					
					~~~bash
					nmcli connection show


nmcli connection delete "Outline TUN Connection"


sudo ip link delete outline-tun1
sudo ip link delete outline-tun0
~~~


~~~bash
	ALTER USER postgres WITH PASSWORD 'new_password';

~~~
for installing to Debian
~~~bash
# 1. Install dependencies
sudo apt update
sudo apt install -y build-essential libssl-dev zlib1g-dev \
libncurses-dev libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm \
libncursesw5-dev xz-utils tk-dev libxml2-dev libxmlsec1-dev libffi-dev liblzma-dev

# 2. Download Python 3.13 source (replace with latest if needed)
cd /usr/src
sudo wget https://www.python.org/ftp/python/3.13.0/Python-3.13.0b1.tgz
sudo tar xvf Python-3.13.0b1.tgz
cd Python-3.13.0b1

# 3. Build and install
sudo ./configure --enable-optimizations
sudo make -j$(nproc)
sudo make altinstall  # ⛔ Use altinstall to avoid overwriting system python3

# 4. Register Python 3.13 in alternatives
sudo update-alternatives --install /usr/bin/python3 python3 /usr/local/bin/python3.13 1
sudo update-alternatives --config python3
~~~