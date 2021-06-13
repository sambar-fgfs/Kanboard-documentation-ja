FreeBSD へのインストール
=======================

.. danger::  **セキュリティ**

    - デフォルトの ユーザー名/パスワード からの変更を忘れないでください。
    - 全ての人がURLから ``data`` ディレクトリへアクセスできるようにしてはいけません。
    - Apache を使用している場合、 ``.htaccess`` を有効にしてください。 (Option ``AllowOverride All``).
    - これはサーバーを正しく設定するために必須です。

パッケージのインストール
--------------------

.. code:: bash

    $ pkg upgrade -y
    $ pkg install -y apache24 mod_php56 kanboard

Apache を ``/etc/rc.conf`` で有効にする:

.. code:: bash

    $ sysrc apache24_enable=yes

Apache に PHPをセットアップする:

.. code:: bash

    $ echo "AddType application/x-httpd-php .php" >> /usr/local/etc/apache24/Includes/php.conf
    $ echo "DirectoryIndex index.php index.html" >> /usr/local/etc/apache24/Includes/php.conf

その後Apacheを起動する:

.. code:: bash

    $ service apache24 start

Apache の docroot に Kanboardフォルダのシンボリックリンクを追加 :

.. code:: bash

    cd /usr/local/www/apache24/data
    ln -s /usr/local/www/kanboard

http://your.server.domain.tld/kanboard を開けば使用できます!

.. 注意::
    もしLDAP統合のような外部の機能を使用する場合、それに応じたPHPモジュールをpkgでインストールしてください。
- フォルダのデータへのアクセス権を調整する必要があるかもしれません。

ports からインストールする
---------------------

一般的に、 3つのパッケージをインストールしなければなりません:

-  Apache
-  mod_php for Apache
-  Kanboard

portsをfetchして展開する…

.. code:: bash

    $ portsnap fetch
    $ portsnap extract

もしくは、既にインストールされている物をアップデートする:

.. code:: bash

    $ portsnap fetch
    $ portsnap update

portsnapについての更なる詳細は `FreeBSD Handbook <https://www.freebsd.org/doc/handbook/ports-using.html>`__ にあります。

Apache をインストールする:

.. code:: bash

    $ cd /usr/ports/www/apache24
    $ make install clean

Apache を ``/etc/rc.conf`` で有効にする:

.. code:: bash

    $ sysrc apache24_enable=yes

mod_php for Apache をインストールする:

.. code:: bash

    $ cd /usr/ports/www/mod_php5
    $ make install clean

portsからKanboardをインストールする:

.. code:: bash

    $ cd /usr/ports/www/kanboard
    $ make install clean

Apache に PHPをセットアップする:

.. code:: bash

    $ echo "AddType application/x-httpd-php .php" >> /usr/local/etc/apache24/Includes/php.conf
    $ echo "DirectoryIndex index.php index.html" >> /usr/local/etc/apache24/Includes/php.conf

その後Apacheを起動する:

.. code:: bash

    $ service apache24 start

http://your.server.domain.tld/kanboard を開けば使用できます!

*注意*:もしLDAP統合のような外部の機能を使用する場合、それに応じたPHPモジュールを ``lang/php5-extensions`` からインストールしてください。

手動でのインストール
-------------------

Kanboard 1.0.16 はFreeBSD portsにあるので、手動インストールは必要ありません。

.. 注意:: `bitbucket <https://bitbucket.org/if0/freebsd-kanboard/>`__ でportsがホストされています。
          コメント、フォーク、アップデートの提案はご自由にどうぞ!
