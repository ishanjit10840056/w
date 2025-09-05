Q. How to use docker on AWS instance.

Host an instance and launch

set machine name

yum install docker* -y (in AWS its present but in redhat or ubuntu do below steps)

Go to install docker engine website

Move to RHEL -> and follow the steps on website to install docker

systemctl start docker

systemctl enable docker

docker info (var/lib/docker where all docker data is stored and the storage driver used is Overlay2)

docker ps -a (to know about the containers running)

docker image ls (to know about the image present)

TO DOWNLOAD DOCKER IMAGES:

Go to docker hub website

search for ubuntu and open it (tags help in separating versions)

copy the command and paste in terminal

Go to website and search httpd -> and copy the command paste in terminal to run

Again search for centos -> copy and paste

docker image ls to look for image downloads

docker --help (to know about the commands)

docker run -it --name devops ubuntu:rolling /bin/bash (it means interactive mode)

name of container, name of image:tag

the shell will change

cat /etc/os-release

take duplicate of instance in another terminal - connect it and then type

docker ps -a

go to docker container

apt update -y

apt install apache2 -y

service apache2 start

apt install curl --> curl is like a command line browser

cd /var/www/html

echo "This is my application one" > index.html

ll

curl http://localhost

cd

mkdir /data

cd /data

touch file.txt{1..10}

ll

exit

and then docker ps -a (in another terminal to check exit status)

BUT WE NEED TO KEEP THE CONTAINER RUNNING ALWAYS

docker start devops (container will start again)

docker inspect devops | less

you will get the IP address for the container also below and the gateway

also it generates a veth network

ip a s

docker image ls

docker run -it --name prod ubuntu:rolling /bin/bash

apt update -y

apt install apache2 -y

cd /var/www/html

echo "Hello all this is application two" > index.html

cd

service apache2 start

ctrl + p then ctrl+q to exit

ip a s

curl http://172.17.0.3

curl http://172.17.0.2

if failed to start comes

then docker attach devops

curl http://172.17.0.2

Entire containerization works on port forwarding

docker run -it --name happybirthday ubuntu:rolling /bin/bash

apt update -y

apt install apache2

echo "aaj tera happy birth day" > index.html

service apache2 start

cd

curl http://172.17.0.4

docker ps -a

docker run -it --name saiyyara -p 8080:80 ubuntu:rolling /bin/bash (gave port number to remove from default port(80) to a assigned port(8080))

cd /var/www/html

echo "Tum jiyo hazaron saal" > index.html

exit (ctrl p + ctrl q)

docker ps -a

curl http://172.17.0.5:8080 (also allow this port 8080 in security group)

Go to aws - select instance and copy public ip -> ip:portnumber

HOW TO STOP AND KILL A DOCER CONTAINER

docker stop sainyara

docker rm sainyara

or docker kill sainyara

By default containers have ephemeral storage (i.e., temporary storage)

After container is deleted or killed the storage also gets removed, so to get the data we do -:
