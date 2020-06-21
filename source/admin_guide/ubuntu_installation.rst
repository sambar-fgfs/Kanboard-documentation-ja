Ubuntuへのインストール
======================

Ubuntu Focal Fossa 20.04 LTS
----------------------------

ApacheとPHPをインストールする:

.. code:: bash

    sudo apt update
    sudo apt install -y apache2 libapache2-mod-php php-cli php-mbstring php-sqlite3 php-opcache php-json php-mysql php-pgsql php-ldap php-gd php-xml
    
(or) Install Nginx and PHP:

.. code:: bash

    sudo apt update
    sudo apt install nginx php-fpm php-mysql php-pgsql php-gd php-mbstring php-sqlite3 php-xml

Install Kanboard:

.. code:: bash

    #適用するバージョン番号r
    version=1.2.24 (訳注:翻訳時の最新版はv1.2.15)

    # https://github.com/kanboard/kanboard/releases より最新リリースをダウンロードする
    wget https://github.com/kanboard/kanboard/archive/v$version.tar.gz
    tar xzvf v$version.tar.gz -C /var/www/html/
    chown -R www-data:www-data /var/www/html/kanboard-$version/data
    
    rm v$version.tar.gz

.. 注意::

    - ``phpenmod`` コマンドでPHP拡張モジュールを有効にしなければなりません。
    - Kanboardのいくつかの特徴は、毎日のバックグラウンドジョブの実行を必要とします。

    

Ubuntu Bionic 18.04 LTS
-----------------------

ApacheとPHPをインストールする:

.. code:: bash

    sudo apt-get update
    sudo apt-get install -y apache2 libapache2-mod-php7.2 php7.2-cli php7.2-mbstring php7.2-sqlite3 \
        php7.2-opcache php7.2-json php7.2-mysql php7.2-pgsql php7.2-ldap php7.2-gd php7.2-xml

(or) Install Nginx and PHP:

.. code:: bash

    sudo apt-get update
    sudo apt-get install nginx php7.2-fpm php7.2-mysql php7.2-pgsql php7.2-gd php7.2-mbstring php7.2-sqlite3 \
        php7.2-xml

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
