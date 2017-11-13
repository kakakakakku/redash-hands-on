# redash-hands-on

## 環境構築

Docker Compose で Redash (v2.0.1) 環境を構築します．任意のディレクトリに Redash リポジトリをクローンし，リリースタグから v2.0.1 に切り替えましょう．

```sh
$ git clone git@github.com:getredash/redash.git
$ cd redash
$ git checkout tags/v2.0.1 -b v2.0.1
```

次に Redash からテストデータを事前に投入した MySQL 5.7 に接続できるように `docker-compose.production.yml` を変更します．以下のように変更をしましょう．

```diff
       - server
     links:
       - server:redash
+  mysql:
+    image: kakakakakku/mysql-57-world-database
+    environment:
+      MYSQL_ALLOW_EMPTY_PASSWORD: "yes"
```

変更をしたら Docker Compose で Redash を起動します．初回はイメージをダウンロードするため，少し時間がかかる場合があります．

```
$ docker-compose -f docker-compose.production.yml run --rm server create_db
$ docker-compose -f docker-compose.production.yml up
```

起動すると，以下の URL で Redash にアクセスできるようになります．

- http://localhost

最初に Admin User と Organization Name を登録しましょう．以下にサンプルを載せておきます．登録が完了すると，Redash にログインできます．

- Admin User
    - Name
        - `admin`
    - Email Address
        - `admin@example.com`
- General
    - Organization Name
        - `hands-on`

![](images/setup.png)

なお，Redash 環境の構築方法は Docker Compose 以外にもあります．興味のある方は，公式ドキュメントを読んでみましょう．

- [Setting up a Redash instance · Redash Help Center](https://redash.io/help-onpremise/setup/setting-up-redash-instance.html)
