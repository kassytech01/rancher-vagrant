Rancher
===================================


インストール方法
---------------------------------

### Vagrantでの起動方法

* os-vagrant

https://github.com/rancher/os-vagrant

* Rancher Server

https://github.com/rancher/rancher

(参考)https://qiita.com/yanoshi/items/816e1c8bc97fd8d426b7

```
 $ docker run -d --restart=unless-stopped -p 8080:8080 rancher/server:stable
```
※rancher/server:latestもありか。

* RancherOSのアップグレード

http://rancher.com/docs/os/v1.2/en/upgrading/

```
$ sudo ros os upgrade
```

### EC2での起動方法

* AmazonLinux

* docker

対応バージョン
http://rancher.com/docs/rancher/v1.6/en/hosts/

構築
---------------------------------


### プライベートカタログ

https://www.https://www.slideshare.net/m-daichang/rancher-composeslideshare.net/m-daichang/rancher-composehttps://www.slideshare.net/m-daichang/rancher-compose

⇒docker-compose.ymlでどうやってStackを作るか？

### Stackへの追加

#### Stackとは

Rancher上ではマイクロサービスのまとまり（コンテナの集合体）をStack(スタック)として管理します。

* [Stack] - [User] -> Add Stack

###### Concourse CI
  * Name:
    * ConcourseCI
  * Description:
    * Concourse CIのwebとworker用のコンテナ管理
  * Optional: docker-compose.yml
    * -> docker-compose.ymlをアップロード
  * Optional: rancher-compose.yml
    * -> rancher-compose.ymlをアップロード

###### Docker Private Registry

###### Rocket.chat


アップグレード
---------------------------------------------------

https://qiita.com/FoxBoxsnet/items/c4f4bc789f336e1af256

```
## Rancher Server 古い方を起動するとする
$ docker run -d --name rancher-server --restart=unless-stopped -p 8080:8080 rancher/server:v1.4.1

## Rancher Server を止める
# docker stop rancher-server

## Volumeを作成する
$ docker create --volumes-from rancher-server --name rancher-data rancher/server:v1.4.1

## 古いRancher Serverを削除する(名前が被るので削除)
$ docker rm rancher-server

## 作成したvolumeをくっつけて起動する (tagは適切に変更する事)
$ docker run -d --name rancher-server --volumes-from rancher-data --restart=unless-stopped -p 8080:8080 rancher/server:v1.5.1
```

### カタログのアップグレード

* docker-compose.ymlとrancher-compose.ymlを記載するなら以下が一番参考になる。

https://www.slideshare.net/m-daichang/rancher-compose

* コミュニティカタログが参考になる

https://github.com/rancher/community-catalog

**TODO:**

⇒rancher-compose.ymlってなんだ？

### その他

#### Docker プライベートレジストリとの連携

##### Create a Private Docker Registry to Integrate with Rancher

* Dockerプライベートレジストリの追加

Concourse CIのビルド用コンテナを登録しておく。（これをやらないと毎回Gradleの依存関係を解決することになり、ビルドに時間が掛かる）

http://rancher.com/create-a-private-docker-registry-to-integrate-with-rancher/
https://rancher.com/docs/rancher/v1.6/en/installing-rancher/installing-server/no-internet-access/#using-a-private-registry


Rancherにプライベートレジストリを追加する。（Amazon ECRも追加できる模様。）

http://rancher.com/docs/rancher/v1.6/en/environments/registries/


http://rancher.com/docs/os/v1.2/en/configuration/private-registries/

⇒何か？

* LinuxのDocker管理ツール「rancher」の紹介
http://morizyun.github.io/blog/docker-manage-rancher-itroduction/
