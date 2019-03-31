OpenSuse へのインストール
========================

OpenSuse Leap 42.3
------------------

.. code:: bash

    # 必要なパッケージをインストールする
    sudo zypper install apache2-mod_php7 php7-openssl php7-gd php7-mbstring php7-mcrypt php7-mysql php7-xmlrpc php7-ctype php7-json

    # php7 を有効にする
    sudo a2enmod php7

    cd /srv/www/htdocs

    # https://github.com/kanboard/kanboard/releases より最新リリースをダウンロードする

    sudo wget https://github.com/kanboard/kanboard/archive/v<version>.zip
    sudo unzip kanboard-<version>.zip

    # フォルダ所有者を変更する
    sudo chown -R wwwrun /srv/www/htdocs/kanboard-<version>/data

    # apache を再起動する
    sudo rcapache2 restart

    # cleanup
    sudo rm kanboard-<version>.zip
