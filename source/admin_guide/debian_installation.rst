Debianへのインストール
======================

Debian 9 (Stretch)
------------------

ApacheとPHPをインストールする:

.. code:: bash

    apt update
    apt install -y apache2 libapache2-mod-php7.0 php7.0-cli php7.0-mbstring \
        php7.0-sqlite3 php7.0-opcache php7.0-json php7.0-mysql php7.0-pgsql \
        php7.0-ldap php7.0-gd php7.0-xml

    systemctl enable apache2 postgresql

Install Kanboard:

.. code:: bash

    version=1.2.5
    wget https://github.com/kanboard/kanboard/archive/v$version.tar.gz
    tar xzvf v$version.tar.gz -C /var/www/
    chown -R www-data:www-data /var/www/kanboard-$version/data

Debian 8 (Jessie)
-----------------

ApacheとPHPをインストールする:

.. code:: bash

    apt-get update
    apt-get install -y php5 php5-sqlite php5-gd unzip
    service apache2 restart

Install Kanboard:

.. code:: bash

    cd /var/www/html

    # https://github.com/kanboard/kanboard/releases より最新リリースをダウンロードする
    wget https://github.com/kanboard/kanboard/archive/v<version>.zip

    unzip kanboard-<version>.zip
    chown -R www-data:www-data kanboard-<version>/data
    rm kanboard-<version>.zip

Debian 7 (Wheezy)
-----------------

ApacheとPHPをインストールする:

.. code:: bash

    apt-get update
    apt-get install -y php5 php5-sqlite php5-gd unzip

Install Kanboard:

.. code:: bash

    cd /var/www

    # https://github.com/kanboard/kanboard/releases より最新リリースをダウンロードする
    wget https://github.com/kanboard/kanboard/archive/v<version>.zip

    unzip kanboard-<version>.zip
    chown -R www-data:www-data kanboard-<version>/data
    rm kanboard-<version>.zip

Debian 6 (Squeeze)
------------------

ApacheとPHPをインストールする:

.. code:: bash

    apt-get update
    apt-get install -y libapache2-mod-php5 php5-sqlite php5-gd unzip

Install Kanboard:

.. code:: bash

    cd /var/www

    # https://github.com/kanboard/kanboard/releases より最新リリースをダウンロードする
    wget https://github.com/kanboard/kanboard/archive/v<version>.zip

    unzip kanboard-<version>.zip
    chown -R www-data:www-data kanboard-<version>/data
    rm kanboard-<version>.zip
