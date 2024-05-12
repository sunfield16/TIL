## docker-compose
docker-composeは複数のコンテナの連携を簡単に行うための設定ファイル。

Dockerでは1つのコンテナを起動するにも様々な設定をつける必要がある。  
これをCLI上で毎回指定するのはミスの可能性もあり危険なので、  
基本的にはdocker-composeを使用することになる。  

docker-composeは[YAML](/Serialization/YAML.md)ファイルであるため、バージョン管理も簡単。

また、起動するコンテナが1つだけでも問題なく使用可能。  
（むしろ1つだけでも、これを使った方が簡単に設定確認・起動ができると思われる）

## 基本の使い方
ファイル名は`compose.yaml`が[推奨されている](https://docs.docker.com/compose/compose-application-model/)。  
下記のような形式で作成する。
```yml
services:
  [コンテナ名]:
    ~このコンテナ用の設定~
  [コンテナ名]:
    ~このコンテナ用の設定~
  [コンテナ名]:
    ...
```

## コンテナ用の設定
### image, build
`image`は使用するイメージを直接指定、`build`は使用するDockerfileがあるディレクトリを指定する。  
どちらか片方のみ使用可能。
```yml
# centos7のイメージから作成する
image: centos:centos7

# このymlのあるディレクトリ直下の`app`ディレクトリにあるDockerfileから作成する
build: ./app
```

### ports
コンテナが開放するポートを指定する。  
複数指定すれば全て開放可能。
```yml
# [ホストPC側のポート]:[コンテナ側のポート]で指定する
ports:
  - 8000:80
```

### volumes
コンテナにマウントするディレクトリを指定する。  
基本的にコンテナを削除するとデータは消滅するが、ホストPCのディレクトリをマウントすることで  
データを永続化させることが可能。
```yml
# [ホストPC側のディレクトリ]:[コンテナ側のマウント先ディレクトリ]で指定する
volumes:
  - "./app/data:/www/app/"
```