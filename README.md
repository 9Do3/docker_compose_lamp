# ローカル開発用Docker Compose

### はじめに
こちらは `Docker` で構築されています。
そのためローカルPCにDockerのインストールが必要です。

**[Docker Desktop](https://hub.docker.com/)**
```
上記から Docker Desctop のインストールを行います。
サインインしないとダウンロードできないので、
アカウント作成していない場合は右上の Get Started からアカウント作成してください。
```

### docker-composeコマンド

```
# 各種コンテナのビルドを行う（一番最初に行う）
docker-compose build

# コンテナのバックグラウンド起動
docker-compose up -d

# コンテナの停止
docker-compose stop

# コンテナの削除（先にコンテナを停止しないと実行できない）
docker-compose rm

# コンテナ/イメージ/ボリューム/ネットワークの一括削除（ローカル環境をクリーンにして作り直したい場合に使用する）
docker-compose down --rmi all --volumes
```

### 環境

今回のコンテナは以下の通りです。

**PHP(+Apache)**
https://hub.docker.com/_/php

```
・使用イメージはphp公式です。
・phpのバージョンは「7.4」です。
・phpの設定をしたい場合は「_php/php-ext.ini」に追記してください。（設定後はコンテナの再起動してください）
・ドキュメントルートは「www」ディレクトリになっています。
・複数案件を入れる場合は「www/cago5」というように配置してください。
・VirtualHostを設定したい場合は「_httpd/conf」内の「default.conf」を複製して設定してください。（設定後はコンテナの再起動してください）
・apacheのアクセス/エラーログは「_httpd/log」配下に出力されます、各種デバッグに使用してください。
```

---

**mysql**
https://hub.docker.com/_/mysql

```
・使用イメージはmysql公式です。
・mysqlのバージョンは「最新」が入ります。（指定する場合は上記リンクの「Tags」から指定バージョンを探して「docker-compose.yml」に設定してください）
・rootユーザーのパスワードは「root」です。
・デフォルトの文字コードは「utf8mb4」です。
・デフォルトの照合順序は「utf8mb4_unicode_ci」です。
・他のコンテナや外部から接続する場合はhostを「mysql」にしてください。
```

---

**phpmyadmin**
https://hub.docker.com/_/phpmyadmin

```
・使用イメージはphpmyadmin公式です。
・phpmyadminのバージョンは「最新」が入ります。（指定する場合は上記リンクの「Tags」から指定バージョンを探して「docker-compose.yml」に設定してください）
・「http://localhost:8080/」でアクセスできます。
```

---

**mailcatcher**
https://hub.docker.com/r/schickling/mailcatcher/

```
・mailcatcherのバージョンは「最新」が入ります。
・smtpポートは「1025」です。
・「http://localhost:1080/」でアクセスできます。
```