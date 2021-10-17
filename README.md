docker run --name camera4 -p 80:80 -p 8889:8889 --device=/dev/video0:/dev/video0 -v /home/ubuntu/rasp-cam/data/var/www:/var/www -v /home/ubuntu/rasp-cam/data/usr:/usr -v /home/ubuntu/rasp-cam/data/etc:/etc -d kerberos/kerberos

docker run --name camera5 -p 80:80 -p 8889:8889 --device=/dev/video0:/dev/video0 -v /home/ubuntu/rasp-cam/data/var/www:/var/www -d kerberos/kerberos

docker stop camera1

docker create --volumes-from camera1 --name camera1-data kerberos/kerberos

docker run --volumes-from camera1-data -v $PWD:/backup busybox tar zcvf /backup/kerberos-data-backup-17-10-2021-2.tar.gz /

docker run --name camera6 -p 80:80 -p 8889:8889 --device=/dev/video0:/dev/video0 --volumes-from camera1-data -d kerberos/kerberos

docker run --name camera7 -p 80:80 -p 8889:8889 --device=/dev/video0:/dev/video0 -v /home/ubuntu/rasp-cam/data/kerberosio/:/etc/opt/kerberosio/ -d kerberos/kerberos