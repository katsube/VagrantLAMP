# VagrantLAMP
ローカルのCentOS7上にLAMP環境を構築するためのファイル郡。自分用に作成しているので、汎用性等はあまり考慮いていません。奇特にも利用いようという方はFork後に各自でカスタマイズしてください。

## 想定環境

### ホスト

+ MacOSX ElCapitan (10.11.6)
+ VirtualBox
+ Vagrant
+ Ansible

### ゲスト 

+ centos/7
+ Apache 2.4
+ MySQL 5.6
* PHP 5.6
+ Memcached, Git, Svn ...

## ホストの環境設定
provisioning用にAnsibleを入れる。

### Ansible
	$ brew install ansible
	$ ansible --version
	ansible 2.2.0.0
	  config file = 
	  configured module search path = Default w/o overrides

### Provisioningの準備
#### RPM
	$ cd provisioning/rpm
	$ wget http://rpms.famillecollet.com/enterprise/remi-release-7.rpm
	$ wget http://dev.mysql.com/get/mysql57-community-release-el7-7.noarch.rpm	

※上記はリポジトリに含まれています。

## 起動
	$ vagrant init centos/7
	$ vagrant up


## メモ
* $HOME/.vagrant.d/boxes/ の下に大元のイメージファイルが保存れる

#### MySQL5.7の設定が面倒だったので、5.6を入れる。
	$ yum --showduplicates --enablerepo=mysql56-community list | grep mysql-community | grep 5.6.
	$ sudo yum --enablerepo=mysql56-community install mysql-community-server-5.6.34-2.el7 

