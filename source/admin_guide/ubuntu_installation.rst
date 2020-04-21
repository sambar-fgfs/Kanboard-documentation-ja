Ubuntuへのインストール
======================

Ubuntu Bionic 18.04 LTS
-----------------------

ApacheとPHPをインストールする:

.. code:: bash

    sudo apt-get update
    sudo apt-get install -y apache2 libapache2-mod-php7.2 php7.2-cli php7.2-mbstring php7.2-sqlite3 \
        php7.2-opcache php7.2-json php7.2-mysql php7.2-pgsql php7.2-ldap php7.2-gd php7.2-xml

(もしくは) Nginx と PHP をインストールする:

.. code:: bash

    sudo apt-get update
    sudo apt-get install nginx php7.2-fpm php7.2-mysql php7.2-pgsql php7.2-gd php7.2-mbstring php7.2-sqlite3 \
        php7.2-xml

Kanboardのインストール:

.. code:: bash

    cd /var/www/html

    # https://github.com/kanboard/kanboard/releases より最新リリースをダウンロードする
    wget https://github.com/kanboard/kanboard/archive/v<version>.zip

    unzip kanboard-<version>.zip
    chown -R www-data:www-data kanboard-<version>/data
    rm kanboard-<version>.zip

.. 注意::

    - ``phpenmod`` コマンドでPHP拡張モジュールを有効にしなければなりません。
    - Kanboardのいくつかの特徴は、毎日のバックグラウンドジョブの実行を必要とします。
