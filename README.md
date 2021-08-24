# CTF_Server

### Install and Configure CTFd Server on Docker (Ubuntu Host) ###

# Ubuntu Host (AWS Lightsail Ubuntu 18.04)#
sudo apt update

sudo apt dist-upgrade

# Install Docker and Docker-Compose on Ubuntu HOST#
(source: https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-18-04 )

sudo apt update

sudo apt install apt-transport-https ca-certificates curl software-properties-common

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable"

sudo apt update

sudo apt install docker-ce -y

sudo apt install docker-compose -y

sudo usermod -aG docker ${USER}

# (optional) Setup Docker Portainer (Container Manager) #
docker pull portainer/portainer

sudo mkdir /opt/portainer /data

docker run -d -p 9000:9000 --restart always --name docker-manager -v /var/run/docker.sock:/var/run/docker.sock -v /opt/portainer:/data portainer/portainer

#Be sure to allow port 9000 on any Firewall or Networking from Cloud Provider
#Access at: http://<ip_address_vpc>:9000

1. Create New Password on initial login.
2. Connect Portainer: Select Local (Manage Local docker environment)
3. "Connect"
4. Select your Local Endpoint - Dashboard Ready!


# Download/Setup CTFd Server for Docker #
#(source: https://github.com/CyberWeaponsFactory/CTF ) #

#(CTF Deployment: https://docs.ctfd.io/docs/deployment/ ) #

cd /opt

sudo git clone https://github.com/CyberWeaponsFactory/CTF.git

cd /opt/CTF

#Modify the docker-compose.yml files, as needed (add - SECRET_KEY= stupidkey123)

sudo nano docker-compose.yml

cd /opt/CTF

docker-compose up

#Be sure to allow port 8000 on any Firewall or Networking from Cloud Provider
#Access at: http://<ip_address_vpn:8000


# Adding CTFd Themes and/or Plugins #
#Unzip Themes to: /opt/CTFd/CTFd/themes/ #

#Unzip Plugins to: /opt/CTFd/CTFd/plugins/ #

cd /opt/CTFd

git clone https://github.com/CyberWeaponsFactory/CTF_Server_Tools.git

sudo cp /opt/CTFd/CTF_Server_Tools/hacker_theme.zip /opt/CTFd/CTFd/themes/

sudo apt install unzip

sudo unzip /opt/CTFd/CTFd/themes/hacker_theme.zip /opt/CTFd/CTFd/themes/


sudo cp /opt/CTFd/CTF_Server_Tools/multiple_choice.zip /opt/CTFd/CTFd/plugins/

sudo unzip /opt/CTFd/CTFd/plugins/multiple_choice.zip /opt/CTFd/CTFd/plugins/

#Log into the CTFd Server Admin Settings to change theme. You should also now have multiple choice challenge questions available for use.

ENJOY!!!

# NEXT STEPS #
#Install and Configure SSL using LetsEncrypt #

#See nginx/letsencrypt solutions #

