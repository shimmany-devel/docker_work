# docker_work
docker files, compose file

===== linux host =====
cd linux-devel
docker build -t linux-devel:18.04

docker images  <-- check created image

cd composer
docker-compose up -d  -->  server running 

docker ps -a  <-- check created server from image

===== windows host =====
if not wsl2, docker image could be created, so take image form image create in linux host

docker image dump (linux host) :  
docker save -o savedfile.tar image:tag   -->  docker save -o linux-devel.tar linux-devel:18.04

move linux-devle.tar to windows host

docker image load (windows host) :
docker load -i savedilf.tar  -->  docker load -i linux-devel.tar

server running (windows host) 
docker run --privileged=true --restart=always -d -it -p 50000:22 --name gncs-build -v C:\shared:/host -h gncs-build gncs_build:latest /bin/bash -c "/etc/init.d/ssh start && /bin/bash"
