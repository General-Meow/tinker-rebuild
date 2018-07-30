# tinker-rebuild
some basic commands to bring tinker back up

### mybind9
docker run -p 53:53 -p 53:53/udp --name mybind9 -d --restart=unless-stopped generalmeow/shadow:mybind9-1.8-arm

### website
docker run -d -p 80:80 --restart=always --name website -v /media/stick/tosh/work/website/main:/usr/share/nginx/html:ro arm32v7/nginx

### samba
docker run -d \
     -p 137:137/udp \
     -p 138:138/udp \
     -p 139:139 \
     -p 445:445 \
     -p 445:445/udp \
     --restart='always' \
     --hostname 'fileserver' \
     -v /media/stick:/share/stick \
     --name samba dastrasmue/rpi-samba:latest \
     -s "fileserver:/share/stick:rw:"

### dyn
docker run -d --name dynu.dns --restart=always -v /home/paul/work/docker/docker-mydyndns/files/config:/etc/ddclient generalmeow/mydyndns:1.0-arm

### deluge
docker run -d -p 8112:8112 --name deluge -v /media/stick/usbstick/deluge/root/deluge generalmeow/deluge:1.1-arm

### nexus 
docker run -d --name nexus -p 8081:8081 -v /home/paul/work/sonatype-work:/home/nexus/sonatype-work generalmeow/nexus:1-arm

### move storage of docker to different directory
```
mkdir work/docker_storage
cd docker_storage
sudo chown -R root:root docker_storage
sudo chmod 701 docker_storage
#stop current containers
docker stop $(docker ps -q)
#stop docker daemon
sudo systemctl stop docker
sudo cp -R /var/lib/docker/ ./docker_storage
cd /var/lib
sudo rm -rf docker
sudo ln -s ~/work/docker_storage docker
sudo service docker start
```
