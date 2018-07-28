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
