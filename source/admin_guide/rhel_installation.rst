RHEL/Centos/Oracle Linux Enterprise へのインストール
=====================================================

.. 警告::

    このページは長い間更新されておらず、古い可能性があります。

.. danger::  **セキュリティ**

    - デフォルトの ユーザー名/パスワード からの変更を忘れないでください。
    - 全ての人がURLから ``data`` ディレクトリへアクセスできるようにしてはいけません。
    - Apache を使用している場合、 ``.htaccess`` を有効にしてください。 (Option ``AllowOverride All``).
    - これはサーバーを正しく設定するために必須です。

Centos 7
--------

PHPとApacheをインストールする:

.. code:: bash

    yum install -y php php-xml php-mbstring php-pdo php-gd unzip wget

デフォルトでは、 Centos 7 は PHP 5.4.16 と Apache 2.4.6 を使用します

Apache を再起動する:

.. code:: bash

    systemctl restart httpd.service

Kanboardのインストール:

.. code:: bash

    cd /var/www/html

    # https://github.com/kanboard/kanboard/releases より最新リリースをダウンロードする
    wget https://github.com/kanboard/kanboard/archive/v<version>.zip

    unzip kanboard-<version>.zip
    chown -R apache:apache kanboard-<version>/data
    rm kanboard-<version>.zip

SELinux の制限
--------------------

SELinux が有効な場合、必ずApacheを実行するユーザーがディレクトリのデータに書き込みできるようにしなければなりません:

.. code:: bash

    chcon -R -t httpd_sys_content_rw_t /var/www/html/kanboard/data

必ず、Kanboardに対してEmail送信と外部ネットワークへリクエストを送ることを許容するようにサーバーを設定してください。SELinuxの例:

.. code:: bash

    setsebool -P httpd_can_network_connect=1

LDAP, SMTP, Webhookやその他の外部統合を使用する場合、外部コネクションを許容することが必要です。
