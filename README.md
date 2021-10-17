docker run --name camera4 -p 80:80 -p 8889:8889 --device=/dev/video0:/dev/video0 -v /home/ubuntu/rasp-cam/data/var/www:/var/www -v /home/ubuntu/rasp-cam/data/usr:/usr -v /home/ubuntu/rasp-cam/data/etc:/etc -d kerberos/kerberos

docker run --name camera5 -p 80:80 -p 8889:8889 --device=/dev/video0:/dev/video0 -v /home/ubuntu/rasp-cam/data/var/www:/var/www -d kerberos/kerberos

docker stop camera1

docker create --volumes-from camera1 --name camera1-data kerberos/kerberos

docker run --volumes-from camera1-data -v $PWD:/backup busybox tar zcvf /backup/kerberos-data-backup-17-10-2021-2.tar.gz /

docker run --name camera6 -p 80:80 -p 8889:8889 --device=/dev/video0:/dev/video0 --volumes-from camera1-data -d kerberos/kerberos

docker run --name camera7 -p 80:80 -p 8889:8889 --device=/dev/video0:/dev/video0 -v /home/ubuntu/rasp-cam/data/kerberosio/:/etc/opt/kerberosio/ -d kerberos/kerberos

docker run --name camera8 -p 80:80 -p 8889:8889 --device=/dev/video0:/dev/video0 -v /home/ubuntu/rasp-cam/data/kerberosio/:/etc/opt/kerberosio/ -v /home/ubuntu/rasp-cam/data/www/:/var/www/ -d kerberos/kerberos

docker run --name camera9 -p 80:80 -p 8889:8889 --device=/dev/video0:/dev/video0 -v /home/ubuntu/rasp-cam/data/kerberosio:/etc/opt/kerberosio -v /home/ubuntu/rasp-cam/data/www:/var/www -d kerberos/kerberos

docker run --name camera10 -p 80:80 -p 8889:8889 --device=/dev/video0:/dev/video0 -v /home/ubuntu/rasp-cam/data/kerberosio:/etc/opt/kerberosio -v /home/ubuntu/rasp-cam/data/www:/ -d kerberos/kerberos

docker run --name camera15 -p 80:80 -p 8889:8889 --device=/dev/video0:/dev/video0 \
-v /home/ubuntu/rasp-cam/data/bin:/bin \
-v /home/ubuntu/rasp-cam/data/boot:/boot \
-v /home/ubuntu/rasp-cam/data/etc:/etc \
-v /home/ubuntu/rasp-cam/data/home:/home \
-v /home/ubuntu/rasp-cam/data/lib:/lib \
-v /home/ubuntu/rasp-cam/data/media:/media \
-v /home/ubuntu/rasp-cam/data/mnt:/mnt \
-v /home/ubuntu/rasp-cam/data/opt:/opt \
-v /home/ubuntu/rasp-cam/data/root:/root \
-v /home/ubuntu/rasp-cam/data/sbin:/sbin \
-v /home/ubuntu/rasp-cam/data/srv:/srv \
-v /home/ubuntu/rasp-cam/data/tmp:/tmp \
-v /home/ubuntu/rasp-cam/data/usr:/usr \
-v /home/ubuntu/rasp-cam/data/var:/var \
 -d kerberos/kerberos