# VagrantLAMP
ローカルに、LAMP環境(CentOS7)を構築するためのファイル郡。自分用に作成しているので汎用性等はあまり考慮していません。奇特にも利用しようという方はFork後に各自でカスタマイズしてください。

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
### VirtualBox, Vagrant
* VirtualBox https://www.virtualbox.org/
* Vagrant https://www.vagrantup.com/

### Ansible
	$ brew install ansible
	$ ansible --version
	ansible 2.2.0.0
	  config file = 
	  configured module search path = Default w/o overrides

### sshfs
	$ brew install homebrew/fuse/sshfs
	$ sshfs --version
	SSHFS version 2.8
	OSXFUSE 3.5.3
	FUSE library version: 2.9.7

事前に「FUSE for MacOS」をインストールする必要あり。
https://osxfuse.github.io/


### vagrant plugin
	$ vagrant plugin install vagrant-sshfs
	$ vagrant plugin install vagrant-cachier
	$ vagrant plugin install vagrant-vbguest

sshfs以外はお好みで。


### hostsを編集
	$ vi /private/etc/hosts
	192.168.11.50   vagrant

## 起動
	$ mkdir foobar; cd foobar
	$ vagrant init centos/7
	$ vagrant up

## 利用方法
* http://vagrant/info.php にアクセスし phpinfo()が表示されれば成功
* htdocs/がドキュメントルートなので、この下にファイルを置いたり、シンボリックリンク貼ればOK。

## メモ
* デフォの共有フォルダの形式だと、なぜかファイルがリアルタイムに同期されなかったので(vagrant reloadしないと見れない…)、ひとまずsshfsにしてます。

#### MySQL5.7の設定が面倒だったので、5.6を入れる。
	$ yum --showduplicates --enablerepo=mysql56-community list | grep mysql-community | grep 5.6.
	$ sudo yum --enablerepo=mysql56-community install mysql-community-server-5.6.34-2.el7 

#### yumリポジトリの取得元
	$ wget http://rpms.famillecollet.com/enterprise/remi-release-7.rpm
	$ wget http://dev.mysql.com/get/mysql57-community-release-el7-7.noarch.rpm	

#### 備忘録
* ~/.vagrant.d/boxes/ の下に大元のイメージファイルが保存される
* .vagrant/machines/default/virtualbox 下に秘密鍵など
