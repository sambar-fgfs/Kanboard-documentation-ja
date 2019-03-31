Microsoft Windows Server へのインストール
========================================

Windows Server と Apache
-------------------------

このガイドは、Windows Server上でApacheとPHPを利用してKanboardをセットアップするために順を追ったヘルプです。

注意: 64 ビット版のプラットフォームでは “x64” を、そうでなければ 32ビットシステム向けの “x86” を選択してください。

Visual C++ Redistributable のインストール
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

PHP と Apache はVisual Studioでコンパイルされているため、まだVC++ Redistributableを導入していない場合には、このライブラリをインストールする必要があります。

1. このライブラリを `Microsoft 公式webサイト <http://www.microsoft.com/en-us/download/details.aspx?id=30679>`__ からダウンロードする
2. インストール先のプラットフォームに合わせて ``vcredist_x64.exe`` か ``vcredist_x86.exe`` のインストーラを実行する

Apache のインストール
~~~~~~~~~~~~~~~~~~~

1. `Apache Lounge <http://www.apachelounge.com/download/>`__ からApacheのバイナリをダウンロードする
2. Apache24 を ``C:\Apache24`` に展開する

サーバー名を決める:

``C:\Apache24\conf\httpd.conf`` を開き、以下のディレクティブを追加する*

::

    ServerName localhost

Apache サービスをインストールする
~~~~~~~~~~~~~~~~~~~~~~~~~~

コマンドプロンプト (``cmd.exe``) を開き、ディレクトリ``C:\Apache24\bin``　に移動する:

.. code:: bash

    cd C:\Apache24\bin

    # Windows サービスのインストール
    httpd.exe -k install

ApacheMonitor のインストール
~~~~~~~~~~~~~~~~~~~~~

-  ``C:\Apache24\bin\ApacheMonitor.exe``をダブルクリックするか、これをスタートアップフォルダに入れる。
-  アイコンを右クリックして、Apacheを開始する

Apache のインストールの確認
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

http://localhost/ を開いたら、"It Works!"とだけ書かれたページが表示されるはずです。

PHP のインストール
~~~~~~~~~~~~~~~~

1. `official PHP website <http://windows.php.net/download/>`__ から、**Thread Safe**なバージョンで、
    Apache同様に x86 or x64 を正確に選択して、最新安定版のPHPをダウンロードする。
2. ``C:\php`` にファイルを展開する
3. PHPフォルダに移動して、``php.ini-production`` ファイルを ``php.ini`` にリネームする

``php.ini`` を編集する:

拡張のディレクトリのコメント化を解除する:

.. code:: ini

    extension_dir = "C:/php/ext"

これらの PHP モジュールのコメント化を解除する:

.. code:: ini

    extension=php_gd2.dll
    extension=php_ldap.dll
    extension=php_mbstring.dll
    extension=php_openssl.dll
    extension=php_pdo_sqlite.dll

タイムゾーンを設定する:

.. code:: ini

    date.timezone = America/Montreal

`PHP documentation <http://php.net/manual/en/timezones.america.php>`__ に、サポートしているタイムゾーンの一覧があります。

PHP モジュールを Apache にロードする:

``C:\Apache24\conf\httpd.conf`` に以下の設定を追加する:

::

    LoadModule php5_module "c:/php/php5apache2_4.dll"
    AddHandler application/x-httpd-php .php

    # configure the path to php.ini
    PHPIniDir "C:/php"

    # change this directive
    DirectoryIndex index.php index.html

Apache を再起動する。

PHP のインストールのテスト*

``phpinfo.php`` という名前で、``C:\Apache24\htdocs``に以下の内容のファイルを作成する:

.. code:: php

    <?php

    phpinfo();

    ?>

http://localhost/phpinfo.php を開いたら、PHPのインストールについての情報が表示されるはずです。

Kanboard のインストール
~~~~~~~~~~~~~~~~~~~~~

-  Zipファイルをダウンロードする
-  ダウンロードしたアーカイブを``C:\Apache24\htdocs\kanboard`` に展開する
-   Kanboardを使うために、 http://localhost/kanboard/ をブラウザで開く
-   初期設定のユーザー名・パスワードは **admin/admin** です。

Windows Server と IIS
----------------------

このガイドは、Windows Server上でIISとPHPを利用してKanboardをセットアップするために順を追ったヘルプです。

PHP のインストール
~~~~~~~~~~~~~~~~

-  サーバーにIIS をインストールする (新しいロールを追加するとともに、 CGI/FastCGIを有効にするのを忘れないでください)
-  公式ドキュメントに従って  PHP をインストールする:

   -  `Microsoft IIS 5.1 と IIS  6.0 <http://php.net/manual/en/install.windows.iis6.php>`__
   -  `Microsoft IIS 7.0 以降 <http://php.net/manual/en/install.windows.iis7.php>`__
   -  `PHP for Windows はここから入手できます <http://windows.php.net/download/>`__

PHP.ini
~~~~~~~

少なくとも、 ``php.ini`` でこれらの拡張が必要です:

.. code:: ini

    extension=php_gd2.dll
    extension=php_ldap.dll
    extension=php_mbstring.dll
    extension=php_openssl.dll
    extension=php_pdo_sqlite.dll

タイムゾーンの設定を忘れないでくささい:

.. code:: ini

    date.timezone = America/Montreal

`PHP documentation <http://php.net/manual/en/timezones.america.php>`__ に、サポートしているタイムゾーンの一覧があります。

.. 注意::

    -  上述した、必要なPHP拡張を有効にするのを忘れないでください。

    -  “the library MSVCP110.dll is missing”エラーが発生した場合、おそらくVisual C++ Redistributable for Visual Studioを再インストールする必要があるでしょう。

IIS モジュール
~~~~~~~~~~~

Kanboardアーカイブに含まれる ``web.config`` ファイルでURL rewritingを有効にします。この設定には`Rewrite module for IIS <http://www.iis.net/learn/extensions/url-rewrite-module/using-the-url-rewrite-module>`__ が必要になります。

このRewriteモジュールが無い場合、IISは Internal Server Error (500) を返します。Kanboard でURL Rewriteを利用しない場合、 ``web.config``ファイルを削除できます。

Kanboard のインストール
~~~~~~~~~~~~~~~~~~~~~

-  Zipファイルをダウンロードする
-  ダウンロードしたアーカイブを``C:\inetpub\wwwroot\kanboard`` に展開する
-  IISのユーザーが ``data`` ディレクトリに書き込み出来るか確認してください。
-   Kanboardを使うために、 http://localhost/kanboard/ をブラウザで開く
-   初期設定のユーザー名・パスワードは **admin/admin** です。
