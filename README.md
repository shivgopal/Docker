# Docker
# Docker Installation on Ubuntu 20.04 and Setup webserver

## Installation

Step 1: Updating the Software Repository

sudo apt update

Step 2: Downloading Dependencies

sudo apt-get install apt-transport-https ca-certificates curl software-properties-common

Step 3: Adding Docker’s GPG Key

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

Step 4: Installing the Docker Repository

sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu  $(lsb_release -cs)  stable"

Step 5: Installing the Latest Docker
#Now you can install the latest Docker version with:
sudo apt-get install docker-ce

Step 6: Verifying Docker Installation
docker --version

Step 7: Enable Docker Service 
#start the Docker service run the following commands:
sudo systemctl start docker
#Enable Docker to run at startup with:
sudo systemctl enable docker
#To check the status of the service, use the command:
sudo systemctl status docker


## Create Dockerfile

FROM centos:7

MAINTAINER shivagni01@gmail.com 

RUN yum update -y

RUN yum install httpd unzip -y

ADD https://www.free-css.com/assets/files/free-css-templates/download/page276/spicy.zip /var/www/html

WORKDIR /var/www/html

RUN unzip spicy.zip

RUN cp -rvf spicy/* .

RUN rm -rf spicy.zip

CMD ["/usr/sbin/httpd","-D","FOREGROUND"]
EXPOSE 80

##Build Image 

docker build -t web-server .

##Run Container
docker container run -itd p 8000:80 web-server

Now we can check our website on browser

public-ip:8000

