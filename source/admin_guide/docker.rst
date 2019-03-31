Docker上でKanboardを実行する
============================

.. 警告:: `ChangeLog <https://github.com/kanboard/kanboard/blob/master/ChangeLog>`_ を見ること無しで盲目的なアップデートをしないでください。
             重大な変更点の確認を怠らないでください。


Docker タグ
-----------

+--------------+-----------------------------------------------------+
| タグ         | 概要                                                |
+==============+=====================================================+
| latest       | 最新の安定リリース                                  |
+--------------+------------------------------------------------------+
| v1.2.x       | Kanboardの特定バージョン                            |
+--------------+-----------------------------------------------------+

環境変数
---------------------

+--------------------------+------------------------------------------------------------------------------------------------+
| 変数                     | 概要                                                                                           |
+==========================+================================================================================================+
| DATABASE\_URL            | ``[database type]://[username]:[password]@[host]:[port]/[database name]``,                     |
|                          | 例: ``postgres://foo:foo@myserver:5432/kanboard``                                              |
+--------------------------+------------------------------------------------------------------------------------------------+
| DEBUG                    | デバッグモードの有効化/無効化: ``true`` or ``false``                                           |
+--------------------------+------------------------------------------------------------------------------------------------+
| API_AUTHENTICATION_TOKEN | カスタムAPIトークン                                                                            |
+--------------------------+------------------------------------------------------------------------------------------------+

ボリューム
-------

+-------------------------------+------------------------------------------------------------------+
| パス                          | 概要                                                             |
+===============================+==================================================================+
| /var/www/app/data             | アプリケーションデータ (Sqliteのデータベース, 添付ファイルなど)  |
+-------------------------------+------------------------------------------------------------------+
| /var/www/app/plugins          | プラグイン                                                       |
+-------------------------------+------------------------------------------------------------------+
| /etc/nginx/ssl                | SSL 証明書                                                       |
+-------------------------------+------------------------------------------------------------------+

カスタム設定ファイル
------------------

- コンテナには ``/var/www/app/config.php``に、カスタム済みの設定ファイルがあります。
- 自作の設定ファイルをデータボリューム上の ``/var/www/app/data/config.php`` に保存することができます。
-  カスタム設定ファイルの新しいパラメーターを利用するために、コンテナを再起動しなければなりません。

コンテナを実行する
---------------------

基本的な使用法
~~~~~~~~~~~

.. code:: bash

    docker pull kanboard/kanboard:v1.2.8
    docker run -d --name kanboard -p 80:80 -t kanboard/kanboard:v1.2.8

Docker Compose
~~~~~~~~~~~~~~

``docker-compose.yml`` ファイルはKanboardのリポジトリ内にあります。ここに、Sqlite の場合の例を示します:

.. code::

    version: '2'
    services:
      kanboard:
        image: kanboard/kanboard:latest
        ports:
          - "80:80"
          - "443:443"
        volumes:
          - kanboard_data:/var/www/app/data
          - kanboard_plugins:/var/www/app/plugins
          - kanboard_ssl:/etc/nginx/ssl
    volumes:
      kanboard_data:
        driver: local
      kanboard_plugins:
        driver: local
      kanboard_ssl:
        driver: local

これは MariaDB での例です:

.. code::

  version: '2'
  services:
    kanboard:
      image: kanboard/kanboard:latest
      ports:
        - "80:80"
        - "443:443"
      volumes:
        - kanboard_data:/var/www/app/data
        - kanboard_plugins:/var/www/app/plugins
        - kanboard_ssl:/etc/nginx/ssl
      environment:
        DATABASE_URL: mysql://kb:kb-secret@db/kanboard
    db:
      image: mariadb:latest
      command: --default-authentication-plugin=mysql_native_password
      environment:
        MYSQL_ROOT_PASSWORD: secret
        MYSQL_DATABASE: kanboard
        MYSQL_USER: kb
        MYSQL_PASSWORD: kb-secret
  volumes:
    kanboard_data:
      driver: local
    kanboard_plugins:
      driver: local
    kanboard_ssl:
      driver: local

Docker Compose を利用して、コンテナを開始してください:

.. code:: bash

    docker-compose up

自分でDockerイメージをビルドする
---------------------------

Kanboardのリポジトリをクローンして、以下のコマンドを実行する*

.. code:: bash

    make docker-image

.. 注意::

    - `Kanboard 公式イメージ <https://hub.docker.com/r/kanboard/kanboard/>`__
    - `Docker の文書 <https://docs.docker.com/>`__
    - Kanboard v1.1.0より前では、 "stable" タグは使用されていません
    - Kanboard v1.2.5より後では、, "latest" タグはmasterブランチの代わりに最新安定リリースを示します
    - EMailを送るには、SMTPを使用するか、Mailgun/Sendgrid/Postmarkプラグインを使用しなければなりません
