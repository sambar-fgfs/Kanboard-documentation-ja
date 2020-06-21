Debianへのインストール
======================

Debian 10 (Buster)
------------------

ApacheとPHPをインストールする:

.. code:: bash

    apt update
    apt install -y apache2 libapache2-mod-php php-cli php-mbstring \
        php-sqlite3 php-opcache php-json php-ldap php-gd php-xml  \
        php-mysql php-pgsql php-curl php-zip

    systemctl enable apache2

Install Kanboard:

.. code:: bash

    version=1.2.13
    wget https://github.com/kanboard/kanboard/archive/v$version.tar.gz
    tar xzvf v$version.tar.gz -C /var/www/html/
    chown -R www-data:www-data /var/www/html/kanboard-$version/data
    
    rm v$version.tar.gz

.. 注意::

    - Kanboardのいくつかの特徴は、毎日のバックグラウンドジョブの実行を必要とします。

