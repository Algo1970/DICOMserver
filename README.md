# DICOMserver

### テスト用DICOMserverの作成

http://r-beginner.hatenadiary.jp/entry/2017/02/19/081201

### CONQUEST on ubuntu16.04LTS

CONQUEST : https://ingenium.home.xs4all.nl/dicom.html

```
#!bin/sh
sudo apt -y update
sudo apt -y install g++         # g++は、GNU GCCのC++コンパイラ
sudo apt -y install apache2 
sudo a2enmod cgi
sudo service apache2 restart

mkdir ~/conquest
cd ~/conquest

sudo apt-get -y install libpq-dev 
sudo apt-get -y install postgresql

sudo su 　　　　　　　　　　　　　　　　   　　# become superuser 
su – postgres 

psql << EOT
\password 
postgres 
postgres 
\q 
createdb conquest                           # create database conquest 
                                   
EOT

exit 
exit


cd conquest
wget http://ingenium.home.xs4all.nl/dicomserver/dicomserver1419.zip
unzip dicomserver1419.zip
chmod 777 maklinux
./maklinux　

./dgate -v -r  # regenerate the database 
./dgate -v     # run the server 


```

http://localhost/cgi-bin/dgate?mode=top にブラウザからアクセスする。




