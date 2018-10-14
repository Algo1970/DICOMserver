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

### 設定変更用にnvimインストール

https://github.com/Algo1970/clinic_server_ubuntu1804

### 接続設定（~/conquest/acrnema.map）

```
/* **********************************************************
 *                                                          *
 * DICOM AE (Application entity) -> IP address / Port map   *
 * (This is file ACRNEMA.MAP)                               *
 *                                                          *
 * All DICOM systems that want to retrieve images from the  *
 * Conquest DICOM server must be listed here with correct   *
 * AE name, (IP adress or hostname) and port number. The    *
 * first entry is the Conquest server itself. The last ones *
 * with * show wildcard mechanism. Add new entries above.   *
 *                                                          *
 * The syntax for each entry is :                           *
 *   AE   <IP adress|Host name>   port number   compression *
 *                                                          *
 * For compression see manual. Values are un=uncompressed;  *
 * ul=littleendianexplicit,ub=bigendianexplicit,ue=both     *
 * j2=lossless jpeg;j3..j6=lossy jpeg;n1..n4=nki private    *
 * js   =lossless jpegLS;  j7=lossy jpegLS                  *
 * jk   =lossless jpeg2000;jl=lossy jpeg2000                *
 * J3NN..j6NN, JLNN or J7NN overrides quality factor to NN% *
 *                                                          *
 ********************************************************** */

CONQUESTSRV1	127.0.0.1	      5678		        un
V*	        	*               1234            un
W*	        	*               666             un
S*		        *               5678            un
KPServer      192.168.47.1    104             un
```
設定が終わったら再起動
```
./dgate -v
```

### DICOM viewer

接続確認済み
- RadiAnt : https://www.radiantviewer.com/

接続不可
- Onis : http://www.onis-viewer.com/ProductInfo.aspx?id=19
- Athena DICOM viewer : https://www.microsoft.com/ja-jp/p/athena-dicom-viewer/9nblggh514ph#activetab=pivot:overviewtab


