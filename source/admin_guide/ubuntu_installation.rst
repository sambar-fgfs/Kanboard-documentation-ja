Ubuntuへのインストール
======================

Ubuntu Xenial 16.04 LTS
-----------------------

ApacheとPHPをインストールする:

.. code:: bash

    sudo apt-get update
    sudo apt-get install -y apache2 libapache2-mod-php7.0 php7.0-cli php7.0-mbstring php7.0-sqlite3 \
        php7.0-opcache php7.0-json php7.0-mysql php7.0-pgsql php7.0-ldap php7.0-gd php7.0-xml

Install Kanboard:

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
