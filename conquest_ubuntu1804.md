# Conquest on ubuntu18.04

result：ubuntu18.04は、2019.01.04の時点ではうまくインストールできない。

gedit conquest.sh
```
#!bin/sh
sudo apt update
sudo apt upgrade
sudo apt install g++         # g++は、GNU GCCのC++コンパイラ
sudo apt install apache2 
sudo a2enmod cgi
sudo service apache2 restart

mkdir ~/conquest
cd ~/conquest

sudo apt install libpq-dev 
sudo apt install postgresql
```

以下は、うまくスクリプトかけないので手作業で、
```
sudo su 　　　　　　　　　　　　　　　　   　　# become superuser 
su – postgres  # 上手くいかない！！！！

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
./maklinux　　　　 # bash: ./maklinux　: そのようなファイルやディレクトリはありません!!!!!

./dgate -v -r  # regenerate the database 
./dgate -v     # run the server 
```
