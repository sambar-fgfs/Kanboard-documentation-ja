OpenSuse へのインストール
========================

.. 警告::

    このページは長い間更新されておらず、古い可能性があります。

.. danger::  **セキュリティ**

    - デフォルトの ユーザー名/パスワード からの変更を忘れないでください。
    - 全ての人がURLから ``data`` ディレクトリへアクセスできるようにしてはいけません。
    - Apache を使用している場合、 ``.htaccess`` を有効にしてください。 (Option ``AllowOverride All``).
    - これはサーバーを正しく設定するために必須です。

OpenSuse Leap 42.3
------------------

.. code:: bash

    # 必要なパッケージのインストール
    sudo zypper install apache2-mod_php7 php7-openssl php7-gd php7-mbstring php7-mcrypt php7-mysql php7-xmlrpc php7-ctype php7-json

    # php7 を有効にする
    sudo a2enmod php7

    cd /srv/www/htdocs

    # https://github.com/kanboard/kanboard/releases より最新リリースをダウンロードする

    sudo wget https://github.com/kanboard/kanboard/archive/v<version>.zip
    sudo unzip kanboard-<version>.zip

    # パーミッションを正しくする(ファイルの所有者を変更する)
    sudo chown -R wwwrun /srv/www/htdocs/kanboard-<version>/data

    #Apache を再起動する
    sudo rcapache2 restart

    # クリーンアップ
    sudo rm kanboard-<version>.zip
