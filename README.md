# DICOMserver

### テスト用DICOMserverの作成

http://r-beginner.hatenadiary.jp/entry/2017/02/19/081201

VMwareで仮想マシン作成。user:postgres, pwd:postgres

### CONQUEST on ubuntu16.04LTS

CONQUEST : https://ingenium.home.xs4all.nl/dicom.html

gedit conquest.sh  
* upgradeがエラー出てると上手くいかない！update, upgradeは手作業で確認してからの方が良いかも。
```
#!bin/sh
sudo apt -y update
sudo apt -y upgrade
sudo apt -y install g++         # g++は、GNU GCCのC++コンパイラ
sudo apt -y install apache2 
sudo a2enmod cgi
sudo service apache2 restart

mkdir ~/conquest
cd ~/conquest

sudo apt-get -y install libpq-dev 
sudo apt-get -y install postgresql
```
ここから手作業で？（スクリプトでは上手くいかない…）
```
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
```

gedit conquest2.sh
```
cd conquest
wget http://ingenium.home.xs4all.nl/dicomserver/dicomserver1419.zip
unzip dicomserver1419.zip
chmod 777 maklinux
./maklinux　

./dgate -v -r  # regenerate the database 
./dgate -v     # run the server 
```

http://localhost/cgi-bin/dgate?mode=top にブラウザからアクセスする。




